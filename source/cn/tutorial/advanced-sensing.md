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
>**说明：** 若开发者安装了OpenCV 库，则可通过`show_rgb`函数调用`cv::imshow()`接口显示解码后的RGB 图像。

* 3. 销毁线程    
调用`vehicle->advancedSensing->stopFPVCameraStream()` 接口，断开与相机的链接，销毁读取相机码流的线程。

#### 以回调函数的方式获取RGB 图像
通过回调函数的方式获取RGB 图像。
* 1. 创建获取相机码流的线程   
调用`vehicle->advancedSensing->startFPVCameraStream(&show_rgb, NULL)`接口，创建获取相机码流的线程，同时在该接口中注册回调函数`show_rgb`，用于处理接收到的码流。
* 2. 销毁线程     
调用`vehicle->advancedSensing->stopFPVCameraStream()`接口，断开与相机的连接，销毁读取相机码流的线程。     

## 使用获取相机H.264 码流的功能
#### 1. 控制应用程序获取相机H.264 码流
控制应用程序接收指定相机的H.264 码流。

```C++
switch (inputChar) {
  case 'a':
    vehicle->advancedSensing->startH264Stream(LiveView::OSDK_CAMERA_POSITION_FPV,
                                       liveViewSampleCb,
                                       (void *) "FPV.h264");
    break;
  case 'b':
    vehicle->advancedSensing->startH264Stream(LiveView::OSDK_CAMERA_POSITION_NO_1,
                                       liveViewSampleCb,
                                       (void *) "MainCam.h264");
    break;
  case 'c':
    vehicle->advancedSensing->startH264Stream(LiveView::OSDK_CAMERA_POSITION_NO_2,
                                       liveViewSampleCb,
                                       (void *) "ViceCam.h264");
    break;
  case 'd':
    vehicle->advancedSensing->startH264Stream(LiveView::OSDK_CAMERA_POSITION_NO_3,
                                       liveViewSampleCb,
                                       (void *) "TopCam.h264");
    break;
}
 
DSTATUS("Wait 10 second to record stream");
sleep(10);
 
switch (inputChar) {
  case 'a':
    vehicle->advancedSensing->stopH264Stream(LiveView::OSDK_CAMERA_POSITION_FPV);
    break;
  case 'b':
    vehicle->advancedSensing->stopH264Stream(LiveView::OSDK_CAMERA_POSITION_NO_1);
    break;
  case 'c':
    vehicle->advancedSensing->stopH264Stream(LiveView::OSDK_CAMERA_POSITION_NO_2);
    break;
  case 'd':
    vehicle->advancedSensing->stopH264Stream(LiveView::OSDK_CAMERA_POSITION_NO_3);
    break;
}
```

#### 2. 保存或处理H.264 码流
基于OSDK 开发的应用程序获取H.264 码流后，即可将获得的码流保存在机载计算机本地，文件名为`userData`，用户可对保存在机载计算机中的H.264 码流执行所需的操作。

```c++
void liveViewSampleCb(uint8_t* buf, int bufLen, void* userData) {
  if (userData) {
    const char *filename = (const char *) userData;
    writeStreamData(filename, buf, bufLen);
  } else {
  DERROR("userData is a null value (should be a file name to log h264 stream).");
  }
}
```

开发者获取指定相机的H.264 码流后，使用`ffplay FPV.h264`命令即可播放所获取的H.264 文件。

## 常见问题
#### 解码器解码时出现错误。
受计算平台算力的制约，基于OSDK 开发的应用程序在编解码时可能会出现如下问题：
* 解码速度较慢：解码器在解码第一帧时需要一段时间时间
* 帧丢失：计算平台算力不足
* 使用FFmpeg 解码时出现报错：请在Ubuntu 16.04 上尝试解码，且确认运行解码器的应用程序正确安装了RNDIS、USB及网口驱动，确保应用程序能够正确识别M210 系列和M300 RTK 的无人机。

## 适用产品
* Matrice 300 RTK 
* Matrice 210 V2 系列
