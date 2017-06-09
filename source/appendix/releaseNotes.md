---
title: Release Notes for Onboard SDK 3.3
version: 3.3
date: 2017-06-13
keywords: [SDK, Hardware Sync, New Features, Updates, release, notes, bugs]
---

## OSDK 3.3 Highlights

- Full rewrite of the Onboard SDK for simplicity, performance and portability
- Tons of new features, outlined below
- Full support for Linux, STM32 and ROS
- Fully re-written ROS wrapper compliant with ROS standards
- New API Reference documentation instead of a protocol spec for ease of use
- New feature guide documentation and feature-specific sample code

If you have an A3, A3 Pro, M600, M600 Pro or an N3, upgrade to this release to receive all the goodness! If you have an M100, stay tuned for more. Support for M210 and M210-RTK is also coming soon!

## New Features

- External hardware time synchronization capability
- Multi-Function IO support (PWM, Digital IO, Analog-Digital Conversion)
- High-rate (200 Hz) angular rate controller
- Increased bounds for attitude and velocity control
- Advanced control modes - feedforward compensation, emergency brake
- Greatly expanded set of telemetry data through a "subscription" paradigm

## Known Issues

- When an RC loses connection mid-flight or is turned off, the telemetry values in the OSDK receive persistent values from the last known stick position.
- If you start the A3/N3 flight controller in A/S/G mode (with the Multiple Flight Modes feature enabled throughh DJI Assistant 2), the onboard SDK will be able to obtain control, thus overriding the `P` mode requirement. Switching out of the non-P mode and switching back to that mode will restore the expected behavior.

#### Old Releases

- Release notes for pre-3.3 releases can be found [here](../M100%20Docs/old-release-notes.html).