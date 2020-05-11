---
title: 如何使用OSDK ？
date: 2020-05-08
version: 4.0.0
keywords: [注册, 选购, 入门, 学习, 进阶, 高级]
---

> **说明：** 本系列文档介绍OSDK V4.0.0 的功能，以及使用OSDK V4.0.0 开发应用程序的步骤和方法，若您仍使用OSDK V 3.9.0 开发应用程序，请下载[OSDK V3.9.0]() 的文档。

使用OSDK 开发应用程序前，需要先注册开发者账号；使用OSDK 开发应用程序时，需要选购飞行平台和计算平台。建议您在使用OSDK 开发应用程序前，先学习无人机的**基础知识**，了解开发应用程序的**注意事项**，借助**实践教程和API 文档**开发应用程序。

<div>
<table>
<tbody>
  <tr>
   <td style="border-right: none;border-left: none;"><div><p><span>
      <img src="../../images/how-to-use/1.png" width="90" style="vertical-align:middle" alt/></span></p></div></td></td>
       <td style="border-right: none;border-left: none;"><div><p><span>
      <img src="../../images/how-to-use/2.png" width="70" style="vertical-align:middle" alt/></span></p></div></td></td>
        <td style="border-right: none;border-left: none;"><div><p><span>
      <img src="../../images/how-to-use/3.png" width="70" style="vertical-align:middle" alt/></span></p></div></td></td>
         <td style="border-right: none;border-left: none;"><div><p><span>
      <img src="../../images/how-to-use/4.png" width="70" style="vertical-align:middle" alt/></span></p></div></td></td>
         <td style="border-right: none;border-left: none;"><div><p><span>
      <img src="../../images/how-to-use/5.png" width="70" style="vertical-align:middle" alt/></span></p></div></td></td>
         <td style="border-right: none;border-left: none;"><div><p><span>
      <img src="../../images/how-to-use/6.png" height="90" width="90" style="vertical-align:middle" alt/></span></p></div></td></td>
  </tr>
  <tr>
   <td style="text-align:center"><a href="https://account.dji.com/register?appId=dji_sdk&backUrl=https%3A%2F%2Fdeveloper.dji.com%2Fuser&locale=en_US" target="_blank">注册账号</a></td>
   <td style="text-align:center"><a href="https://www.dji.com/cn/products/compare-m200-series?site=brandsite&from=nav" target="_blank" >选购无人机</a></td>
   <td style="text-align:center"><a href="../purchaseguide/hardware.html">选购硬件平台</a></td>
   <td style="text-align:center"><a href="https://developer.dji.com/user/apps/#allhtml">应用注册</a></td>
   <td style="text-align:center"><a href="../quickstart/run-the-sample.html">运行示例程序</a></td>
   <td style="text-align:center"><a href="https://www.dji.com/cn/downloads/softwares/assistant-dji-2-for-matrice">模拟与调试</a></td>
  </tr>
</tbody>
</table>
</div> 


## 1. 注册DJI 开发者账号

* <a href="https://account.dji.com/register?appId=dji_sdk&backUrl=https%3A%2F%2Fdeveloper.dji.com%2Fuser&locale=en_US" target="_blank">注册</a>成为DJI 的开发者时，请务必**认真**阅读使用DJI SDK 的<a href="https://developer.dji.com/cn/policies/privacy/">协议、条款和政策</a>。
* 为方便您获得便捷高效的服务，请**正确地**填写注册信息。

## 2. 选用开发工具
选购开发应用程序时所需使用的飞行平台和计算平台。

* [选购硬件产品](../purchaseguide/hardware.html)
* [选购开发平台](../purchaseguide/development-platform.html)

## 3. 开发应用程序
#### 开发前准备
使用OSDK 开发应用程序前，建议先学习开发应用程序所需的基础知识、了解OSDK 的功能，根据实际的开发需求选购所需的飞行平台和计算平台，选择合适的开发平台。

* 学习无人机基础知识和控制原理：如俯仰、偏航、滚转和升降等基础知识  
* 了解OSDK 支持的[功能](./feature-list.html)   
* 选购[飞行平台](../purchaseguide/hardware.html)和[计算平台](../purchaseguide/hardware.html)   
* 选择[开发平台](../purchaseguide/development-platform.html)   

#### 开始开发应用程序
使用OSDK 开发应用程序时，**请正确地连接**所选购的飞行平台、计算平台以及第三方传感设备，**正确地配置**应用程序开发环境，通过运行示例代码编译后的程序，了解使用OSDK 开发应用程序的方法。

* 在使用OSDK 开发应用程序前，请先阅读[开发须知](../quickstart/attention.html)中的内容，避免因操作不当损毁飞行平台或计算平台；
* [连接](../quickstart/device-connection.html)飞行平台、计算平台、第三方传感设备和计算机；
* [安装](../quickstart/development-environment.html)开发OSDK 的软件，准备相关工具链和库；
* 通过[跨平台移植](../quickstart/porting.html)(如有需要)，将基于OSDK 开发的应用程序移植到不同的软硬件平台上；
* [编译](../quickstart/run-the-sample.html)示例代码，通过运行示例程序，了解使用OSDK 的方法；
* 根据[开发引导](../quickstart/integrateOSDK.html)中的文档，了解OSDK 的工作原理和接口调用方式，快速实现所需使用的应用功能。

#### 开发功能完善的应用程序
* 根据实际的使用需求，使用[实践教程](../tutorial/basic-control.html)和OSDK API 文档，设计应用程序。
* 借助[DJI Assistant 2](https://www.dji.com/cn/downloads) 等工具调试应用程序，完善应用程序的功能，提高应用程序的性能。

## 获取技术支持服务

* 查看<a href="../FAQ/faq.html">帮助文档</a>
* 在<a href="https://bbs.dji.com/forum-79-1.html?from=developer">DJI 技术支持社区</a>上寻求帮助

* 获取技术支持服务  
	* 使用<a herf="https://formcrafts.com/a/dji-developer-feedback-cn">问题反馈</a>表单  
	* 向DJI SDK 团队发送<a href="mailto:dev@dji.com">邮件</a>
