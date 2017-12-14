---
title: Advanced Sensing - Target Tracking Sample
date: 2017-10-10
version: 3.4
keywords: [sample, camera, stereo, image, openCV, disparity, disparity, VGA, QVGA]
---

## Target Tracking with Main Camera and Gimbal

Assuming you have followed the [basic samples of camera stream](./advanced-sensing-camera-stream.html) to access the image frames from the cameras on M210, the target tracking sample is a full application demonstrating what we can do with the camera streams.

This sample will rotate the gimbal automatically to follow (point to) the object selected by the user from the main camera frame. The following image shows the result of an M210 tracking a Phantom 4 using onboard SDK. 

![M210_tracking_phantom4](../images/samples/target_tracking.gif)

The source code of this sample is located in `onboardsdk/samples/linux/advanced-sensing/camera_stream_target_tracking`. Since this sample depends on third a third party open-source library from github, it's not built by default. 
To build this sample, use the following command.
```
cmake -DADVANCED_SENSING=ON -DTARGET_TRACKING_SAMPLE=ON
make
```
After building the onboardsdk, from the `build` folder, you can run the sample with the following command.
```
bin/camera-stream-target-tracking UserConfig.txt
```

When the program starts, the main camera frame is displayed on screen. The user needs to use the mouse to select an object to be tracks and then press 'g'. Then the gimbal will move to point to that object, so that the object is in the center of the image. When the object moves, the gimbal will try to follow it. A line will be drawn to indicate the vector from the center of the object bounding box and the center of the image, when is the direction that the gimbal will move.

The target tracker library we are using is the [KCFcpp](https://github.com/joaofaro/KCFcpp), which implements the [Kernelized Correction Filter](http://www.robots.ox.ac.uk/~joao/circulant/). While this tracker works really well and fast based on our tests, the purpose of this sample is not to create a perfect tracking system, but to demonstrate how to use the image information from the main camera on the M210 as feedback and send gimbal control command as input to form a closed-loop system.

This sample use the polling method (sample \#1 in [camera stream samples](./advanced-sensing-camera-stream.html)) to get image from the main camera. To facilitate the user mouse and keyboard input, and maintain a simple state machine to keep track of the current status, we create a class `TrackingUtility`.

When the user select the object of interest by drawing a bounding box in the image and press 'g', a KCF Tracker is created:
```
tracker = new KCFTracker(true, true, false, false);
tracker->init(roi, frame);
```
After that, every time a new frame is grabbed, we run the tracking algorithm to obtain a new bounding box of the object
```
roi = tracker->update(frame);
```
And we calculate the distance in pixels between the center of the bounding box and the center of the image.
```
dx = (int)(roi.x + roi.width/2  - mainImg.width/2);
dy = (int)(roi.y + roi.height/2 - mainImg.height/2);
```
Based on the distance, we calculate the yaw rate and pitch rate of the gimbal with a simple linear relationship: 10 pixels of difference will be translated to 1 deg/s rotation speed set-point. To avoid gittering when the object is near the center of the image, we introduce a dead zone such that when distance is less than 10 pixels, we set the rotation speed to 0. After that, we send the gimbal speed set point with:
```
DJI::OSDK::Gimbal::SpeedData gimbalSpeed;
gimbalSpeed.roll     = 0;
gimbalSpeed.pitch    = pitchRate;
gimbalSpeed.yaw      = yawRate;
gimbalSpeed.gimbal_control_authority = 1;
vehicle->gimbal->setSpeed(&gimbalSpeed);
```

To stop the tracking and select a new object to track, press 's'. To quit the program, press the ESC key.

