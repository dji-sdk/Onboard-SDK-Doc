---
title: Camera Manager samples
date: 2019-09-24
version: 3.9
keywords: [sample, camera, gimbal, photo, video, tracking, stabilize]
---

## Concept
DJI cameras have many functions and parameters available on the mobile APP for users to operate,
such as taking photos/videos,setting the camera's ISO/aperture/shutter/exposure values, etc.

We have also provided a series of interfaces since OSDK 3.9 to meet user requirements for
these functions and parameters, and wrapped these interfaces within the class `CameraManager`.
In Onboard SDK, `CameraManagerAsyncSample` and `CameraManagerSyncSample` demonstrate the usage
of the APIs in the class `CameraManager`. (Temporarily support for Matrice 210 V2 and Matrice 210 RTK V2)

## Goals

The samples provide the users to show how to use `CameraManager` to operate the camera devices. Different from original
Camera APIs, CameraMananger is an abstraction of a manager to all the camera modules on the aircraft. In other words,  developers
can use the APIs to control all the camera modules.

In the implementation of the samples, we show the demonstration of how to use the following features:
1. Camera Parameters setting and getting, including:
      * Exposure Mode
      * EV(Exposure compensation Value)
      * ISO Value
      * Shutter Speed Value
      * Aperture Value
      * Focus Mode
2. Focus Point
3. Tap Zoom Point
4. Continuous Zoom
5. Shoot Photo
6. Record Video

The samples have two implementation methods: synchronous method and asynchronous method. All the basic APIs of `CameraManager`
are wrapped in CameraManagerAsyncSample and CameraManagerSyncSample. So when developers build up their sample, it's
a choice to initialize an instance of them in the implementation and quickly get use of the APIs.

The camera samples are only available on Linux and STM32 platform.

Here are two typical sample tutorials:<br>
[Camera function - tap zoom](/cn/sample-doc/CameraManager-operational-function.html)<br>
[Camera parameter setting - aperture](/cn/sample-doc/CameraManager-parameter-setting.html)<br>


## Camera Functions Support List
|                                        |   X4S  |   X5S  |   X7   |  Z30   |   XT   |  XT2   |
|--------------------------------------  |--------|--------|--------|--------|--------|--------|
|  Set/Get Camera Work Mode              |   √    |   √    |   √    |   √    |    √   |   √    |
|  Set/Get Camera Focus Mode             |   √    |   √    |   √    |   √    |    ×   |   ×    |
|  Set/Get Exposure Mode                 |   √    |   √    |   √    |   ×    |    ×   |   ×    |
|  Set/Get ISO                           |   √    |   √    |   √    |   √    |    ×   |   ×    |
|  Set/Get Aperture                      |   √    |   √    |   √    |   ×    |    ×   |   ×    |
|  Set/Get Shutter                       |   √    |   √    |   √    |   ×    |    ×   |   ×    |
|  Set/Get EV(Exposure Compensation)     |   √    |   √    |   √    |   ×    |    ×   |   ×    |
|  Set/Get Tap Zoom Parameters           |   ×    |   ×    |   ×    |   √    |    ×   |   ×    |
|  Set/Get Tap Zoom Point                |   ×    |   ×    |   ×    |   √    |    ×   |   ×    |
|  Set/Get Focus Point                   |   √    |   √    |   √    |   ×    |    ×   |   ×    |
|  Set/Get Shoot-Photo Mode              |   √    |   √    |   √    |   ×    |    ×   |   ×    |
|  Shoot Single Photo                    |   √    |   √    |   √    |   √    |    √   |   √    |
|  Set/Get Interval Shooting Parameters  |   √    |   √    |   √    |   ×    |    ×   |   ×    |
|  Shoot Interval Photo                  |   √    |   √    |   √    |   √    |    √   |   √    |
|  Set/Get AEB Shooting Parameters       |   √    |   √    |   √    |   ×    |    ×   |   ×    |
|  Shoot AEB Photo                       |   √    |   √    |   √    |   ×    |    ×   |   ×    |
|  Set/Get Burst Shooting Parameters     |   √    |   √    |   √    |   ×    |    ×   |   ×    |
|  Shoot Burst Photo                     |   √    |   √    |   √    |   √    |    ×   |   ×    |
|  Record Video                          |   √    |   √    |   √    |   √    |    √   |   √    |
