---
title: Advanced Sensing - Camera Stream Samples
date: 2017-12-19
version: 3.5
keywords: [sample, camera, stream, image, OpenCV]
---

## Introduction
The Advanced Sensing - Camera Stream samples demonstrate how to use the [camera stream APIs](../guides/component-guide-advanced-sensing-camera-stream.html) of the onboard SDK to access the image frames from the FPV camera and the main gimbaled camera (Zenmuse X4S, Zenmuse X5S).

To build the samples, follow the steps in [Sample Setup](./sample-setup.html) to build with Advanced Sensing support.

Two samples are provided here to demonstrate different ways of accessing and processing the camera images.

## Sample 1 Polling and Viewing Images in Main Loop

The source code of this sample is located in `onboardsdk/samples/linux/advanced-sensing/camera_stream_poll_sample/camera-stream-poll-sample.cpp`. After building the onboardsdk, from the `build` folder, you can run the sample with the following command.
```
bin/camera-stream-poll-sample UserConfig.txt
```
The sample will ask you to choose which camera images (FPV camera, main camera or both) you want to view. Note that you need to **turn on the RC** to be able to connect to the main camera. The sample code is pretty straight forward. After setting up the OSDK environment and obtain a pointer to vehicle, as all Linux samples do, it takes the following steps to access the camera images (taking FPV camera for example)

1. Call `vehicle->advancedSensing->startFPVCameraStream()` with empty input parameters. The OSDK will start a thread to read raw compressed data from and camera and decode to image frames.

2. In the main loop, call `vehicle->advancedSensing->newFPVCameraImageIsReady()` to check if a new frame is available. If so, call `vehicle->advancedSensing->getFPVCameraImage(fpvImage)` to get a copy of the image in the variable `fpvImage`. 

   The helper function `show_rgb` will call `cv::imshow()` to display the image if OpenCV is installed.

3. Before quitting the program, call `vehicle->advancedSensing->stopFPVCameraStream()` to disconnect from the camera and stop the camera reading thread.

## Sample 2 Accessing the Images with Callback Functions

The source code of this sample is located in `onboardsdk/samples/linux/advanced-sensing/camera_stream_poll_sample/camera-stream-callback-sample.cpp`. After building the onboardsdk, from the `build` folder, you can run the sample with the following command.
```
bin/camera-stream-callback-sample UserConfig.txt
```
In this sample, accessing the camera images takes only two steps (taking FPV camera for example).

1. Call `vehicle->advancedSensing->startFPVCameraStream(&show_rgb, NULL)`. 

   Note that different from sample \#1, we passed in a callback function `show_rgb` to the function. Then in addition to the camera reading thread, the OSDK will also create another callback thread, such that whenever a new image frame is ready, the callback function will be called automatically in that callback thread, to do the processing.
   
2. Before quitting the program, call `vehicle->advancedSensing->stopFPVCameraStream()` to disconnect from the camera and stop the camera reading thread and the callback thread.

Note that in this sample, you can either view the FPV camera image or the main camera image, but not both simultaneously. This is because the callback functions for FPV camera and main camera are running in their independent callback threads, and OpenCV's imshow cannot run in different threads. If in your programs, the callback functions do some other type of processing or use other multi-thread friendly library to view the image, then you can start both cameras with different callback functions.
