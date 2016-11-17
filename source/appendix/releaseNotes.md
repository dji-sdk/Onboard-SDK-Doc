---
title: Release Notes for Onboard SDK 3.1.9.1
version: 3.1.9.1
date: 2016-11-18
keywords: [Precision Trajectory, Mission Planning, Velodyne Puck Lite LiDAR]
---

## Highlights - Hotfix Release (v3.1.9.1)

* Hotfix release for A3 FW 1.5.0.0 (users on M100 or older versions of A3 (< 1.3.0.0) will have the same functionality as before)
* Fixes activation, version checks, obtain/release control that might have broken for some users on the latest A3 firmware.
* Introduces a new version macro - versionA3_32 - that users with the 1.5.0.0 FW should enter into their UserConfig file (or in the GUI for Qt)
* A non-A3 specific bug has been fixed related to Qt sample compilation issues. 

#### Notes for using Onboard SDK with the new A3 v1.5.0.0 FW
* Starting with this firmware, A3 units will respond differently to flight mode switch positions. The default switch positions of (P,A,F) have been replaced by (P,S,A) respectively.  
* Previously, Onboard SDK was available in F mode - with this release, the Onboard SDK is available in P mode. 
* If you desire a manual override (a switch position that disables the Onboard SDK), you can go to DJI Assistant 2 ->Basic Settings -> Remote Controller Settings and check the box that says Multiple Flight Modes.
* With Multiple Flight Modes enabled, the SDK will not work in S and A mode switch positions. You may use the S mode switch position for manual override.
* With Multiple Flight Modes disabled, the SDK **will work in all mode switch positions**. This is because without Multiple Flight Modes enabled, all mode switch positions map to mode P.

---

## Highlights - Last Major Release (v3.1.9)

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