---
title: Versioning Map
date: 2017-06-01
version: 3.3
keywords: [OSDK version, SDK version, version, firmware]
---

## Versioning

Firmware upgrades are delivered to DJI Products through firmware packages available on DJI Assistant 2. The firmware versioning system for the flight controller differs from the firmware **package** versioning system ; the firmware package contains firmware for other components as well as the flight controller.

The Onboard SDK is only concerned with the flight control version. Activating the Onboard SDK requires the flight controller firmware version to be supported by the Onboard SDK.

See the table below to determine which firmware package available on DJI Assitant 2 works with which version of the OSDK.

#### Finding your Firmware Package Version

1. Open DJI Assistant 2 and connect your flight controller/aircraft to Assistant.
2. Navigate to the Firmware Upgrade tab.
3. Note down the version that says `Current` on the side. If none say `Current`, you need to upgrade your firmware.
4. Use the table below to find the corresponding flight controller firmware version.

#### Mapping Firmware Package Version to Flight Control Version

| Aircraft/FC       | Firmware Package Version | Flight Controller Version  | OSDK Version Support      |
|---------------    |--------------------------|----------------------------|----------------------     |
| **A3/A3 Pro**     | **<Insert latest>**      | **3.2.36.7**               | **OSDK 3.3 (Current)**    |
|                   | 1.7.0.5                  | 3.2.15.50                  | OSDK 3.2                  |
|                   | 1.7.0.0                  | 3.2.15.37                  | OSDK 3.2                  |
|                   |                          |                            |                           |
| **N3**            | **<Insert Latest>**      | **3.2.36.7**               | **OSDK 3.3 (Current)**    |
|                   | 1.7.0.0                  | 3.2.15.37                  | OSDK 3.2                  |
|                   |                          |                            |                           |
| **M600/M600 Pro** | **<Insert Latest>**      | **3.2.36.7**               | **OSDK 3.3 (Current)**    |
|                   | 1.0.1.20                 | 3.2.15.62                  | OSDK 3.2                  |
|                   | 1.0.0.80                 | 3.2.15.00                  | OSDK 3.2                  |
|                   |                          |                            |                           |
| **M100**          | 1.3.1.0                  | 3.1.10.0                   | OSDK 3.2                  |
