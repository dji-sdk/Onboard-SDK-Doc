---
title: 配置开发环境
date: 2020-05-08
version: 4.0.0
keywords: [环境搭建, 配置开发环境, OSDK 开发环境]
---

## 获取基础软件

* [DJI Assistant 2](https://www.dji.com/cn/downloads)
* [DJI Pilot](https://www.dji.com/cn/downloads)
* [Onboard SDK 软件开发工具包](https://github.com/dji-sdk/Onboard-SDK)
* [Mobile SDK 软件开发工具包](https://developer.dji.com/user)  （可选）

## 配置Linux 开发环境
> **说明：** 如下安装步骤以在Manifold 2 为例，介绍配置使用OSDK 开发应用程序的开发环境的步骤。

#### 1. 安装开发工具     
  * C++ 编译器：GCC 5.4.0/5.5.0 版本
  * CMake：2.8 及以上版本
  * Linux：Ubuntu 16.04 (如需要使用高级传感功能，请使用Libusb库)

#### 2. 添加UART 读写权限     
请按如下步骤为Linux 中指定的用户添加UART 读写权限：
  1. 使用`sudo usermod -a -G dialout $USER`命令将用户添加至`dialout` 组中。
  2. 重新登录所添加的账户后，该账户即可获取UART 读写权限。

#### 3. 添加DJI USB 设备节点
如需在M210 系列的无人机上使用OSDK 中的视觉功能，使Linux 系统能够获取并标识DJI 的设备，请按如下步骤，在Linux 中添加DJI USB 设备节点：
  1. 在`/etc/udev/rules.d/`目录下创建文件`DJIDevice.rules`。
  2. 在`DJIDevice.rules`文件中添加`SUBSYSTEM=="usb", ATTRS{idVendor}=="2ca3", MODE="0666"`。
  3. 重新启动电脑后，系统即可识别DJI USB 设备。

## 配置ROS 开发环境
> **说明** 如下安装步骤以在Manifold 2 为例，介绍配置使用OSDK 开发应用程序的开发环境的步骤。

#### 1. 安装开发工具
* 安装C编译器：GCC 5.4.0/5.5.0 版本，C++ 11
* CMake：2.8.3 及以上版本
* 安装工具链
  ```shell
    mkdir catkin_ws
    cd catkin_ws
    mkdir src
    cd src
    catkin_init_workspace
  ```

#### 2. 安装依赖软件

##### (1) 安装DJI Onboard SDK 
从[Github](https://github.com/dji-sdk/Onboard-SDK) 上获取DJI Onboard SDK，并在DJI Onboard SDK 目录下使用如下命令安装DJI Onboard SDK。

```c++
 $mkdir build 
 $cd build 
 $cmake.. 
 $sudo make -j7 install
```

##### (2) 安装nema-comms
使用如下命令安装nema-comms
`
$sudo apt install ros-{release}-nmea-comms 
`
> **说明：** 在ROS 系统上使用高级视觉功能时，请务必安装nema-comms。

##### (3) 安装ACM 驱动
安装ACM（Abstract Control Model）驱动后，开发者使用机载计算机或第三方开发平台通过USB 接口能够实现应用程序仿真和外部供电功能。
使用`dmesg` 命令可查询系统中ACM 驱动的信息，如 图.1 所示。
    <div>
<div style="text-align: center"><p>图1. 安装ACM 驱动</p>
</div>
<div style="text-align: center"><p><span>
      <img src="../../images/Linux/acm_dmesg.png" width="450" style="vertical-align:middle" alt/></span></p>
</div></div>

##### (4) 安装FFmpeg
安装[FFmpeg](http://www.ffmpeg.org) 后，开发者使用机载计算机或第三方开发平台能够实现视频相关功能。    
请使用如下命令安装FFmpeg：
```c
sudo apt-get install libavcodec-dev libswresample-dev
```

##### (5) 安装OpenCV 3.x
安装[OpenCV](https://opencv.orgg) 后，开发者使用机载计算机或第三方开发平台能够以可视化的方式获取立体感知及对象识别等应用功能的信息。    

#### 3. 添加设备权限
##### (1) 添加UART 读写权限     
  请按如下步骤为Linux 中指定的用户添加UART 读写权限：
  1. 使用`sudo usermod -a -G dialout $USER`命令将用户添加至`dialout` 组中。
  2. 重新登录所添加的账户后，该账户即可获取UART 读写权限。

##### (2) 安装LibUSB 并添加DJI USB 设备节点
* 安装LibUSB        
安装LibUSB 后，开发者使用Manifold 和第三方开发平台能够获取无人机接收到的图像数据。    
使用如下命令安装LibUSB：1.0.17及更高版本。  

`sudo apt-get install libusb-1.0-0-dev`

* 添加DJI USB 设备节点      
如需在M210 系列的无人机上使用OSDK 中的视觉功能，使Linux 系统能够获取并标识DJI 的设备，请按如下步骤，在Linux 中添加DJI USB 设备节点：
  1. 在`/etc/udev/rules.d/`目录下创建文件`DJIDevice.rules`。
  2. 在`DJIDevice.rules`文件中添加`SUBSYSTEM=="usb", ATTRS{idVendor}=="2ca3", MODE="0666"`。
  3. 重新启动电脑后，系统即可识别DJI USB 设备。  

#### 4. 设置波特率
ROS 默认订阅的主题相对较多，为保证ROS 与基于OSDK 开发的应用程序间有足够的通信带宽，UART 的波特率应大于921600。

>**说明** 
> * 由于Manifold 2-G 的波特率可能与实际值略有偏差，因此请将波特率设置为1000000，详情请参见Manifold 2 <a href="https://dl.djicdn.com/downloads/manifold-2/20190528/Manifold_2_Production_Information_v1.0_Multi.pdf">使用说明书</a>。 
> * 仅Linux 和ROS 系统支持使用DJI 的高级视觉功能。
> * 使用DJI 无人机的视觉功能实现高级应用时，请添加应用程序所需的驱动程序和第三依赖库。
> * 如下安装步骤以在Manifold 2 为例，介绍配置使用OSDK 开发应用程序的开发环境的步骤。

## 配置STM32 开发环境
#### 1. 安装开发工具       
  [Keil MDK](http://www2.keil.com/mdk5/)  5.22 及以上（armcc 5.06）

#### 2. 使用Keil软件      
激活Keil MDK 软件后，使用Keil Pack Installer 或<a href="http://www.keil.com/dd2/Pack/" target="_blank">手动下载</a>最新的STM32F4xx_DFP.2.x.x 驱动包，如 图2.安装Pack 包 所示。
<div>
<div style="text-align: center"><p>图2.安装Pack 包</p>
</div>
<div style="text-align: center"><p><span>
      <img src="../../images/STM32_Keil_PackInstall.png" width="600" style="vertical-align:middle" alt/></span></p>
</div></div>
