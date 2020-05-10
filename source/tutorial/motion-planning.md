---
title: Motion Planning
date: 2020-05-08
version: 4.0.0
keywords: [Waypoint Mission, Hotpoint Mission]
---
> **NOTE** This article is **Machine-Translated**. If you have any questions about this article, please send an <a href="mailto:dev@dji.com">E-mail </a>to DJI, we will correct it in time. DJI appreciates your support and attention.     

## Overview
DJI OSDK provides a Motion Planning to meet the user's needs for controlling drone flight automation. Developers use the motion planning could design waypoint or Hotpoint Mission with their logic.

## Waypoint Mission
The Waypoint Mission is a control function that controls the drone to fly according to the specified route. Developers can call the DJI OSDK interface to control the drone to **specified altitude** to **specified location** and execut the corresponding actions. The drone can also controlled to execute repeatedly mission, to achieve automatic cruise and other functions.

#### Waypoint
When using waypoint, developer need to specify the number of waypoints and the corresponding waypoint's type.
* Number     
Developers need to use the API interface in the OSDK to specify the waypoints that the drone need fly to. DJI OSDK supports developers add up to 65535 waypoints in a mission, at least is 2.
* Type       
The type refers to the way that the drone fly to the waypoint, which includes curvature flight, straight flight and coordinated turn.
  * Curvature flight    
     * In continuous Curvature Mode, the drone will not stop when it reaches the designated waypoint.
     * In continuous Curvature mode, the dronr will stay at the waypoint.
     * In discontinuous curvature mode, the dronr will stay at the waypoint.
  * Straight Flight    
     * Enter Straight
     * Straight Exit
  * Coordinated Turn: The drone will turns ahead before reaching the waypoint

#### Action

When using Waypoint Mission, the developer could add corresponding actions for the drone at the waypoint, such as taking pictures, recording videos, or hovering.
* Action     
The action is mainly composed by action ID, trigger and the actuator.
  * Action ID:Developer can specify a globally unique action ID to identify the action.
   * Trigger: The trigger is trigger the drone to execut actions, it composed by the type, the parameters corresponding to the trigger type, and each trigger only supports one trigger type.
   * Actuator: The actuator could executes user-specified actions, it composed by the type and the number of the actuator, the parameters of the corresponding actuator, and each actuator supports only one type of execution.
* Number      
DJI OSDK supports developers to add a total of 65535 actions in the mission.
* Action management:
   * Support camera focus zoom action configuration to be automatically executed in the ground station.
   * Support gimbal angle‘s incremental
   * Support multiple camera configuration to an action
* Action trigger
If you want to trigger the drone to execut the specified action during the Waypoint Mission, you need to specified the condition that trigger the action:
   * Timing
   * Distance
   * Serial Actions 
   * Parallel Actions
   * Waypoint trigger (The drone will end the Waypoint Mission in the specified waypoint.) 

#### Speed Control
The developer could configure different speeds for specified waypoints (set multiple speeds for the same waypoint), and supports developers to modify or query the global cruise speed of the drone.

#### Disconnection Control
The developer could configure the control logic to drone when the remote controller is lost.

> **NOTE**
> * When the application developed based on OSDK is used to control the drone to execut missions, users can use the remote controller control the speed, altitude, and the direction of the drone.
> * The drone only can execut one mission. After uploading a new mission, the existing mission will be overwritten.
> * In the Waypoint Mission, the waypoint doesn’t related to the action necessary.

#### Workflow
The workflow of the Waypoint Mission is as follows:
  1. Upload the overall information of the Waypoint      The Waypoint Mission includes the waypoint ID, the total number of waypoints, the number of repetitions, the action for the end of the waypoint, the maximum flight speed and the cruising speed.
2. Upload Waypoint Information     
   * Basic Parameters: waypoint coordinates (the longitude, latitude and height relative to the takeoff point), waypoint type, direction type and flight speed.
   * Optional Parameters: buffer distance, heading angle, steering mode, point of interest, single point maximum flight speed, single point cruising speed.
     > **NOTE** Only after sets all the basic parameters, the developer could set the optional parameters of the waypoint information.
3. Set action information (optional)     
Set the action ID, trigger and actuator
4. Upload the information of the Waypoint Mission 
5. Control the drone to execut Waypoint Mission 
After uploading the drone waypoint and corresponding action's information, the developer can control the drone to execute the Waypoint Mission such as starting, stopping or pausing,etc.

