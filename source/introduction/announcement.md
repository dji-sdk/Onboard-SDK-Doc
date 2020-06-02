---
title: Announcement 
date: 2020-05-08
keywords: [OSDK]
---
## OSDK Beta Firmware Application
Onboard SDK 4.0.0 have been released. If developers need to develop the Application on Matrice 200 V2 series, please use the latest firmware, but the firmware are still in the testing, so developers could apply the testing permission from <a href="mailto:dev@dji.com" target="_blank" rel="external"> DJI SDK Team </a> and obtain the testing firmware.

> **NOTE**
> * When applying for the firmware, please provide the account which logging in the DJI Assistant 2.
> * Please use the test firmware in the safe area. Damage caused by using the test firmware is not covered by the warranty.

## OSDK 4.0 Released
* Add Support [Matrice 300 RTK](https://www.dji.com/matrice-300)
   * Get grayscale images and camera internal/external parameters 
   * Obstacle Avoidance enable/disable switches
* Add <a href="../tutorial/SDK-mop.html"><b>SDK Interconnection</b></a>
   * MSDK、OSDK、PSDK communication seamlessly
   * Massive data communication
* Add <a href="../tutorial/gimbal-manager.html"><b> GimbalManagement</b></a>
* Add <a href="../tutorial/advanced-sensing.html"><b>Obtain camera’s H264 Stream</b></a>
* Add Camera's Media FIles Downloading
* Upgrade Waypoints 2.0（Only support [Matrice 300 RTK](https://www.dji.com/cn/matrice-300)） 
  * large-scale waypoints (65535)
  * flexible actions configuration
* Fix the failure of gimbal control in Matrice 210 V2 Series while flying.
* Fix the failure of obstacle avoidance switches in Matrice 210 V2 Serial while using speed control.

#### Platform Supports
* STM32 Platform: Rebuild the STM32 platform’s sample also support porting to RTOS
* Qt: End up support

> **NOTE** If you still using OSDK V3.9.x, please download the documentation of [OSDK V3.9.x](https://terra-1-g.djicdn.com/71a7d383e71a4fb8887a310eb746b47f/osdk/OSDK-3.9.0.zip).

## <a href="https://terra-1-g.djicdn.com/71a7d383e71a4fb8887a310eb746b47f/general/DJI_Media_File_Metadata_WhitePaper.zip">DJI Media File Metadata WhitePaper</a> Released
DJI Media File Metadata White Paper set to describe the organization and technical standard of metadata stored in media formats, as well as guidelines in acquiring metadata in DJI products. It is provided to users for analyzing modeling or other post-workflow, which is essential for pro users and developers to do in-depth post-work.