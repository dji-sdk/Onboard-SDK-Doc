---
title: Onboard SDK Architectural Overview 
version: 3.3
date: 2017-05-20
keywords: [architecture guide]
---

## Introduction

DJI Onboard SDK is an open source communication software library designed to provide developers access to the capabilities of DJI's aircraft, handled camera and sensor products. The software library provides low level control communication between aircraft and computer companion platform (of your choice) mounted directly on aircraft's chasis. This communication allows for onborad, real time processing and can be used to program your aircraft to perform complex missions and tasks.

*Note: If you haven't read the [Quick Start](../quick-start/index.html) guide yet, please do so first.*

## Hierarchy

User application accesses the DJI Onboard SDK through several main classes illustrated in the diagram below.

[![Software Architecture](../images/common/djiosdk-3.3-Vehicle-High-Level.png)](..images/common/djiosdk-3.3-Vehicle-High-Level.png)

### API Layer

* **Vehicle**: Manages activation, encapsulation of hardware and software components. This class holds basic product properties and contains the main product components.
* **Control**: Component class providing flight controller features.
* **Mission Manager**: Missions are controlled through the mission manager. It provides control of mission preparation, execution, termination, pausing and resumption as well as provides access to the currently executing mission.
* **HotPoint**: Class providing HotPoint mission features.
* **WayPoint**: Class providing WayPoint mission features.
* **Subscriber**: Telemetry software component class providing telemetry to collect data from flight controller. 
* **Broadcast**: Telemetry software component class providing telemetry to collect data from flight controller.
* **Camera**: Software component class providing handled camera features.
* **Gimbal**: Software component class providing handled gimbal features.
* **MFIO**: Software component class providing handled MFIO features.

### Protocol Layer

* **Protocol Layer**: Software component class implementing transportation layer for DJI OPEN Protocol.

### Driver Layer

* **USART Driver**: Software component class implementing USART protocol communication.

### Hardware Layer

* **Flight Controller**: Hardware component situated on aircraft.
* **Camera**: Hardware component situated on aircraft.
* **Gimbal**: Hardware component situated on aircraft.
* **MFIO**: Hardware I/O component situated on aircraft.

## Vehicle

## Hardware Components

## Mission
