---
title: DJI Onboard SDK Command Line Example
version: v3.1.7 
date: 2016-07-01
github: https://github.com/dji-sdk/Onboard-SDK/tree/3.1/sample/commandline
keywords: [hotpoint mission]
---

## Introduction

This command line example is a frontend for the DJI Script C++ implementation of the Onboard API. DJI Script implements all the functionality exposed by the OPEN protocol in the form of callable *commands* that are designed to operate on strings passed at the command line. The script creates a linked list with *tasks* received from the commandline frontend, and securely implements the send functionality of the API. 

The command line example also implements threading and a hardware driver for the Onboard Embedded System (OES) of choice (currently any linux computer with a serial port).

With it you can run the following commands:

* Activation
* Obtain/Release Flight Control 
* Take Off 
* Landing 
* Go Home 
* Movement Control - Position/Attitude/Velocity
* Gimbal Control
* Camera Control
* Waypoint Task
* Hotpoint Task
* Follow Me Task

 > The command line example will soon be replaced entirely with the [new Linux](../Linux/README.html) example.

## Setup

### 1. Hardware

The [Hardware Setup](../../hardware-setup/index.html) guide talks about setting up your OES of choice. Make sure your setup matches that in the document before proceeding further. 

### 2. Software

**Toolchain**

To build the command line example, you need:

1. A supported C++ compiler (currently, only gcc/g++ 4.8.1 or older.*)
2. A bash shell
3. GNU Make

All of these should be available with an installation of Ubuntu 14.04.

*Newer versions of gcc/g++ also work - they generate compilation warnings, but these can safely be ignored. Future releases will correct this problem.*

**Compilation**

1. Set your serial port, baud rate, and drone/SDK version in `User_Config.h` inside the `sample/commandline/Linux/inc` directory.
2. Open up a terminal inside the `sample/commandline/Linux` directory and type `make` at the command prompt.
3. To access the serial port, add your username to the dialout group by typing `sudo usermod -a -G dialout $USER` (you do not need to replace $USER with your username). **Then logout and login again.**

**Using the Simulator**

1. Connect your M100/A3 to a PC through USB.
2. Open up DJI Assistant 2. Click on the DJI M100/A3 button. If this button doesn't show up, try disconnecting and reconnecting the USB.
3. Click on the Simulator tab, and then click on the 'Open' button. A separate window should pop up in a few seconds.
![Sim1](../../images/cmdline/Simulator_Open.png)
4. In the main window, click on 'Start Emulating'.
![Sim2](../../images/cmdline/Simulator_StartEmulating.png)

## Activation

The first time a drone/OES combination is used, it needs to be activated. Activation requires an App ID and a key got from the DJI website, and requires an internet connection and an RC connected to a mobile device running DJI GO. The image below shows the flow of information during activation:
![ActivationSetup](../../images/common/activation_1.png)

1. [Enable API control](../../quick-start/index.html#3-Enable-Flight-Controller-API-control) and [get an app ID and key](../../quick-start/index.html#5-Onboard-Application-Registration).
2. Navigate to `sample/commandline/Linux/key.txt` and enter your App ID and Key in place of the defaults in that file.
3. Navigate to the `sample/commandline/Linux/bin` folder and run the commandline example by typing `./onboardSDK`. 
    
    *Note: At this point, the commandline example will automatically attempt to activate your setup. If everything is setup as explained, you will see an 'Automatic Activation Successful' message. If you do, skip steps 4 and 5. You are done with activation!*
    ![Auto Activation](../../images/cmdline/Cmdline_autoActivate.png)

4. Once the example is running, type `--SS load ../key.txt`. Your App ID and Key should be displayed on the terminal.
![SS_Load](../../images/cmdline/Cmdline_ActivationStep1.png)

5. Next, type `--CA ac`. You should receive some feedback on the terminal. If the message says 'Activated Successfully', you are done. Else, follow the error message to debug.
![CA_Ac](../../images/cmdline/Cmdline_ActivationStep2.png)
![Activation_Successful](../../images/cmdline/Cmdline_ActivationSuccessful.png)

## Operation

Operating the Commandline example is a lot like the activation process you just went through. Here is a sample workflow for running some common tasks:

![Workflow](../../images/cmdline/Cmdline_Workflow.png)

Note that loading your key and performing the activation step is necessary each time. After the first time, the activation command merely performs a local activation check and you are not required to be connected to the internet.
The sample will attempt automatic activation each time it is started.

## Examples

#### Hotpoint Mission

Let us go through this workflow for a sample task of operating a hotpoint mission in simulation. Before you follow this example, make sure that (1) Your RC is powered on and (2) You are in simulation mode.

#### 1. Welcome Screen
In general, for running any single task you are presented with a screen that looks like this:
![HowToOperate](../../images/cmdline/Cmdline_HowToOperate1.png) 

#### 2. Activation

For the purposes of this example, assume that the automatic activation did not go through. Let us load the key and activate the device as in the activation section.
![Activation_Successful](../../images/cmdline/Cmdline_ActivationSuccessful.png)

#### 3. Obtain flight control.

![CA ct 1](../../images/cmdline/Cmdline_HP_2.png)

We type `--CA ct 1` to obtain control and `--CA ct 0` to release control. I this case, since we want to obtain control, we type `--CA ct 1`.

#### 4. Takeoff.

Once we have successfully obtained control, we proceed to takeoff. You should see the following message indicating that we have succeeded in taking off. 

![FC tk 4](../../images/cmdline/Cmdline_HP_4.png)
![FC tk 4](../../images/cmdline/Cmdline_HP_5.png)

The vehicle should hover at 1m in the simulation.

#### 5. Execute a hotpoint mission

Type `--help HP` to see syntax. Note that Lat, Lon are to be input in radians. In this exampe, we simply convert the Lat/Lon displayed in the simulator to radians and input that as location.

![HP success](../../images/cmdline/Cmdline_HP_6.png)

The aircraft should now be executing a hotpoint mission in simulation. When the mission is done, type `--HP stop` to exit hotpoint mode.

#### 6. Return to home and land

Similar to takeoff, type `--FC tk 1` to return home. `--FC tk 6` executes landing.

#### 7. Release Control

The `--CA ct 0` command will now allow you to release control.

> A3 support is currently in beta. Please file issues on the github repo if you find any!
