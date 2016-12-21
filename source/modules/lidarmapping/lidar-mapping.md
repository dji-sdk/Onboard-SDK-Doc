---
title: LiDAR Mapping [beta]
version: 3.1.9
date: 2016-10-14
---

## Introduction

The LiDAR Mapping integration of the Onboard SDK enables users to build a 3-D map of the environment by making use of the pre-existing open source [LOAM package](http://wiki.ros.org/loam_velodyne). 
The LOAM package allows users to generate a realtime map using the [Velodyne PUCK Lite](http://velodynelidar.com/vlp-16-lite.html) LiDAR sensor.
 
A new feature addition is the ability to generate the maps created by LOAM to an industry standard LAS file format by making use of the Onboard SDK's **pointcloud_LAS** library. 

![3-D Map](../../images/modules/lidarmapping/pointcloudimage.png)


 
