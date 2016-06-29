---
title: Release Notes for Onboard SDK 3.1.5
date: 2016-06-24
---

**Important**: Developers who update firmware from 2.3 to 3.1 should update their usage of onboard SDK to this version. This file summarizes what has been changed. For detailed usage and definations of new features, please refer to the reference documentation.

New developers should start with the [Getting Started Guide](../quick-start/index.html)

## Protocol Updates from firmware 2.3 to firmware 3.1

### New Commands

|CMD SET|CMD ID|Description|
|-------|------|-----------|
|0x01|0x05|Arm/Disarm the Drone|
|0x03||Gound Station Protocol|
|0x04|0x00|Synchronize Timestamp|
|0x05||Virtual RC Protocol|

### Changed Commands

|CMD SET|CMD ID|Difference|2.3|3.1|
|-------|------|---|---|---|
|0x00|0x00|Version Query Result|2.3.10.0|3.1.10.0|
|0x00|0x01|App Level Removed|`typedef struct{ `<br>&nbsp;&nbsp;`uint32_t app_id;`<br>&nbsp;&nbsp;`uint32_t app_level;`<br>&nbsp;&nbsp;`uint32_t app_version;`<br>&nbsp;&nbsp;`uint8_t app_bundle_id[32];`<br>`} sdk_activation_info_t;`|`typedef struct{ `<br>&nbsp;&nbsp;`uint32_t app_id;`<br>&nbsp;&nbsp;~~`uint32_t app_level;`~~<br>&nbsp;&nbsp;`uint32_t app_version;`<br>&nbsp;&nbsp;`uint8_t app_bundle_id[32];`<br>`} sdk_activation_info_t;`|
|0x00|0x01|Activation SDK Version|0x02030a00|M100: 0x03010a00 <br>A3: 0x03016400|
|0x01|0x03|Attitude Control Flag|`bit7&6: HORI_MODE`<br>`bit5&4: VERT_MODE`<br>`bit3: YAW_MODE`<br>`bit2&1: HORI_FRAME`<br>`bit0: YAW_FRAME`|`bit7&6: HORI_MODE`<br>`bit5&4: VERT_MODE`<br>`bit3: YAW_MODE`<br>`bit2&1: HORI_FRAME`<br>`bit0: STABLE_FLAG`|

### New Broadcast Data

|CMD Set|CMD ID|Description|
|-------|------|-----------|
|0x02|0x03|Mission Status Push Info|
|0x02|0x04|Mission Events Push Info|

### Changed Broadcast Data

|Struct Changed|2.3|3.1|
|--------------|---|---|
|Time Stamp|`uint32_t`|`typedef struct`<br>`{`<br>&nbsp;&nbsp;`uint32_t time;`<br>&nbsp;&nbsp;`uint32_t asr_ts;`<br>&nbsp;&nbsp;`uint8_t sync_flag;`<br>`}sdk_time_stamp_t;`|
|Velocity|`typedef struct`<br>`{`<br>&nbsp;&nbsp;`float32 x;`<br>&nbsp;&nbsp;`float32 y;`<br>&nbsp;&nbsp;`float z;`<br>&nbsp;&nbsp;`uint8_t health_flag:1;`<br>&nbsp;&nbsp;`uint8_t sensor_id:4;`<br>&nbsp;&nbsp;`uint8_t reserved:3;`<br>`} velocity_data_t;`|`typedef struct`<br>`{`<br>&nbsp;&nbsp;`float32 x;`<br>&nbsp;&nbsp;`float32 y;`<br>&nbsp;&nbsp;`float z;`<br>&nbsp;&nbsp;`uint8_t health_flag:1;`<br>&nbsp;&nbsp;`uint8_t reserved:7;`<br>`} velocity_data_t;`|
|Ctrl Device|`typedef struct`<br>`{`<br>&nbsp;&nbsp;`uint8_t cur_ctrl_dev_in_navi_mode: 3;`<br>&nbsp;&nbsp;`uint8_t serial_req_status: 1;`<br>&nbsp;&nbsp;`uint8_t reserved: 4;`<br>`} ctrl_device_t;`|`typedef struct`<br>`{`<br>&nbsp;&nbsp;`uint8_t cur_api_ctrl_mode;`<br>&nbsp;&nbsp;`uint8_t cur_ctrl_dev_in_navi_mode: 3;`<br>&nbsp;&nbsp;`uint8_t serial_req_status: 1;`<br>&nbsp;&nbsp;`uint8_t vrc_enable_flag: 1;`<br>&nbsp;&nbsp;`uint8_t reserved: 3;`<br>`} ctrl_device_t;`|

## Onboard SDK Library Updates

- We have cleaned up data structures, core logic, and example usage.
- This library is compatible with both 2.3 and 3.1 firmware.
- The 2.3 branch and old library are archived for reference.

## `F` Mode Updates [IMPORTANT]

**Important:** With firmware 3.1, developers are now able to obtain onboard SDK control immediately when the drone is powered on with the remote controller's mode switch in the `F` position.  Previously, with firmware 2.3, develoeprs had to toggle the mode switch out of `F` mode and then return to `F` mode in order to obtain control.

Please consider the user experience and design of your application to ensure that inadvertent SDK control of the vehicle is not allowed.
