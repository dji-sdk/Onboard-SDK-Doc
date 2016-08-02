---
title: DJI Onboard SDK C++ Linux Example
version: v3.1.8 
date: 2016-08-05
github: https://github.com/dji-sdk/Onboard-SDK/tree/3.1/sample/Linux
---

  > All-new example for DJI Onboard SDK v3.1.8!

## Introduction

The new C++ Linux example is meant to showcase recommended application-layer usage of the DJI Onboard API. This example eases a new developer into the world of programming for drones - many API functions have been wrapped in easy-to-use implementations and a feedback mechanism is implemented so the developer always knows the result of his/her commands. Packaged with the new example is a new pthread-based threading implementation as well as an efficient serial device driver that implements many checks (on x86 systems) to ensure reliable communication between your OES and your drone.   


The following user-facing functionality is available in the new Linux sample: 

* Activation
* Obtain/Release Flight Control 
* Take Off 
* Landing 
* Go Home 
* Movement Control - Position/Attitude/Velocity control modes
* Waypoint Functionality
* Compatible with brand new iOS Mobile OSDK App
* Sample Waypoint Mission implementation
* Sample Position Control implementation

The example is extensible - if you want to build additional functionality, it is easy to do so within the framework of this example.  

---
## Setup

##### 1. Hardware

The [Hardware Setup](../../hardware-setup/index.html) guide talks about setting up your OES of choice. Make sure your setup matches that in the document before proceeding further. 

##### 2. Software

**Toolchain**

To build the command line example, you need:

* A supported C++ compiler (Tested with gcc 4.8.1/5.3.1)
* A bash shell
* GNU Make

All of these should be available with an installation of Ubuntu 14.04/16.04.

**Compilation**

* First, we need to create the directories `objs` and `bin` inside the `sample/Linux` directory. To do this, open up a terminal inside the `sample/Linux` directory and type `mkdir bin; mkdir objs` at the command line. 
* Next, type `make` at the command prompt.
* To access the serial port, add your username to the dialout group by typing `sudo usermod -a -G dialout $USER` (you do not need to replace $USER with your username). **Then logout and login again.**  

**Using the Simulator**

* Connect your M100/A3 to a PC through USB.
* Open up DJI Assistant 2. Click on the DJI M100/A3 button. If this button doesn't show up, try disconnecting and reconnecting the USB.
* Click on the Simulator tab, and then click on the 'Open' button. A separate window should pop up in a few seconds.
![Sim1](../../images/Linux/Simulator_Open.png)
* In the main window, click on 'Start Emulating'.
![Sim2](../../images/Linux/Simulator_StartEmulating.png)

---
## Activation

The first time a drone/OES combination is used, it needs to be activated. Activation requires an App ID and a key got from the DJI website, and requires an internet connection and an RC connected to a mobile device running DJI GO. The image below shows the flow of information during activation:
![ActivationSetup](../../images/common/activation_1.png)

