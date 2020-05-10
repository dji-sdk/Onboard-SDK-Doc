---
title: 选择第三方开发平台
date: 2020-05-08
version: 4.0.0
keywords: [开发须知, 硬件选购, 软件版本, 固件版本]
---
请根据所选用的操作系统对OSDK 功能的支持差异和示例程序的资源占用情况，选择使用OSDK 开发应用程序的开发平台。

## 平台与编译链选择
* 选择Linux
   * 操作系统版本：Ubuntu 16.04
   * 编译链工具：gcc/g++ 5.4.0
   * 推荐平台：Manifold 2-C/2-G

* 选择ROS 
   * 操作系统版本: kinetic
   * 编译链：gcc/g++ 5.4.0
   * 推荐平台：Manifold 2-C/2-G

* 选择FreeRTOS
   * 操作系统版本：FreeRTOS v10.2.1
   * 编译链：armcc
   * 推荐平台：STM32F4 系列

## 功能支持对比
<div>
<table>
<thead>
   <th>功能分类</th>
   <th>功能名称</th>
   <th width=200>功能描述</th>
   <th>Linux</th>
   <th>RTOS</th>
   <th>ROS</th>
   <th width=120>适配机型</th>
   <th>备注</th>
</thead>
<tbody>
    <tr>
    <tr>
    <th rowspan="3">控制类</th>
     <td>时间同步</td>
     <td>获取无人机飞行控制器的时间戳，获取硬同步信号如NMEA 数据UTC 时间，订阅PPS 信号</td>
     <td>✓</td>
     <td>✓</td>
     <td>✓</td>
     <td> M300 RTK</br>M200 RTK V2</br>M200 V2</td>
     <td rowspan="6">-</td>
    </tr>
    <tr>
     <td>基础控制</td>
     <td>设置并获取飞行控制器的参数执行基本的飞行任务实现无人机基础控制</td>
     <td>✓</td>
     <td>✓</td>
     <td>✓</td>
     <td>M300 RTK</br>M200 RTK V2</br>M200 V2</td>
    </tr>
      <tr>
      <td>运动规划</td>
      <td>航点任务热点任务</td>
      <td>✓</td>
      <td>✓</td>
      <td>✓</td>
      <td>M300 RTK</br>M200 RTK V2</br>M200 V2</td>
    </tr>
    <tr>
      <th rowspan="3">管理类</th>
      <td>信息管理</td>
      <td>获取无人机飞行控制器广播信息订阅无人机飞行控制器的数据</td>
      <td>✓</td>
      <td>✓</td>
      <td>✓</td>
      <td>M300 RTK</br>M200 RTK V2</br>M200 V2</td>
    </tr>
    <tr>
     <td>云台管理</td>
     <td>控制云台转动和重置设置云台基本参数，获取云台当前的状态和基本信息</td>
     <td>✓</td>
     <td>✓</td>
     <td>✓</td>
     <td>M300 RTK</br>M200 RTK V2</br>M200 V2</td>
    </tr>
    <tr>
     <td>相机管理</td>
     <td>控制相机执行拍照、录像及变焦等基础动作设置相机快门、光圈及ISO 等基本参数</td>
     <td>✓</td>
     <td>✓</td>
     <td>✓</td>
     <td> M300 RTK</br>M200 RTK V2</br>M200 V2</td>
    </tr>
    <tr>
      <th rowspan="3">拓展类</th>
      <td>高级视觉功能</td>
      <td>获取相机的图像和码流（获取原码流和H.264 码流）实现对象识别等功能</td>
      <td>✓</td>
      <td>-</td>
      <td>✓</td>
      <td> M300 RTK</br>M200 RTK V2</br>M200 V2</td>
      <td>M200 RTK V2 和M200 V2 无人机仅支持获取主相机原码流及H.264 码流</td>
    </tr>
        <tr>
      <td>SDK 互联互通</td>
      <td>MSDK、PSDK与OSDK 通信</td>
      <td>✓</td>
      <td>✓</td>
      <td>将要支持</td>
      <td>M300 RTK</br>M200 RTK V2</br></td>
      <td >-</td>
    </tr>
</tbody>
</table>
</div>

