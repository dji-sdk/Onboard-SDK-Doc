---
title: 基础控制功能
date: 2020-05-08
version: 4.0.0
keywords: [飞控， 无人机控制，无人机参数， 基本功能， joystick， 基本功能]
---
## 概述
使用OSDK 的无人机飞行控制功能，能够设置并获取无人机各项基础参数，控制无人机执行基础飞行动作，通过Joystick 功能控制无人机执行复杂的飞行动作。

## 基础概念
### 无人机基础信息
OSDK 开放了设置无人机基础参数的接口，开发者通过设置并获取无人机的基础参数，能够实现对无人机的精准控制：
* 开启或关闭RTK功能和避障功能（水平避障和顶部避障）
* 设置无人机的返航点和返航高度

具有[消息订阅](./massage-manager.html)功能的应用程序，能够方便用户获取无人机基础参数的信息：
* 获取RTK功能和避障功能的状态（水平避障和顶部避障）
* 获取无人机返航点和返航高度

### 无人机基础飞行动作
无人机的基础飞行动作主要包含无人机锁定、无人机起飞降落和无人机返航三类，开发者使用OSDK 提供的接口，即可根据实际的控制需求，控制无人机执行指定的飞行动作。
<div>
<div style="text-align: center"><p>表1. 基础飞行动作 </p></div>
<div>
  <table>
    <thead>
      <tr>
      <th>功能类型</th>
      <th>基本功能</th>
      <th>功能说明</th>
      </tr>
    </thead>
<tbody>
      <tr>
         <td rowspan=2>无人机锁定</td>
         <td>解锁</td>
         <td>无人机解锁后，无人机的螺旋桨会怠速旋转，但不会飞离地面</td>
      </tr>
      <tr>
         <td>上锁</td>
         <td>无人机上锁后，无人机的螺旋桨由怠速旋转状态变为静止状态</td>
      </tr>
      <tr>
         <td rowspan=5>起飞和降落</td>
         <td>自动起飞</td>
         <td>使用该功能时，无人机会自动起飞1.2 米（该高度不可调整）</td>
      </tr>
      <tr>
         <td>自动降落</td>
         <td>使用该功能时，无人机会自动降落</td>
      </tr>
      <tr>
         <td>取消自动降落</td>
         <td>使用该功能时，无人机在下降多过程中会停止降落，并悬停在空中</td>
      </tr>
      <tr>
         <td>降落确认</td>
         <td>当无人机已降落到离地面一定距离时，用户使用该功能可确认无人机降落到地面</td>
      </tr>
      <tr>
         <td>强制降落</td>
         <td>无视降停面的状态，强制无人机降落（降落速度较快）</td>
      </tr>
      <tr>
         <td rowspan=2>无人机返航</td>
         <td>返航</td>
         <td>使用该功能时，无人机会自动返航</td>
      </tr>
      <tr>
         <td>取消返航</td>
         <td>使用该功能时，无人机会悬停在空中</td>
      </tr>
</tbody>
</table>
</div>

> **说明**
> * 不同型号的无人机在执行起飞、降落和返航动作时的高度可能会有差异，详情请参见选购机型的说明书。
> * 无人机解锁后，若未接收到起飞指令，无人机将自动上锁，螺旋桨会停止旋转，若无人机解锁失败，请根据错误码查询解锁失败的原因。


### Joystick 功能     
Joystick 是一个无人机综合控制功能，使用Joystick 功能时，开发者根据实际的应用需要，通过调用Joystick 中的接口，**同时设置无人机使用的坐标系、水平控制的模式、垂直控制的模式、yaw角度控制的模式和悬停模式**，才能设计出满足使用需求的无人机飞行控制逻辑。

#### 设置坐标系
* 机体坐标系  
机体坐标系以无人机的重心为原点，无人机机头前进的方向为X轴，机头前进方向的右侧为Y轴，Z轴与X轴、Y轴相互垂直交于重心且指向无人机下方（遵循“右手法则”）。在机体坐标下，无人机围绕X轴、Y轴和Z轴旋转时的飞行动作，可称为横滚（无人机仅绕X轴旋转）、俯仰（无人机仅绕Y轴旋转）和偏航（无人机仅绕Z轴旋转）。  

* 大地坐标系  
大地坐标系也称世界坐标系或当地水平坐标系，在该坐标系中，无人机指向地球正北的方向为X轴，正东的方向为Y轴，X轴与Y轴相互垂直，Z轴竖直指向无人机下方，在满足“右手法则”的前提下，Z轴将根据无人机飞行的实际情况调节角度，因此该坐标系也称为“北-东-地（N-E-D）坐标系”。

