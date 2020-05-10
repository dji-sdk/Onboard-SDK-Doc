---
title: Time Synchronization
date: 2020-05-08
version: 4.0.0
keywords: [Sync, Timestamp, IMU, INS, PPS, sync, shutter, GPS, RTK, NMEA]
---
> **NOTE** This article is **Machine-Translated**. If you have any questions about this article, please send an <a href="mailto:dev@dji.com">E-mail </a>to DJI, we will correct it in time. DJI appreciates your support and attention.     

## Overview
OSDK provides the time synchronization for developers to synchronize the time in the sensors, onboard computer and the drone. It also supports the synchronization of time between drones and GPS systems.

>**NOTE** 
> * Only the **drone with RTK** support Time Synchronization.
> * Before using the time synchronization function, please keep the communication status between the drone and the RTK satellite in the good condition from DJI Pilot or a Mobile APP developed based on MSDK APP, as shown in Figure 1.    
<div>
<div style="text-align: center"><p>Figure 1 Communication Status </p>
</div>
<div style="text-align: center"><p><span>
      <img src="../../images/positioning_prerequisites.png" width="500" alt/></span></p>
</div></div>

## Time Synchronization
Time synchronization is the function that uses PPS signals to synchronize with GPS satellites; the application developed with the "time synchronization" could improve the accuracy of the camera's exposure time and achieve precise positioning ，etc. this function support Developers obtain the RTK data in 1 Hz and GPS data in 5 Hz.

The process of the Time Synchronization is as follows:
1. The drone sends the PPS and UTC time stamp through the hardware, which is used to synchronize the time with the onboard computer and the sensor;
2. When the communication status between the drone and the RTK or GPS satellite is good, the drone will send the RTK data packet at a frequency in 1 Hz and the GPS data packet in 5 Hz, which contain the NMEA data.

> **NOTE** The UTC time stamps generated from the drone on the pulses rising edge (from 0V to 3.3V).

## Develop With Time Synchronization
#### Subscribe NMEA's Information
* Asynchronous
```c++
void subscribeNMEAMsgs(VehicleCallBack cb, void *userData);
void unsubscribeNMEAMsgs();
```

* Synchronize
```c++
bool getNMEAMsg(NMEAType type, NMEAData &nmea);
```

#### Subscribe the time stamp of the UTC
* Asynchronous
```c++
void subscribeUTCTime(VehicleCallBack cb, void *userData);
void unsubscribeUTCTime();
```

* Synchronize

```c++
bool getUTCTime(NMEAData &utc);
```

#### Subscribe the time of the drone
* Asynchronous
```c++
void subscribeFCTimeInUTCRef(VehicleCallBack cb, void *userData);
void unsubscribeFCTimeInUTCRef();
```
* Synchronize
```c++
bool getFCTimeInUTCRef(DJI::OSDK::ACK::FCTimeInUTC &fcTimeInUTC);
```

#### Subscribe the PPS of the drone
* Asynchronous
```c++
void subscribePPSSource(VehicleCallBack cb, void *userData);
void unsubscribePPSSource();
```

* Synchronize
```c++
bool getPPSSource(PPSSource &source);
```

After synchronize the time of the drone, sensor and onboard computer, the PPS hardware pulse output by the deone is as shown in Figure 2. 

<div>
<div style="text-align: center"><p>Figure 2.Time Synchronization Signal</p>
</div>
<div style="text-align: center"><p><span>
      <img src="../../images/samples/pps-uart-logic-analyzer.png" width="550" style="vertical-align:middle" alt/></span></p>
</div></div>
      
