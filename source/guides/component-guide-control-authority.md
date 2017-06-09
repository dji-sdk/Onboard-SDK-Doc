---
title: Flight Controller
date: 2016-12-13
keywords: [flight mode switch, control authority, control presidence]
---

## Introduction

In a typical Onboard SDK application, there are several potential sources of aircraft control. The aircraft's flight controller arbitrates which source is in control at any one time. The different sources of control, and their control priority from highest to lowest is:

1. Remote Controller
2. Mobile Device (with a DJI Mobile SDK based application, connected to the Remote Controller)
3. Onboard Computer (with a DJI Onboard SDK based application, connected directly to the aircraft)

This guide describes how to transfer control between different control sources, and what functionality is available to the Onboard Computer in these scenarios.

## Remote Controller

The remote controller has the highest priority for control authority, and can regain control from the mobile device or onboard computer at any time.

This is always done by switching the Flight Mode Switch on the remote controller. 

For all DJI products except A3/N3 and M600/M600 Pro, there will be at least one switch position that allows SDK control, and another that disables it. 

A3 and N3 stand alone flight controllers have two possibilities, based around if **Multiple Flight Modes** is enabled or disabled (this is enabled/disabled in DJI Assistant).

* **Enabled**: Similar to all other products - a particular position will disable SDK automation and another will enable it
* **Disabled**: In this case, all switch positions will allow Onboard SDK automation - simply changing the switch position will give the remote controller control authority.

M600 and M600 Pro behave like A3/N3 with Multiple Flight Modes disabled.

## Mobile SDK

The Mobile SDK will have control authority whenever:

* Remote controller flight mode switch is in the position that enables SDK automation
* The Mobile SDK is sending a command to execute a flight maneuver (e.g. executing a mission, or using virtual sticks).

Whenever the Mobile SDK is not executing a flight maneuver, the remote controller will have control authority.

## Onboard SDK

Several prerequisites are required to enable control authority for the Onboard SDK:
* Flight mode switch must be in correct position (unless using A3/N3 with Multiple Flight Modes disabled, or using M600/M600 Pro)
* Onboard computer application must have activated the Onboard SDK
* Onboard computer application must request and receive control authority

Talk about ASG modes somewhere


In a typical Onboard SDK setup, the drone can be controlled by (1) the Remote Controller (2) the Mobile Device and/or (3) the Onboard Computer. The priority is generally set as (1) > (2) > (3). However 

This is to prevent the dangerous situation of code failing and the user not being able to take control of the drone to shut it down.

The remote controller always enjoys top priority for control. The flight controller can enter API Control Mode (Programmable Mode) if the following conditions are met:


Your RC is conencted and powered on.
The 'enable API control' box is checked in the assistant software.
The mode selection bar of the remote controller is placed at the F position.
To request control of the drone, your app must call the flight control request function exposed by the Onboard SDK library.

Note that this does not mean the user will always be able to use RC sticks to control the aircraft; for example, in F mode (P mode for A3/N3 FW > 1.5.0.0) the sticks are unavailable when the SDK is executing movement control. The correct way to assert the RC's control precedence is to make sure the above conditions for API control are unmet - usually the easiest way to do so is to switch the RC out of F mode into P or A mode. For A3/N3 FW > 1.5.0.0, please see mode switch changes.

![Control-Authority-State-Diagram](../images/common/Control-Authority-State-Diagram.png)