#### 设置水平控制模式
* 姿态角控制模式：在该模式下，水平方向的指令为无人机的姿态角。(在机体坐标系下，该角度为roll 和pitch)
* 速度控制模式：在该模式下，水平方向的指令为无人机的速度
* 位置控制模式：在该模式下，水平方向的指令为无人机的位置
>**说明：** 当位置指令的模不为0时，无人机会以指定的速度向前飞行，否则，无人机将悬停在指定的位置。

* 角速度控制：在该模式下，水平方向的指令为无人机的旋转角速度

##### 设置无人机悬停模式
仅在**水平控制模式中的速度控制**模式下，开发者可以设置无人机的悬停模式：    
* 开启稳定模式：开启稳定模式后，无人机将在指定的位置上悬停
* 关闭稳定模式：关闭稳定模式后，无人机将按照速度命令飞行，当无人机的前进速度为0时候，无人机可能会随风飘动     

#### 设置垂直控制模式
* 速度控制模式：控制无人机垂直方向的速度
* 位置控制模式：控制无人机垂直方向的位置，该位置为相对于起飞点的绝对位置
* 油门控制模式：控制无人机的油门

#### 设置yaw角度控制模式
* 角度控制模式：在该模式下，yaw方向旋转的指令为yaw 的角度
* 角速率控制模式：在该模式下，yaw方向旋转的指令为yaw 的角速率

### 无人机高度
DJI 的无人机在执行飞行任务过程中的基础高度概念如 表2.无人机高度概念 所示。

<div>
<div style="text-align: center"><p>表2.无人机高度说明</div>
<table>
<thead>
<th style="border-left: none;"></th>
<th>相对起飞高度</th>
<th>融合高度</th>
<th>GPS 高度</th>
<th>RTK 高度</th>
<th>对地高度</th>
</thead>
<tbody>
<tr>
 <th style="border-left:none">基本含义</th>
<td>无人机相对于起飞点的高度变化量</td>
<td>以气压计值为初始值，使用融合算法并借助无人机上所有传感器的数据输出的高度值</td>
<td>基于GPS 卫星输出的实时椭球高</td>
<td>基于RTK 技术输出的实时椭球高</td>
<td>借助无人机上的测距传感器获得的无人机与当前下方物体的距离</td>
</tr>
<tr>
 <th style="border-left:none">数据来源</th>
<td>IMU(可能包括视觉传感器、GPS 和RTK)和气压计</td>
<td>IMU(可能包括视觉传感器、GPS 和RTK)和气压计</td>
<td>GPS 卫星</td>
<td>RTK 卫星</td>
<td>TOF 或超声波和IMU</td>
</tr>
<tr>
 <th style="border-left:none">高度0 点</th>
<td>无人机离地起飞的点</td>
<td>标准气压的海平面</td>
<td>WGS84坐标系	</td>
<td>RTK 坐标系（C2000，WGS84或用户指定的坐标系）</td>
<td>无人机正下方坚硬物体的表面（如地面）</td>
</tr>
<tr>
 <th style="border-left:none">应用场景</th>
<td>用于获取无人机当前已飞行的高度</td>
<td>用于更加精准稳定地控制无人机执行飞行任务</td>
<td>用于分析无人机的飞行任务和飞行状态</td>
<td>用于精准测绘和航点飞行等飞行任务</td>
<td>用于无人机安全降落（避障和降速）</td>
</tr>
<tr>
 <th style="border-left:none">有效量程</th>
<td>数千米</td>
<td>数千米</td>
<td>数千米</td>
<td>数千米</td>
<td>10 米内</td>
</tr>
<tr>
 <th style="border-left:none">获取方法</th>
<td>通过DJI Pilot 获取该信息</br>基于MSDK 开发的移动端APP 可订阅该信息</td>
<td>基于MSDK 开发的移动端APP 可订阅该信息</td>
<td>基于MSDK 开发的移动端APP 可订阅该信息</td>
<td>基于MSDK 开发的移动端APP 可订阅该信息</td>
<td>通过DJI Pilot 获取该信息</br>基于MSDK 开发的移动端APP 可订阅该信息</td>
</tr>
<tr>
 <th style="border-left:none">数据误差</th>
<td>有，受无人机飞行距离的影响，高度精度会受影响</td>
<td>有，受无人机飞行距离的影响，高度精度会受影响</td>
<td>无</td>
<td>无</td>
<td>无</td>
</tr>
<tr>
 <th style="border-left:none">可靠度</th>
