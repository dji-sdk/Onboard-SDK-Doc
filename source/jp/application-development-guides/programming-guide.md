---
title: Programming Guide 
date: 2016-06-24
---

All structures and functions are implemented in `DJI_Type.h`and`DJI_API.h`. For more details, please refer to the source code.

## System Configuration

Before starting with the official library, developers should create a serial device driver for their own platform by inheriting the `HardDriver` class,  implementing the lock and unlock functions, together with several other virtual functions, and then create a new API sample with their inherited class working as the pointer to the hardware interface. You will also need to create two life-long threads(or one, at least) running sendPoll and readPoll functions repeatedly. (Note: the frequency should be lower 100Hz)

We provide example programs in Linux and Windows platform with QT and terminal environment - these examples can help you get pointers on building your own framework to work with the DJI Onboard SDK library. We also provide a ROS interface and an STM32 embedded system example.  

## Callback Mechanism

For all commands which have return values mentioned in OPEN Protocol, developers can get the return value by callback functions.

Activation function in QT sample code as an example:   

1.Define the callback function.  

```c
static void activationCallback(CoreAPI* api, Header* protocolHeader, UserData userData);
```

2.Pass the name of callback function when you call activate.

```c
api->activate(&data, DJIonboardSDK::activationCallback, this);
```

3.The meaning of return values(result) is explained for each command in the [OPEN Protocol](../introduction/index.html#CMD-Val-ACK-Val) document.

## Activation

```c
api->activate(&data, DJIonboardSDK::activationCallback, this);
```

## Obtain/Release Control Authorization

Before obtaining Control Authorization, please ensure that: 

* The 'enable API control' box is checked in the assistant software.
* The mode selection switch of the remote controller is placed at the F position.

```c
api->setControl(true, DJIonboardSDK::setControlCallback, this);
```

## Take off, Land and Return to home (RTH)

For the return value of this function please refer to [Request Switch Result](../introduction/index.html#CMD-ID-0x02-Request-Switch-Result)(Below codes do not use callback function).  

```c
flight->task(type);
```

## Movement Control


We recommend developers to send their Movement Control commands at 50Hz frequency. Developers can implement that by `usleep(20000)`、`ros::Duration(1/50)` or other ways which depend on the development environment.

For Movement Control, specific meanings of arguments are decided by the control mode byte. For more info about Movement Control, please refer to [Control mode byte part in Appendix](../appendix/index.html#Control-Mode-Byte).

We recommend developers to use `HORI_POS` mode for horizontal movement. More details are shown in [Position-Control(HORI_POS)](#position-control-hori-pos) in this document. In this mode, speed and attitude are controlled by autopilot, thus developers do not need to worry about that.
    
Please note that certain conditions are required for some control modes to be functional:

* Only when the GPS signal is good (health\_flag >=3)，horizontal position control (HORI_POS) related control modes can be used.
* Only when GPS signal is good (health\_flag >=3)，or when Gudiance system is working properly with Autopilot，horizontal velocity control(HORI_VEL)related control modes can be used.

```c
FlightData data;
data.flag = flightFlag;
data.x = flightx;
data.y = flighty;
data.z = flightz;
data.yaw = flightyaw;
flight->setFlight(&data);
```

## Receive Flight Data

If developers want to get Flight Data, please check the available items on the SDK tab of DJI Assistant 2.

Developers need to declare correct structure variables to save Flight Data. The DJI_API.h and DJI_Type.h files contain sample structs for correctly accepting all kinds of broadcast data. 

Get quaternion as an example:  

1. Declare quaternion struction

```c
typedef struct QuaternionData
{
    float32_t q0;
    float32_t q1;
    float32_t q2;
    float32_t q3;
} QuaternionData;

QuaternionData q;
```


2、Get the quaternion

```c
q = flight->getQuaternion()
```

Other data types and functions to obtain the corresponding data sent outside from autopilot, please refer `DJI_Type.h`

```c
typedef struct BroadcastData
{
    unsigned short dataFlag;
    TimeStampData timeStamp;
    QuaternionData q;
    CommonData a;
    VelocityData v;
    CommonData w;
    PossitionData pos;
    MagnetData mag;
    RadioData rc;
    GimbalData gimbal;
    FlightStatus status;
    BatteryData battery;
    CtrlInfoData ctrlInfo;

    //! @note these variables are not send from FMU,
    //! just a record for user.
    uint8_t controlStatus;
    uint8_t activation;
} BroadcastData;

```

## GPS to North-East Coordinate
Convert GPS to North-East-Down Coordinate. (GPS in radian，North-East Coordinate in meter)
For example, `origin_longti` and `origin_lati` , as the longitude and latitude of original position，are decided by developers and the position of UAV taking off is recommended to be the original position. `longti` and `lati` are longitude and latitude of UAV's current posistion. `x` and `y` are offset to the original position in the North and the East directions. The unit of offset is meter.

~~~c
#define C_EARTH (double) 6378137.0
/* From GPS to Ground */
{
    double dlati = lati-origin_lati;
    double dlongti= longti-origin_longti;

    double x = dlati * C_EARTH;
    double y = dlongti * C_EARTH * cos(lati / 2.0 + origin_lati / 2.0);
}
~~~

## Quaternion to RPY

Convert quaternion to roll, pitch and yaw in radian in body coordinate.

~~~c
    api_quaternion_data_t q;
    DJI_Pro_Get_Quaternion(&q);

    float roll  = atan2(2.0 * (q.q3 * q.q2 + q.q0 * q.q1) , 1.0 - 2.0 * (q.q1 * q.q1 + q.q2 * q.q2));
    float pitch = asin(2.0 * (q.q2 * q.q0 - q.q3 * q.q1));
    float yaw   = atan2(2.0 * (q.q3 * q.q0 + q.q1 * q.q2) , - 1.0 + 2.0 * (q.q0 * q.q0 + q.q1 * q.q1));
~~~

## Position Control(HORI_POS)

The input horizatal arguments are the offset between current position and target position, when `HORI_POS` is the mode of horizontal movement control. The unit of offset is meter.

For example, in ground frame, `target` is target position and `current` is UAV's current position. The coordinates of these positions are caculated by GPS, Guidance or other sensors. In most cases, GPS is the correct way to make this work.

Because, for the autopilot, the maximum frequency of receiving data is 50Hz, the frequency of calculating offset should be over 50Hz to ensure the closed-loop control is vaild.  

~~~c
void update_offset()
{
    offset_x = target_x - current_x;
    offset_y = target_y - current_y;
}

/* Command thread */

FlightData data;
data.flag = 0x90;
data.x = offset_x;
data.y = offset_y;
data.z = target_z;
data.yaw = target_yaw;
flight->setFlight(&data);

~~~

