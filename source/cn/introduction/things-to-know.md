---
title: Things to Know 
date: 2016-06-24
---

This page outlines a few things you should know about Onboard SDK and drones in general before you start programming.

## Control Precedence

In a typical Onboard SDK setup, the drone can be controlled by (1) Remote Controller (2) Mobile Device and (3) Onboard Embedded System (OES). The priority is set as (1) > (2) > (3). This is to prevent the dangerous situation of code failing and the user not being able to take control of the drone to shut it down. 

The **remote controller always enjoys top priority** for control. The flight controller can enter API Control Mode (Programmable Mode) if the following conditions are met:

* Your RC is conencted and powered on.
* The 'enable API control' box is checked in the assistant software.
* The mode selection bar of the remote controller is placed at the F position.

To request control of the drone, your app must call the flight control request function exposed by the Onboard SDK library.

## Frames of Reference

Description of aircraft movement is dependent on the location and orientation of coordinate axes that make up a coordinate system (or frame of reference). Many coordinate systems exist, but the two used in the DJI Onboard SDK are relative to the aircraft body (body frame), and relative to the ground (world frame).

### 1. Body Frame

  ![bFrame](../../images/common/axis.png)

Aircraft translation in positive X, Y and Z is therefore defined in the Body Coordinate System as forward, right and downward translation respectively.

Aircraft rotation is also described with these same axes using the coordinate right hand rule to define the direction of positive rotation.

If the aircraft rotates around the Pitch axis (Y axis) it will move in the X axis direction. Moreover, if the Pitch angle is positive, the direction will be backwards, or in the negative X axis. Care must therefore be taken when using roll, pitch and yaw to move an aircraft.

### 2. Ground Frame
  
![gFrame](../../images/common/CoordinateSystemNED.png)

  + North - x axis
  + East - y axis
  + Down - z axis*

A popular ground or world coordinate system used for aircraft aligns the positive X, Y and Z axes with the directions of North, East and down. This convention is called North-East-Down or NED. In this convention, X and Y are then consistent with the right hand rule and normal navigation heading angles. A heading angle of 0° will point toward the North, and +90° toward the East.

The origin for a NED coordinate system is usually a point in the world frame (like take-off location).

> **Note:** *To alleviate this issue of the unnatural downward-pointing positive Z, we adjust the direction of vertical control in order to make the height or vertical velocity to be positive upwards. In other words, giving a positive velocity will make the UAV ascend. This adjustment does not affect the directions and the orders of the other two axis. We are not defining a left-handed co-ordinate system; the actual computations on the flight controller happen in an NED frame.*

## Quaternions  

We use the Hamilton Convention for the order of quaternions. That means our quaternion data structure will be of the form [q0, q1, q2, q3] where q0 is the scalar part.

If you are unfamiliar with quaternions, this [CH Robotics page](http://www.chrobotics.com/library/understanding-quaternions) is a pretty good introduction. 
