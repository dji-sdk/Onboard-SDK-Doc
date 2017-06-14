---
title: Software Environment Setup Guide
date: 2017-06-01
version: 3.3
keywords: [hardware setup，M100 UART Connector, A3 UART Connector, N3 UART]
---

This guide details the software environment needed to work with the Onboard SDK. 

## All Platforms

#### Download the SDK and Required Tools

- <a href="https://github.com/dji-sdk/Onboard-SDK" target="_blank">Download</a> the onboard SDK repository from Github
- <a href="https://www.dji.com/product/matrice600/info#downloads" target="_blank">Download</a> the DJI PC Assistant 2 software for Windows/Mac
- <a href="http://www.dji.com/product/goapp" target="_blank">Download</a> the DJI GO App to your mobile device

#### Update Firmware

- Connect your computer to the Micro-USB port on the M100/600 or A3/N3. For the M210 (support coming soon!), use the USB-A to USB-A cable provided with the aircraft.
- Update your aircraft/flight controller with the latest released firmware. Please visit the [Compatibility Matrix](../appendix/versioning.html) to find out which SDK version your firmware supports.

#### Enable OSDK API

The OSDK API needs to be enabled to allow communication between the onboard computer and the aircraft or flight controller.

- With your aircraft/flight controller connected to your PC/Mac, launch DJI Assistant 2 and check the box marked `Enable API Control` on the `SDK` page.

![Enable API Control](../images/common/N1UI.png)

#### Onboard SDK Application Registration

- You must register as a developer with DJI and create an OSDK application ID and Key pair. Please go to <a href="https://developer.dji.com/register/" target="_blank">https://developer.dji.com/register/</a> to complete registration.

#### Flight Platform Activation

Each new vehicle or flight controller must be activated the first time it is used with an OSDK application. 

The OSDK provides APIs for this activation, and all OSDK samples implement the activation.


## Ubuntu Linux

##### Toolchain

To build standalone Linux applications based on the OSDK, you need:

* A supported C++ compiler - currently only GCC (Tested with gcc 4.8.1/5.3.1)
* A bash shell
* CMake >= 2.8
* A modern Linux distribution

To make sure your Linux environment is ready to run OSDK applications, follow the [Linux Platform Guide](../sample-doc/sample-setup.html#linux-oes) on the Sample Setup page and run a sample app.


## STM32

##### Toolchain Requirements
- Keil MDK > 5.22 (armcc 5.06)
- Windows PC to run Keil

##### Toolchain Setup

- Configure the USART3 port to a baudrate of 230400 in your sample app
- To download (flash) the App binary to the STM32 board, connect the PC to the STM32's "mini-USB" port.
- In order for Keil to build code for the target board, you need to use Keil's `Pack Installer` to install the latest STM32F4xx_DFP.2.x.x pack, as shown below.
- Alternatively, you can download manually from <a href="http://www.keil.com/dd2/Pack/" target="_blank">http://www.keil.com/dd2/Pack/</a> and import the downloaded file from Pack Installer.)

![Keil_PackInstall](../../images/STM32/STM32_Keil_PackInstall.png)

To make sure your STM32 environment is ready to run OSDK applications, follow the [STM32 Platform Guide](../sample-doc/sample-setup.html#stm32-oes) on the Sample Setup page and run a sample app.

## Linux with ROS

##### Software Requirements:

* Install C, C++ Compiler and Development Tools by installing ``build-essential``
* Install CMake 2.8.3 or newer
* <a href="http://wiki.ros.org/ROS/Tutorials/InstallingandConfiguringROSEnvironment">Install ROS and its dependencies</a>
* Operating System: Ubuntu 16.04 (x86/ARM)
* ROS version: ROS Kinetic

##### Toolchain Setup

* If you don't have a catkin workspace, create one as follows:
```
mkdir catkin_ws
cd catkin_ws
mkdir src
cd src
catkin_init_workspace
```

To make sure your ROS environment is ready to run OSDK applications, follow the [ROS Platform Guide](../sample-doc/sample-setup.html#ros-oes) on the Sample Setup page and run a sample app.