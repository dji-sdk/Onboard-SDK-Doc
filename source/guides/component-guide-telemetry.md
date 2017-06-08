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

### Available Broadcast Data

Broadcast data arives in a package containing state information for components listed below: 

* **Timestamp**
* **Hardware Synchronization Timestamp**
* **Quaternion**
* **Angular Rate**
* **Velocity**
* **Gyroscope Reading**
* **Velocity Information**
* **Global Position**
* **Relative Position**
* **GPS Information**
* **RTK**
* **Magnetometer**
* **Remote Controller**
* **Gimbal**
* **Flight Status**
* **Battery**

### Available Broadcast Frequencies 

* **0 Hz**
* **1 Hz**
* **10 Hz**
* **50 Hz**
* **100 Hz**
* **200 Hz**
* **400 Hz**

### NOTE:

By allowing flexibility of setting frequencies for each Broadcast component individually, developer must implement logic for clarifying data availability. For example, if you specify GPS at 50Hz and Gyroscope at 10Hz, the whole data packet from broadcast will come in at 50Hz but Gyroscope will only come in every 5 data packages. See DJI Onboard API for details.


## Subscription

Data subscription is a new and improved paradigm, introduced in Onboard SDK 3.3, to retrieve telemetry data from the flight controller. User subscribes to telemetry data as data packets by specifying a frequency and a list of telemetry topics. Below are some advantages of using subscription over broadcast:
* A more robust hand-shake mechanism
* Additional telemetry data available
* Supports higher frequency
* Supports hardware sync feature
