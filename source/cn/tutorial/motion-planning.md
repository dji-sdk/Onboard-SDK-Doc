---
title: 运动规划
date: 2020-05-08
version: 4.0.0
keywords: []
---

## 概述
DJI OSDK 为满足用户对控制无人机飞行自动化的需求，提供了运动规划功能；开发者使用运动规划功能，可根据实际的使用需求设计相应的航点任务和热点任务，制定控制无人机自动化飞行的控制逻辑。

## 航点任务
航点规划是一个控制无人机按照指定的航线飞行，实现无人机飞行自动化的控制功能。开发者通过调用DJI OSDK 的接口，能够控制无人机以**指定的高度**飞往**指定位置**并执行相应动作，根据实际的使用需求，还可控制无人机重复多次执行指定的任务，实现自动化巡航等功能。

#### 航点
开发者在使用航点任务时，需要指定航点数量和对应的航点类型。
* 航点数量    
使用航点任务时，开发者需使用OSDK 中的API 接口指定无人机所需飞达的航点，DJI OSDK 支持开发者在一个任务中最多添加65535 个航点，至少2个航点。
* 航点类型     
航点类型是指无人机在执行航点任务时，飞向该航点的方式，其中包含曲率飞行、直线飞行和协调转弯。
   * 曲率飞行     
      * 无人机以曲率连续的方式执行飞行任务时，到达指定的航点不停留。
      * 无人机以曲率连续的方式执行飞行任务时，在航点处停留。
      * 无人机以曲率不连续的方式执行飞行任务时，在航点处停留。
   * 直线飞行
      * 直线进入
      * 直线退出
  * 协调转弯：无人机在到达航点前提前转弯

#### 动作

开发者在使用航点任务时，开发者或用户可为无人机在指定的航点处添加对应的动作，如拍照、录像或悬停等。
* 动作信息   
动作信息主要由动作ID、触发该动作的触发器和执行该动作的执行器组成。
   * 动作ID，开发者可指定全局唯一的动作ID 标识用户设置的动作。 
   * 触发器：触发无人机执行动作的触发器，包含触发器的类型，以及该触发类型所对应的参数。每个触发器仅支持一种触发类型。
   * 执行器：执行用户指定动作的模块，包含执行器的类型和执行器的编号，以及该执行器所对应的参数。每个执行器仅支持一种执行类型
* 动作数量     
DJI OSDK 支持开发者最多在一个任务中总共可添加65535 个动作。
* 动作管理：
   * 支持将相机对焦变焦的动作配置到地面站中自动执行。
   * 支持云台角度增量控制
   * 支持配置多个云台多个相机
* 动作触发    
如需在无人机执行航点任务的过程中，触发无人机执行指定的动作，需要添加触发该动作的条件：
   * 定时触发
   * 距离触发
   * 动作串行触发
   * 动作并行触发
   * 航点触发：无人机在航点飞行时，在第N个航点结束航点任务

#### 速度控制
OSDK 为开发者提供了速度控制功能，能够使开发者为指定的航点配置不同的速度（为同一个航点设置多个速度），支持开发者在无人机执行航线飞行任务时，修改或查询无人机全局巡航速度。

#### 断连控制
新增支持配置遥控器失联后继续执行航线任务的功能。

> **说明** 
> * 基于OSDK 开发的应用程序在控制无人机执行任务时，用户可使用遥控器控制无人机如无人机的飞行速度、飞行高度和飞行航向等。
> * 无人机每次只能执行一个自动化飞行任务，上传新的任务后，已有的飞行任务将会被覆盖。
> * 在航点任务中，无人机的航点与无人机的动作没有必然关系，开发者可根据实际情况添加航点和无人机飞行时的动作。

#### 工作流程
航点任务功能按如下流程，控制无人机执行航点任务：
1. 上传航线任务的整体信息     
一个航点任务包含航点任务的ID、航点任务的航点数、任务重复次数、航点任务结束后的动作、最大飞行速度和巡航速度。
2. 上传航点信息      
   * 基础参数：航点坐标（设置航点的经度、纬度和相对于起飞点的高度）、航点类型、航向类型和飞行速度。
   * 可选参数：缓冲距离、航向角度、转向模式、兴趣点、单点最大飞行速度、单点巡航速度。
      > **说明：** 仅开发者设置航点信息所有的基础参数后，才能设置航点信息的可选参数。
3. 设置动作信息（可选）      
设置动作的ID、触发器和执行器
4. 上传无人机的航点任务的信息        
5. 控制无人机执行航点任务      
上传无人机航点和对应的动作信息后，开发者即可通过指定的接口控制航点任务，如开始、停止或暂停任务，设置或获取巡航速度等。  

