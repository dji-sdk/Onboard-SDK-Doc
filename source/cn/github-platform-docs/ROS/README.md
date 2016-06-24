---
title: DJI Onboard SDK ROS例程 
date: 2016-06-24
---

## 简介

此ROS例程实现了以下功能：

* 激活 Matrice100 （以下简称M100）
* 获取 M100 控制权
* 释放 M100 控制权
* 向 M100 发送起飞指令
* 向 M100 发送降落指令
* 向 M100 发送返航指令
* 对 M100 进行姿态控制
* 对 M100 进行云台角度控制
* 向 M100 发送相机控制指令
* 向 M100 发送虚拟遥控指令
* 向 M100 发送锁定/解锁指令
* 向 M100 发送同步时间戳指令
* 设置 M100 外发数据频率
* 利用航点任务接口实现航点任务
* 利用热点任务接口实现热点任务
* 利用跟随任务接口实现跟随任务
* 控制 M100 进行 (x,y,z) 坐标导航
* 控制 M100 进行 GPS 坐标导航
* 通过姿态控制指令实现 M100 的航点飞行任务
* 通过 WebSocket 向 M100 发送网页地图生成的航点指令
* 通过 MAVLink 和 QGroundControl 控制 M100

## 如何使用

1. 按照文档配置好 M100 
2. 将激活信息输入至launch file：`dji_sdk/launch/sdk_manifold.launch`
	* Drone Version （飞控版本：“M100” 或 “A3”）
	* APP ID （在官网注册key后得到）
	* Communication Key（在官网注册key后得到）
	* Uart Device Name（串口设备名称）
	* Baudrate（比特率）
3. 运行 `roslaunch dji_sdk sdk_manifold.launch` 来启动核心包。
4. 将 `dji_sdk/include/dji_sdk` 下的客户端头文件`dji_drone.h` 引用到你自己的 ROS 包中，并运行它（我们也提供了python版本的客户端`dji_drone.py`）

## 系统架构

* [dji_sdk](../ROS_Example/ros_corePackage.html): 核心 ROS 包，处理所有与 M100 的串口通信并提供了 `dji_drone.h`的头文件供开发者引用。
* [dji_sdk_demo](../ROS_Example/ros_demo_client_package.html): 一个调用 `dji_drone.h` 控制 M100 的例子。
* [dji_sdk_web_groundstation](../ROS_Example/ros_map_waypoint_navigation_package.html): 基于 WebSocket 的网页版地面站，依赖 ROS-bridge-suite 。
* [dji_sdk_read_cam](../ROS_Example/ros_video_decoding_package.html): Manifold专用 ROS 包，对禅思 X3 云台的视频信息进行解码输出视频流。默认通过`CATKIN_IGNORE`禁用，需要手动启用。
* [dji_sdk_dji2mav](../ROS_Example/ros_dji2mav_0.2.1_package.html): MAVLink 协议转接器，使得 M100 可以支持任意使用 MAVLink 为协议的地面站软件。

![ROS Software Structure](../../../images/ROS/ROSSoftwareStructure.jpg)

[点击查看大图](https://raw.githubusercontent.com/dji-sdk/Onboard-SDK-ROS/2.3/dji_sdk_doc/structure.jpg)

## Read First

[DJI SDK Challenge: Onboard SDK Part I](./whatToKnowI.html)

# 系统环境

此 ROS 包在如下系统中进行测试；
* 操作系统：Ubuntu 14.04， DJI Manifold
* ROS 版本：ROS Indigo
