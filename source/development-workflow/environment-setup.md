---
title: Software Environment Setup Guide
date: 2017-06-01
version: 3.3
keywords: [hardware setup，M100 UART Connector, A3 UART Connector, N3 UART]
---

## Platform-independent Software Environment Setup

#### Download the SDK and Required Tools

- <a href="https://github.com/dji-sdk/Onboard-SDK" target="_blank">Download</a> the onboard SDK repository from Github
- <a href="https://www.dji.com/product/matrice600/info#downloads" target="_blank">Download</a> the DJI PC Assistant 2 software for Windows/Mac
- <a href="http://www.dji.com/product/goapp" target="_blank">Download</a> the DJI GO App to your mobile device

#### Update Firmware

- Connect your computer to the Micro-USB port on the M100/600 or A3/N3. For the M210, use the USB-A to USB-A cable provided with the aircraft.
- Update your aircraft/flight controller with the latest released firmware. Please visit the [Compatibility Matrix](@todo) to find out which SDK version your firmware supports.

#### Enable Flight Controller API control

- With your aircraft/flight controller connected to your PC/Mac, launch DJI Assistant 2 and check the box marked `Enable API Control` on the `SDK` page.

![Enable API Control](../images/common/N1UI.png)

#### Onboard SDK Application Registration

- You must register as a developer with DJI and create an OSDK application ID and Key pair. Please go to <a href="https://developer.dji.com/register/" target="_blank">https://developer.dji.com/register/</a> to complete registration.

#### Flight Platform Activation

Each new vehicle or flight controller must be activated with the DJI server on first SDK use to enable communication with your application.

- We provide APIs for activation.
- All samples implement activation, so if you are trying out a sample app it will automatically activate.

## Ubuntu Linux OES: Software Setup

##### Toolchain

To build standalone Linux applications based on the OSDK, you need:

* A supported C++ compiler (Tested with gcc 4.8.1/5.3.1)
* A bash shell
* CMake >= 2.8
* A modern Linux distribution

## STM32 OES: Software Setup


You'll need to use the <a href="http://developer.dji.com/onboard-sdk/downloads/" target="_blank">DJI Assistant 2 software</a> to set the baud rate of the M100's `UART_CAN2` port to **230400**, which is the one we use to configure USART3 in the example App.

To download (flash) the App binary to the STM32 board, connect the PC to the STM32's "mini-USB" port. To set the baud rate of the M100 or to run the simulator, connect the PC to the M100's "micro-USB" port.

##### Toolchain Setup

The example App is developed and tested with MDK-ARM Version 5.22 or later. In order for Keil to build code for the target board, you need to use Keil's `Pack Installer` to install the latest STM32F4xx_DFP.2.x.x pack, as shown below. (Alternatively, you can download manually from <a href="http://www.keil.com/dd2/Pack/" target="_blank">http://www.keil.com/dd2/Pack/</a> and import the downloaded file from Pack Installer.)

![Keil_PackInstall](../../images/STM32/STM32_Keil_PackInstall.png)


##### Serial Terminal Debugging

Set the baud rate of your serial terminal software (here we use the open-source <a href="http://realterm.sourceforge.net" target="_blank"> RealTerm </a>) to be **115200**, which is the one we use to configure USART2 in the example App. Configure the serial terminal to display the received information in Ascii mode and send commands in Hex mode.

![Realterm Setup](../../images/STM32/STM32_Realterm.png)

## Linux OES with ROS: Software Setup

##### Tested Environment:

* Operating System: Ubuntu 14.04, Manifold
* ROS version: ROS Indigo
> **Note:** Onboard SDK ROS has also been beta tested with Ubuntu Xenial 16.04LTS and ROS Kinetic Kame. We currently do not support `rosinstall` or `apt-get` for this configuration.
> **Note:** Onboard SDK ROS also supports N3 and A3 FW 1.5.0.0 and newer with OSDK 3.2.0. See [Notes](../../appendix/releaseNotes.html#notes-for-using-onboard-sdk-with-the-new-a3-v1-5-0-0-fw).

##### Software Requirements:

* Install C, C++ Compiler and Development Tools by installing ``build-essential``
* Install CMake 2.8.3 or newer
* <a href="http://wiki.ros.org/ROS/Tutorials/InstallingandConfiguringROSEnvironment">Install ROS and its dependencies</a>

##### Compilation:

1. Assuming you have ROS environment installed and configured, cd into your catkin workspace and run ``catkin_make``. Make sure the source code is in the `src` directory of your catkin workspace.
<br>OR</br>
2. Refer to our .travis.yml build script to install and configure ROS from scratch and then follow with running ``catkin_make`` from catkin workspace.

