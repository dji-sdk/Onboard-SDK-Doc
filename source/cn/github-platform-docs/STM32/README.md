---
title: DJI Onboard SDK STM32 例程 
date: 2016-06-24
---

## 简介

> **Note: The STM32 example code is currently undergoing a major revamp. We expect to have a new version very soon which fixes many longstanding bugs and makes operation simpler and more reliable. Some of these instructions may not work with the current release and are meant for the newer version.** 

本示例程序使用[STM32F407 Discovery](http://www.st.com/content/st_com/en/products/evaluation-tools/product-evaluation-tools/mcu-eval-tools/stm32-mcu-eval-tools/stm32-mcu-discovery-kits/stm32f4discovery.html)开发板，使用MDK-ARM (Keil uVision)工具链开发和调试。本例程演示了如何使用Onboard SDK提供的API进行嵌入式程序开发。

整个系统的结构如下图所示
![system diagram](../../../images/STM32/STM32_System_Structure.png) 

系统运行时，用户在PC上向STM32的USART2口发送命令。根据命令的内容，固件程序调用Onboard SDK通过USART3口于M100通讯，并把反馈信息发送给用户。

在使用本例程前请确认你已经**仔细阅读过**有关OnboardSDK的**所有文档**。

## 环境配置

### 硬件接口

![hardware setup](../../../images/STM32/STM32_hardware_setup.jpg)

首先使用USB-TTL转接线连接PC的USB口和STM32的USART2接口(`PA2`，`PA3`分别是STM32端发送和接收）。使用M100附带的串口线连接STM32的USART3口(`PB10`，`PB11`分别是发送和接收)和M100的`UART_CAN2`。使用[DJI Assistant 2](http://developer.dji.com/onboard-sdk/downloads/)软件将M100的`UART_CAN2`接口的波特率设为**230400**（因为固件程序中将USART3波特率配置为230400)。使用DJI Assistant 2时需要通过micro-USB连接PC和M100。STM32开发板通过mini-USB口烧写程序。

### 编译环境

本例程使用MDK-ARM (Keil uVision) 5.12版本开发。推荐使用更新版本的Keil进行。Keil5系列软件中没有包含芯片器件库，需要自行安装，否则会提示缺少芯片器件库。推荐使用Keil的`Pack Installer`安装最新的STM32F4xx_DFP.2.x.x包，如下图所示。开发者也可以自行下载STM32F4xx_DFP.2.x.x包，网址是http://www.keil.com/dd2/Pack/，然后使用`Pack Installer`手动安装。

![Keil_PackInstall](../../../images/STM32/STM32_Keil_PackInstall.png)

### 编译本例程

首先使用git来取得Onboard SDK和示例程序的源码:
> git clone --recursive https://github.com/dji-sdk/Onboard-SDK.git

然后在Keil uVision中打开工程`samples
/STM32/OnBoardSDK_STM32/Project/OnBoardSDK_STM23.uvprojx`。在编译之前，开发人员需要在`OnboardSDK_STM32/User/Activate.cpp`文件里输入正确的APP KEY和APP ID。

使用菜单选项`Project->Build Target`编译程序，使用`Flash->Download`把输出的二进制固件烧写到STM开发板上。

### 配置串口调试程序

为了从PC和STM32开发板进行串口通讯，用户需要在串口终端程序(这里我们使用开源的[RealTerm](realterm.sourceforge.net))中将波特率设置为**115200**（与固件程序USART2的波特率一致），并设置为Ascii接收，Hex发送模式。

![Realterm Setup](../../../images/STM32/STM32_Realterm.png) 

## 激活

为了使STM32获得飞机的控制权，首先需要发送激活指令。激活的目的是向M100确认本程序有合法的APP ID和APP KEY。

通过串口终端发送如下二进制命令
> 0xFA 0xFB 0x01 0xFE

![Activation Successfully](../../../images/STM32/STM32_Activation_Successfully.png)

第一次激活需要互联网连接，即STM32 <==> M100 <==> 遥控器 <==> DJI GO APP <==> Internet，因为M100需要在连接官网验证APP ID和APP KEY。之后每次使用前仍需发送激活指令，但是不再需要Internet。

## 操作指南

本例程实现了一个简单的命令协议。用户通过串口向STM32发送命令。下图是一次完整任务发送的命令序列。
![Example Sequence](../../../images/STM32/STM32_Example_Sequence.png) 

### 指令格式

每一帧命令由下面几部分组成。
> 帧头(2字节: 0xFA, 0xFB), 指令码(2字节), 数据(可选), 帧尾(1字节: 0xFE)

STM32收到帧尾"0xFE"会立即开始执行命令。已经支持的命令如下，需要更多指令请自行添加：

|指令内容            | 指令代码             |
|:------------------|:------------------|  
|获取当前版本信息      | 0xFA 0xFB 0x00 0xFE |
|发送激活指令 		| 0xFA 0xFB 0x01 0xFE | 
|请求控制权   		|0xFA 0xFB 0x02 0x01 0xFE|  
|释放控制权   	 	|0xFA 0xFB 0x02 0x00 0xFE | 
|解锁电机   		 	|0xFA 0xFB 0x03 0x01 0xFE|  
|锁定电机  		 	|0xFA 0xFB 0x03 0x00 0xFE|  
|运动控制            |0xFA 0xFB 0x04 0x01 Flag  x_H  x_L  y_H  y_L  z_H  z_L  yaw_H yaw_L 0xFE|
|运动控制调试         |0xFA 0xFB 0x04 0x02 Flag  x_H  x_L  y_H  y_L  z_H  z_L  yaw_H yaw_L 0xFE|
|一键返航  		 	|0xFA 0xFB 0x05 0x01 0xFE|  
|一键起飞  		 	|0xFA 0xFB 0x05 0x02 0xFE|  
|一键降落  		 	|0xFA 0xFB 0x05 0x03 0xFE|  
|虚拟遥控开启（A档）     |0xFA 0xFB 0x06 0x01 0xFE  |
|虚拟遥控开启（F档）     |0xFA 0xFB 0x06 0x02 0xFE  |
|虚拟遥控关闭 	 	|0xFA 0xFB 0x06 0x00 0xFE | 
|开始热点飞行 	    |0xFA 0xFB 0x07 0x00 Altitude Angular_Speed Radius 0xFE|
|结束热点飞行         |0xFA 0xFB 0x07 0x01 0xFE |
|获取广播信息         |0xFA 0xFB 0x08 0x00 0xFE |

## 命令示例

### 运动控制

Onboard SDK为开发者提供了非常灵活的方式来控制飞机的运动。上表中的运动控制需要用户发送如下数据
+ 控制模式
+ X-轴控制量 (高位字节x_H和低位字节x_L)
+ Y-轴控制量 (高位字节y_H和低位字节y_L)
+ Z-轴控制量 (高位字节z_H和低位字节z_L)
+ Yaw-轴控制量 (高位字节yaw_H和低位字节yaw_L)

控制模式决定了每个轴(X, Y, Z, Yaw)控制量的物理意义，例如速度，位置，角度，角速度等。完整模式的列表请参考开放协议。

下面是一个运动控制命令的例子
> 0xFA 0xFB 0x04 0x01 **0x48 0x00 0x64 0x00 0xC8 0x00 0x64 0x00 0x05** 0xFE

上例中，控制模式为 0x48 (0b 0100 1000)表示X, Y, Z速度控制和Yaw角速度控制，ground参考系。

STM接收到上面的命令后，会把每个轴控制量的高位字节和低位字节组成一个整数，然后除以100，作为发送给100的数据。在上面的命令中，X轴速度设为1米/秒, Y轴速度设为2米/秒，Z轴速度设为1米/秒，Yaw角速度设为0.05弧度/秒。

如果我们按照一键起飞==>上面的运动控制指令==>一键降落的顺序向飞机发送指令的话，将在模拟器中得到如下的结果
![Movement Control](../../../images/STM32/STM32_Movement_Control.png)

注意，在进行运动控制时，程序需要连续不断地（推荐频率为50赫兹）向飞机发送运动控制命令，而不是发送一次就停止。在STM32例程中，当用户向串口发送一次运动控制命令后，程序会开启一个50Hz的计时器，来连续向飞机发送相同指令。要停止自动发送，用户只要发送任何0x04 0x01开头的命令，飞机就会回到悬停状态。

为了方便用户确保发送正确的控制量高字节和低字节，我们提供了一个"运动控制调试"命令。例如下面的命令

> 0xFA 0xFB 0x04 **0x02** 0x48 0x00 0x64 0x00 0xC8 0x00 0x01 0x00 0x05 0xFE

会向串口终端打印换算后的X，Y，Z，Yaw的控制量，而不会真的向飞机发送命令。

### 热点飞行

在热点模式下，飞机会绕着某个中心点，以用户给定的高度，角速度，和半径飞行。STM32例程中，中心点就是热点飞行开始时飞机的位置。下面的命令会让飞机在高度10米，角速度15度/秒，半径20米，绕圈飞行。

> 0xFA 0xFB 0x07 0x00 0x0a 0x0F 0x14 0xFE 

![Hot Point](../../../images/STM32/STM32_HotPoint.png)

### 获取广播数据

获取广播数据只要发送命令
> 0xFA 0xFB 0x08 0x00 0xFE

现在打印了当前的时间戳和剩余电量，需要更多数据请自行添加。
