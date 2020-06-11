---
title: 高级感知功能
date: 2020-05-08
version: 4.0.0
keywords: [目标识别, CNN]
---
## 概述
为帮助开发者在没有GPS 或RTK 卫星等应用场景中实现无人机的自动化飞行控制，实现如精准悬停和避障等功能，DJI 开放了无人机视觉感知系统，开发者通过使用OSDK 提供的API 即可获取DJI 无人机视觉感知系统的码流数据，并生成时差图以及点云图，结合图像识别算法，开发出满足特定使用场景需求的应用程序。

> **说明**
> * 仅使用Linux 和ROS 系统开发的应用程序支持开发者使用DJI 的高级感知功能。
> * 使用DJI OSDK 的高级感知功能时，需使用USB 线接收无人机视觉感知系统的原始图像数据。

## 基础概念

### 相机码流
为满足开发者使用OSDK 开发的应用程序对获取相机码流的功能，OSDK 提供了获取相机码流的功能，支持获取FPV 相机或获取I 号云台相机H.264 码流和RGB 图像。

> **说明**
> * M210 系列无人机支持获取FPV 相机和I 号云台上相机的H.264 码流或RGB 图像；M300 RTK 无人机**支持获取FPV 相机和所有云台相机的H.264 码流**。
> * 由于获取FPV 相机码流和获取I 号云台上相机码流的回调函数在各自独立的线程中运行，OpenCV 的imshow 模块仅支持在一个线程中运行，因此仅支持开发者获取FPV 相机或获取I 号云台相机H.264 码流和RGB 图像。
> * 获取相机码流后，请安装FFmpeg 等解码器解码。
> * 有关H.264 标准码流的相关参考请参见<a href="https://www.itu.int/rec/T-REC-H.264-201906-I/en">H.264 码流标准</a> 。

#### 分辨率和帧频
OSDK 支持开发者获取M210 系列和M300 RTK 无人机上I 号云台上相机的码流，开发者或用户可根据实际的使用需求挂载不同型号的相机，根据相机的型号以及相机的工作模式，指定帧速率，获取所需的码流。
* 拍照模式：
  * FPV 相机码流：支持获取分辨率为608x448 的图像。   
  * 相机模式：支持获取分辨率为1440x1080（1080p）、960x720（720p）的图像。   
* 视频模式：支持获取分辨率为1920x1080（1080p）、1280x720（720p）的视频。    
> **说明：** 获取FPV 相机和主相机码流的帧速率均为30 FPS。

#### 相机H.264 码流
获取M210 系列和M300 RTK 无人机上相机H.264 码流的流程如下所示：   
1. 使用获取相机H.264 码流的功能前，**请开发者根据实际的使用需要先实现**`liveViewSampleCb`函数，用于获取并处理相机H.264 码流。   
2. 调用`startH264Stream()`接口，指定所需获取码流的相机、接收相机H.264 码流的回调函数和用户信息；    
3. 开启无人机和机载计算机，运行使用基于OSDK 开发的应用程序，此时无人机将会向机载计算机推送H.264 码流；    
4. 机载计算机接收到H.264 码流的数据后，将触发（作为入参传入开发者设置的回调函数中）基于OSDK 开发的应用程序；    
5. **开发者根据实际需求设计的函数**`liveViewSampleCb`在获取相机H.264 码流后，将对所获得的H.264 码流执行存储、解码及转发等相应的操作。   

### 无人机视觉感知系统
DJI 无人机的视觉感知系统主要由无人机视感知传感器和视觉感知算法构成，在无人机飞行的过程中，感知传感器能够获取周围环境的状态，协助无人机刹车、避障和精确悬停。
* Matrice 210 V2 系列无人机仅支持开发者获取无人机前视感知传感器和下视感知传感器的码流数据；
* Matrice 300 RTK 支持开发者获取无人机上所有感知传感器的码流数据。

> **说明** 
> * 在悬停期间若无人机受到外部干扰，无人机将会返回到原悬停点。
> * 使用立体感知功能时，若无人机与无人机遥控器断开连接，无人机将会悬停。

##### 图像类型
立体感知功能支持开发者获取的图像类型和分辨率如下所示：
* M300 RTK：支持开发者以20 FPS，640x480 的分辨率，获取VGA 灰度图像。
* M210 V2：
   * 前视视觉传感器：以10 FPS 或20 FPS，640x480 的分辨率，获取VGA 灰度图像；以20 FPS，320x240的分辨率获取灰度图像；以10 FPS，320x240 的分辨率获取视差图。
   * 下视视觉传感器：以20 FPS，320x240 的分辨率获取QVGA 灰度图。