## Hotpoint
Hotpoint Mission is a function that control the drone to fly around a certain area (point of interest) with a specified flight radius. When using Hotpoint Mission, developers need to set the coordinates point, flying height and flying radius and other parameters to control the drone fly around the certain area.

> **NOTE** When the application developed based on OSDK controls the drone to execut Hotpoint, users can use the remote controller to adjust the flight status of the drone, such as altitude, angle and flying radius.

## Develop With Waypoint Mission
When developing With Waypoint Mission, please use `WaypointV2MissionOperator` class to implement Waypoint Mission function.

#### Preparation
Before using the Waypoint Mission, please initializing the drone, obtaining the permission from the drone, creating an instance and executing the Waypoint Mission.
 
* Initialize the drone
```c
LinuxSetup linuxEnvironment (argc, argv);
Vehicle * vehicle = linuxEnvironment.getVehicle ();
if (vehicle == NULL)
{
 std :: cout << "Vehicle not initialized, exiting. \ n";
 return -1;
}
```

* Get control permission
```c
/*! Obtain Control Authority */
vehicle-> control-> obtainCtrlAuthority (functionTimeout);
```

* Instantiate the object      
Create the instantiate object of the waypoint missions and execute waypoint missions

```c
/*! Initialize a new WaypointV2 mission sample */
auto * sample = new WaypointV2MissionSample (vehicle);

/*! run a new WaypointV2 mission sample */
sample-> runWaypointV2Mission ();
```

#### 1. Initialization
Initialize the Waypoint Mission, send the information of the Waypoint Mission to flight controller. The overall information of the Waypoint Mission includes the cruise speed, disconnection control, and waypoint information. The waypoint information includes waypoint's height, latitude and longitude, etc.

```C++
ret = initMissionSetting (timeout);
if (ret! = ErrorCode :: SysCommonErr :: Success)
return ret;
sleep (timeout);
...
...
/*Set overall information of Waypoint Mission*/
WayPointV2InitSettings missionInitSettings;
missionInitSettings.missionID = rand ();
missionInitSettings.repeatTimes = 1;
missionInitSettings.finishedAction = DJIWaypointV2MissionFinishedGoHome;
missionInitSettings.maxFlightSpeed ​​= 10;
missionInitSettings.autoFlightSpeed ​​= 3;
missionInitSettings.exitMissionOnRCSignalLost = 1;
missionInitSettings.gotoFirstWaypointMode = DJIWaypointV2MissionGotoFirstWaypointModePointToPoint;
missionInitSettings.mission = generatePolygonWaypoints (radius, polygonNum);
missionInitSettings.missTotalLen = missionInitSettings.mission.size ();
this-> actions = generateWaypointActions (actionNum);
ErrorCode :: ErrorCodeType ret = vehiclePtr-> waypointV2Mission-> init (& missionInitSettings, timeout);
/*Set waypoint information in Waypoint Mission*/
missionInitSettings.mission = generatePolygonWaypoints (radius, polygonNum);
/* Set the action information of the drone (optional)*/
this-> actions = generateWaypointActions (actionNum);

std :: vector <DJIWaypointV2Action> actionVector;
for (uint16_t i = 0; i <actionNum; i ++)
{
  DJIWaypointV2SampleReachPointTriggerParam sampleReachPointTriggerParam;
 sampleReachPointTriggerParam.waypointIndex = i; /* Set the action number*/
 sampleReachPointTriggerParam.terminateNum = 0;
 /* Set trigger*/
 auto * trigger = new DJIWaypointV2Trigger (DJIWaypointV2ActionTriggerTypeSampleReachPoint, & sampleReachPointTriggerParam);
 /* Set actuator*/
 auto * cameraActuatorParam = new DJIWaypointV2CameraActuatorParam (DJIWaypointV2ActionActuatorCameraOperationTypeTakePhoto, nullptr);
 auto * actuator = new DJIWaypointV2Actuator (DJIWaypointV2ActionActuatorTypeCamera, 0, cameraActuatorParam);
 auto * action = new DJIWaypointV2Action (i, * trigger, * actuator);
 actionVector.push_back (* action);
}
return actionVector;
```


#### 2. Upload Or Download Waypoint Missions
* Upload Waypoint Mission


```c++
uploadWaypointMission(timeout);
if(ret != ErrorCode::SysCommonErr::Success)
return ret;
sleep(waitTime);
```

* Download Waypoint Missions

