---
title: Announcement 
date: 2020-05-08
keywords: [OSDK]
---
## OSDK 4.0 Released

#### What's new
* <a href="../tutorial/SDK-mop.html"><b>SDK Interconnection</b></a>
  * MSDK、OSDK、PSDK communication seamlessly
  * Support M300 RTK 
  * Massive data communication
* <a href="../tutorial/gimbal-manager.html"><b>Multiple gimbal control</b></a>
* <a href="../tutorial/advanced-sensing.html"><b>Obtain camera’s H264 Stream</b></a>
* Camera's media fIles downloading
* Get gray scale images and camera internal/external parameters (only support Matrice 300 RTK)
* Obstacle Avoidance enable/disable switches (only support Matrice 300 RTK)

#### Upgrade
* Waypoints 2.0（Only support Matrice 300 RTK） 
  * large-scale waypoints (65535)
  * flexible actions configuration

#### Bug Fixes
* Gimbal Control Bug: Fix the failure of gimbal control in Matrice 210 V2 Series while flying.
* Obstacle Avoidance Bug: Fix the failure of obstacle avoidance switches in Matrice 210 V2 Serial while using speed control.

#### Platform Supports
* STM32 Platform: Rebuild STM32 platform sample and apply RTOS porting.
* Qt: End up support.

> **NOTE** This series of documentation introduces the functions of **OSDK V4.0.0**, as well as the steps and methods of developing software using OSDK V4.0.0. If you are still using OSDK V3.9.x, please download the documentation of [OSDK V3.9.x](https://terra-1-g.djicdn.com/71a7d383e71a4fb8887a310eb746b47f/osdk/OSDK-3.9.0.zip).

## <a href="https://terra-1-g.djicdn.com/71a7d383e71a4fb8887a310eb746b47f/general/DJI_Media_File_Metadata_WhitePaper.zip">DJI Media File Metadata WhitePaper</a> Released
DJI camera's Metadata White Paper set describe organization and technical standard of metadata stored in media formats, as well as guidelines in acquiring metadata in DJI products. It is provided to users for analyzing modeling or other post-workflow, which is essential for pro users and developers to do in-depth post-work.