##### 元数据
无人机视觉传感器产生的图像主要包含帧索引和时间戳两种元数据。
* 时间戳：无人机上的视觉传感器同时共享一个计时器，该计时器与M210 V2 系列无人机上的时钟同步，有关时间同步的详细说明请参见[时间同步](../tutorial/synchronization.html)。
* 帧索引：开发者订阅感知灰度图后，无人机感知灰度图将会附带帧索引。订阅或取消订阅感知灰度图，将不会改变或中断帧索引的序号。


### 获取无人机的图像
使用高级视觉功能时，开发者需要调用指定的API 通过USB 接口在应用程序运行的周期内订阅（或退订）相机视觉传感器的图像，并使用回调函数**在专用的读取线程内**获取订阅的图像。
> **说明**
> * 获取无人机视觉传感器图像时，建议安装OpenCV 以显示图像。
> * 为避免处理视觉传感器图像的工作阻塞主线程，请创建一个独立的线程处理无人机视觉传感器的图像。
> 在ROS 系统上使用高级视觉功能时，请使用`ROS services`订阅并通过`image_view`显示视觉传感器的图像。   

## 使用目标跟踪功能
下文以使用KCFcpp 库实现目标跟踪功能的步骤，介绍使用DJI 无人机视觉传感器或相机的图像数据，控制云台的流程和方法，开发者可在合法的使用范围内使用第三方库开发出更为完善的应用程序。

> **说明** 
> * 使用KCFcpp 库编译目标跟踪的示例代码时，请使用命令 `cmake -DADVANCED_SENSING=ON -DTARGET_TRACKING_SAMPLE=ON  
make` 编译该程序。
> * 从键盘中输入g 后，即可创建KCF跟踪器；选择跟踪新的对象时请输入s，如需退出该程序，请按ESC 键。
#### 1. 指定跟踪目标
为了方便用户指定所需跟踪的目标，OSDK 提供了`TrackingUtility`类，用于获取目标对象和跟踪状态。

```c++
tracker = new KCFTracker(true, true, false, false);
tracker->init(roi, frame);
```

#### 2. 获取目标对象 
目标跟踪算法根据视觉传感器或相机每一帧的图像，确定目标图像的位置并计算目标对象移动的距离（单位：1 px）。
```c++
/*获取目标对象*/
roi = tracker->update(frame);
/*确定目标对象移动的位置*/
dx = (int)(roi.x + roi.width/2  - mainImg.width/2);
dy = (int)(roi.y + roi.height/2 - mainImg.height/2);
```

#### 3. 计算云台转动角度
根据目标对象移动的状态，计算云台所需改变的偏航角度和俯仰角度，并将该角度发送给`DJI::OSDK::Gimbal::SpeedData gimbalSpeed;
`。
* 目标对象每变化10个像素的位置，无人机云台转动1度/秒。
* 若目标对象变动的距离小于10像素，无人机的云台将不会转动。      

```c++
DJI::OSDK::Gimbal::SpeedData gimbalSpeed;
gimbalSpeed.roll     = 0;
gimbalSpeed.pitch    = pitchRate;
gimbalSpeed.yaw      = yawRate;
gimbalSpeed.gimbal_control_authority = 1;
vehicle->gimbal->setSpeed(&gimbalSpeed);
```


## 使用获取相机RGB 图像的功能
#### 以轮询的方式获取RGB 图像
在主线程中以轮询的方式获取RGB 图像。
* 1. 创建主线程
调用`vehicle->advancedSensing->startFPVCameraStream()`接口创建一个线程，用于读取相机原始的码流并解码成图像。

* 2. 检查码流状态    
开发者在主循环中，需调用`vehicle->advancedSensing->newFPVCameraImageIsReady()`接口，检查相机码流的状态，若相机中有可用的码流，则调用`vehicle->advancedSensing->getFPVCameraImage(fpvImage)` 获取该图像。
> **说明：** 若开发者安装了OpenCV 库，则可通过`show_rgb`函数调用`cv::imshow()`接口显示解码后的RGB 图像。

* 3. 销毁线程    
调用`vehicle->advancedSensing->stopFPVCameraStream()` 接口，断开与相机的链接，销毁读取相机码流的线程。

#### 以回调函数的方式获取RGB 图像
通过回调函数的方式获取RGB 图像。
* 1. 创建获取相机码流的线程   
调用`vehicle->advancedSensing->startFPVCameraStream(&show_rgb, NULL)`接口，创建获取相机码流的线程，同时在该接口中注册回调函数`show_rgb`，用于处理接收到的码流。
* 2. 销毁线程     
调用`vehicle->advancedSensing->stopFPVCameraStream()`接口，断开与相机的连接，销毁读取相机码流的线程。     

## 使用获取相机H.264 码流的功能
#### 1. 开始获取相机H.264 码流
控制应用程序接收指定相机的H.264 码流。

```C++
LiveView::LiveViewErrCode startH264Stream(LiveView::LiveViewCameraPosition pos, H264Callback cb, void *userData);
```
#### 2. 停止获取H.264 码流
控制应用程序停止接收相机的H.264 码流。

