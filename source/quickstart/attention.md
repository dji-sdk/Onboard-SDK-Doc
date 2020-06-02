---
title: Attention
date: 2020-05-08
version: 4.0.0
keywords: [attention, hardware purchase, software version, firmware version]
---
> **NOTE** 
> * This article is **Machine-Translated**. If you have any questions about this article, please send an <a href="mailto:dev@dji.com">E-mail </a>to DJI, we will correct it in time. DJI appreciates your support and attention.
> * This series of documentation introduces the functions of **OSDK V4.0.0**, as well as the steps and methods of developing software using OSDK V4.0.0. If you are still using OSDK V3.9.x, please download the documentation of [OSDK V3.9.x](https://terra-1-g.djicdn.com/71a7d383e71a4fb8887a310eb746b47f/osdk/OSDK-3.9.0.zip).

Before using OSDK to develop the application, please read this document carefully to avoid improper operation and accidental damage to the drone or onboard computer.

## Firmware Upgrade 
Before to develop the application, please use **DJI Assistant 2** to upgrade the firmware of the drone and hardware platform, for details please refer to [Firmware Release](../appendix/firmware.html)。

## Enable OSDK Control
In order to allow programs developed based on OSDK to communicate normally with the flight platform, please enable the OSDK API control function in DJI Assistant2, as shown in Figure 1.

<div>
<div style="text-align: center"> <p> Figure 1.Enable API Control</p>
</div>
<div style="text-align: center"> <p> <span>
      <img src="../images/common/N1UI.png" width="500" alt /> </span> </p>
</div> </div>

## Permission Statement
The DJI drone;s flight controller can adjust the controlled subject according to the actual flight status and user's need. The level of drone control authority is in order from remote controlle, Mobile APP based on MSDK and the applications developed based on OSDK.

#### Remote Controller
In the DJI control system, the DJI remote control has the highest control authority, and developers can obtain the control right to control the DJI drone at any time.
In P mode, developers can use OSDK to control drones to achieve automated flight:
* In P mode, the drone relies on GNSS and visual positioning system to avoid obstacles to ensure the safety of drone flight;
* When the drone is performing tasks, the user can use the remote control to control the drone and change the flight status of the drone:
   * In the waypoint task, the user can use the joystick to control the flight speed and yaw angle of the drone;
   * Hotpoint mission: Users can control the speed, flight radius (execution of hotspot missions), flight direction and yaw angle of the drone using the joystick.

#### Mobile APP based on MSDK
After the mobile terminal APP developed based on MSDK is connected to the remote control of DJI, in P mode, it can control the drone to perform the specified flight actions, receive the status information of the drone and simple flight control, such as takeoff, landing, camera Control or gimbal control.
* In P mode, use the mobile terminal APP developed based on MSDK to send control commands to the drone.
* When the mobile terminal APP based on MSDK is no longer used to send control commands to the drone, the remote control will gain control of the drone.
* When an application developed based on OSDK controls a drone to perform a specified task, a mobile APP developed based on MSDK can preempt the application's control of the drone, giving priority to controlling the drone to perform the specified actions to ensure that there is no Man-machine and user safety.

#### Application developed based on OSDK
After installing an onboard computer running an application developed based on OSDK to a DJI drone, the user can control the drone in a specified mode.
The steps to control the DJI drone based on the application developed by OSDK are as follows:
1. Adjust the flight mode to P mode
2. Activate the application developed based on OSDK
3. Obtain control permission to control the DJI drone

#### Disconnected Control
When DJI's drone is in flight, if disconnected from the remote controller or onboard computer, it will execute the control of the drone flight according to the following logic:
* When developer **only uses the remote controller** to control the DJI drone to perform the flight mission, if the signal between the DJI drone and the remote control is interrupted, the DJI drone will fellow the **disconnection control strategy** sette'd on the Mobile App which developed based on MSDK.
* When the user uses the remote control and **connects to the onboard computer** to control the drone, the drone will automatically execute the flight task according to the logic in the onboard computer. Switch the gear (random switch only) and then user could control the drone with the remote controller; if the signal between the onboard computer and the DJI drone is interrupted, the developer needs to specify the corresponding control strategy, such as hovering, landing, or returning. Developer **uust enable the safe return function** to ensure that the onboard computer and the DJI drone can return safely according to the specified return strategy when the connection is lost, as shown in Figure 2.

<div>
<div style="text-align: center"> <p> Figure 2. Enable SDK Failsafe Action </p>
</div>
<div style="text-align: center"> <p> <span>
      <img src="../images/guides/sdk-failsafe.png" width="500" alt /> </span> </p>
</div> </div>

## Simulate and Debug
In order to reduce the occurrence of damage to the drone or accidents due to internal failures of applications developed based on OSDK, DJI strongly requires developers to use the simulator in DJI Assistant 2 to simulate the flight status of the drone , And according to the data and log information in the simulator **debug** application, reduce the risk of drone damage or accidents, and avoid unnecessary losses.
* Before using OSDK to develop applications, please obey the laws of the local please. **The safety issues or legal disputes caused by the use of OSDK are not related to DJI**. DJI does not assume any responsibility for any use of OSDK legal risks and responsibilities.
* Before using flight mission, please simulate the application in DJI Assistant 2.

> **NOTE** The data generated by DJI Assistant 2 simulation application is the test data when the application is simulated. Developers cannot obtain the raw data of the drone in the simulation.

#### Using DJI Pilot
When Matrice 210 V2 and Matrice 210 RTK V2 ware equipped with Onboard Computer, developer could use DJI Pilot simulate the Application which based on OSDK, it is necessary to use DJI Pilot to simulate the application which developed based on OSDK, and the steps is as follows:
1. Copy the configuration file **“UserConfig.txt"** of the corresponding platform (/onboard SDK/sample/platform) in the OSDK development package to the directory that the application is executed;
2. Copy the configuration tool **M210configtool** of the corresponding platform (/utility/bin) in the OSDK  development package to the directory that the application is executed;
3. Execute with the following command
```c
./M210ConfigTool --usb-port /dev/ttyACM0 --config-file UserConfig.txt --usb-connected-flight on
```
> **NOTE**
>* This command will fail after restart the drone and development platform. Please use the command to start the drone's simulation feature before you need.
>* DJI pilot does not have the visual interface, developer only could view the status of the Application by the Map, Attitude, Altitude, Speed and other data.

#### Using DJI assistant 2
 enables developers to use the emulator in DJI assistant 2 to simulate osdk based applications.
 
#### Using DJI Assistant 2
After connecting the M300 RTK to DJI Assistant 2, developer can use the simulator in DJI Assistant 2 to simulate the flight of the drone.