---
title: Release Notes for Onboard SDK 3.1.9
version: 3.1.9
date: 2016-10-14
keywords: [Precision Trajectory, Mission Planning, Velodyne Puck Lite LiDAR]
---

## Highlights

* Onboard SDK 3.1.9 adds an exciting, major new component - Precision Trajectory Mission Planning (beta)
* Velodyne Puck Lite: New features allow real-time logging in the popular ASPRS-approved LAS file format
* Threaded Callbacks: The callback mechanism has been completely revamped for more efficient, robust code
* CMake: Onboard SDK is now fully CMake-based, allowing easy integration with other projects
* Wrapper API: New higher-level API allows easy usage of common OSDK functions
* Linux Sample: Support added for Camera and Gimbal control samples, LiDAR LAS logging and Precision Trajectory execution

> The 3.1.9 release has a noticeable increase in total file size - don't be alarmed if it takes longer to clone!

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

* 3.1.9 brings with it a move to native CMake builds - all libraries  and executables in the SDK can now be build with a [single cmake call](../introduction/architecture-guide.html#cmake-library-build-structure) at the top level
* A new, higher-level OSDK [Wrapper API](../introduction/architecture-guide.html#levels-of-abstraction) allows users to call better encapsulated, more intuitive functions for accomplishing common larger tasks rather than using multiple lower-level CoreAPI calls for accomplishing the same thing
* A new threading model for asynchrononous programming allows callbacks to be run on a [separate thread](../application-development-guides/programming-guide.html#asynchronous-programming-callback-mechanism), freeing up the read thread for its primary purpose

#### [Updated C++ Linux Examples](../github-platform-docs/Linux/README.html)

* The synchronous Linux sample from 3.1.8 has been updated and now has interfaces to all features of the Onboard SDK - Wrapper API, LiDAR and Precision Trajectories
* A new asynchronous Linux sample that uses the new threaded callbacks has been created. This sample has fewer features and is intended mostly as a reference for the new programming model.
* The MOS iOS app now supports more features when used with the synchronous Linux sample.

## Backward Compatibility

The new CMake-based modularization makes it easy to link your code to individual Onboard SDK libraries. Link with djisodk-core, djiosdk-platform or djiosdk-wrapper as desired.  

The coreAPI library has been renamed to djiosdk-core, but is functionally backward compatible with older samples. There are new virtual functions that might need implementation in your serial device drivers - or you can use linuxSerialDevice, which has been packaged up into djiosdk-platform.

Note that you will be unable to build the Linux samples on platforms other than Ubuntu 16.04/14.04 on x86_64 or Ubuntu 14.04 on ARM. This is due to new feature dependencies; this behavior will change in a future release.