## 热点任务
航点任务是一种控制无人机以指定的飞行半径**围绕**某一区域（兴趣点）飞行的控制功能。在使用热点任务时，开发者需设置兴趣点的坐标，无人机的飞行高度及飞行半径等参数，控制无人机围绕某一区域飞行。    
> **说明：** 基于OSDK 开发的应用程序在控制无人机执行任务时，用户可使用遥控器调整无人机的飞行状态，如飞行高度，航向角和环绕半径等。

## 使用航点任务功能
如需使用航点任务，请使用DJI OSDK 的WaypointV2MissionOperator 类实现航点任务功能。
#### 飞行前准备
在使用航点任务前，请先完成无人机飞行准备，如初始化无人机、获取控制无人机的权限，创建实例并执行航点任务。
 
* 初始化无人机的飞行环境
```c
LinuxSetup linuxEnvironment(argc, argv);
Vehicle* vehicle = linuxEnvironment.getVehicle();
if (vehicle == NULL)
{
 std::cout << "Vehicle not initialized, exiting.\n";
 return -1;
}
```

* 获取无人机的控制权限
```c
/*! Obtain Control Authority*/
vehicle->control->obtainCtrlAuthority(functionTimeout);
```

* 创建航点任务的示例，并执行航点任务
```c
/*! Initialize a new WaypointV2 mission sample*/
auto *sample = new WaypointV2MissionSample(vehicle);

/*! run a new WaypointV2 mission sample*/
sample->runWaypointV2Mission();
```

#### 1. 航点任务初始化
初始化航点任务的信息，向无人机飞行控制器发送航点任务的整体信息和航点信息，其中航点任务的整体信息包括无人机的巡航速度、断连控制和航点信息等；航点信息包含航点高度，航点经纬度等。

```C++
ret = initMissionSetting(timeout);
if(ret != ErrorCode::SysCommonErr::Success)
return ret;
sleep(timeout);
......
......
/*设置航点任务的整体信息*/
WayPointV2InitSettings missionInitSettings;
missionInitSettings.missionID = rand();
missionInitSettings.repeatTimes = 1;
missionInitSettings.finishedAction = DJIWaypointV2MissionFinishedGoHome;
missionInitSettings.maxFlightSpeed = 10;
missionInitSettings.autoFlightSpeed = 3;
missionInitSettings.exitMissionOnRCSignalLost = 1;
missionInitSettings.gotoFirstWaypointMode = DJIWaypointV2MissionGotoFirstWaypointModePointToPoint;
missionInitSettings.mission = generatePolygonWaypoints(radius, polygonNum);
missionInitSettings.missTotalLen = missionInitSettings.mission.size();
this->actions = generateWaypointActions(actionNum);
ErrorCode::ErrorCodeType ret = vehiclePtr->waypointV2Mission->init(&missionInitSettings,timeout);
/*设置航点任务中航点的信息*/
missionInitSettings.mission = generatePolygonWaypoints(radius, polygonNum);
/*设置无人机的动作信息（可选）*/
this->actions = generateWaypointActions(actionNum);

std::vector<DJIWaypointV2Action> actionVector;
for(uint16_t i = 0; i < actionNum; i++)
{
  DJIWaypointV2SampleReachPointTriggerParam sampleReachPointTriggerParam;
 sampleReachPointTriggerParam.waypointIndex = i;/*设置动作的编号*/
 sampleReachPointTriggerParam.terminateNum = 0;
 /*设置触发器*/
 auto *trigger = new DJIWaypointV2Trigger(DJIWaypointV2ActionTriggerTypeSampleReachPoint,&sampleReachPointTriggerParam);   
 /*设置执行器*/
 auto *cameraActuatorParam = new DJIWaypointV2CameraActuatorParam(DJIWaypointV2ActionActuatorCameraOperationTypeTakePhoto, nullptr);
 auto *actuator = new DJIWaypointV2Actuator(DJIWaypointV2ActionActuatorTypeCamera, 0, cameraActuatorParam);
 auto *action = new DJIWaypointV2Action(i, *trigger,*actuator);
 actionVector.push_back(*action);
}
return actionVector;
```


#### 2. 上传或下载航点任务
* 上传航点任务

```c++
uploadWaypointMission(timeout);
if(ret != ErrorCode::SysCommonErr::Success)
return ret;
sleep(waitTime);
```

* 下载航点任务

```c
std::vector<DJIWaypointV2> mission;
dowloadWaypointMission(mission,timeout);
if(ret != ErrorCode::SysCommonErr::Success)
return ret;
sleep(timeout);
```

#### 3. 上传“动作”（可选）
在上传无人机所需执行的“动作”的过程中，无人机会检查“动作”的合法性检查，若检查不通过，则无法上传动作（但不影响无人机飞行），详情请参考相应的错误码。
```c++
uploadWapointActions(timeout);
if(ret != ErrorCode::SysCommonErr::Success)
return ret;
sleep(timeout);
```

