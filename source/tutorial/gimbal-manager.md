---
title: Gimbal Management
date: 2020-05-08
version: 4.0.0
keywords: [Gimbal Control]
---

> **NOTE** This article is **Machine-Translated**. If you have any questions about this article, please send an <a href="mailto:dev@dji.com">E-mail </a>to DJI, we will correct it in time. DJI appreciates your support and attention.     

## Overview
Using the "Gimbal Control" function of the OSDK, developers could control the gimbal execute the action according to the logic designed by developer.

## Concept
### Gimbal Angle
#### Joint angle and attitude angle
Figure 1 shows the joints of the gimbal. The joint of the gimbal is the motor to drive the payload. This tutorial uses the body coordinate system to describe the joint angle of the gimbal.  

<div>
<div style="text-align: center"><p>Figure1. Joint Angle  </p>
</div>
<div style="text-align: center"><p><span>
      <img src="../../images/joint-angle-en.png" width="220" alt/></span></p>
</div></div>
  
#### Attitude and attitude angle
Figure 2 shows the attitude of the payload, according to the control command, the gimbal could spin the payload to a different position. This tutorial uses the geodetic coordinate system (NED, North East Coordinate System) to describe the attitude angle of the payload, this angle is also called Euler-Angle.

<div>
<div style="text-align: center"><p>Figure 2 Attitude Angle  </p>
</div>
<div style="text-align: center"><p><span>
      <img src="../../images/gimbal_up-en.png" width="500" alt/></span></p>
</div></div>
   


### Gimbal Control 
#### Control Method 
There are three control methods:
* Absolute Angle Control     
 According to the user's command, the gimbal will rotate from the current position to the specified position within a specified time.
* Speed ​​Control     
Users could control the rotation speed of the gimbal. 
  
  > **NOTE**
    >* In the Angle Control, the rotation time of the gimbal is limited by the maximum rotation speed and maximum acceleration of the gimbal, and the actual rotation angle is limited by the limit angle of the gimbal.
    > * In the Speed Control, the gimbal rotates for 0.5s according to the speed specified by the user. When the gimbal rotates to the limit angle, it will stop.

* Gimbal mode     
The current gimbal control function of OSDK **only supports** free mode, in this mode, when the drone's attitude changes, the gimbal will not rotate.


### Gimbal’s Information
Applications developed based on the OSDK can obtain the current information of the specified Gimbal. For details, please refer to **OSDK API Documentation**.

## Develop With GimbalManager

#### 1. Initialization
Befor using GimbalManager developer need call the class `GimbalManagerSyncSample` to create the object of the GimbalManager and initialize the gimbal specified.

```c++
GimbalManagerSyncSample *g = new GimbalManagerSyncSample(vehicle);
ret = vehicle->gimbalManager->initGimbalModule(PAYLOAD_INDEX_0,
                                                "Sample_gimbal_1");

if (ret != ErrorCode::SysCommonErr::Success)
{
  DERROR("Init Camera module Sample_gimbal_1 failed.");
  ErrorCode::printErrorCodeMsg(ret);
}
ret = vehicle->gimbalManager->initGimbalModule(PAYLOAD_INDEX_1,
                                                "Sample_gimbal_2");
```

#### 2. Obtain The Information 
After initial the GimbalManager developer could obtain the information of the gimbal.

```c++
DSTATUS("Current gimbal %d angle (p,r,y) = (%0.2f°, %0.2f°, %0.2f°)", PAYLOAD_INDEX_0,
      g->getGimbalData(PAYLOAD_INDEX_0).pitch,
      g->getGimbalData(PAYLOAD_INDEX_0).roll,
      g->getGimbalData(PAYLOAD_INDEX_0).yaw);
```

### 3. Route The Gimbal
Using the interface `GimbalManagerSyncSample` to control the attitude of the gimbal.

```c++
GimbalModule::Rotation rotation;
        rotation.roll = 0.0f;
        rotation.pitch = 25.0f;
        rotation.yaw = 90.0f;
        rotation.rotationMode = 0; 
        rotation.time = 0.5;
        g->rotateSyncSample(PAYLOAD_INDEX_0, rotation);
```

### 4. Gimbal Reset
The application developed based on OSDK support reset the pitch and yaw axes of the gimbal.

```c++
g->resetSyncSample(PAYLOAD_INDEX_0);
```


