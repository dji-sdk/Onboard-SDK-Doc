---
title: Safety
date: 2020-05-08
version: 4.0.0
keywords: [OSDK, Safety]
---
> **NOTE** This article is **Machine-Translated**. If you have any questions about this article, please send an <a href="mailto:dev@dji.com">E-mail </a>to DJI, we will correct it in time. DJI appreciates your support and attention.     

Before using the sample provided by DJI OSDK or using applications developed based on OSDK, please read the content in this document carefully to avoid damaging the drone or causing unnecessary safety problems due to illegal operations.

## Disclaimer
* Before using the application developed by OSDK, please check the laws and regulations of the region where the flight is located, **The safety issues or legal disputes caused by the use of OSDK are not related to DJI, and DJI will not be responsible for all the consequences of using OSDK Any legal risks and liabilities**.
* Before using flight mission, please simulate the application developed with DJI OSDK in DJI Assistant 2.
* When using the application developed by OSDK to perform tasks, please follow the User's manual to ensure that the drone is in a well state when performing the task.
* **DJI will not obtain private data of third-party users in any way and for any reason.** Developers should use DJI OSDK's advanced visual function interface to develop applications with object recognition and other functions, and should develop **functions to protect user privacy data, such as data encryption and obfuscation**, where no one uses DJI DJI will not be held responsible for any incidents involving user privacy data leakage.

## Development and Testing
When using OSDK to develop applications, to protect developers from accidents, please note the following:
* When using OSDK to develop applications or test applications developed based on OSDK, please remove the blades on the drone;
* When the drone's motor is rotating, please do not get close;
* Do not input high-power current to the power output interface of the drone;
> **NOTE** When connecting the drone to user’s computer using USB, the drone will enter the security protection mode. In this mode, the user cannot use the remote control or OSDK to control the drone to unlock or start the Motor.

## Inspection
In order to prevent the application of sudden failures, emergencies, and illegal operations from damaging the drone or generating security incidents, before executing the application, **please check the following configuration information**:
* **Check The Key Configuration**
      1. Please set the **baud rate and port name** of the program in the onboard computer or the third-party onboard computer correctly;
      2. Please set the **APP ID** and **APP KEY** for Application activation.
* **Check Device Status**
      1. Make sure that the battery power of the drone and remote control exceeds 50%;
      2. Make sure that the baud rate of DJI Assistant 2, the application and the terminal tool are the same.
   > **NOTE** To change the baud rate, please restart the flight platform, remote control and computing platform.
* **Check Device Connection**
      1. Please follow the steps and requirements in [Device Connection](./device-connection.html) to connect the onboard computer or third-party onboard computer to the drone or multi-rotor flight control system;
      2. The drone remote control is turned on (you need to open the remote control software to ensure that the software can access the Internet), the remote control **must** be connected to the drone.
      3. When activating the application for the first time or changing the information in the application, such as the APP ID and APP KEY, please connect to DJI Assistant 2 and activate the application when connected to the network.

## Flight Environment
* Do not use DJI's drones and applications developed using OSDK in extreme weather conditions such as high winds, rain, and snow.
* Do not use the drone in a dense floor and crowded environment.
* Please do not fly in areas with high voltage lines, communication base stations or transmission towers to avoid the interference of the remote control with wireless signals.
* Affected by environmental factors, the performance of the drone will be affected when the drone is flying at high altitudes. Please fly with caution.