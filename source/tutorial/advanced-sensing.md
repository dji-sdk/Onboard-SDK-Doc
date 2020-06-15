---
title: Advanced Sensing
date: 2020-05-08
version: 4.0.0
keywords: [target identification, CNN]
---
> **NOTE** This article is **Machine-Translated**. If you have any questions about this article, please send an <a href="mailto:dev@dji.com">E-mail </a>to DJI, we will correct it in time. DJI appreciates your support and attention.     

## Overview
To help developers use automatic flight control in application scenarios without GPS or RTK satellites, use Precise Hovering and Obstacle Avoidance, DJI has opened the drone's visual perception system. Developers use API in OSDK can obtain the camera’s stream of the DJI drone's visual perception system, generate time-diff-maps and cloud-maps, combined with image recognition algorithms, developer could develop the applications that meet the specific needs.

> **NOTE**
> * Applications developed on Linux and ROS systems allow developers use DJI's advanced perception features.
> * When using the advanced perception function of DJI OSDK, developer need to use a USB cable to receive the raw image data from the drone's visual perception system.

## Concepts

### Camera‘s Stream
In order to satisfy the function of developers using OSDK to obtain the camera’s stream, OSDK provides the function to obtaining the camera’s stream, supports obtaining the FPV camera and main camera's H.264 tream and RGB images.

> **NOTE**
> * M210 series support H.264 bitstream or RGB images of FPV cameras and main cameras; M300 RTK **support H.264 bitstreams of FPV cameras and others cameras**.
> * The callback functions for obtaining the FPV camera's stream and obtaining the main camera's stream run in separate threads, OpenCV's module imshow only supports running in one thread, so developers are allowed to obtain FPV cameras or main camera's H.264 stream and RGB images.
> * After obtaining the camera’s stream, please install a decoder such as FFmpeg for decoding.
> * The details of the H.264 criterion please refer to <a href="https://www.itu.int/rec/T-REC-H.264-201906-I/en">H.264 Criterion</a>.

#### Resolution And Frame Rate
OSDK supports developers to obtain the main camera’s stream which on the M210 series and M300 RTK. Developers or users can mount different models of cameras and specified the frame rate, obtain the required code stream according the mode and module of the camera.
* Shut Mode:
  * FPV Camera code stream: support to obtain images with a resolution of 608x448.
  * Camera Mode: Support to obtain images with resolutions of 1440x1080 (1080p) and 960x720 (720p).
* Video Mode: Support to obtain videos with resolutions of 1920x1080 (1080p) and 1280x720 (720p).
> **NOTE** The frame rate of both FPV camera and main camera’s stream is 30 FPS.

