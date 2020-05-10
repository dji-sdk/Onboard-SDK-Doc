---
title: OSDK Feature List
date: 2020-05-08
version: 4.0.0
keywords: [OSDK, feature overview]
---
> **NOTE** This article is **Machine-Translated**. If you have any questions about this article, please send an <a href="mailto:dev@dji.com">E-mail </a>to DJI, we will correct it in time. DJI appreciates your support and attention.     

It is convenience for developers to use the latest version of the OSDK, use that could help you to use the new features to develop the program, please pay attention to the release information of the DJI OSDK.

> **NOTE**
> * This article is **Machine-Translated**. If you have any questions about this article, please send an <a href="mailto:dev@dji.com">E-mail </a>to DJI, we will correct it in time. DJI appreciates your support and attention.
> * The Mobile APP is DJI Pilot or a Mobile APP developed by MSDK.
> * The Payload is a device developed by PSDK.
> * The onboard computer is a computing device, such as Manifold, running the program based on OSDK.

## Control Functions
#### Time Synchronization
* Obtain NMEA data: Obtain the data of the positioning system used by the drone, such as GPS, Galileo, Beidou and GLONASS, etc.
* Get PPS data: get the hardware trigger pulse signal of the drone
* Obtain UTC time: Obtain uniform UTC time

#### Basic Control
* Set or obtain parameters of drone's flight controller, such as return altitude, obstacle avoidance status, etc.
* Perform basic flight tasks, such as take-off, landing and return
* Basic drone control functions, such as speed control, attitude control and position control

#### Motion Planning
* Waypoint Mission: control the DJI drone to achieve autonomous flight according to preset multiple waypoints
* Hotspot Mission: control the drone to fly around the set points of interest

## Management Functions
#### Message Management
* Broadcast: The application developed by OSDK can receive the data actively pushed by the drone to other modules, and at the same time broadcast the data of the third-party sensor to the third-party information receiving device
* Message subscription: applications developed using OSDK can record the data that users need to subscribe

#### Gimbal Management
* Gimbal control: control the rotation angle and angular velocity of the gimbal
* Information acquisition: Obtain the current angle and angular velocity of the gimbal

#### Camera Management
* Parameter setting: set the camera parameters such as aperture, exposure time and resolution
* Camera control: control the camera to realize functions such as taking pictures, recording videos and pointing zoom
* Stream acquisition: Obtain the RGB stream and H.264 stream of the camera


## Expanding Functions

#### SDK Interconnection
* Communicate with mobile APP developed based on MSDK
* Communicate with load equipment developed based on PSDK

#### Advanced Vision
* Object recognition
* Get perceptual grayscale image

> **NOTE** The OSDK functions supported by different operating systems and development platforms are different. For details, please refer to [Development Platform](../purchaseguide/development-platform.html)
