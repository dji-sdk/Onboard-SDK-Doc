---
title: DJI Onboard SDK ROS Demo Client Package
version: v3.1.7
date: 2016-07-01
github: https://github.com/dji-sdk/Onboard-SDK-ROS/tree/3.1/dji_sdk_demo
keywords: [ros demo client package]
---

This package is a demonstration of how to use dji_sdk core package and its `dji_drone.h` class as a custom client. 

Main Components:
  
  * dji_sdk_lib: implementation of Onboard SDK protocol
  * dji_sdk: core package that is a group of packed APIs from dji_sdk_lib. All received data from the drone are published into ROS topics and all command sending APIs have become ROS services

## How to use

  * Install and configure your hardware components
  * If your aircraft is not activated, go back to our activation guide and continue after your device is activated
  * Compile dji_sdk and sdj_sdk_demo packages
  * To start communication between your Onboard Embedded System and the aircraft, first launch the core node ``roslaunch dji_sdk sdk_manifold.launch`` and in separate terminal launch the client ``rosrun dji_sdk_demo dji_sdk_client``. Send controll commands from the client to the core node and monitor the result in the core node terminal or use Simulator as part of the Assistant software to monitor aircraft movements.
