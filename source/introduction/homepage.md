---
title: Onboard SDK Documentation Home
date: 2017-06-01
version: 3.3
keywords: [homepage, key features, hardware overview, registration, enable flight controller API control, safety]
---
> New Major Release! Onboard SDK 3.3 is a full redesign of the DJI OSDK. Please read the docs for the best developer experience!

The DJI Onboard SDK (OSDK) allows you to build powerful, automated drone applications for supported DJI vehicles (<a href="http://www.dji.com/product/matrice100" target="_blank">Matrice 100</a>, <a href="http://www.dji.com/product/matrice600" target="_blank">Matrice 600</a> or <a href="http://www.dji.com/matrice-200-series" target="_blank">Matrice 210/210-RTK</a>) or flight controllers (<a href="http://www.dji.com/product/a3" target="_blank">A3</a> or <a href="http://www.dji.com/product/n3" target="_blank">N3</a>).

This document helps you get started with the various aspects of building OSDK applications.

Note. OSDK 3.3 does not support Matrice 100, please refer to [here](../M100%20Docs/main.html) for previous documentation.

## Get Started Immediately

Developers can get started immediately by following the steps to [run a sample application](../quick-start/quick-start.html). If you haven't been here before, please read the rest of this document.

## Introduction

This section introduces and compares the products compatible with the DJI OSDK, and outlines the SDK itself.

- [Hardware Support](../hardware-setup/index.html)
- [Onboard SDK Introduction](onboard-sdk-introduction.html)
- [OSDK Architectural Overview](architecture-guide.html)

## Concepts to Understand

DJI Products use technologies that might not be fully familiar to software developers. See the concepts page to understand more about the technologies to take full advantage of the capablities of DJI aircraft or flight controllers.
- [Flight Control Concepts](things-to-know.html)

## Guides

The features available through the OSDK are detailed in our Feature Guides. These guides provide useful information about various aspects of interacting with specific modules offered through the Onboard SDK.

Be sure to read through all the guides available on the Feature Overview page before you start writing OSDK Applications!

//TODO - remove this
- [Feature Overview](../features/overview.html)


## Development Workflow

This section provides a step-by-step guide taking you through the entire development process.

- [Prerequisites](../development-workflow/workflow-prereq.html)
- [Hardware Setup](../development-workflow/hardware-setup.html)
- [Environment Setup](../development-workflow/environment-setup.html)
- [Integrating the OSDK into your Application](../development-workflow/integrate-sdk.html)
- [Running your OSDK Application](../development-workflow/run-applicaiton.html)

## Sample Code

We provide a number of samples designed to showcase example end-to-end implementations of various OSDK modules. Each sample application has implementations as standalone Linux programs, ROS nodes and STM32 applications.

- [Telemetry Sample](../sample-doc/telemetry.html)
- [Flight Control Sample](../sample-doc/flight-control.html)
- [GPS Missions Sample](../sample-doc/missions.html)
- [Camera/Gimbal Control Sample](../sample-doc/camera-gimbal-control.html)
- [Multi-Function IO Sample](../sample-doc/mfio.html)
- [Mobile SDK Communication](../sample-doc/msdk-comm.html)

## API Reference

Detailed reference for OSDK APIs can be found in the [API Reference](@todo) section.

## Appendix

TODO - should EULA, Release Notes and Porting Guide be removed?

- [FAQ](../appendix/FAQ.html)
- [EULA](http://developer.dji.com/policies/eula/)
- [Release Notes](../appendix/releaseNotes.html)
- [Porting Guide for OSDK 3.3](../appendix/porting-guide.html)

## Safety

Please comply with local regulations during the development of your application. Please refer to <a href="http://flysafe.dji.com/" target="_blank">http://flysafe.dji.com/</a> for more information. ***The operator must maintain sole responsibility for the safe operation of the vehicle, including maintaining the ability to take manual control of the vehicle at all times to maintain safety in the event of a malfunction of any aspect of the Onboard SDK modules.***