#### Get H.264 Stream
The process of obtaining the H.264 stream of the camera on the M210 series and M300 RTK is as follows:
1. Before using the function of obtaining the camera H.264 stream, **Please implement the liveViewSampleCb` function**, which is used to obtain and process the camera H.264 stream.
2. Call the interface `startH264Stream ()` to specify the camera that the stream, the callback function, the H.264 stream and user's information needs to receive which from the camera;
3. Turn on the drone and onboard computer, run the application developed based on OSDK. At this time, the drone will push the H.264 stream to the onboard computer;
4. After received the data of the H.264 stream, onboard computer will trigger (as an input to the callback function set by the developer) an application which developed based on OSDK;
5. After obtaining the camera H.264 code stream, `liveViewSampleCb` which designed by developer will perform corresponding operations such as storage, decoding and forwarding works.

### Visual Perception System
The visual perception system of the DJI's drone is composed of the visual perception sensor and visual perception algorithm. During the flight of the drone, the perception sensor can obtain the state of the surrounding environment, assist drone to brake, avoid obstacle and accuracy hover.
* Matrice 210 V2 series only supports developers to obtain the code stream data of the drone's forward-looking sensor and downward-looking sensor;
* Matrice 300 RTK supports developers to obtain the bitstream data of all sensory sensors.

> **NOTE**
> * If the drone is disturbed by external interference during hovering, the drone will return to the original hovering point.
> * When using the stereo perception function, if the drone is disconnected from the drone remote control, the drone will hover.

##### Image Type
The image types that the stereoscopic perception function supports is as follows:
* M300 RTK: Support developers to obtain VGA grayscale images at 20 FPS and 640x480 resolution.
* M210 V2:
   * Forward-looking vision sensor: obtain VGA grayscale image at 10 FPS or 20 FPS, 640x480 resolution; obtain grayscale image at 20 FPS, 320x240 resolution; obtain disparity map at 10 FPS, 320x240 resolution.
   * Downward vision sensor: obtain QVGA grayscale image at 20 FPS, 320x240 resolution.

##### Metadata
The image generated by the drone's visual sensor contains two metadata: frame index and time stamp.
* Timestamp: The visual sensors on the drone share a timer at the same time, which is synchronized with the clock on the M210 V2 series drone. For details about time synchronization, please refer to [Time Synchronization](./synchronization.html).
* Frame Index: After subscribe the perception grayscale image, the drone's perception grayscale image will be accompanied by the frame index. Subscribing or unsubscribing to the perceptual grayscale image will not change or interrupt the frame index sequence number.

### Get The Image
When using Advanced Sensing functions, developers need to call the specified API to subscribe (or unsubscribe) the image of the camera through the USB during the application execution, and use the callback function **in the dedicated reading thread** to get subscribed images.

> **NOTE**
> * It is recommended to install OpenCV to display the image when acquiring the image of drone's vision sensor.
> * In order to blocking the main thread, please create a separate thread to process the image of the visual sensor of the drone.
> When using Advanced Sensing functions on the ROS system, please using `ROS services` and `image_view`to subscribe and display the image.

## Target Tracking
The following steps to use the KCFcpp library to achieve the Target Tracking.

> **NOTE**
> * When using the KCFcpp library to compile sample code for target tracking, please use the command `cmake -DADVANCED_SENSING=ON -DTARGET_TRACKING_SAMPLE=ON
make` to compile the program.
> * After entering g from the keyboard, developer can create a KCF tracker; enter s choose the object to track, ESC for exit.

#### 1. Specify The Target
In order to specify the target easily, OSDK provides the `TrackingUtility` class, which is used to obtain the target object and tracking status.

```c++
tracker = new KCFTracker (true, true, false, false);
tracker-> init (roi, frame);
```

#### 2. Get The Object
The target tracking algorithm calculates the distance based on the position of the image (unit: 1 px).

```c++
/* Get the object */
roi = tracker-> update (frame);
/* Calculates the distance */
dx = (int) (roi.x + roi.width / 2-mainImg.width / 2);
dy = (int) (roi.y + roi.height / 2-mainImg.height / 2);
```

#### 3. Calculate The Rotation
According to the moving state of the target object, calculate the yaw angle and pitch angle that the gimbal needs to change, and send the angle to `DJI::OSDK::Gimbal::SpeedData gimbalSpeed;`.

* 1 degree/second for 10 pixels
* If less than 10 pixels, the drone's gimbal will not rotate.

```c++
DJI :: OSDK :: Gimbal :: SpeedData gimbalSpeed;
gimbalSpeed.roll = 0;
gimbalSpeed.pitch = pitchRate;
gimbalSpeed.yaw = yawRate;
gimbalSpeed.gimbal_control_authority = 1;
vehicle-> gimbal-> setSpeed ​​(& gimbalSpeed);
```


## Get The RGB Image
#### Polling
Obtain RGB images by polling in the main thread.
* 1. Create the main thread     
Call the `vehicle-> advancedSensing-> startFPVCameraStream ()` interface to create a thread for reading the original code stream of the camera and decoding it into an image.

* 2. Check the stream status      
In the main loop, the developer needs to call the `vehicle-> advancedSensing-> newFPVCameraImageIsReady ()` interface to check the status of the camera’s stream. If there is a stream available in the camera, then call `vehicle-> advancedSensing-> getFPVCameraImage (fpvImage ) `Get the image.
> **NOTE** If the developer installs the OpenCV library, the `cv::imshow ()` interface can be called through the `show_rgb` function to display the RGB Image which decoded.

* 3. Destroy the thread     
Call the `vehicle-> advancedSensing-> stopFPVCameraStream ()` interface to disconnect the camera and destroy the thread that reads the camera code stream.

#### Callback
Get the RGB image through the callback function.
* 1. Create a thread to get the camera’s stream     
Call the `vehicle-> advancedSensing-> startFPVCameraStream (& show_rgb, NULL)` interface to create a thread to get the camera code stream, and register the callback function `show_rgb` in this interface to process the received code stream.
* 2. Destroy the thread    
Call the `vehicle-> advancedSensing-> stopFPVCameraStream ()` interface to disconnect from the camera and destroy the thread that reads the camera code stream.

## Get the H.264 Stream
#### 1. Start to get the camera H.264 stream  
Control the application to receive the H.264 stream of the specified camera.

```C++
LiveView::LiveViewErrCode startH264Stream(LiveView::LiveViewCameraPosition pos, H264Callback cb, void *userData);
```

#### 2. Stop getting the H.264 stream
Control the application stop getting the H.264 stream of the specified camera.

```c++
LiveView::LiveViewErrCode stopH264Stream(LiveView::LiveViewCameraPosition pos);
```

#### 3. Save or Process H.264 stream
After obtaining the H.264 stream, the application developed based on OSDK would option the H.264 stream for developer.

```c++
typedef void (*H264Callback)(uint8_t* buf, int bufLen, void* userData);
```

> **NOTE** 
> * After obtains the H.264 stream, developer could use `ffplay FPV.h264` to play the H.264 file which obtained.
> * Using the sample (djiosdk-liveview-sample)  offered by the OSDK, developer could obtain the h.264 stream and recorded as the H.264 file, which named 'userData'.    
> * Using Sample camera-stream-callback-sample and camera-stream-poll-sample. Developer could decode the H.264 stream and implement the required functionality.

#### Parsing
The developer can use Elecard StreamEye Tools, H264Visa and other H.264 decoding software to decode and analyze the H.264 stream obtained by OSDK.             
The following is the analysis result of the stream obtained by using Sample djiosdk-liveview-sample, the video is recorded in the room for 9~10 seconds.

<div>
<div style="text-align: center"><p>Table1.The analysis result of the H.264</p></div>
<table>
<thead>
<tr> 
  <th colspan="2" ></th>
   <th>M300 FPV</th>
   <th>M210 V2 FPV</th>
   <th>Z30</th>
   <th>XTS</th>
   <th colspan="1" >X7</th>
   <th colspan="1" >H20T</th>
  </tr>
  </thead>
<tbody>
 <tr> 
  <th colspan="2" ></th>
   <th>M300 FPV</th>
   <th>M210 V2 FPV</th>
   <th>Z30</th>
   <th>XTS</th>
   <th colspan="1" >X7</th>
   <th colspan="1" >H20T</th>
  </tr>
 <tr> 
     <td colspan="2" >Video Stream Type</td>
     <td>AVC/H.264</td>
     <td>AVC/H.264</td>
     <td>AVC/H.264</td>
     <td>AVC/H.264</td>
     <td>AVC/H.264</td>
     <td>AVC/H.264</td></tr>
 <tr> 
     <td colspan="2" >Resolution</td>
     <td>608 x 448</td>
     <td>608 x 448</td>
     <td>1280 x 720</td>
     <td>640 x 512</td>
     <td>1280 x 720</td>
     <td>1920 x 1080</td></tr>
 <tr> 
     <td colspan="2" >Profile</td>
     <td>Main:4.1</td>
     <td>Main:4.1</td>
     <td>Main:4.1</td>
     <td>High:5.0</td>
     <td>High:4.0</td>
     <td>High:4.0</td></tr>
 <tr> 
  <td colspan="2" >Aspect Ratio</td>
     <td>4 x 3</td>
     <td>4 x 3</td>
     <td>16 x 9</td>
     <td>5 x 4</td>
     <td>16 x 9</td>
     <td>16 x 9</td></tr>
 <tr> 
  <td colspan="2" >Interlaced</td>
     <td>No</td>
     <td>No</td>
     <td>No</td>
     <td>No</td>
     <td>No</td>
     <td>No</td></tr>
 <tr> 
  <td colspan="2" >File Size (Bytes)</td>
     <td>867619</td>
     <td>877819</td>
     <td>4559469</td>
     <td>5472872</td>
     <td>8765755</td>
     <td>17243162</td></tr>
 <tr> 
  <td colspan="2" >Frames Count</td>
     <td>271</td>
     <td>274</td>
     <td>300</td>
     <td>240</td>
     <td>294</td>
     <td>299</td></tr>
 <tr> 
  <td rowspan="3" >Frame Size</td>
     <td>Max</td>
     <td><p>5095</p></td>
     <td>5875</td>
     <td>34848</td>
     <td>53368</td>
     <td>45846</td>
     <td>71881</td></tr>
 <tr><td>Avg</td>
     <td>3201</td>
     <td>3203</td>
     <td>15198</td>
     <td>22803</td>
     <td>29815</td>
     <td>57669</td></tr>
 <tr><td>Min</td>
     <td>1990</td>
     <td>1456</td>
     <td>4164</td>
     <td>11025</td>
     <td>18532</td>
     <td>51506</td></tr>
 <tr> 
  <th rowspan="2" ><p>I Frame</p></th><td>Max</td>
     <td><p>4802</p></td>
     <td>4641</td>
     <td>0</td>
     <td>51729</td>
     <td>0</td>
     <td>0</td></tr>
 <tr><td>Avg</td>
     <td>4243</td>
     <td>4117</td>
     <td>0</td>
     <td>37054</td>
     <td>0</td>
     <td>0</td></tr>
 <tr> 
  <th rowspan="2" ><p>P Frame</p></th><td>Max</td>
     <td><p>5095</p></td>
     <td>5875</td>
     <td>34848</td>
     <td>53368</td>
     <td>45846</td>
     <td>71881</td></tr>
 <tr><td>Avg</td>
     <td>3177</td>
     <td>3183</td>
     <td>15198</td>
     <td>22312</td>
     <td>29815</td>
     <td>57669</td></tr>
 <tr> 
  <th rowspan="2" ><p>B Frame</p></th><td>Max</td>
     <td><p>0</p></td>
     <td>0</td>
     <td>0</td>
     <td>0</td>
     <td>0</td>
     <td>0</td></tr>
 <tr><td>AVG</td>
     <td>0</td>
     <td>0</td>
     <td>0</td>
     <td>0</td>
     <td>0</td>
     <td>0</td></tr>
 <tr> 
  <th rowspan="2" ><p>FrameRate</p></th><td>Declared</td>
     <td><p>30.00</p></td>
     <td>30.00</td>
     <td>0.00</td>
     <td>25.00</td>
     <td>25.00</td>
     <td>30.00</td></tr>
 <tr><td>Real</td>
     <td>30.00</td>
     <td>30.00</td>
     <td>30.00</td>
     <td>25.37</td>
     <td>25.39</td>
     <td>30.00</td></tr>
 <tr> 
  <th rowspan="3" ><p>BitRate (bit/s)</p></th><td>Max</td>
     <td>846960</td>
     <td>835680</td>
     <td>3988324</td>
     <td>5367808</td>
     <td>6789069</td>
     <td>14462654</td></tr>
 <tr><td>Avg</td>
     <td>768240</td>
     <td>768720</td>
     <td>3647523</td>
     <td>4628379</td>
     <td>6056010</td>
     <td>13840574</td></tr>
 <tr><td>Min</td>
     <td>731040</td>
     <td>709920</td>
     <td>3070083</td>
     <td>4179404</td>
     <td>5401762</td>
     <td>13307293</td></tr></tbody></table>
</div>

## FAQ
#### An error occurred while the decoder was decoding.
Restricted by the computing power of the computing platform, the applications developed based on OSDK may have the following problems when encoding and decoding:
* Slow decoding speed: the decoder takes a while to decode the first frame
* Frame loss: insufficient computing power on the computing platform
* An error occurs when decoding using FFmpeg: Please try to decode on Ubuntu 16.04, and make sure that the application running the decoder is correctly installed with RNDIS, US B and network port drivers to ensure that the application can correctly identify the M210 series and M300 RTK.

#### Unable to analyse the Z30's H.264 stream
Z30 adopts Main Profile technology and USES GDR encoding format, developers cannot decode the H.264 video stream of camera Z30 by FFMpeg decoding method by using the sample provided by OSDK, but according to the actual development environment, developers can choose other decoders such as hardware decoder or JM decoder to decode the H.264 stream of the Z30.  

## Products
* Matrice 300 RTK: Support Z30、XTS、XT2、H20、H20T and don't need use controller could get the video stream.
* Matrice 210 V2 Series: Only support mount X4S、X5S、X7、Z30、XTS、XT2、H20、H20T on the Gimbal I, and don't need use controller could get the video stream.
> **NOTE** OSDK doesn't support obtain and switch the camera images of the camera which has multiple light sources. If you want to switch it, please switch it on the DJI Pilot.