---
title: Release Notes for Onboard SDK 3.1.7
date: 2016-07-01
---
## Highlights

* This release is a major cleanup and bugfix release for Onboard SDK 3.1
* Over a hundred bugs have been squashed
* Code has much-improved comments and is easier to follow
* Introduces an alpha version of a unit-testing suite for the core library
* Provides the capability to build the core library independently of the samples for easier integration into larger projects
* Introduces an alpha version of Doxygen-style code commenting and pre-generated html doxygen documentation

New developers should start with the revamped [Getting Started Guide](../quick-start/index.html).

## Major Fixes

#### Core Library

* Code style updated to a more modern GNU-like style. Change affects indentations and new functions/variables/structs introduced in this release. Older functions, variables, structs and classes are untouched. 
* Many elements of code have been identified as sub-optimal; we have started marking these structs/functions for deprecation in a future release. We are fully backwards compatible for this release - no old elements have been removed, but users are encouraged to move to the newer elements introduced as part of this release. Doxygen-style comments document the changes and planned replacements; users should look into the core library or go to `doc/doxygen-doc/html/index.html` to see doxygen code documentation.

    Some examples (**This table is not exhaustive!**): 

|Old element|Planned New element|Description|File|
|-------|------|---------|--------|
|MagnetData|MagData|Name change|DJI_Type.h|
|PositionData|PositionData|Struct member restructuring|DJI_Type.h|
|toRadioData|toRCData|Function interface change|DJI_VirtualRC.h|
|toEulerianAngle|toEulerAngle|Function interface change|DJI_Flight.h|

>To re-iterate: these changes are **planned for a future release**. In this release, both old and new versions co-exist.    

* Replaced all uses of `palstance` with `YawRate`
* CMake support for Linux platforms added
* Unit testing framework introduced
* Setter/getter added for open protocol transmission session status

#### Qt

* UI elements have been cleaned up and the behavior of a number of buttons has been changed. New button behavior is a lot more informative.

|Functionality|Fixed Issues|
|---------|---------|
|Display Scaling|Added support for Hi-res displays|
|Qt function discovery|Changed many functions to allow Qt to automatically find them|
|Button behavior|Arm, activation, hotpoint buttons are interactive/more informative|
|Waypoint functionality|<ul><li>Intermittent crashes fixed</li><li>Lat/Lon input changed from radians to degrees</li>Revamped layout and added indications for the order of operations</ul>|
|Hotpoint Functionality|Lat,Lon can now be entered in degrees|
|UI| Unused buttons and tabs removed. UI looks a lot cleaner.| 

* Build has been updated to work with the newest Qt release (5.6). DJI Script dependencies have been removed to streamline Qt build. 

#### Commandline Linux

* The commandline linux sample has undergone a major revamp. Many functions have been fixed:

|Functionality|Fixed Issues|
|-------|---------|
|Activation|<ul><li>Version mismatch error fixed</li><li>Reliability improved</li><li>Feedback messages improved</li></ul>|
|Waypoint|<ul><li>"Not enough waypoints" error fixed</li><li>Much clearer steps of operation </li><li>Bus error on Manifold fixed</li></ul>|
|Hotpoint|<ul><li>No execution though success message appears - fixed</li><li>Bus error on Manifold fixed</li></ul>|
|VirtualRC|Functionality has now been implemented|
|Flight Control|<ul><li>No execution - fixed </li><li>Unbounded motion fixed</li><li>Bus error on Manifold fixed</li></ul>|

* Directory structure has changed to a more standard structure. ManifoldPlatform folder has been removed and the Linux example now consolidates all linux-based platforms.
* Automatic activation sequence added
* User Configuration file added
* On-screen information at the interactive prompt updated to be more useful 

#### ROS

