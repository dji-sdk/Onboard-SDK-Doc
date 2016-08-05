---
title: Release Notes for Onboard SDK 3.1.8
version: 3.1.8
date: 2016-08-05
---

## Highlights

* Onboard SDK 3.1.8 brings many brand new features and builds upon the stability of 3.1.7
* Mobile-Onboard SDK: iOS app for controlling the OSDK functions through mobile device
* Ping ADS-B Sense-and-Avoid sensor integration with iOS control app
* Velodyne Puck Lite LiDAR sensor integration and tutorial
* Support for synchronous programming paradigm and revamped programming guide
* New C++ Linux example with Onboard SDK best practices
* Many bugfixes and cleanup

## New Feature Descriptions

Click on the titles below to go to the full documentation for each feature.

#### [Mobile-Onboard SDK(MOS) iOS App](../github-platform-docs/MobileOnboardSDK/Mobile-OSDK.html)

* Call entire sequences, custom missions or simple Onboard SDK API calls through an iOS app
* Connects to the OSDK through Mobile SDK - Onboard SDK Transparent Transmission link
* Perfect for real-world tests where you do not want to deal with wireless UART modules

#### [PingRX: Air traffic awareness](../sensor-integration-guides/ping/README.html)

* With the ultra-lightweight PingRX integrated with Onboard SDK, you can now receive information about air traffic up to 100 miles from your drone
* Great for deployments near commercial airspace - Ping data is available in OSDK for you to implement sense-and-avoid
* We provide a companion iOS App to view air traffic data in your area on a map

#### [Velodyne Puck Lite LiDAR: A new era in drone sensing](../sensor-integration-guides/velodyne/readme.html)

* The Puck Lite LiDAR gives you a high-frequency, highly accurate 3D point cloud of its surroundings up to 100m
* Revolutionize your mapping, inspection or survey application with the power of drones and LiDAR
* Allows you to implement LiDAR SLAM or sophisticated sense-and-avoid when paired with the Onboard SDK
* Integration with new, Core i5-based x86 OES for powerful processing

#### [New Programming Paradigm](../application-development-guides/programmming-guide.html)

* The 3.1.8 release offers a complete set of synchronous API call overloads - now you can maintain a linear flow of execution with these blocking functions
* A synchronous (blocking) function returns to the caller only after it has been executed and an acknowledgement from the aircraft has been received.
* Synchronous functions return acknowledgements from the aircraft to user code for further processing and decision making

#### [New C++ Linux Example](../github-platform-docs/Linux/README.html)

* Built from the ground up as a reference best practice example program on Linux
* Includes an efficient serial device driver, memory management, pthread-based threading and synchronous API calls
* Supports three modes of operation - Interactive (like the old commandline sample), mobile commands from the MOS app and a new programamtic mdoe for users to execute entire complex sequences of code without interactivity. Perfect for deployment.


---

## Previous Release - 3.1.7

### Highlights

* This release is a major cleanup and bugfix release for Onboard SDK 3.1
* Over a hundred bugs have been squashed
* Code has much-improved comments and is easier to follow
* Introduces an alpha version of a unit-testing suite for the core library
* Provides the capability to build the core library independently of the samples for easier integration into larger projects
* Introduces an alpha version of Doxygen-style code commenting and pre-generated html doxygen documentation

New developers should start with the revamped [Getting Started Guide](../quick-start/index.html).

### Major Fixes

##### Core Library

* Code style updated to a more modern GNU-like style. Change affects indentations and new functions/variables/structs introduced in this release. Older functions, variables, structs and classes are untouched.
* Many elements of code have been identified as sub-optimal; we have started marking these structs/functions for deprecation in a future release. We are fully backwards compatible for this release - no old elements have been removed, but users are encouraged to move to the newer elements introduced as part of this release. Doxygen-style comments document the changes and planned replacements; users should look into the core library or go to `doc/doxygen-doc/html/index.html` to see doxygen code documentation.

    Some examples (**This table is not exhaustive!**):

|Old element|Planned New element|Description|File|
|-------|------|---------|--------|
|MagnetData|MagData|Name change|DJI_Type.h|
|PositionData|PositionData|Struct member restructuring|DJI_Type.h|
|toRadioData|toRCData|Function interface change|DJI_VirtualRC.h|
|toEulerianAngle|toEulerAngle|Function interface change|DJI_Flight.h|

>To re-iterate: these changes are **planned for a future release**. In this release, both old and new versions co-exist.    

* Replaced all uses of `palstance` with `YawRate`
* CMake support for Linux platforms added
* Unit testing framework introduced
* Setter/getter added for open protocol transmission session status

##### Qt

* UI elements have been cleaned up and the behavior of a number of buttons has been changed. New button behavior is a lot more informative.

|Functionality|Fixed Issues|
|---------|---------|
|Display Scaling|Added support for Hi-res displays|
|Qt function discovery|Changed many functions to allow Qt to automatically find them|
|Button behavior|Arm, activation, hotpoint buttons are interactive/more informative|
|Waypoint functionality|<ul><li>Intermittent crashes fixed</li><li>Lat/Lon input changed from radians to degrees</li>Revamped layout and added indications for the order of operations</ul>|
|Hotpoint Functionality|Lat,Lon can now be entered in degrees|
|UI| Unused buttons and tabs removed. UI looks a lot cleaner.|

* Build has been updated to work with the newest Qt release (5.6). DJI Script dependencies have been removed to streamline Qt build.

##### Commandline Linux

* The commandline linux sample has undergone a major revamp. Many functions have been fixed:

|Functionality|Fixed Issues|
|-------|---------|
|Activation|<ul><li>Version mismatch error fixed</li><li>Reliability improved</li><li>Feedback messages improved</li></ul>|
|Waypoint|<ul><li>"Not enough waypoints" error fixed</li><li>Much clearer steps of operation </li><li>Bus error on Manifold fixed</li></ul>|
|Hotpoint|<ul><li>No execution though success message appears - fixed</li><li>Bus error on Manifold fixed</li></ul>|
|VirtualRC|Functionality has now been implemented|
|Flight Control|<ul><li>No execution - fixed </li><li>Unbounded motion fixed</li><li>Bus error on Manifold fixed</li></ul>|

* Directory structure has changed to a more standard structure. ManifoldPlatform folder has been removed and the Linux example now consolidates all linux-based platforms.
* Automatic activation sequence added
* User Configuration file added
* On-screen information at the interactive prompt updated to be more useful

##### ROS

* ROS repository will now follow the same version numbers as the core repo. The current release is tagged as 3.1.7.
* ROS Onboard SDK is now based on the latest [Onboard SDK](https://github.com/dji-sdk/Onboard-SDK) library.
* 'Draw a Circle' example is revamped and implements the movement control fuctionality exposed by the open protocol. The example is now using closed-loop control.
* Waypoint and Virtual RC exmaples have been improved.
* Tested with Ubuntu 16.04 LTS/ROS Kinetic Kame - to use this configuration, install the ROS Onboard SDK from source. APT and rosinstall are not supported for this configuration
* DJI A3 Flight Controller has been tested with ROS Onboard SDK.

##### STM32

* Fixed activation errors due to version not being set.
* Fixed movement control commands - developers can now successfully execute all movement control commands through the STM32. Documentation has also been updated to reflect the same.
* Added user parameters in hotpoint mode.
* DJI A3 Flight Controller has been tested with the STM32.
