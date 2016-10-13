---
title: Release Notes for Onboard SDK 3.1.9
version: 3.1.9
date: 2016-10-12
keywords: [Precision Trajectory, Mission Planning, Velodyne Puck Lite LiDAR]
---

## Highlights

* Onboard SDK 3.1.9 adds an exciting, major new component - Precision Trajectory Mission Planning (beta)
* Velodyne Puck Lite: New features allow real-time logging in the popular ASPRS-approved LAS file format
* Threaded Callbacks: The callback mechanism has been completely revamped for more efficient, robust code
* CMake: Onboard SDK is now fully CMake-based, allowing easy integration with other projects
* Wrapper API: New higher-level API allows easy usage of common OSDK functions
* Linux Sample: Support added for Camera and Gimbal control samples, LiDAR LAS logging and Precision Trajectory execution

## New Feature Descriptions

Click on the titles below to go to the full documentation for each feature.

#### [Precision Trajectory Mission Planning](../modules/missionplan/README.html)

* Plan, visualize and fly complex trajectories with unmatched flexibility
* Use the DJI SketchUp plugin to import 3D models and geolocate trajectories around infrastructure
* Execute spiral trajectories at desired speeds around objects of interest while automatically taking pictures and video
* Get repeatable and precise trajectories that do not depend on the waypoint interface
* Many more features coming up in the near future!

#### [Velodyne Puck Lite LiDAR: New features](../sensor-integration-guides/velodyne/readme.html)
* Record real-time LiDAR data into the industry-standard LAS file format
* Import our LAS recordings into top commercial software such as Autodesk AutoCAD(r) Map3D, Merrick's MARS and open-source tools like CloudCompare
* Standalone recorder allows you to have a lean tool for collecting LiDAR scans for analysis
* Integration with Onboard SDK Linux interactive sample for easy LiDAR logging from within Onboard SDK


#### SDK Improvements

* 3.1.9 brings with it a move to native CMake builds - all libraries  and executables in the SDK can now be build with a [single cmake call]() at the top level
* A new, higher-level OSDK [Wrapper API]() allows users to call better encapsulated, more intuitive functions for accomplishing common larger tasks rather than using multiple lower-level CoreAPI calls for accomplishing the same thing
* A new threading model for asynchrononous programming allows callbacks to be run on a [separate thread](), freeing up the read thread for its primary purpose

#### [Updated C++ Linux Examples](../github-platform-docs/Linux/README.html)

* The synchronous Linux sample from 3.1.8 has been updated and now has interfaces to all features of the Onboard SDK - Wrapper API, LiDAR and Precision Trajectories
* A new asynchronous Linux sample that uses the new threaded callbacks has been created. This sample has fewer features and is intended mostly as a reference for the new programming model.

## Previous Release - 3.1.8

## Highlights

* Onboard SDK 3.1.8 brings exciting new features and builds upon the stability of 3.1.7
* Mobile-Onboard SDK: iOS sample app for controlling the OSDK functions through a mobile device
* Ping ADS-B Sense-and-Avoid sensor integration with iOS sample app
* Velodyne Puck Lite LiDAR sensor integration and tutorial
* Support for synchronous programming paradigm and revamped programming guide
* New C++ Linux example with Onboard SDK best practices
* Many bugfixes and cleanup

## New Feature Descriptions

Click on the titles below to go to the full documentation for each feature.

#### [Mobile-Onboard SDK (MOS) iOS App](../github-platform-docs/MobileOnboardSDK/Mobile-OSDK.html)

* Call entire sequences, custom missions or simple Onboard SDK API calls through an iOS app
* Connects to the OSDK through Mobile SDK - Onboard SDK Transparent Transmission link
* Perfect for real-world tests where you do not want to deal with wireless UART modules

#### [PingRX: Air traffic awareness](../sensor-integration-guides/ping/README.html)

* With the PingRX ADS-B receiver integrated with Onboard SDK, you can now receive information about air traffic up to 100 miles from your drone
* Great for deployments near commercial airspace - Ping data is available in OSDK for you to implement sense-and-avoid of aircraft that are transmitting ADS-B data
* We provide a companion iOS App using the Onboard SDK Transparent Transmission link to view air traffic data on a map on your mobile device

#### [Velodyne Puck Lite LiDAR: A new era in drone sensing](../sensor-integration-guides/velodyne/readme.html)

* The Puck Lite LiDAR gives you a dense 3D point cloud of its surroundings with up to 100m range
* Revolutionize your mapping, inspection or survey application with the power of DJI drones and LiDAR
* Allows you to implement LiDAR SLAM or sophisticated sense-and-avoid when paired with the Onboard SDK
* Integration with new, Core i5-based x86 OES for powerful processing

#### [New Programming Paradigm](../application-development-guides/programming-guide.html)

* The 3.1.8 release offers a complete set of synchronous API call overloads - now you can maintain a linear flow of execution with these blocking functions
* A synchronous (blocking) function returns to the caller only after it has been executed and an acknowledgement from the aircraft has been received.
* Synchronous functions return acknowledgements from the aircraft to user code for further processing and decision making

#### [New C++ Linux Example](../github-platform-docs/Linux/README.html)

* Built from the ground up as a reference best practice example program on Linux
* Includes an efficient serial device driver, memory management, pthread-based threading and synchronous API calls
* Supports three modes of operation - Interactive (like the old commandline sample), mobile commands from the MOS app and a new programamtic mode for users to execute entire complex sequences of code without interactivity

## Backward Compatibility

To make older applications work with the 3.1.8 Core API, developers will need to implement the `wait(int timeout)`, `notify()`, `lockACK()` and `freeACK()` functions in their HardDriver-inherited serial device driver. For example implementations of these functions we recommend reading through `platform/LinuxSerialDevice.h` and `platform/LinuxSerialDevice.cpp` on Github.