```c
std::vector<DJIWaypointV2> mission;
dowloadWaypointMission(mission,timeout);
if(ret != ErrorCode::SysCommonErr::Success)
return ret;
sleep(timeout);
```

#### 3. Upload "Action" (optional)
In the process of uploading the "action", the drone will check the legality of the "action". If the check fails, the action cannot be uploaded (but does not affect the drone execute the Waypoint Mission), for details please refer to the corresponding error code.

```c++
uploadWapointActions(timeout);
if(ret != ErrorCode::SysCommonErr::Success)
return ret;
sleep(timeout);
```

#### 4. Execute Waypoint Missions

* Start to execute Waypoint Mission     
Before start to execute the Waypoint Mission, the deonr will check the mission's information uploaded by the user, if fails, the drone will not be able to execut the Waypoint Mission, for details, please check the error code information.

```c
startWaypointMission(timeout);
if(ret != ErrorCode::SysCommonErr::Success)
return ret;
sleep(40);
```

* Pause      
Control the drone pause to execute the Waypoint Mission.

```c
pauseWaypointMission(timeout);
if(ret != ErrorCode::SysCommonErr::Success)
return ret;
sleep(5);
```

* Resume      
Control the drone continue to execut the Waypoint Mission from the paused point.

```c
resumeWaypointMission(timeout);
if(ret != ErrorCode::SysCommonErr::Success)
return ret;
```

#### 5. Global Cruise Speed
Set or get the cruising speed of the drone while execut Waypoint Missions.

* Set Global Cruise Speed
```c
setGlobalCruiseSpeed(1.5, timeout);
if(ret != ErrorCode::SysCommonErr::Success)
return ret;
sleep(timeout);
```

* Get Global Cruise Speed
```c
getGlobalCruiseSpeed(timeout);
if(ret != ErrorCode::SysCommonErr::Success)
return ret;
sleep(timeout);
```

## Develop With Hotpoint 
When develop with Hotpoint, please use the class `HotpointMission`  to implement Waypoint Mission.

> **NOTE** The following describes the steps and methods for controlling the drone to execut Hotpoint Mission in a synchronized manner.

#### 1. Initialization   
Before using the Hotpoint Mission, please initialize the Hotpoint, set the hotpoint‘s information, includes the latitude and longitude of the interest points, flight radius and relative flight height.

```c
 vehicle->missionManager->init(DJI_MISSION_TYPE::HOTPOINT, responseTimeout,NULL);
```
#### 2. Set Hotpoint
Developer need to specify the hotpoint for the drone.

```c
    vehicle->missionManager->hpMission->setHotPoint(broadcastGPosition.longitude, broadcastGPosition.latitude, initialRadius);;
```

#### 3. Take Off
Before control the drone execute the Hotpoint Mission, developer needs control the drone take off.

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

#### 4. Start Hotpoint Mission
Control the drone start to execute the Hotpoint Mission.      

```c 
 std::cout << "Start with default rotation rate: 15 deg/s" << std::endl;
  ACK::ErrorCode startAck = vehicle->missionManager->hpMission->start(responseTimeout);
  if (ACK::getError(startAck))
  {
    ACK::getErrorCodeMessage(startAck, __func__);
  }
```

#### 5. Pause
Pause the Hotpoint Mission which the drone is executing.

```c++
  std::cout << "Pause for 5s" << std::endl;
  ACK::ErrorCode pauseAck =
    vehicle->missionManager->hpMission->pause(responseTimeout);
  if (ACK::getError(pauseAck))
  {
    ACK::getErrorCodeMessage(pauseAck, __func__);
  }
```

#### 6. Resume
Control the drone continue to execut the Hotpoint Mission from the paused point.   
```c
std::cout << "Resume" << std::endl;
  ACK::ErrorCode resumeAck =
    vehicle->missionManager->hpMission->resume(responseTimeout);
  if (ACK::getError(resumeAck))
  {
    ACK::getErrorCodeMessage(resumeAck, __func__);
  }
```

#### 7. Update  
Developer can update the parameters such as radius of the hotpoint when the drone executing the Hotpoint Mission.
```c
  std::cout << "Update radius to 1.5x: new radius = " << 1.5 * initialRadius
            << std::endl;
  vehicle->missionManager->hpMission->updateRadius(1.5 * initialRadius);
```

#### 8. Stop
Control the drone stop executing the Hotpoint Mission.
```c
std::cout << "Stop" << std::endl;
  ACK::ErrorCode stopAck =
    vehicle->missionManager->hpMission->stop(responseTimeout);
```