#### 4. 控制无人机执行航点任务

* 开始执行航点任务
无人机开始执行航点任务前，将先检查用户上传的任务信息，若检查失败，无人机将无法执行航点任务，详情请查看错误码信息。

```c
startWaypointMission(timeout);
if(ret != ErrorCode::SysCommonErr::Success)
return ret;
sleep(40);
```

* 暂停执行航点任务
控制无人机暂停执行航点任务。

```c
pauseWaypointMission(timeout);
if(ret != ErrorCode::SysCommonErr::Success)
return ret;
sleep(5);
```

* 恢复执行航点任务
控制无人机从暂停的位置，继续执行为完成的航点任务。
```c
resumeWaypointMission(timeout);
if(ret != ErrorCode::SysCommonErr::Success)
return ret;
```

#### 5. 设置无人机的巡航速度
设置或获取无人机在执行航点任务时的巡航速度。
* 设置巡航速度
```c
setGlobalCruiseSpeed(1.5, timeout);
if(ret != ErrorCode::SysCommonErr::Success)
return ret;
sleep(timeout);
```

* 获取巡航速度
```c
getGlobalCruiseSpeed(timeout);
if(ret != ErrorCode::SysCommonErr::Success)
return ret;
sleep(timeout);
```

## 使用热点任务功能
如需使用航点任务，请使用DJI OSDK 的HotpointMission 类实现航点任务功能。       
> **说明：** 如下介绍以同步的方式介绍控制无人机执行热点任务的步骤和方法。     

#### 1. 初始化热点任务   
在使用热点任务前，请先初始化热点任务，并调用接口设置热点任务的信息。其中热点任务的信息包括无人机执行热点任务时兴趣点的经纬度信息、飞行半径和相对飞行高度等。    
```c
 vehicle->missionManager->init(DJI_MISSION_TYPE::HOTPOINT, responseTimeout,NULL);
```

#### 2. 设置热点(兴趣点)
控制无人机执行热点任务时，需为无人机指定热点（兴趣点）
```c
    vehicle->missionManager->hpMission->setHotPoint(broadcastGPosition.longitude, broadcastGPosition.latitude, initialRadius);;
```

#### 3. 控制无人机起飞
控制无人机执行热点任务时，需先控制无人机起飞。

```c
  ACK::ErrorCode takeoffAck = vehicle->control->takeoff(responseTimeout);
  if (ACK::getError(takeoffAck))
  {
    ACK::getErrorCodeMessage(takeoffAck, __func__);

    if(takeoffAck.info.cmd_set == OpenProtocolCMD::CMDSet::control
       && takeoffAck.data == ErrorCode::CommonACK::START_MOTOR_FAIL_MOTOR_STARTED)
    {
      DSTATUS("Take off command sent failed. Please Land the drone and disarm the motors first.\n");
    }
```

#### 4. 开始执行热点任务
控制无人机根据热点任务中的信息执行热点任务。      

```c 
 std::cout << "Start with default rotation rate: 15 deg/s" << std::endl;
  ACK::ErrorCode startAck = vehicle->missionManager->hpMission->start(responseTimeout);
  if (ACK::getError(startAck))
  {
    ACK::getErrorCodeMessage(startAck, __func__);
  }
```

#### 5. 暂停执行热点任务
控制无人机暂停执行的热点任务。

```c++
  std::cout << "Pause for 5s" << std::endl;
  ACK::ErrorCode pauseAck =
    vehicle->missionManager->hpMission->pause(responseTimeout);
  if (ACK::getError(pauseAck))
  {
    ACK::getErrorCodeMessage(pauseAck, __func__);
  }
```

#### 6. 恢复执行热点任务
控制无人机从暂停的位置，继续执行为完成的热点任务。   
```c
std::cout << "Resume" << std::endl;
  ACK::ErrorCode resumeAck =
    vehicle->missionManager->hpMission->resume(responseTimeout);
  if (ACK::getError(resumeAck))
  {
    ACK::getErrorCodeMessage(resumeAck, __func__);
  }
```

#### 7. 更新飞行数据
在无人机执行热点任务的过程中，开发者可更新无人机的参数，如下以更新飞行半径为例。
```c
  std::cout << "Update radius to 1.5x: new radius = " << 1.5 * initialRadius
            << std::endl;
  vehicle->missionManager->hpMission->updateRadius(1.5 * initialRadius);
```

#### 8. 停止执行热点任务
控制无人机停止执行热点任务。
```c
std::cout << "Stop" << std::endl;
  ACK::ErrorCode stopAck =
    vehicle->missionManager->hpMission->stop(responseTimeout);
```

