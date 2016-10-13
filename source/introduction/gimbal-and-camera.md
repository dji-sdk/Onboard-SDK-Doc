---
title: Gimbal And Camera
date: 2016-10-12
keywords: [gimbal, camera]
---

## Introduction

X3 and X5 camera fixed to an aircraft will record images that pitch and roll with the aircraft as it moves. Multi rotor aircraft need to pitch and roll simply to move horizontally, and so getting a stable horizontal shot is not possible.

A gimbal is used to keep a camera or sensor horizontal when its mount (e.g. aircraft) is moving. The gimbal has three motors controlling rotation in orthogonal axes. The gimbal feeds gyroscope information back to the motor controllers to compensate for rotational movement of the mount.

In addition to stabilization, the three motors can be used to control the direction the camera is pointing, and can be used to smoothly track a target, or pan a shot. The three axes of rotation are referred to as Pitch, Roll and Yaw, and the gimbal orientation is referred to as its attitude. Explanations of these axes can be found in the [Flight Control Concepts](https://developer.dji.com/mobile-sdk/documentation/introduction/flightController_concepts.html).

Gimbals have mechanical limits (or stops) to their rotation around each axis. When a sensor is mounted on a gimbal, many data and control lines are required to go from mount to sensor. These control lines are usually bundled in a cable assembly or flex circuit, both of which will limit the available rotation of the gimbal. Additionally, gimbals will also limit rotation so cameras cannot see landing gear or the product itself.

The DJI Onboard SDK gives access to gimbal capabilities and control.

# Gimbal

## Work Modes

The gimbal has several work modes that define how the gimbal follows aircraft movement, and how many axes are available for control.

- FPV (First Person View) Mode: Only pitch is controllable. Yaw and roll will be fixed relative to the product while pitch remains controllable.
- Yaw Follow Mode: Pitch and roll are controllable. Yaw will follow the products heading.
- Free Mode: Pitch, roll and yaw are all controllable, meaning the gimbal can move independently of the product's yaw. In this mode, even if the product yaw changes, the camera will continue pointing in the same world direction.

## Moving The Gimbal

Through the DJI Onboard SDK, the gimbal can be moved in two ways:

- Move to an angle over a duration
- Move at a speed in a direction

When using angle mode to rotate the gimbal's pitch, roll and yaw, the rotation angle of the gimbal can be defined as either Absolute(relative to the aircraft heading), or Relative (relative to its current angle). When using speed to rotate the gimbal's pitch, roll and yaw, the direction can either be set to clockwise or counter-clockwise.

## Reset

The gimbal can be reset by setting its pitch, roll and yaw to 0 degrees. The reset position is pointing horizontally and being in the same direction as product heading.

## Calibration

Gimbals will be automatically calibrated on power up. During calibration, the product should be stationary (not flying, or being held) and horizontal. For gimbal with adjustable payloads, the payload should be present and balanced before doing a calibration. At the moment, there is no option to calibrate the Gimbal through Onboard SDK APIs.

# Camera

The camera captures photos and videos. Many different modes of operation, resolutions, frame rates, exposure settings, picture settings and file types can be selected. Cameras have local storage to hold the media which will typically be an SD card, and in some cases an SSD (solid state drive).

This guide covers the large array of settings, modes and functionality provided by DJI cameras. A more general description of camera concepts can be found [here](https://developer.dji.com/mobile-sdk/documentation/introduction/camera_concepts.html).

Supported camera controls are:

- Still imahe  capture
- Video capture
 

## See our Linux sample for detailed description for Gimbal and Camera controls

## Todo give a link to questions 
