---
title: Telemetry
date: 2017-03-07
keywords: [telemetry, broadcast, subscription]
---

## Introduction

DJI Onboard SDK provides telemetry data to aid the development of users' applications. These data can be obtained via subscription or broadcast fashion. Example of the data include: 
* Sensor readings such as gyroscope and magnetometer
* Fusion data such as attitude and global position
* Aircraft information such as battery, gimbal, and flight status


## Broadcast

In data broadcast mechanism, the flight controller publishes the telemetry data at a fix frequency. The telemetry data will be updated according to the configured frequencies, which can be set via APIs or DJI Assistant 2. 

## Subscription

Data subscription is a new and improved paradigm to retrieve telemetry data from the flight controller introduced in Onboard SDK 3.3. User subscribes to telemetry data as data packets by providing a specified frequency and a list of telemetry topics. Below are some advantages of using subscription over broadcast:
* A more robust hand-shake mechanism
* Additional telemetry data available
* Supports higher frequency
* Supports Hardware sync feature
