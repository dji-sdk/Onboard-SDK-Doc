---
title: Prerequisites
date: 2019-02-20
version: 3.3
keywords: [prerequisites, info, assistant, standalone]
---

# Required

To build an Onboard SDK based application the following are required:

- Programming experience in C++
- Experience with embedded systems might be needed for third party sensor or actuator integrations.
- A [compatible](../appendix/versioning.html) DJI vehicle/flight controller
- Your own Onboard Computer with an available TTL UART port.
    - For x86 platforms, we recommend small-form-factor PCs that can be powered from the aircraft's bus
    - The [DJI Manifold](https://store.dji.com/product/manifold) is an excellent computer meant to harness the full potential of DJI OSDK
    - Among embedded systems, we recommend the STM32F4 (and the Discovery board).
- Software tools to build the SDK. See [Environment Setup](environment-setup.html) for each platform.
- Windows PC/Mac to run the required software tools
- An iOS or Android mobile device to run DJI Go for first time application activation (requires internet connection)


# Optional

- An iOS device to run the [Mobile-Onboard SDK Sample](https://github.com/dji-sdk/Mobile-OSDK-iOS-App) application, and a MacOS laptop with XCode 7 to compile and load this application
- For M210 Developers interested in [Advanced Sensing](../guides/component-guide-advanced-sensing-stereo-camera.html), an Onboard Computer with USB 2.0 is required. Please check out [M210 Checklist](../M210-Docs/main.html) for more details.