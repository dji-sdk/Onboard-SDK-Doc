---
title: Advanced Sensing - Stereo Camera
date: 2017-11-23
keywords: [stereo, disparity map, monotone, VGA, QVGA, USB]
---

## Introduction

The advanced forward and downward stereo vision positioning systems (VPS) on DJI Matrice 210 gives the aircraft precise hovering and collision avoidance capabilities, even without satellite positioning support. The VPS also allows it to brake instantly and hover when joystick controls are released. If disturbed during a hover, it will track the aircraft's movement and return it to its original hovering point. 

As an OSDK developer, you have access to this image data to expand the capabilities of your application. Besides the image data, OSDK also provides access to a pre-processed disparity map for front stereo as well as ROS interfaces for neat integration into ROS image and stereo vision workflows.

![m210_front_stereo](../../images/guides/m210_stereo_composite.png)

## Image workflow, Resolution, and Frame Rate

Unlike other features in OSDK that use the serial line to communicate to the drone, Advanced Sensing utilizes USB to receive raw image data. Please follow [M210 checklist](../M210-Docs/main.html) for instructions to set up your aircraft. Currently this feature only supports M210.

The Advanced Sensing feature works within the subscription mechanism. The user only needs to call the corresponding API once and passes a callback function to subscribed images, raw image data will start broadcasting through USB. Note that users need to and are responsible to unsubscribe from the images within each power cycle.

Available image data includes:

#### Front Stereo cameras

* Grayscale image in VGA (640x480) resolution at 10 or 20 fps.
* Grayscale image in QVGA (320x240) resolution at 20 fps.
* Disparity map in QVGA (320x240) resolution at 10 fps.

#### Down Stereo cameras

* Grayscale image in QVGA (320x240) resolution at 20 fps.

## Meta Data

All images come with frame index and timestamp as metadata. Frame index for QVGA images starts whenever the drone is powered and will continue no matter whether the developer subscribes to it or not. On the other hand, the frame index for VGA images follows the user's subscription workflow. If the user subscribes and unsubscribes to VGA images, the frame index will continue from the last subscribed image. For time stamp, all four cameras are triggered at the same time and share the same timer. The timer is synchronized to the clock of the flight controller on M210 V2 (Please update to the latest FW in DJI assistant 2). 
Please follow [Time Sync](../guides/component-guide-time-sync.html) for more detail. 

![m210_flying_with_stereo_imgs](../../images/samples/m210_all_image.gif)



