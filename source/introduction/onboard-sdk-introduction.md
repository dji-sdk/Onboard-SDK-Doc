---
title: Onboard SDK Introduction
date: 2017-06-01
version: 3.3
keywords: [get started, key features, hardware overview, registration, enable flight controller API control, safety]
---

The DJI Onboard SDK is an open source communication software library designed to provide developers access to the capabilities of DJI's aircraft, handled camera and sensor products. The software library provides low level control communication between aircraft and computer companion platform (of your choice) mounted directly on aircraft's chasis. This communication allows for onborad, real time processing and can be used to program your aircraft to perform complex missions and tasks.

While designing this software library, we created distinct list of features developer can implement. At the same time,  to maintain simple to use and understand SDK, we hide complex, low level components like flight stabilization, battery management, rotor configuration, etc. These components managed by the flight controller itself.

The SDK includes:

* **Communication library**: Supports Linux, ARM, STM32.
* **Aircraft simulator and visualization tool**: Used for initial (User App) activation, aircraft configuration and flight tests.
* **Sample code and developer guides**: Check out our sample code demonstrating core workflow of flight control, camera and gimbal control, telemetry, missions, and mobile communication. 
* **API documentation**: Detailed reference to Onboard SDK API.

## Feature Overview

Many of DJI's product features and capabilities are accessible to developers through the SDK. Developers can automate flight and missions, control the camera and gimbal, receive real time video and sensor data, download saved media from the product, receive real-time feedback, and even more. Our SDK designed for you to invent and experiment. We offer a number of modules that integrate with core SDK to provide for precision missions, trajectories, collision avoidance and LiDAR mapping <link here>.

##### Flight Control

The DJI Onboard SDK allows variety of powerful, high-frequency (up to 200 Hz) control modes and missions to control flight:

* **Attitude Control**
* **Velocity Control**
* **Position Control**
* **Missions**

##### Camera and Gimbal Control

Handled DJI camera and gimbal can be programmed to take following actions:

* **Take Picture**: in-motion and still image capture.
* **Take Video**: in-motion and still video capture.
* **Gimbal Position Control**: in-motion and still position control.
* **Gimbal Velocitry Control**: in-motion and still velocity control.

##### Hardware Synchronization Control

TODO ...

##### MFIO Control

TODO ...

##### Aircraft Telemetry

Rich sensor data and aircraft state is available through the SDK in real-time (up to 200 Hz):

Inertial Sensor Data

* **GPS**<br> 
* **RTK**<br>
* **Compass**<br>
* **Barometer**<br>

Aircraft Status Data

* **Flight Velocity**<br>
* **Flight Altitude**<br>
* **Gimbal Status**<br>
* **Battery Status**<br>
* **Qaternion**<br>
* **Acceleration**<br>
* **Palstance**<br>

##### Mobile Communication

While your aircraft can be completely programmed, we also support mobile communication control. It is bidirectional data link between your OES (Onboard Embedded System) and a mobile device developed in conjunction with DJI's Mobile SDK. This link can be established by using the Matrix 100 or Matrix 600 built-in lightbridge communication system or by using a <a href="http://www.dji.com/product/lightbridge-2" target="_blank">Lightbridge 2</a> with the A3/N3.


We provide C++ source APIs to make sending and receiving data over the serial port easy and encourage you to use them in your applications.

