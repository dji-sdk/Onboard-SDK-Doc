---
title: Mobile SDK sample
date: 2017-03-07
keywords: [Mobile, communication]
---

## Introduction

As mentioned in the guide, the Mobile - Onboard SDK communication was developed to combine the benefits of Mobile and Onboard SDK APIs by establishing a connection between a Mobile Device and an Onboard Computer. Developers are able to send any data from their Mobile Device to OES and vice versa.

This implementation provides an alternative way to run/test your OnboardSDK code with an aircraft in the real world. The commands are sent from the iOS app to the Onboard Computer, data is parsed in the Onboard SDK code and the respective functions are executed accordingly. For example, clicking on the 'Take Off' button on the iOS app results in the command being sent to the OES, the parser on the Onboard SDK sample reads the command and calls the 'Take Off' function accordingly. After completion of 'Take Off', the returned Flight Controller ACK is sent to the iOS app.

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
- Go to the info.plist and add an entry with "DJIAppKey" for key and the registration ID as value. 
- Hit Run and let Xcode fix any issues that show up. 
- The app can now be launched on your iOS device. 
- Below is a screenshot of the app after successful Take Off. 
![MOS app](../../images/common/MOSDKApp.jpg)

## Code work flow



## Support

### Linux 

The supported commands are: 

* Obtain Control
* Release Control  
* Arm
* Disarm 

ACK returned will be displayed on the Mobile app. 


### ROS

The supported commands are:  

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

ACK returned will be displayed on the Mobile app.


### STM32

STM32 platform responds to mobile commands by default. **When not in simulator mode, sending mobile commands will cause the motor to spin and drone to fly. Use with care!** The supported commands are: 

* Obtain Control
* Release Control
* Arm
* Disarm

ACK returned will be displayed on the Mobile app.
