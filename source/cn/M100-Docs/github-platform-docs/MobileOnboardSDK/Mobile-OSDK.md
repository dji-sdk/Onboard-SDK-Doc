---
title: Mobile Onboard SDK communication using Data Transparent Transmission
version: 3.2.0
date: 2016-12-23
keywords: [iOS Mobile Onboard SDK app]
---

> New for 3.2.0: Advanced Features Tab with support for LiDAR Mapping, LiDAR Collision Avoidance and Precision Missions!
## Introduction

The Mobile Onboard SDK communication uses the Data Transparent Transmission protocol. As mentioned in the [Data Transparent Transmission](../../application-development-guides/data-transparent-transmission.html) section, the Data Transparent Transmission was developed to combine the benefits of Mobile and Onboard SDK APIs by establishing a connection between a Mobile Device and an OES. Via the Data Transparent Transmission, developers are able to send any data from their Mobile Device to OES and vice versa. 

This implementation provides an alternative way to run/test your OnboardSDK code with an aircraft in the real world. The commands are sent from the iOS app to the OES, data is parsed in the Onboard SDK code and the respective functions are executed accordingly. For example, clicking on the 'Take Off' button on the iOS app results in the command being sent to the OES, the parser on the Onboard SDK sample reads the command and calls the 'Take Off' function accordingly. After completion of 'Take Off', the returned Flight Controller ACK is sent to the iOS app (Returned ACK is only supported in Linux example for this release). 

Basic architecture of the Mobile Onboard SDK communication is shown. The image below shows commands being sent from Mobile to Onboard SDK.  

![MOS Mobile to OES](../../images/common/MOSDK_A3N3_1.png)

The image below shows the ACK being returned to mobile. 

![MOS ACK return](../../images/common/MOSDK_A3N3_2.png)


## Setup
# iOS Mobile Onboard SDK app 

The iOS app can be side loaded to your phone using Xcode on a Macintosh system. Below are the list of instructions to side load the MOS app to your iOS device. 

- Create Mobile app on the DJI developer website. You will need the Bundle ID and Key to be entered in the Xcode project. An example Bundle ID is shown in the below image. 
![MOS app](../../images/common/createApp.png)
- Login using your Apple ID and download Xcode from the App store. 
- Launch Xcode and setup your Apple ID in the Preferences - Account section. 
- Download source for iOS app from [here](https://github.com/dji-sdk/Mobile-OSDK-iOS-App)
- Launch the MOS.xcodeproj 
- Click on the 'MOS' project on Xcode to view the General settings. 
- In the General settings change bundle ID to the one registered on the DJI developer portal. In the below image, the same example Bundle ID is being used. 
![MOS app](../../images/common/bundleID.png)
- Go to the MOSProductCommunicationManager.m and enter registration ID from the DJI developer portal. 
- Hit Run and let Xcode fix any issues that show up. 
- The app can now be launched on your iOS device. 
- Below is a screenshot of the app after successful Take Off. 
![MOS app](../../images/common/MOSDKApp.jpg)


## Operation

### Linux

You can enable mobile command input by running `./djiosdk-linux-sample -mobile` (and optionally another argument `path_to_trajectory_json` if you want to execute a pre-planned precision spiral). 

The supported commands are: 

* Obtain Control
* Release Control 
* Take Off 
* Landing 
* Arm
* Disarm 
* Go Home
* Gimbal Control Demo
* Draw Square Demo 
* Waypoint Mission Demo
* Precision Trajectory Execution

Linux supports ACK returned from the Flight Controller. ACK returned will be displayed on the Mobile app. 


### ROS

You can enable mobile command input by choosing number 37 on the list. This will allow you to send commands from the Mobile device. The supported commands are: 

* Obtain Control
* Release Control 
* Take Off 
* Landing 
* Get SDK Version
* Arm
* Disarm 
* Go Home
* Take Photo 
* Start Video
* Stop Video 
* Draw Circle Demo 
* Draw Square Demo 
* Gimbal Control Demo 
* Attitude Control Demo 
* Virtual RC Test 

ROS does not supports ACK returned from the Flight Controller. This will be supported in a future release. 


### STM32

STM32 platform responds to mobile commands by default. **When not in simulator mode, sending mobile commands will cause the motor to spin and drone to fly. Use with care!** The supported commands are: 

* Obtain Control
* Release Control
* Activation
* Take Off
* Landing
* Arm
* Disarm
* Go Home
* Local Navigation Test

STM32 supports ACK returned from the Flight Controller. ACK returned will be displayed on the Mobile app. 
