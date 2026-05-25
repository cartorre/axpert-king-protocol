# Axpert King Rack 5KW 48V - Protocol Documentation

**Firmware:** CPU 75.09 / Secondary 15.09  
**Model:** Axpert King Rack 5KW (Voltronic Power)  
**Protocol Version:** PI30  
**Date:** May 25, 2026  
**Based on:** Real device testing and protocol analysis

---

## 📋 Table of Contents

1. [Hardware Specifications](#1-hardware-specifications)
2. [LCD Programs](#2-lcd-programs)
3. [Supported Commands](#3-supported-commands)
4. [QPIRI Command - Device Ratings](#4-qpiri-command---device-ratings)
5. [QDI Command - Default Values](#5-qdi-command---default-values)
6. [QFLAG Command - Status Flags](#6-qflag-command---status-flags)
7. [QPIGS Command - Operational Status](#7-qpigs-command---operational-status)
8. [QMOD Command - Operation Mode](#8-qmod-command---operation-mode)
9. [Write Commands](#9-write-commands)
10. [Firmware 75.09 Specifics](#10-firmware-7509-specifics)
11. [API Integration](#11-api-integration)

---

## 1. Hardware Specifications

| Parameter | Value |
|-----------|-------|
| Rated Power | 5000W / 5000VA |
| Battery Voltage | 48V |
| Battery Type Supported | LIb Protocol (Lithium) |
| Maximum Charging Current | 140A |
| AC Input Voltage | 230V |
| Frequency | 50Hz |
| MPPT | Integrated (up to 4000W) |
| Communication | USB HID + RS232 + WiFi |
| Certification | CE |

## 2. LCD Programs

### Program 01 - Output Source Priority

- **USB** - Utility First
- **SUB** - Solar → Utility → Battery
- **SBU** - Solar → Battery → Utility

### Program 02 - Maximum Charging Current

Range: 10A to 140A

### Program 05 - Battery Type

| Code | Type | Description |
|------|------|-------------|
| 0 | AGM | AGM Lead-acid |
| 1 | FLD | Flooded |
| 2 | USE | User-Defined |
| 3 | PYL | Pylontech |
| 5 | WEC | WECO |
| 6 | SOL | Soltaro |
| 7 | LIA | LIa Protocol |
| 8 | LIB | LIb Protocol |

### Program 06 - Auto Restart When Overload

- **LFD** - Disable
- **LFE** - Enable

### Program 07 - Auto Restart When Over Temperature

- **LFD** - Disable
- **LFE** - Enable

### Program 09 - Output Frequency

50Hz / 60Hz

### Program 10 - Operation Logic

- **Auto** - Automatically
- **Online** - Force line mode
- **ECO** - ECO mode

### Program 11 - Maximum Utility Charging Current

Range: 2A to 60A

### Program 12 - Back to Grid Voltage (SBU/SUB)

Range: 44V to 57V

### Program 13 - Back to Battery Voltage

Range: 48V to 64V

### Program 16 - Solar Energy Priority

| Code | Mode | Utility Charge |
|------|------|----------------|
| SbL-UCb | Solar → Battery first | Allowed |
| SbL-UdC | Solar → Battery first | Disallowed |
| SLb-UCb | Solar → Load first | Allowed |
| SLb-UdC | Solar → Load first | Disallowed |

### Program 18 - Alarm Control

AON (ON) / AOF (OFF)

### Program 19 - Auto Return to Default Screen

ESP (Return) / LSP (Stay)

### Program 20 - Backlight Control

LON (ON) / LOF (OFF)

### Program 22 - Beeps While Primary Source Interrupted

AON (ON) / AOF (OFF)

### Program 23 - Bypass Function

Forbidden / Disabled / Enabled (BYE)

### Program 25 - Record Fault Code

FDS (Disable) / FDE (Enable)

### Program 26 - Bulk Charging Voltage (C.V.)

Range: 48.0V to 64.0V

### Program 27 - Float Charging Voltage

Range: 48.0V to 64.0V

### Program 28 - AC Output Mode

SIG (Single) / PAL (Parallel) / 3P1/3P2/3P3 (Three-phase)

### Program 29 - Low DC Cut-off Voltage

Range: 40.0V to 54.0V

### Program 32 - Bulk Charging Time (C.V. Stage)

Auto / 5min to 900min

### Program 34 - Battery Equalization Voltage

Range: 48.0V to 64.0V

### Program 35 - Battery Equalized Time

Range: 5min to 900min

### Program 36 - Battery Equalized Timeout

Range: 5min to 900min

### Program 37 - Equalization Interval

Range: 0 to 90 days

### Program 40 - Reset PV/Output Data

No Reset / Reset

### Program 42 - Rewrite USB Parameter

Disable / Enable

### Program 43 - Export Data Log

Disable / Enable

### Program 93 - Erase All Data Log

Disable / Enable

### Program 94 - Data Log Recorded Interval

3 / 5 / 10 / 20 / 30 / 60 minutes

### Programs 95-99 - Internal Clock

- 95: Minutes (00-59)
- 96: Hours (00-23)
- 97: Day (01-31)
- 98: Month (01-12)
- 99: Year (00-99)

---

## 3. Supported Commands

### Read Commands

| Command | Response | Description |
|---------|----------|-------------|
| QPIGS | Full status | All operational parameters |
| QPIRI | Ratings | Device nominal values |
| QDI | Default values | Factory default values |
| QFLAG | Flags | Status flags |
| QMOD | Mode | P/S/L/B/F/H |
| QVFW | Firmware | Main CPU firmware version |
| QID | Serial | Device serial number |
| QPI | Protocol | Protocol version (PI30) |

### Unsupported Commands

QOPM, QCHGS, QPOP, QPCP, QOPLG, DAT, PMN - Not implemented in this firmware.

---

## 4. QPIRI Command - Device Ratings

**Sample:** `(230.0 21.7 230.0 50.0 21.7 5000 5000 48.0 48.0 40.5 51.7 51.7 8 02 140 1 2 1 9 01 0 0 49.0 0 1 000 0`

| Index | Value | Field |
|-------|-------|-------|
| 0 | 230.0 | Grid rating voltage (V) |
| 1 | 21.7 | Grid rating current (A) |
| 2 | 230.0 | Output rating voltage (V) |
| 3 | 50.0 | Output rating frequency (Hz) |
| 4 | 21.7 | Output rating current (A) |
| 5 | 5000 | VA rating |
| 6 | 5000 | Watt rating |
| 7 | 48.0 | Battery rating voltage (V) |
| 8 | 48.0 | Battery re-charge voltage (V) |
| 9 | 40.5 | Back to grid voltage (V) |
| 10 | 51.7 | Battery bulk voltage (V) |
| 11 | 51.7 | Battery float voltage (V) |
| **12** | **8** | **Battery type (8 = LIb Protocol)** |
| 13 | 02 | Output source priority (2 = SBU) |
| 14 | 140 | Max charge current (A) |
| 15 | 1 | Input voltage range (1 = UPS) |
| 16 | 2 | Output mode |
| 17 | 1 | Charger source priority |
| 18 | 9 | Machine type |
| 19 | 01 | Topology |

---

## 5. QDI Command - Default Values

**Sample:** `(230.0 50.0 0030 42.0 54.0 56.4 46.0 60 1 0 2 0 0 0 0 0 1 1 0 0 1 0 54.0 0 1 000 0`

| Index | Value | Field |
|-------|-------|-------|
| 0 | 230.0 | Output voltage (V) |
| 1 | 50.0 | Output frequency (Hz) |
| 2 | 0030 | Max utility charge current (A) |
| 3 | 42.0 | Cut-off voltage (V) |
| 4 | 54.0 | Float voltage (V) |
| 5 | 56.4 | Bulk voltage (V) |
| 6 | 46.0 | Back to grid voltage (V) |
| 7 | 60 | Max charging current (A) |
| 8 | 1 | Operation logic |
| 9 | 0 | Output source priority |
| 10 | 2 | Charger source priority |
| 11 | 0 | Bypass function |

---

## 6. QFLAG Command - Status Flags

### ⚠️ CRITICAL: Inverted Logic on Firmware 75.09

- **Uppercase (E, B, C...) = OFF (Disabled)**
- **Lowercase (e, b, c...) = ON (Enabled)**

**Sample Response:** `(EbckxyDajuvzm`

| Pos | Flag | State | Meaning |
|-----|------|-------|---------|
| 0 | E | ❌ OFF | Buzzer alarm |
| 1 | b | ✅ ON | Overload bypass |
| 2 | c | ✅ ON | Power saving mode |
| 3 | k | ✅ ON | LCD reset to default |
| 4 | x | ✅ ON | Overload restart |
| 5 | y | ✅ ON | Over-temperature restart |
| 6 | D | ❌ OFF | Backlight |
| 7 | a | ✅ ON | Alarm on source interrupt |
| 8 | j | ✅ ON | Fault code record |

---

## 7. QPIGS Command - Operational Status

**Sample:** `(235.9 49.9 229.9 50.0 2666 2488 053 341 49.20 000 096 0034 0004 091.8 49.06 00050 00010110 00 00 00348 110`

| Index | Value | Description |
|-------|-------|-------------|
| 0 | 235.9 | Grid voltage (V) |
| 1 | 49.9 | Grid frequency (Hz) |
| 2 | 229.9 | Output voltage (V) |
| 3 | 50.0 | Output frequency (Hz) |
| 4 | 2666 | Output apparent power (VA) |
| 5 | 2488 | Output active power (W) |
| 6 | 053 | Load percent (%) |
| 7 | 341 | Bus voltage (V) |
| 8 | 49.20 | Battery voltage (V) |
| 9 | 000 | Battery charge current (A) |
| 10 | 096 | Battery capacity (%) |
| 11 | 0034 | Heatsink temperature (°C) |
| 12 | 0004 | PV input current (A) |
| 13 | 091.8 | PV input voltage (V) |
| 14 | 49.06 | SCC voltage (V) |
| 15 | 00050 | Battery discharge current (A) |
| 16 | 00010110 | Device status flags |
| 19 | 00348 | PV input power (W) |

---

## 8. QMOD Command - Operation Mode

| Code | Mode | Description |
|------|------|-------------|
| P | Power On | Starting up |
| S | Standby | Idle / Charging |
| L | Line | Using Grid power |
| B | Battery | Using Battery power |
| F | Fault | Error state |
| H | Power Saving | Energy saving mode |

---

## 9. Write Commands

### ⚠️ All write commands require CRC16

| Command | Function | Description |
|---------|----------|-------------|
| POP00 | USB Mode | Utility → Solar → Battery |
| POP01 | SUB Mode | Solar → Utility → Battery |
| POP02 | SBU Mode | Solar → Battery → Utility |
| PCP00 | Charger: Utility | Charge from grid first |
| PCP01 | Charger: Solar | Charge from solar first |
| PCP02 | Charger: Solar+Util | Charge from solar and grid |
| PCP03 | Charger: Solar Only | Charge from solar only |
| POPLG00 | Operation: Auto | Automatic logic |
| POPLG01 | Operation: Online | Force line mode |
| POPLG02 | Operation: ECO | ECO mode |

---

## 10. Firmware 75.09 Specifics

### 🔄 Inverted QFLAG Logic

Confirmed by LCD comparison: uppercase = OFF, lowercase = ON. All previous firmwares use the opposite logic.

### 🔌 Missing LCD Programs

Program 03 (AC Input Voltage Range) and Program 04 (Power Saving) are not available in the menu. UPS/APL function is controlled indirectly by Program 15.

### 📡 Communication Protocol

- Protocol version: PI30
- USB HID communication via `/dev/hidraw0`
- CRC16 mandatory for write commands
- Read commands work without CRC on HID

### 🔋 Lithium Battery Support

- LIb Protocol (code 8 in QPIRI)
- Direct BMS communication via CAN/RS485 port
- Automatic charge voltage configuration

### 🕐 Internal Clock

Programs 95-99 for manual time setting. Date/time commands (DAT, PMN) are rejected with NAK.

---

## 11. API Integration

This documentation is part of a complete solar monitoring system with:

- REST API with full command support
- MQTT for real-time data streaming
- InfluxDB for historical data storage
- Angular Frontend with real-time dashboard

### API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/axpert/latest` | Latest inverter data |
| GET | `/api/axpert/source` | Current energy source |
| GET | `/api/axpert/config` | Device configuration |
| GET | `/api/axpert/read-config` | Read raw configuration |
| POST | `/api/axpert/send` | Send command with response |
| POST | `/api/axpert/raw` | Send raw command |
| POST | `/api/axpert/mode/:mode` | Change mode (USB/SUB/SBU) |

### Related Repositories

- [skymax-demo](https://github.com/manio/skymax-demo) - Original C implementation
- [docker-voltronic-homeassistant](https://github.com/ned-kelly/docker-voltronic-homeassistant) - Docker HA integration

---

**✅ Documented:** May 25, 2026  
**🔧 Firmware:** CPU 75.09 / Secondary 15.09  
**📡 Protocol:** PI30 with CRC16 for write operations
