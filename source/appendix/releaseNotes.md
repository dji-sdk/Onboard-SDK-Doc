---
title: Release Notes for Onboard SDK 3.3.1
version: 3.3.1
date: 2017-08-30
keywords: [SDK, Hardware Sync, New Features, Updates, release, notes, bugs, M100, Qt]
---

## Release Date

2017.08.03

## Highlights

- **M100 backwards compatibility:** All M100 features previously supported on OSDK 3.2 are now fully supported on 3.3.1. The 3.3 ROS wrapper, compliant with ROS standards, is now also compatible with M100.
- **Beta QT Sample:** Reintroduced with fully featured implementation of OSDK 3.3 features
- **Waypoint & Hotpoint read API calls:** Ability to read missions' settings and Waypoint index settings from an aircraft.

## Supported Firmware
- A3/A3 Pro: 1.7.1.5
- N3: 1.7.1.5
- M100: 1.3.1.0
- M600/M600 Pro: 1.0.1.60

## Bug Fixes:
- **Control authority UNKNOWN_ACK_ERROR_CODE:** fixed incorrect messaging when trying to obtain or release control.
- **Gimbal mount status check:** SDK will now check whether gimbal is mounted during initialization of vehicle object.
- **STM32 memory footprint:** Reduced OSDK memory footprint by 60%.
- **Receive container firmware version:** Fixed incorrect version which was set in receive container.

## Known Issues
- **Potential SerialDevice infinite loop:** If aircraft is connected incorrectly and there’s no data on the serial line, the read thread might loop indefinitely.
- **GCC7 compilation:** OSDK will not compile correctly using GCC7.
- **QT Sample M100 Compatibility:** Some M100-specific feature are not supported in QT Sample.

<hr>

## Previous Releases

### OSDK 3.3 Highlights

- Full rewrite of the Onboard SDK for simplicity, performance and portability
- Tons of new features, outlined below
- Full support for Linux, STM32 and ROS
- Fully re-written ROS wrapper compliant with ROS standards
- New API Reference documentation instead of a protocol spec for ease of use
- New feature guide documentation and feature-specific sample code

If you have an A3, A3 Pro, M600, M600 Pro or an N3, upgrade to this release to receive all the goodness! If you have an M100, stay tuned for more. Support for M210 and M210-RTK is also coming soon!

Please visit the [Version Compatibility](../appendix/versioning.html) page to finds out what firmware you need to be running to take advantage of OSDK 3.3. Note that though this documentation mentions M600/Pro support in most places, the flight control firmware for OSDK 3.3 support is not out yet. The projected release date for this firmware is end-July.

### New Features

- External hardware time synchronization capability
- Multi-Function IO support (PWM, Digital IO, Analog-Digital Conversion)
- High-rate (200 Hz) angular rate controller
- Increased bounds for attitude and velocity control
- Advanced control modes - feedforward compensation, emergency brake
- Greatly expanded set of telemetry data through a "subscription" paradigm

### Known Issues

- When an RC loses connection mid-flight or is turned off, the telemetry values in the OSDK receive persistent values from the last known stick position.
- If you start the A3/N3 flight controller in A/S/G mode (with the Multiple Flight Modes feature enabled through DJI Assistant 2), the onboard SDK will be able to obtain control, thus overriding the `P` mode requirement. This happends because the flight controller upon boot-up assert P-mode. Switching out of the non-P mode and switching back to that mode will restore the expected behavior.

#### Old Releases

- Release notes for pre-3.3 releases can be found [here](../M100-Docs/old-release-notes.html).