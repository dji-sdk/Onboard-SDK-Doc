---
title: Announcement 
date: 2020-05-08
keywords: [OSDK]
---
## OSDK 4.0 Released
#### Hightlights
* SDK Interconnection: Add MSDK/OSDK/PSDK interconnection feature to satisfy the needs of massive data communication.
* Waypoints 2.0: Add Waypionts 2.0 basic feature to satisfy the needs of large-scale waypoints and flexible actions configuration (only supported by Matrice 300 RTK).
* Camera Media FIles Downloading: Add camera photo and video files downloading feature. 
* Camera H264 Stream: Add camera H264 stream acquisition API.

#### Other New Features
* Perception Data: Add APIs for getting gray scale images and camera internal/external parameters (only supported by Matrice 300 RTK).
* Obstacle Avoidance Switches: Add APIs for Obstacle Avoidance enable/disable switches (only supported by Matrice 300 RTK).
* Gimbal Function: Add GimbalManager Class to support multiple gimbal control.

#### Supported Products（Firmware）
* Matrice 300 RTK : v01.00.01.07
* Matrice 210 RTK V2 : v01.00.0670
* Matrice 210 V2 : v01.00.0670

#### Bug Fixes
* Gimbal Control Bug: Fix the failure of gimbal control in Matrice 210 V2 Series while flying.
* Obstacle Avoidance Bug: Fix the failure of obstacle avoidance switches in Matrice 210 V2 Serial while using speed control.

#### Platform Supports
* STM32 Platform: Rebuild STM32 platform sample and apply RTOS porting.
* Qt: End up support.

> **NOTE** This series of documentation introduces the functions of **OSDK V4.0.0**, as well as the steps and methods of developing software using OSDK V4.0.0. If you are still using OSDK V3.9.x, please download the documentation of [OSDK V3.9.x](https://terra-1-g.djicdn.com/71a7d383e71a4fb8887a310eb746b47f/osdk/OSDK-3.9.0.zip).

## <a href="https://terra-1-g.djicdn.com/71a7d383e71a4fb8887a310eb746b47f/general/DJI_Media_File_Metadata_WhitePaper.zip">DJI Media File Metadata WhitePaper</a> Released
DJI camera's Metadata White Paper set describe organization and technical standard of metadata stored in media formats, as well as guidelines in acquiring metadata in DJI products. It is provided to users for analyzing modeling or other post-workflow, which is essential for pro users and developers to do in-depth post-work.