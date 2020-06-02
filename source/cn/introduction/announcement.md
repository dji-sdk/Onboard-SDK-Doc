---
title: 最新公告
date: 2020-05-08
keywords: [OSDK, 功能概览]
---
## OSDK 内测固件申请说明
Onboard SDK 4.0.0 已正式发布，在Matrice 200 V2 系列无人机上开发应用程序时，需使用最新的无人机固件，但该固件仍在测试阶段，尚未正式发布。
如需使用最新的固件，请向<a href="mailto:dev@dji.com"> DJI SDK 团队 </a>申请内测权限，获取Matrice 200 V2 系列无人机的内测固件。

> **说明**
> * 申请内测固件时，请提供登录DJI Assistant 2 的账号。
> * 内测固件目前还在内测阶段，请在安全范围内使用内测固件，因使用内测固件而导致无人机损坏不在保修范围内。

## OSDK 4.0 正式发布
* 新增支持[Matrice 300 RTK](https://www.dji.com/cn/matrice-300)
   * 获取[Matrice 300 RTK](https://www.dji.com/cn/matrice-300) 的感知数据
   * 设置[Matrice 300 RTK](https://www.dji.com/cn/matrice-300) 的避障开关
* 新增<a href="../tutorial/SDK-mop.html"><b>SDK互联互通</b></a>功能
  * MSDK、OSDK、PSDK 跨平台无缝通信
  * 支持大量数据的高速传输
* 新增<a href="../tutorial/gimbal-manager.html"><b>多云台控制与管理</b></a>功能
* 新增<a href="../tutorial/advanced-sensing.html"><b>获取相机的H.264 码流</b></a>功能
* 新增相机媒体文件下载功能
* [航点任务](../tutorial/motion-planning.html)功能升级（需使用[Matrice 300 RTK](https://www.dji.com/cn/matrice-300)）
  * 海量航点，最多支持65535 个航点
  * 动作灵活配置需求
* 修复M210 V2系列无人机在飞行时OSDK 对云台控制失效的问题
* 修复M210 V2系列无人机在速度控制模式下飞行时，避障开关失效的问题

> **说明：** 若您仍使用OSDK V3.9.0 开发应用程序，请下载[OSDK V3.9.x](https://terra-1-g.djicdn.com/71a7d383e71a4fb8887a310eb746b47f/osdk/OSDK-3.9.0.zip) 的文档。

#### 平台支持
* STM32 Platform：支持将基于OSDK 开发的应用程序移植到FreeRTOS 上
* QT: 终止对Qt 平台的支持

## <a href="https://terra-1-g.djicdn.com/71a7d383e71a4fb8887a310eb746b47f/general/DJI_Media_File_Metadata_WhitePaper.zip">DJI 媒体文件元数据白皮书</a> 正式发布
DJI 相机媒体文件元数据白皮书正式发布，该文档描述了存储媒体文件元数据的格式和各个字段的含义。
开发者通过使用该白皮书，能够了解媒体文件中各个元数据以及相应字段的信息，在利用媒体文件元数据的基础上实现图像分析或建模等行业应用。