<td>不可靠</td>
<td>不可靠</td>
<td>基本可靠</td>
<td>可靠</td>
<td>可靠</td>
</tr>
<tr>
 <th style="border-left:none">误差（噪声）水平</th>
<td>低</td>
<td>低</td>
<td>高 </td>
<td>低</td>
<td>低</td>
</tr>
<tr>
 <th style="border-left:none">影响因素</th>
<td>受温度，湿度，气压影响</td>
<td>受温度，湿度，气压影响</td>
<td>受GPS 卫星强度影响，短期误差大，长期误差相对较小</td>
<td>受RTK 卫星工作状态和RTK 基站精度的影响，总体误差小</td>
<td>无人机正下方坚硬物体表面的性质（如质地和纹理）</td>
</tr>
</tbody>
</table>
<div>

## 使用无人机飞行控制功能    
使用无人机飞行控制功能需要先实例化对象，再设置无人机的基础参数，最后再使用Joystick 中的功能。

#### 1. 实例化对象
为方便开发者使用OSDK 开发应用程序，请在使用OSDK 开发应用程序前先实例化无人机的对象。

```c
FlightSample* flightSample = new FlightSample(vehicle);
```

#### 2. 设置无人机基础参数
使用`flightSample` 和 `flightController` 中的接口设置无人机的基础参数。
> **说明：** 为方便开发者快速设置无人机的基础参数，OSDK 将`flightController` 中的接口封装在 `flightSample`
中，使用`flightController` 或 `flightSample` 中的接口均可设置无人机的基础参数。

```c
flightSample->monitoredTakeoff();
vehicle->flightController->setCollisionAvoidanceEnabledSync(
  FlightController::AvoidEnable::AVOID_ENABLE, 1);

/*! 飞行较长的距离 */
flightSample->moveByPositionOffset((FlightSample::Vector3f){0, 0, 30}, 0);

/*! 飞行较短的距离 */
flightSample->moveByPositionOffset((FlightSample::Vector3f){10, 0, 0}, 0);

/*!设置无人机当前位置为返航点 */
flightSample->setNewHomeLocation();

/*! 设置无人机返航高度 */
flightSample->setGoHomeAltitude(50);

/*! 飞至另一个位置 */
flightSample->moveByPositionOffset((FlightSample::Vector3f){20, 0, 0}, 0);

vehicle->flightController->setCollisionAvoidanceEnabledSync(
FlightController::AvoidEnable::AVOID_DISABLE, 1);
/*! 返航并确认降落*/
flightSample->goHomeAndConfirmLanding();

vehicle->flightController->setCollisionAvoidanceEnabledSync(
FlightController::AvoidEnable::AVOID_ENABLE, 1);
```

#### 3. 使用Joystick 中的功能
使用Joystick 功能需要先设置Joystick 的模式和对应的控制指令，再执行Joystick 指令，实现对无人机的控制。如下代码以在`flightSample->moveByPositionOffset()`中，使用Joystick 功能控制无人机在水平和垂直方向上运动到指定的位置。

1. 设置joystick的模式
```c
  FlightController::JoystickMode joystickMode = {
    FlightController::HorizontalLogic::HORIZONTAL_POSITION,
    FlightController::VerticalLogic::VERTICAL_POSITION,
    FlightController::YawLogic::YAW_ANGLE,
    FlightController::HorizontalCoordinate::HORIZONTAL_GROUND,
    FlightController::StableMode::STABLE_ENABLE,
  };
  vehicle->flightController->setJoystickMode(joystickMode);
```
> **说明：** 若在无人机飞行的过程中不改变Joystick 中的设置项，则仅在无人机开始执行飞行任务时设置Joystick 模式即可。

2. 设置Joystick 控制指令并执行Joystick 功能   
> **说明：** `joystickCommand`中z轴方向的位置是相对于起飞点高度的绝对高度。

```c
while (elapsedTimeInMs < timeoutInMilSec) {

限定无人机飞行范围
......
// 设置Joystick 控制指令
FlightController::JoystickCommand joystickCommand = {
                    positionCommand.x, positionCommand.y,
                    offsetDesired.z + originHeightBaseHomepoint, yawDesiredInDeg};
vehicle->flightController->setJoystickCommand(joystickCommand);

// 执行Joystick 功能
vehicle->flightController->joystickAction();
......
判断无人机是否进入设定位置的阈值
                                         }
```
