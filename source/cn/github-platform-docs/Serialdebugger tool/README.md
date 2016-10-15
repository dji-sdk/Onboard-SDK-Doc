---
title: DJI Onboard SDK Serial Port Debugger 
date: 2016-06-24
keywords: [serial port debugger]
---

## Intro

As finding a serialport debugger which support baudrate 921600 and 230400 is a difficult work,
we provide a simple debugger. 

## Compile & Run Environment

The below environment are required.
* Qt Ver: QT 5.4 or later
* Compiler Ver: MinGW 4.9.2 or later; MSVC2012 or later

## Config and compile

1. Open *V1Viewer.pro* locates at *tools/serialportDebugger*.

2. Select a proper compiler and click *Configure Project* to proceed.

3. During the init process, enter the following info into the GUI interface including:

* uart device name (e.g. COM1, COM2)
* baudrate

>Note: the 'baudrate' needs to be consistent with the setting in the DJI N1 PC assistant.
