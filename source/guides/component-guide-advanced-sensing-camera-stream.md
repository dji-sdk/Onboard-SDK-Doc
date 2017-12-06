---
title: Advanced Sensing - Camera Video Stream
date: 2017-12-06
keywords: [main camera, fpv camera, RGB, FFmpeg]
---

## Introduction

**On DJI Matrice 210** (M210), the Onboard SDK has access to the live camera stream from both the fpv camera and the main camera (the one mounted on the gimbal). This is part of the Advanced Sensing feature. As a result, in addition to viewing the live video frame from the DJI Go App, developers can write powerful onboard applications that read the image frames from the cameras, process and analyze them and take actions (such as rotate the gimbal or move the drone) if necessary.

The camera stream data is transmitted through the USB connection between the M210 and the onboard computer, same as the stereo vision data. The **RC must be turned on** for the main camera stream to be transmitted, while the FPV camera stream is always available.

## APIs to use the camera stream feature

The Advanced Sensing library provides a set of simple APIs for developers to start, stop the camera streams, and check availability and obtain a copy of the latest image frame, for both the FPV camera and the main camera, listed as follows
```
  bool startFPVCameraStream(DECODECALLBACK cb = NULL, void * cbParam = NULL);
  bool startMainCameraStream(DECODECALLBACK cb = NULL, void * cbParam = NULL);

  void stopFPVCameraStream();
  void stopMainCameraStream();

  bool newFPVCameraImageIsReady();
  bool newMainCameraImageReady();

  bool getFPVCameraImage(CameraRGBImage& copyOfImage);
  bool getMainCameraImage(CameraRGBImage& copyOfImage);
```
Through the above APIs, developers have 2 ways to access the images
1. If developers provide a callback function for a camera stream, then that function will be called automatically in an independent thread when a new frame is available. 
2. Otherwise, developers can obtain a copy of the image by polling in the main thread.

For details of the APIs, please refer to the API Ref and the samples. 

## Supported cameras, Resolution and Frame Rates

Different cameras can be mounted on the gimbal of the M210. The Onboard SDK can get main camera stream from the Zenmuse X4S and Zenmuse X5S.

The images from the FPV camera stream are 608x448. The images from the main camera stream is 1280x720 when the live stream is set to video mode in DJI Go App, or 960x720 when in camera mode. The resolution of  the main camera stream is the same regardless which camera is mounted to the gimbal.

The frame rates for both FPV camera stream and the main camera stream are 30 FPS.

## Limitations
Under the hood, the data transmitted from the M210 to the onboard computer is compressed video stream at 30 fps. The onboard SDK uses FFmpeg to decode the video stream and outputs each decoded image frame. As a result, 
1. It takes a little time, around 1 second, for the decoder to decode the first frame. Developers will see some error messages spit out by FFmpeg.
2. There is a small delay in the image frames due to the encoding/transmission/decoding procedure.
3. Depending on the computing power and the image processing running, drop of frame may happen.

