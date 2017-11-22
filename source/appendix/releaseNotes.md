---
title: Release Notes for Onboard SDK 3.4
version: 3.4
date: 2017-11-22
keywords: [SDK, Hardware Sync, New Features, Updates, release, notes, bugs, M100, M600, M210, Qt]
---

## Release Date

2017.11.22

## Highlights

- **Support for M210 and M210 RTK:** 
OSDK features are now supported for M210. Currently, hardware synchronization and Multi-function IO are not supported.
- **Stereo vision data from M210 and M210 RTK:** Raw images and disparity map from stereo camera pairs of M210 are now available.
- **M600 backward compatibility:** Supports M600 firmware 1.0.1.20.
- **ROS RTK support:** RTK data via ROS topics.
- **Protocol layer refactor:** Improved performance and better abstraction.
- **Platform Manager:** Better abstraction layer for different computing platforms.
- **Dynamic logging control:** Developers can now start or stop logging.
- **Encryption flag:** Implemented getter/setter to modify encryption flag.

## Supported Firmware

Please download the latest [DJI Assistant 2](https://www.dji.com/matrice-200-series/info#downloads) for M210/M210 RTK support.

- A3/A3 Pro: 1.7.1.5
- N3: 1.7.1.5
- M100: 1.3.1.0
- M600/M600 Pro: 1.0.1.65
- M210/M210 RTK: 1.1.0410

## Bug Fixes

- **Multi-threaded segmentation fault fix:** Prevents access to unallocated memory in callback thread.
- **Qt sample failed to initialize serial port:** Fixed QThreadManager with renamed pure virtual functions and added mutex to protect init function from being called in two threads.
- **OpenProtocol activation fix:** Performs activation before using encryption.
- **Waypoint push data event handling:** Waypoint PushData variable was not set properly.
- **Local position reference state fix:** Returns state when setting local position.

<hr>

## Previous Releases

### OSDK 3.3.1 Highlights

- **M100 backwards compatibility:** All M100 features previously supported on OSDK 3.2 are now fully supported on 3.3.1. The 3.3 ROS wrapper, compliant with ROS standards, is now also compatible with M100.
- **Beta QT Sample:** Reintroduced with fully featured implementation of OSDK 3.3 features
- **Waypoint & Hotpoint read API calls:** Ability to read missions' settings and Waypoint index settings from an aircraft.

### Supported Firmware

- A3/A3 Pro: 1.7.1.5
- N3: 1.7.1.5
- M100: 1.3.1.0
- M600/M600 Pro: 1.0.1.60

### Bug Fixes:

- **Control authority UNKNOWN_ACK_ERROR_CODE:** fixed incorrect messaging when trying to obtain or release control.
- **Gimbal mount status check:** SDK will now check whether gimbal is mounted during initialization of vehicle object.
- **STM32 memory footprint:** Reduced OSDK memory footprint by 60%.
- **Receive container firmware version:** Fixed incorrect version which was set in receive container.

### Known Issues

- **Potential SerialDevice infinite loop:** If aircraft is connected incorrectly and there’s no data on the serial line, the read thread might loop indefinitely.
- **GCC7 compilation:** OSDK will not compile correctly using GCC7.
- **QT Sample M100 Compatibility:** Some M100-specific feature are not supported in QT Sample.

#### Old Releases

- Release notes for pre-3.3 releases can be found [here](../M100-Docs/old-release-notes.html).