1. [Enable API control](../../quick-start/index.html#3-Enable-Flight-Controller-API-control) and [get an app ID and key](../../quick-start/index.html#5-Onboard-Application-Registration).
2. Navigate to `sample/Linux/UserConfig.txt` and enter your App ID and Key in place of the defaults in that file.
3. Proceed to the instructions under [Operation](#Operation)

---
## Operation

To run the Linux sample, follow these steps:

* Navigate to `sample/Linux/UserConfig.txt` and enter your serial port in the `DeviceName` and baud rate in the `BaudRate` field.  
    * The default baudrate is `230400`. If you change this, remember to also change it in DJI Assistant 2.  
    * The default port is `/dev/ttyUSB0`. This should be correct if you are using a USB-Serial adapter. On Manifold, you will be using `/dev/ttyTHSx` (x = 0,1,2) - refer to the [Hardware Setup Guide](../../hardware-setup/index.html) for more information.   
* In the `sample/Linux/` folder, assuming you have already executed `make`, run `bin/onboardSDK mode_of_operation` where `mode_of_operation` can be (more information about the modes [here](#modes-of-operation)):  
    * `-interactive` : Recommended mode for new developers. Shows a basic terminal UI and users can execute single commands with key presses.  
    * `-mobile` : Use with the brand new Mobile OSDK App. Useful for mobile-based triggering of OSDK commands with keys on iOS device.  
    * `-programmatic` : Use for automated execution. By default, the sample will first takeoff, then execute a waypoint mission, then automatically land and exit.
* Proceed to run the sample in one of these modes. Before the sample enters one of the three modes, it will attempt to activate the drone and obtain control. If everything goes well, you should see the following information on the terminal:

    ![Activate_TakeControl](../../images/Linux/AllGood.png)

> Note that the activation step is necessary each time. After the first time, the activation command merely performs a local activation check and you are not required to be connected to the internet.  
The sample will attempt automatic activation each time it is started.

#### Workflow

![Workflow](../../images/Linux/OSDK_Workflow.png)

## Modes of Operation  

##### Interactive Mode 

The interactive mode is meant to give you a taste of the kinds of things you can do with the DJI Onboard SDK. The UI looks similar to the old [Commandline](../commandline/README.html) sample, but is easier to operate. The UI looks like this:

![Interactive_1](../../images/Linux/Interactive_1.png)

As the UI tells us, the sample has already activated and taken control on our behalf. Let's try the takeoff command - to do so, press `e` and then hit the enter key.

![Interactive_2](../../images/Linux/Interactive_2.png)

Once you have taken off, you may try some of the flight control functionality. After you have landed, type the exit letter - `j` - to let the sample clean up before exiting.

![Interactive_3](../../images/Linux/Interactive_3.png)


##### Mobile Mode 

The mobile mode is especially useful when you want to test out functionality on the Onboard SDK in a staged or interactive manner - simply make your code poll for commands from the companion mobile app and execute your mission/task/commands based on the mobile command sent. The mobile link is set up through DJI's Onboard SDk <--> Mobile SDK Data Transparent Transmission functionality. The mobile app is iOS only for now and can be downloaded [here](http://repo-not-yet-set-up).

When you run the program in mobile mode, you can see a simple message after the standard initialization: 

![Mobile_1](../../images/Linux/Mobile_1.png)

The mobile mode listens to mobile commands for 15 minutes before exiting.

##### Programmatic Mode

This is the most powerful mode of the new Linux sample - you can implement a complex, custom mission involving local navigation, trajectory following and waypoints using the programmatic mode. Together with [core API calls](../../application-development-guides/programming-guide.html), you can add hotpoint missions, automated picture and video to your automated program in this mode.

By default, the programmatic mode starts with automated, monitored takeoff (checks to see if takeoff actually executed, as well as how stable the takeoff is). Users can enter their own core API calls or Linux-sample calls after the takeoff returns and before landing is called. Here is the relevant code in `main.cpp`:

![Programmatic_code](../../images/Linux/programmatic-code.png)   

Line `97` is an example of an application layer function called within the programmatic mode. 

The result of this code is something like this:

![Programmatic result](../../images/Linux/Programmatic_1.png)



## Examples

The new Linux Application comes with two examples you can call through Interactive, Mobile or Programmatic mode:  

#### 1. Waypoint Mission Example

This example takes your current position (lat, lon, alt) and traces out a square of side 20 m. It will go north, then east, then south, and then west; if you are unaware of where your aircraft is pointing then **make sure to leave a clearing of 20m in all directions** when you try this example.

To try out the sample:   
* In interactive mode, first takeoff with the `e` key and then try the waypoint sample with the `f` key.
* In mobile mode, first takeoff from the `Core Functions` tab. Then go to the `Custom Missions` tab and choose `Waypoint Mission Test`.
* In programmatic mode, call `wayPointMissionExample` after calling `monitoredTakeoff`. 

The output looks like this (takeoff - waypoint test - landing):

![Waypoint_Simulator](../../images/Linux/waypointGndView.png)

#### 2. Draw a Square : Position Control Example.

The Position control example shows how to execute custom trajectories in local coordinates, useful for planning in a local space, executing complex trajectories and for use in GPS denied environments (with [DJI Guidance](https://store.dji.com/) or [Velodyne Puck](https://velodynelidar.com), for example) This example builds on the movement control functionality offered by the core API and adds a very simple receding setpoint algorithm to maintain constant speed. This sample will draw a square of side 10m and then proceed to draw two diagonals. First, the drone ascends 10 m from its current location. Then, it first moves right, then forward, then left, and backwards to its starting point. Then it will draw a diagonal at +45 degrees, go left along the side of the square, and draw the other diagonal at -45 degrees. **Leave a clearing of 10m around the drone before trying this example.**

The implementation of this example in `LinuxFlight.cpp` can serve as a great reference for any custom patterns you might want to draw.

To try out the sample:
* In interactive mode, first takeoff with the `e` key and then try the Draw a Square sample with the `g` key.
* In mobile mode, first takeoff from the `Core Functions` tab. Then go to the `Custom Missions` tab and choose `Draw a Square`.  
* In programmatic mode, call `drawSqrPosCtrlSample` after calling `monitoredTakeoff`. 

The output looks like this:

> A3 support is currently in beta. Please file issues on the github repo if you find any!
