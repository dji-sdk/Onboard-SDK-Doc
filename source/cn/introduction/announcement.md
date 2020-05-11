---
title: 最新公告
date: 2020-05-08
keywords: [OSDK, 功能概览]
---

## OSDK 4.0 正式发布
#### 新增功能
* <a href="../tutorial/SDK-mop.html"><b>SDK互联互通</b></a>
  * MSDK、OSDK、PSDK 跨平台无缝通信
  * 支持M300 RTK 
* <a href="../tutorial/gimbal-manager.html"><b>多云台控制与管理</b></a>
* <a href="../tutorial/advanced-sensing.html"><b>获取相机的H.264 码流</b></a>
* 相机媒体文件下载
* 获取Matrice 300 RTK 感知数据
* 设置Matrice 300 RTK 的避障开关

#### 功能升级
* 航点任务（需使用Matrice 300 RTK） 
  * 海量航点，最多支持65535 个航点
  * 动作灵活配置需求

#### 问题修复
* 云台控制失效：修复M210 V2系列无人机在飞行时OSDK 对云台控制失效的问题
* 避障开关失效：修复M210 V2系列无人机在速度控制模式下飞行时，避障开关失效的问题

#### 平台支持
* STM32 Platform：支持FreeRTOS移植。
* Qt: 终止Qt平台支持。

## <a href="https://terra-1-g.djicdn.com/71a7d383e71a4fb8887a310eb746b47f/general/DJI_Media_File_Metadata_WhitePaper.zip">DJI 媒体文件元数据白皮书</a> 正式发布
DJI 相机媒体文件元数据白皮书正式发布，该文档描述了存储媒体文件元数据的格式和各个字段的含义。
开发者通过使用该白皮书，能够了解媒体文件中各个元数据以及相应字段的信息，在利用媒体文件元数据的基础上实现图像分析或建模等行业应用。