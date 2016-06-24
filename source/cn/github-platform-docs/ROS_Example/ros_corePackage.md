---
title: DJI Onboard SDK ROS Core Package 
date: 2016-06-24
---

This package is a ROS core package. It is a group of packed APIs from dji_sdk_lib that is our Onboard SDK protocol implementation. All received data from the drone are published into ROS topics and all command sending APIs have become ROS services.

## How to use

  * Install and configure your hardware components
  * If your aircraft is not activated, go back to our activation guide and continue after your device is activated
  * To start communication between your Onboard Embedded System and the aircraft, launch the core node ``roslaunch dji_sdk sdk_manifold.launch``
