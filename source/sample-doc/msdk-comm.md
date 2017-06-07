---
title: Mobile SDK sample
date: 2017-03-07
keywords: [Mobile, communication]
---


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