* ROS repository will now follow the same version numbers as the core repo. The current release is tagged as 3.1.7.
* ROS Onboard SDK is now based on the latest [Onboard SDK](https://github.com/dji-sdk/Onboard-SDK) library.
* 'Draw a Circle' example is revamped and implements the movement control fuctionality exposed by the open protocol. The example is now using closed-loop control.
* Waypoint and Virtual RC exmaples have been improved.
* Tested with Ubuntu 16.04 LTS/ROS Kinetic Kame - to use this configuration, install the ROS Onboard SDK from source. APT and rosinstall are not supported for this configuration
* DJI A3 Flight Controller has been tested with ROS Onboard SDK.

#### STM32

* Fixed activation errors due to version not being set.
* Fixed movement control commands - developers can now successfully execute all movement control commands through the STM32. Documentation has also been updated to reflect the same.
* Added user parameters in hotpoint mode.
* DJI A3 Flight Controller has been tested with the STM32.

---
## Previous Release

### Onboard SDK 3.1.5 Release Notes


**Important**: Developers who update firmware from 2.3 to 3.1 should update their usage of onboard SDK to this version. This file summarizes what has been changed. For detailed usage and definations of new features, please refer to the reference documentation.

New developers should start with the [Getting Started Guide](../quick-start/index.html)

### Protocol Updates from firmware 2.3 to firmware 3.1

#### New Commands

|CMD SET|CMD ID|Description|
|-------|------|-----------|
|0x01|0x05|Arm/Disarm the Drone|
|0x03||Gound Station Protocol|
|0x04|0x00|Synchronize Timestamp|
|0x05||Virtual RC Protocol|

#### Changed Commands

|CMD SET|CMD ID|Difference|2.3|3.1|
|-------|------|---|---|---|
|0x00|0x00|Version Query Result|2.3.10.0|3.1.10.0|
|0x00|0x01|App Level Removed|`typedef struct{ `<br>&nbsp;&nbsp;`uint32_t app_id;`<br>&nbsp;&nbsp;`uint32_t app_level;`<br>&nbsp;&nbsp;`uint32_t app_version;`<br>&nbsp;&nbsp;`uint8_t app_bundle_id[32];`<br>`} sdk_activation_info_t;`|`typedef struct{ `<br>&nbsp;&nbsp;`uint32_t app_id;`<br>&nbsp;&nbsp;~~`uint32_t app_level;`~~<br>&nbsp;&nbsp;`uint32_t app_version;`<br>&nbsp;&nbsp;`uint8_t app_bundle_id[32];`<br>`} sdk_activation_info_t;`|
|0x00|0x01|Activation SDK Version|0x02030a00|M100: 0x03010a00 <br>A3: 0x03016400|
|0x01|0x03|Attitude Control Flag|`bit7&6: HORI_MODE`<br>`bit5&4: VERT_MODE`<br>`bit3: YAW_MODE`<br>`bit2&1: HORI_FRAME`<br>`bit0: YAW_FRAME`|`bit7&6: HORI_MODE`<br>`bit5&4: VERT_MODE`<br>`bit3: YAW_MODE`<br>`bit2&1: HORI_FRAME`<br>`bit0: STABLE_FLAG`|

#### New Broadcast Data

|CMD Set|CMD ID|Description|
|-------|------|-----------|
|0x02|0x03|Mission Status Push Info|
|0x02|0x04|Mission Events Push Info|

#### Changed Broadcast Data

|Struct Changed|2.3|3.1|
|--------------|---|---|
|Time Stamp|`uint32_t`|`typedef struct`<br>`{`<br>&nbsp;&nbsp;`uint32_t time;`<br>&nbsp;&nbsp;`uint32_t asr_ts;`<br>&nbsp;&nbsp;`uint8_t sync_flag;`<br>`}sdk_time_stamp_t;`|
|Velocity|`typedef struct`<br>`{`<br>&nbsp;&nbsp;`float32 x;`<br>&nbsp;&nbsp;`float32 y;`<br>&nbsp;&nbsp;`float z;`<br>&nbsp;&nbsp;`uint8_t health_flag:1;`<br>&nbsp;&nbsp;`uint8_t sensor_id:4;`<br>&nbsp;&nbsp;`uint8_t reserved:3;`<br>`} velocity_data_t;`|`typedef struct`<br>`{`<br>&nbsp;&nbsp;`float32 x;`<br>&nbsp;&nbsp;`float32 y;`<br>&nbsp;&nbsp;`float z;`<br>&nbsp;&nbsp;`uint8_t health_flag:1;`<br>&nbsp;&nbsp;`uint8_t reserved:7;`<br>`} velocity_data_t;`|
|Ctrl Device|`typedef struct`<br>`{`<br>&nbsp;&nbsp;`uint8_t cur_ctrl_dev_in_navi_mode: 3;`<br>&nbsp;&nbsp;`uint8_t serial_req_status: 1;`<br>&nbsp;&nbsp;`uint8_t reserved: 4;`<br>`} ctrl_device_t;`|`typedef struct`<br>`{`<br>&nbsp;&nbsp;`uint8_t cur_api_ctrl_mode;`<br>&nbsp;&nbsp;`uint8_t cur_ctrl_dev_in_navi_mode: 3;`<br>&nbsp;&nbsp;`uint8_t serial_req_status: 1;`<br>&nbsp;&nbsp;`uint8_t vrc_enable_flag: 1;`<br>&nbsp;&nbsp;`uint8_t reserved: 3;`<br>`} ctrl_device_t;`|

### Onboard SDK Library Updates

- We have cleaned up data structures, core logic, and example usage.
- This library is compatible with both 2.3 and 3.1 firmware.
- The 2.3 branch and old library are archived for reference.

### `F` Mode Updates [IMPORTANT]

**Important:** With firmware 3.1, developers are now able to obtain onboard SDK control immediately when the drone is powered on with the remote controller's mode switch in the `F` position.  Previously, with firmware 2.3, develoeprs had to toggle the mode switch out of `F` mode and then return to `F` mode in order to obtain control.

Please consider the user experience and design of your application to ensure that inadvertent SDK control of the vehicle is not allowed.
