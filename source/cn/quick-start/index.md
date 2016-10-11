---
title: Get Started 
date: 2016-07-01
keywords: [get started, key features, hardware overview, registration, enable flight controller API control, safety]
---

## Getting Started with the Onboard SDK

DJI's onboard SDK allows you to connect your own Onboard Embedded System (OES) to a supported DJI vehicle (<a href="http://www.dji.com/product/matrice100" target="_blank">Matrice 100</a> or <a href="http://www.dji.com/product/matrice600" target="_blank">Matrice 600</a>) or flight controller (<a href="http://www.dji.com/product/a3" target="_blank">A3</a>) using a common serial port (TTL UART). This setup opens up an exciting opportunity to integrate your own hardware with DJI's flying platforms.  New applications and commercial uses for aerial robotics awaits and we can't wait to see what you build, so lets get started!

### Prerequisites

This SDK is for developers with:

- programming experience in C and C++
- embedded systems knowledge
- a DJI <a href="http://www.dji.com/product/matrice100" target="_blank">Matrice 100</a> vehicle, a DJI <a href="http://www.dji.com/product/matrice600" target="_blank">Matrice 600</a> vehicle, or DJI <a href="http://www.dji.com/product/a3" target="_blank">A3</a> flight controller integrated into your own vehicle
- your own Onboard Embedded System (OES) with an available com port (TTL UART)
- Windows PC to run the required software tools
- an iOS or Android mobile device to run DJI Go

## Key Features

The onboard SDK enables deep interaction between your OES and a DJI flight controller.  Using the APIs you can, for example, use a sensor connected to your embedded system to control the trajectory of the vehicle, collect telemetry data in real-time, trigger a camera to take photos, or send data through the vehicle's downlink to a mobile device. Your OES must have a TTL UART port available for the onboard SDK to use.

### Flight Control

  - A variety of control modes are available including real-time attitude control, velocity control, position control, and complete waypoint mission planning. 
  
### Vehicle Telemetry

  - A robust set of vehicle state information is available in real-time including inertial sensors, attitude, heading, velocity, position, battery info, and vehicle status.
  
### Data Transmission

  - A bidirectional data link between your embedded device and a mobile device (in conjunction with DJI's mobile SDK) can be established by using the M100 or M600 built-in lightbridge communication system or by using a <a href="http://www.dji.com/product/lightbridge-2" target="_blank">Lightbridge 2</a> with the A3.

### Camera and Gimbal Control

 - A supported DJI camera and gimbal can be controlled with commands to take pictures, videos, and adjust gimbal position.

We provide C/C++ source APIs to make sending and receiving data over the serial port easy and encourage you to use them in your applications.  Alternatively, developers can use our protocol specification to write their own communication drivers.

## Hardware Overview
- If you are using an M100 or M600 vehicle, you should assemble and familiarize yourself with flying the vehicle before attempting to proceed with onboard SDK development.
- If you are using an A3 flight controller with Lightbridge 2 and your own vehicle, then you should familiarize yourself with flying your vehicle before attempting to proceed with onboard SDK development.
- Generically, you will be working with one of the setups in the following diagram:
![Hardware Setup](../../images/common/GenericHWSetup.png)

> Note that to accomplish the setup steps below, you will need to use the vehicle remote controller connected to a mobile device running the DJI Go app and your mobile device must have a connection to the internet.


## Setup

### 1. Download the SDK and Required Tools

- <a href="https://github.com/dji-sdk/Onboard-SDK" target="_blank">Download</a> the onboard SDK repository from Github
- <a href="https://www.dji.com/product/matrice600/info#downloads" target="_blank">Download</a> the DJI PC Assistant 2 software for Windows
- <a href="http://www.dji.com/product/goapp" target="_blank">Download</a> the DJI GO APP to your mobile device
     
### 2. Update Firmware

- Connect your computer to the Micro-USB port on the M100/600 or A3
- Update your <a href="http://www.dji.com/product/matrice100/info#downloads" target="_blank">M100</a>, <a href="http://www.dji.com/product/matrice600/info#downloads" target="_blank">M600</a> or <a href="http://www.dji.com/product/a3/info#downloads" target="_blank">A3</a> with the latest released firmware

### 3. Enable Flight Controller API control

- With your M100/M600 or A3 connected to your computer, launch DJI PC Assistant 2 and check the box "Enable API Control”.

![Enable API Control](../../images/common/N1UI.png)

### 4. Connect Your Onboard Embedded System (OES)

- If you are using one of our supported platforms, we provide detailed instructions in our [Hardware Setup Guide](../hardware-setup/index.html).

- The [Hardware Setup Guide](../hardware-setup/index.html) also lists the pin diagram for the [M100 UART connector](../hardware-setup/index.html#M100-UART-Connector) and the [A3 UART connector](../hardware-setup/index.html#A3-UART-Connector) so that you may build your own cable compatible with your OES.

- A3 flight controller can be accessed on the M600 by pulling off the top-cover. 

- You can power your embedded system from your own battery or if you are using an M100/600, you can pull power from the vehicle bus. See your M100 or M600 manual for details.

- Secure your embedded system to the vehicle near the center of mass. Ensure that the total vehicle weight is within the maximum takeoff weight specificed for your vehicle.

   
### 5. Onboard Application Registration

- You must register as a developer with DJI and create an onboard SDK application ID and Key pair. Please go to <a href="https://developer.dji.com/register/" target="_blank">https://developer.dji.com/register/</a> to complete registration. 

### 6. Set up your Software Environment

Choose one of these examples to begin using the onboard SDK in a particular software environment:

- [QT GUI Environment in Windows and Linux Example](../github-platform-docs/PureQT/README.html)

- [Command Line Environment in Windows and Linux Example](../github-platform-docs/commandline/README.html)

- [ROS on Linux Example](../github-platform-docs/ROS/README.html)

- [STM32 ARM Example](../github-platform-docs/STM32/README.html)

### 7. Flight Platform Activation

- You should have completed activation using one of the examples above.
- After successful activation, you are ready to start developing! 

> Note: Each new vehicle or flight controller to be used must be activated once to enable communication with your application.

## Safety

Please comply with local regulations during the development of your application. Please refer to <a href="http://flysafe.dji.com/" target="_blank">http://flysafe.dji.com/</a> for more information.

## Next Steps

Now that you are setup and communicating with a DJI flight control system, we would encourage you to explore our platform guides and reference documentation to help jumpstart your development. We would recommend reading our [Architecture Guide](../introduction/architecture-guide.html) next. The revamped [Programming Guide](../application-development-guides/programming-guide) is a good place to visit once you have some familiarity with the examples and want to know more about the internals.


Also, take a look at our [FAQ](../appendix/FAQ.html) for some answers to common questions. After that, feel free to contact us with any issues.

### Reference Documents

- [Release Notes for Onboard SDK 3.1.8](../appendix/releaseNotes.html)
     >Note: v3.1.8 of the Onboard SDK was released on 08/05/16 and introduces many great new features.  Check it out!

- [OPEN Protocol](../introduction/index.html) & [Appendix](../appendix/index.html) 

- [Data Transparent Transmission](../introduction/data-transparent-transmission.html)  

- [Programming Guide](../application-development-guides/programming-guide.html)

- [Ground Station Protocol](../introduction/ground-station-protocol.html)

- [Virtual RC](../introduction/virtual-rc-protocol.html)
 
- [Ground Station Programming Guide](../application-development-guides/ground-station-programming-guide.html)

- [FAQ](../appendix/FAQ.html)
