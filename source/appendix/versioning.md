---
title: Versioning Map
date: 2017-06-01
version: 3.3
keywords: [OSDK version, SDK version, version, firmware]
---

## Versioning

The firmware versions for the flight controller differ from the firmware packages available for download through DJI Assistant 2; the firmware package contains firmware for other components as well as the flight controller.

The Onboard SDK is only concerned with the flight control version. Activating the Onboard SDK requires the flight controller firmware version to be passed as an argument.

On all platforms other than the STM32, this versioning is automatically handled as part of the Vehicle constructor. However on the STM32, users need to provide the version manually.

#### Finding your Firmware Package Version

1. Open DJI Assistant 2 and connect your flight controller/aircraft to Assistant.
2. Navigate to the Firmware Upgrade tab.
3. Note down the version that says `Current` on the side. If none say `Current`, you need to upgrade your firmware.
4. Use the table below to find the corresponding flight controller firmware version.

#### Mapping Firmware Package Version to Flight Control Version

| Aircraft/FC    	| Firmware Package Version 	| Flight Controller Version  	|
|----------------	|--------------------------	|----------------------------	|
| A3/A3 Pro      	| 1.7.0.5                  	| 3.2.15.50                  	|
|                	| 1.7.0.0                  	| 3.2.15.37                  	|
|                	|                          	|                            	|
| N3             	| 1.7.0.0                  	| 3.2.15.37                  	|
|                	|                          	|                            	|
| M600/ M600 Pro 	| 1.0.1.20                 	| 3.2.15.62                  	|
|                	| 1.0.0.80                 	| 3.2.15.00                  	|

#### Using this version in the STM Sample

Once you have your flight controller version (3.x.yz.wv), simply replace the periods `.` with commas `,` and enter them on the `user_act_data.version = Version::FW(3, x, yz, wv)` line.
