---
title: Get Started
date: 2017-06-01
version: 3.3
keywords: [get started, key features, hardware overview, registration, enable flight controller API control, safety]
---


## Key Features

The Onboard SDK enables deep interaction between your OES and a DJI vehicle/flight controller.  Using the APIs you can, for example, use a sensor connected to your embedded system to control the trajectory of the vehicle, collect telemetry data in real-time, trigger a camera to take photos, or send data through the vehicle's downlink to a mobile device. Your OES must have a TTL UART port available for the OSDK to use.

##### Flight Control

  - A variety of powerful, high-frequency (up to 200 Hz) control modes are available including attitude control, velocity control, position control, and complete waypoint mission planning.

##### Vehicle Telemetry

  - A robust set of vehicle state information is available in real-time (up to 200 Hz) including inertial sensors, attitude, heading, velocity, position, battery info, and vehicle status.

##### Data Transmission

  - A bidirectional data link between your OES and a mobile device (in conjunction with DJI's mobile SDK) can be established by using the M100 or M600 built-in lightbridge communication system or by using a <a href="http://www.dji.com/product/lightbridge-2" target="_blank">Lightbridge 2</a> with the A3/N3.

##### Camera and Gimbal Control

 - A supported DJI camera and gimbal can be controlled with commands to take pictures, videos, and adjust gimbal position and velocity.


We provide C++ source APIs to make sending and receiving data over the serial port easy and encourage you to use them in your applications.