```c++
LiveView::LiveViewErrCode stopH264Stream(LiveView::LiveViewCameraPosition pos);
```

#### 3. 保存或处理H.264 码流
基于OSDK 开发的应用程序获取H.264 码流后，开发者即可对所获取的H.264 码流执行所需的操作。

```c++
typedef void (*H264Callback)(uint8_t* buf, int bufLen, void* userData);
```

> **说明** 
> * 开发者获取指定相机的H.264 码流后，使用`ffplay FPV.h264`命令即可播放所获取的H.264 文件。   
> * 借助OSDK 提供的Sample (djiosdk-liveview-sample) 获取H.264 码流数据，并将接收到的H.264 码流数据以H.264 文件的形式记录在本地，该文件名为`userData`。
> * 使用Sample camera-stream-callback-sample和camera-stream-poll-sample 可借助FFMpeg 对H.264 码流解码。开发者可借助Sample 实现所需的功能。

#### H.264 码流解析
开发者使用Elecard StreamEye Tools，H264Visa等H.264 解码软件，即可解码和分析使用OSDK 获取的H.264 码流，如下为使用Sample djiosdk-liveview-sample 获取DJI 无人机上相机码流的分析结果，该视频均在室内录制，时长为9~10秒。

<div>
<div style="text-align: center"><p>表1.相机H.264 码流分析结果</p></div>
<table>
<tbody>
 <tr> 
  <th colspan="2" ><br></th><th>M300 FPV</th><th>M210 V2 FPV</th><th>Z30</th><th>XTS</th><th colspan="1" >X7</th><th colspan="1" >H20T</th></tr>
 <tr> 
  <th colspan="2" >Video Stream Type</th><td>AVC/H.264</td>
     <td>AVC/H.264</td>
     <td>AVC/H.264</td>
     <td>AVC/H.264</td>
     <td>AVC/H.264</td>
     <td>AVC/H.264</td></tr>
 <tr> 
  <th colspan="2" >Resolution</th><td>608 x 448</td>
     <td>608 x 448</td>
     <td>1280 x 720</td>
     <td>640 x 512</td>
     <td>1280 x 720</td>
     <td>1920 x 1080</td></tr>
 <tr> 
  <th colspan="2" >Profile</th><td>Main:4.1</td>
     <td>Main:4.1</td>
     <td>Main:4.1</td>
     <td>High:5.0</td>
     <td>High:4.0</td>
     <td>High:4.0</td></tr>
 <tr> 
  <th colspan="2" >Aspect Ratio</th><td>4 x 3</td>
     <td>4 x 3</td>
     <td>16 x 9</td>
     <td>5 x 4</td>
     <td>16 x 9</td>
     <td>16 x 9</td></tr>
 <tr> 
  <th colspan="2" >Interlaced</th><td>No</td>
     <td>No</td>
     <td>No</td>
     <td>No</td>
     <td>No</td>
     <td>No</td></tr>
 <tr> 
  <th colspan="2" >File Size (Bytes)</th><td>867619</td>
     <td>877819</td>
     <td>4559469</td>
     <td>5472872</td>
     <td>8765755</td>
     <td>17243162</td></tr>
 <tr> 
  <th colspan="2" >Frames Count</th><td>271</td>
     <td>274</td>
     <td>300</td>
     <td>240</td>
     <td>294</td>
     <td>299</td></tr>
 <tr> 
  <th rowspan="3" ><p>Frame Size</p></th><td>Max</td>
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


## 常见问题
#### 解码器解码时出现错误。
受计算平台算力的制约，基于OSDK 开发的应用程序在编解码时可能会出现如下问题：
* 解码速度较慢：解码器在解码第一帧时需要一段时间时间
* 帧丢失：计算平台算力不足
* 使用FFmpeg 解码时出现报错：请在Ubuntu 16.04 上尝试解码，且确认运行解码器的应用程序正确安装了RNDIS、USB及网口驱动，确保应用程序能够正确识别M210 系列和M300 RTK 的无人机。

#### 无法解析相机Z30 的H.264 码流数据 
由于Z30 采用Main Profile技术，使用GDR 编码格式，因此开发者使用OSDK 提供的Sample，无法通过FFMpeg 解码方式解码相机Z30 的H.264 视频流，但开发者可根据实际的开发环境选用其他解码器，如硬件解码器或JM 解码器等对相机Z30 的H.264 码流数据解码。

## 适用产品
* Matrice 300 RTK：支持挂载Z30、XTS、XT2、H20、H20T（开发者无需使用遥控器即可获取视频流）
* Matrice 210 V2 系列：仅支持在主云台上挂载X4S、X5S、X7、Z30、XTS、XT2、H20、H20T （开发者无需使用遥控器即可获取视频流）
> **说明：** OSDK暂不支持同时获取和切换支持多种光源的相机的图像，如需切换，请在DJI Pilot 中设置切换相机的图像。
