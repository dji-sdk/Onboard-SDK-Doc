---
title: Things to Know 
date: 2016-06-24
keywords: [control precedence, body frame, ground frame, quaternions]
---

This page outlines a few things you should know about Onboard SDK and drones in general before you start programming.

## Control Precedence

In a typical Onboard SDK setup, the drone can be controlled by (1) Remote Controller (2) Mobile Device and (3) Onboard Embedded System (OES). The priority is set as (1) > (2) > (3). This is to prevent the dangerous situation of code failing and the user not being able to take control of the drone to shut it down. 

The **remote controller always enjoys top priority** for control. The flight controller can enter API Control Mode (Programmable Mode) if the following conditions are met:

* Your RC is conencted and powered on.
* The 'enable API control' box is checked in the assistant software.
* The mode selection bar of the remote controller is placed at the F position.

To request control of the drone, your app must call the flight control request function exposed by the Onboard SDK library.

Note that this **does not mean** the user will always be able to use RC sticks to control the aircraft; for example, in F mode ([P mode for A3/N3 FW > 1.5.0.0](../appendix/releaseNotes.html#Notes-for-using-Onboard-SDK-with-the-new-a3-v1-5-0-0-fw)) the sticks are unavailable when the SDK is executing movement control. The correct way to assert the RC's control precedence is to make sure the above conditions for API control are unmet - usually the easiest way to do so is to switch the RC out of F mode into P or A mode. For A3/N3 FW > 1.5.0.0, please see [mode switch changes](../appendix/releaseNotes.html#Notes-for-using-Onboard-SDK-with-the-new-a3-v1-5-0-0-fw).