---
title: Flight Control sample
date: 2017-03-07
keywords: [sample, samples, Flight control, flightcontrol, position, positioncontrol, control]
---

## Introduction 

The flight control sample demonstrates sending control commands to the aircraft using the Position control command. The sample allows you to run two operations: 

* Take off and Land aircraft
* Take off, flight motion using Position Control and Land aircraft. 

## Goals 

The sample demonstrates a closed loop controller with position commands sent to the aircraft using the positionAndYawCtrl API. It subscribes to the following topics: 
 
1. TOPIC_STATUS_FLIGHT at 10Hz
2. TOPIC_STATUS_DISPLAYMODE at 10Hz
3. TOPIC_QUATERNION at 50Hz
4. TOPIC_GPS_FUSED at 50 Hz

The flight control sample is available on Linux, ROS and STM32. 

## Code work flow 

[![Flight Control code workflow](../images/samples/flightcontrol_flowchart.jpg)](../images/samples/flightcontrol_flowchart.jpg)

## Output 

The output of the flight control sample in simulation is as shown below. 

[![Flight Control sample simulation](../images/samples/flight_control_loop.gif)](../images/samples/flight_control_loop.gif)
