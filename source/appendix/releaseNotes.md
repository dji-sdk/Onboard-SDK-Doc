---
title: Release Notes for Onboard SDK 3.6
version: 3.6
date: 2018-02-01
keywords: [SDK, M210, Point Cloud, Camera, Disparity Map, collision avoidance]
---

## Release Date

2018.02.01

## OSDK 3.6 Highlights

- **Major stereo vision stack update:** New samples have been added for better rectification, disparity, and point cloud projection, accurate to a few cm.
- **3D object localization sample:** Building on this stack, we now showcase a CNN-based 3D object detection and localization sample.
- **Multiple performance improvements and bugfixes:** Over twenty bugs have been fixed, and error handling and reporting have been made more robust.

## Supported Firmware

Please download the latest [DJI Assistant 2](https://www.dji.com/matrice-200-series/info#downloads) for M210/M210 RTK support.

- A3/A3 Pro: 1.7.1.5+
- N3: 1.7.1.5+
- M100: 1.3.1.0+
- M600/M600 Pro: 1.0.1.65+
- M210/M210 RTK: 1.1.0410+

## Bug Fixes

- **Samples hang when no data on serial line:** The read thread now quits as expected, allowing clean exit.
- **Memory Leaks:** Fixed a few memory leaks in osdk-core, mainly related to buffers.
- **Flight Control Sample height/altitude references:** Previously, flight control samples used an incorrect reference for height, causing unpredictable real-world behavior. This has been fixed.
- **Many other smaller bugfixes:** Undefined return values, uninitialized variables, unreliable initial connection, etc.

## Improvements

- **Components initialize on successful activation:** All components of Vehicle are now only initialized after activating successfully to allow error handling without the use of exceptions.
- **Actionable error messages:** Errors at various stages will now offer possible causes and remedies.
- **Subscription cleanup:** The vehicle initialization routine will automatically clean up if a previous subscription exists in an unclean state. There is a similar fix for the Advanced Sensing library as well.

## Developer Notes
- Since program components are no longer initialized prior to activation, please ensure that the first API your program calls after initialization is *activate*.
- Please be sure to update your Advanced Sensing binary to 2.0.1, supporting x86 and 64-bit ARMv8.

<hr>

## Previous Releases

### OSDK 3.5 Highlights

- **Access to live camera streams of M210 and M210 RTK**: both FPV camera and main gimbaled camera
- **Comprehensive Samples for live camera streams APIs**: from basic data accessing samples to more advanced target tracking samples
- **More complete license information is added**

### OSDK 3.4 Highlights

- **Support for M210 and M210 RTK:** 
OSDK features are now supported for M210. Currently, hardware synchronization and Multi-function IO are not supported.
- **Stereo vision data from M210 and M210 RTK:** Raw images and disparity map from stereo camera pairs of M210 are now available.
- **M600 backward compatibility:** Supports M600 firmware 1.0.1.20.
- **ROS RTK support:** RTK data via ROS topics.
- **Protocol layer refactor:** Improved performance and better abstraction.
- **Platform Manager:** Better abstraction layer for different computing platforms.
- **Dynamic logging control:** Developers can now start or stop logging.
- **Encryption flag:** Implemented getter/setter to modify encryption flag.

#### Supported Firmware

Please download the latest [DJI Assistant 2](https://www.dji.com/matrice-200-series/info#downloads) for M210/M210 RTK support.

- A3/A3 Pro: 1.7.1.5
- N3: 1.7.1.5
- M100: 1.3.1.0
- M600/M600 Pro: 1.0.1.65
- M210/M210 RTK: 1.1.0410

#### Bug Fixes

- **Multi-threaded segmentation fault fix:** Prevents access to unallocated memory in callback thread.
- **Qt sample failed to initialize serial port:** Fixed QThreadManager with renamed pure virtual functions and added mutex to protect init function from being called in two threads.
- **OpenProtocol activation fix:** Performs activation before using encryption.
- **Waypoint push data event handling:** Waypoint PushData variable was not set properly.
- **Local position reference state fix:** Returns state when setting local position.

### Old Releases

- Release notes for pre-3.3 releases can be found [here](../M100-Docs/old-release-notes.html).
