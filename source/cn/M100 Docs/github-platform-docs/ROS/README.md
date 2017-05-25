---
title: DJI Onboard SDK ROS Example
version: v3.2.0
date: 2016-12-23
github: https://github.com/dji-sdk/Onboard-SDK-ROS
keywords: [ros example]
---

## Introduction

This ROS example implements functionality of the DJI Onboard-SDK. It consists of the core library and client packages demonstrating communication with Matrice 100 and A3/N3 flight controllers. The flight controller type can be defined in the launch file of the core package at any time. Onboard SDK functionality offered in a wrapped header file called dji\_drone.h which user can include and use directly for his/her own demo applications. We also provide a python version called dji\_drone.py. To have our samples run as quickly as possible, we implemented a sample code for hardware driver that you can use as is to ensure safe serial communication between your flight controller and an Onboard Embedded System (OES) of your choice.


Supported commands and  actions:

* Activation
* Obtain/Release Flight Control
* Take Off
* Landing
* Go Home
* Gimbal Control
* Attitude Control
* Photo Taking
* Start/Stop Video Recording
* Virtual RC Control
* Broadcast Frequency Control
* Arm/Disarm Control
* Timestamp Synchonization
* Native Waypoint
* Hotpoint
* Local Navigation (go to specified local position)
* Global Navigation (go to specified global position)
* Waypoint Navigation (fly through a series of GPS coordinates)
* WebSocket With Baidu Map (for navigation)
* MAVLink And QGroundStation

**New with OSDK 3.2.0** Advanced Features:

* [LiDAR Collision Avoidance](../../modules/collision-avoidance/collision-avoidance.html) in manual flight mode
* [LiDAR Mapping](../../modules/lidarmapping/lidar-mapping.html)

Software Functionality:

* [dji\_sdk](../ROS_Example/ros_corePackage.html): the core package handling the communication with Matrice 100/A3/N3, which provides a header file `dji_drone.h` for future use
* [dji\_sdk\_demo](../ROS_Example/ros_demo_client_package.html): an example package of using `dji_drone.h` to control the Matrice 100/A3/N3
* [dji\_sdk\_web_groundstation](../ROS_Example/ros_map_waypoint_navigation_package.html): a WebSocket example using ROS-bridge-suite, where a webpage groundstation is provided
* [dji\_sdk\_read_cam](../ROS_Example/ros_video_decoding_package.html): a X3 video decoding package for Manifold, CATKIN_IGNOREd by defualt
* [dji\_sdk\_dji2mav](../ROS_Example/ros_dji2mav_0.2.1_package.html): a protocol converter making M100 compatiable with all MAVLink-protocol-dependent softwares

![ROS Software Structure](../../images/ROS/ROSSoftwareStructure.jpg)
[click to see fullsize image](../../images/ROS/ROSSoftwareStructure.jpg)

## Setup 

### 1. Hardware

The [Hardware Setup](../../hardware-setup/index.html) guide talks about setting up your platform of choice. Make sure your setup matches that in the document before proceeding further. 


### 2. Software

Tested Environment:

* Operating System: Ubuntu 14.04, Manifold
* ROS version: ROS Indigo
> **Note:** Onboard SDK ROS has also been beta tested with Ubuntu Xenial 16.04LTS and ROS Kinetic Kame. We currently do not support `rosinstall` or `apt-get` for this configuration.   
> **Note:** Onboard SDK ROS also supports N3 and A3 FW 1.5.0.0 and newer with OSDK 3.2.0. See [Notes](../../appendix/releaseNotes.html#notes-for-using-onboard-sdk-with-the-new-a3-v1-5-0-0-fw).

Software Requirements:

* Install C, C++ Compiler and Development Tools by installing ``build-essential``
* Install CMake 2.8.3 or newer
* <a href="http://wiki.ros.org/ROS/Tutorials/InstallingandConfiguringROSEnvironment">Install ROS and its dependencies</a>

Compilation:

1. Assuming you have ROS environment installed and configured, cd into your catkin workspace and run ``catkin_make``. Make sure the source code is in the `src` directory of your catkin workspace.
<br>OR</br>
2. Refer to our .travis.yml build script to install and configure ROS from scratch and then follow with running ``catkin_make`` from catkin workspace.
3. You can pass `-DUSE_COLLISION_AVOIDANCE=ON` for compiling with [LiDAR Collision Avoidance](../../modules/collision-avoidance/collision-avoidance.html) and `-DUSE_POINTCLOUD2LAS=ON` for building with [LiDAR Mapping](../../modules/lidarmapping/lidar-mapping.html).


## Activation

Before you start exploring DJI Onboard SDK functionality via our ROS examples, you will need to go through the "Activation" process.

Activation Process:

1. Follow steps (3) and (5) in the [Setup](../../quick-start/index.html#Setup) section of the Quick Start guide
2. Update core launch file dji_sdk/launch/sdk_manifold.launch with information below:
    * Starting from OSDK 3.2.1, you no longer need to enter your drone version.
    * app_id: registered APP ID
    * enc_key: registered App Key 
    * serial_name: /dev/ttyTHS1 (default on Manifold)
    * baud_rate: 230400
3. Complete activation:
    * Turn on your aircraft and its remote controller (make sure they are paired)
    * Download the latest DJI GO application on your mobile device and sign in to your DJI developer account you created earlier
    * Run "roslaunch dji_sdk sdk_manifold.launch" to initiate activation command
    * Here is how your activation environment will look like:
![Activation Setup](../../images/common/activation_1.png)
    * Here is successful activation example:
![Activation Successful](../../images/ROS/ROSActivationSuccessful_1.png)


## How To Operate

Now, after completing activation process, you can start exploring our ROS examples or start working on your own application demo. 

Additionally, ROS functions can also be initiated from an iOS Mobile app that runs on your mobile device connected to the RC. This enables users to test the functions easily in the field. You can read about it [here](../../github-platform-docs/MobileOnboardSDK/Mobile-OSDK.html)

</br>

Whenever you develop your own ROS package, include the ``dji_drone.h`` from ``dji_sdk/include/dji_sdk`` into your package (there is also a python version ``dji_drone.py`` in ``dji_sdk/src``). Make sure to build and link your target package with DJI Onboard SDK library residing under ``dji_sdk_lib``.

## Examples

This is a communication example involving Simulator as part of the Assistant software.

* Connect your aircraft to the PC running Assistant software via USB cable
* Start Simulator
* On Manifold, launch core node (``roslaunch dji_sdk sdk_manifold.launch``) and the client node (``rosrun dji_sdk_demo dji_sdk_client``) in separate terminals
![ROS Communication](../../images/ROS/ROSExample.png)
* Via client node, send flight commands to the aircraft (see result in the simulator)</br>
![Simulator Take Off Mission](../../images/ROS/SimulatorTakeOff.png)

</br></br>
For further reading about Onboard SDK ROS, please refer to [ROS OSDK Additional Info](./whatToKnowI.html)
