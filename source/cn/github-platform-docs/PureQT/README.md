---
title: DJI Onboard SDK QT例程 
date: 2016-06-24
---

## 简介

QT 例程是我们基于 QT 平台实现的 SDK 例程，它可以运行在 Windows 或者 Linux 平台上并可以完成如下命令：

* 激活
* 获取控制权
* 释放控制权
* 起飞
* 降落
* 自动返航
* 姿态控制
* 云台控制
* 相机控制
* 虚拟遥控
* 航点指令
* 热点环绕指令
* 智能跟随指令

开发者可以通过程序的图形界面来进行交互和测试。

## 调试与运行环境

我们成功测试了如下运行环境：

* QT 版本： QT 5.4 或更新。
* 编译器版本： MinGW 4.9.2 或更新；MSVC2012或更新。

下面是在manifold内安装QT的步骤：

* sudo apt-get update
* sudo apt-get install qtcreator

至此，已经安装了qt5.2.1，但是缺少webkit和串口驱动

* sudo apt-get install libqt5webkit5

至此就只剩下串口驱动了

* sudo apt-get install libudev-dev
* git clone git://code.qt.io/qt/qtserialport.git
* cd qtserialport
* git checkout origin/old/5.2
* cd ..
* mkdir qtserialport-build
* cd qtserialport-build
* qmake ../qtserialport/qtserialport.pro
* make
* sudo make install

现在有了5.2版本的串口驱动，但是这个驱动是不能正常使用的

* cd ../qtserialport/
* git checkout origin/5.3
* cd ../qtserialport-build/
* make

这次make会失败，不要理他，继续执行下面的步骤

* sudo make install
* make

这次make会成功

* sudo make install

完成安装。用sudo权限开启qtcreator。

* sudo qtcreator

默认串口名称为ttyTHS1

## 硬件安装

* 为了能够与 M100 的 N1 主控进行通信，开发者需要自行购买 USB 转 TTL 的串口转接模块。
* 为了更好的监控飞机状态，我们建议开发者在调试的时候运行 DJI GO 来实时查看飞机当前状态信息。

## 配置和编译

1. 打开 `onboardSDK` 中`PureQT` 目录下的 `onboardSDK.pro` 载入 QT 例程。
2. 选择合适的编译器并编译项目。
3. 在程序中选择好正确的设备和波特率，以及配置好激活所需的 APP ID 与 key

## 运行

在 QT 中点击绿色三角来运行程序，你可以在模拟器中对其进行测试。


