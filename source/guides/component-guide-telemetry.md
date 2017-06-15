---
title: Telemetry
date: 2017-03-07
keywords: [telemetry, broadcast, subscription]
---

## Introduction

DJI aircraft caries telemetry system for the safety of the pilots and persons on the ground during flights. Telemetry from an on-board flight system is the primary source of real-time measurement and status information transmitted to the pilot.
DJI Onboard SDK provides API to read telemetry data in real time in subscription or broadcast fashion. 

Example of the data include:
 
* Sensor readings such as gyroscope and magnetometer
* Fusion data such as attitude and global position
* Aircraft information such as battery, gimbal, and flight status

## Broadcast

In data broadcast mechanism, the data package arrives at a pre-configured frequency. The frequency can be modified across your application via DJI Onboard API or it can be changed via DJI Assistant 2 before the flight.

#### Available Broadcast Data

Broadcast data arives in a package containing state information for components listed below: 

* **Timestamp**
* **Hardware Synchronization Timestamp**
* **Quaternion**
* **Angular Rate**
* **Velocity**
* **Gyroscope Reading**
* **Global Position**
* **Relative Position**
* **GPS**
* **RTK**
* **Magnetometer**
* **Remote Controller**
* **Gimbal**
* **Flight Status**
* **Battery**

#### Available Broadcast Frequencies 

* **0 Hz**
* **1 Hz**
* **10 Hz**
* **50 Hz**
* **100 Hz**

#### NOTE:

By allowing flexibility of setting frequencies for each Broadcast component individually, developer must implement logic for clarifying data availability. For example, if you specify GPS at 50Hz and Gyroscope at 10Hz, the whole data packet from broadcast will come in at 50Hz but Gyroscope will only come in every 5 data packages. See DJI Onboard API for details.


## Subscription

Data Subscription is a new and improved paradigm introduced in DJI Onboard SDK 3.3.  Like Broadcast, it offers real-time telemetry data transmission from the flight controller to the DJI Oonboard SDK. In addition to Broadcast, it provides more variety of status information data sets or "Topics" as well as flexible frequency configuration.

#### How It Works

You can choose a set of "Topics" or Subscription data sets, add them to a Subscription package and configure the package to arrive on prefered frequency. There are total of five packages available to a user to configure via DJI Onboard API. Each package can be set to individual frequency and has fixed-size buffer of 300-Bytes allowing user to add as many Telemetry Topics per package as desired.

#### Available Subscription Topics and Their MAX Frequencies

Each Subscription package may contain state information for components listed below:

* **Hardware Synchronization**: 400Hz
* **Quaternion**: 200Hz
* **Acceleration**: 400Hz
* **Angular Rate**: 400Hz
* **Velocity**: 200Hz
* **Barometer Altitude**: 200Hz
* **GPS**: 50 Hz
* **RTK**: 50 Hz
* **Compass**: 100 Hz 
* **Remote Controller**: 50 Hz
* **Gimbal**: 50 Hz
* **Flight Status**: 50 Hz
* **Battery**: 50 Hz
* **Display Mode**: 50 Hz
* **Landing Gear**: 50 Hz
* **Motor**: 50 Hz

#### Note: Broadcast and Subscription can be used interchangeably.
