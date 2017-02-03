---
title: Release Notes for Onboard SDK 3.2.0
version: 3.2.1
date: 2017-02-02
keywords: [Precision Missions, Mission Planning, Velodyne Puck Lite LiDAR, Collision Avoidance, LiDAR, 3.2, Mapping, Point Clouds]
---

## OSDK 3.2.1 Highlights

This hotfix release is targeted at simplifying versioning for the OSDK.

* A new automated versioning system means that users no longer have to provide their firmware versions for activation
* Future proofing for newer FC firmware - the SDK will not require hotfixes to work with newer firmware
* Developers can now have features targeting specific hardware or firmware: The `versionData` struct has three new members to help with identifying the Hw/Fw/ID of your system:

| Member                    | Data Type                             | Range of values                             | Comments                                                                                                                                                                                                                                               |
|---------------------------|---------------------------------------|---------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `hwVersion`     | NULL-terminated char array of size 12 | "M100", "A3", "N3", "pm820v3", "pm820v3pro" | Hardware type (pm820v3 is an M600)                                                                                                                                                                                                                     |
| `swVersion`     | uint32                                | > 0x02030A00                                | Flight control firmware version (starts from 2.3.10.0 for M100, represented here in hex, and linearly increasing as newer FW are introduced. For reference, the A3/N3 FW package 1.7.0.0 is flight control FW 3.2.15.37, represented as 0x03020F25).   |
| `hw_serial_num` | NULL-terminated char array of size 16 | -                                           | The unique serial number of your hardware. You can also see this number in DJI Go in the About menu.                                                                                                                                                   |

New getter functions `getHwVersion()`, `getFwVersion()` and `getHwSerialNum` replace `getSDKVersion()`. The `setVersion()` call has been removed.
Take a look at the Linux sample to see how version checks by hardware and firmware could be used in your programs.

---
## OSDK 3.2.0 Highlights

The 3.2.0 major release for Onboard SDK advances the state of the art in drone SDKs with advanced features first unveiled at [DJI Airworks](www.dji.com/newsroom/news/dji-enterprise-launches-airworks-conference), such as LiDAR Collision Avoidance, LiDAR Mapping, and improved Precision Missions available for DJI developers as plug-and-play modules. 

* [LiDAR Collision Avoidance](../modules/collision-avoidance/collision-avoidance.html) [beta] - Get 360&deg; awareness and safety in manual flight and in precision missions with static and dynamic obstacle avoidance
* [LiDAR Mapping](../modules/lidarmapping/lidar-mapping.html) [beta] - Simply flick a switch to start building fully registered, relative scan-matched 3D maps with up to 3cm relative accuracy. Compatible with manual flight and with precision missions
* [Precision Missions](../modules/missionplan/README.html) - Fly complex flight paths with incredible accuracy with new gain tunings and improvements across the board to the precision missions suite. Now with support for A3-based custom aircraft, and integrations for mapping and collision avoidance
* Updated [MOS](../github-platform-docs/MobileOnboardSDK/Mobile-OSDK.html) iOS app - New switches and buttons make it easier than ever to execute these advanced features in the field
* Updated [Linux](../github-platform-docs/Linux/README.html) and [ROS](../github-platform-docs/ROS/README.html) sample apps - call new features in interactive, mobile or programmatic APIs with the updated Linux and ROS samples. Building any of the new modules is as simple as passing a parameter at compile time for the Linux and ROS samples.
* Updated Core API with improved thread safety, new API calls for waypoint missions and new tests for gimbal and camera.

As always, head over to [Github](https://github.com/dji-sdk/Onboard-SDK) (or [ROS github](https://github.com/dji-sdk/Onboard-SDK-ROS)) for the latest release!

Developers are also encouraged to view the [EULA](http://developer.dji.com/policies/eula/) for closed-source binaries provided as part of the Onboard SDK.

---

###### Notes for using Onboard SDK with the new A3 v1.5.0.0 FW

**Note: These notes also apply to N3 Flight controllers.**
* Starting with this firmware, A3 units will respond differently to flight mode switch positions. The default switch positions of (P,A,F) have been replaced by (P,S,A) respectively.  
* Previously, Onboard SDK was available in F mode - this FW onwards, the Onboard SDK is available in P mode.
* If you desire a manual override (a switch position that disables the Onboard SDK), you can go to DJI Assistant 2 ->Basic Settings -> Remote Controller Settings and check the box that says Multiple Flight Modes.
* With Multiple Flight Modes enabled, the SDK will not work in S and A mode switch positions. You may use the S mode switch position for manual override.
* With Multiple Flight Modes disabled, the SDK **will work in all mode switch positions**. This is because without Multiple Flight Modes enabled, all mode switch positions map to mode P.