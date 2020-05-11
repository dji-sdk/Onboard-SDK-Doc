---
title: Basic Control
date: 2020-05-08
version: 4.0.0
keywords: [Flight control, drone control, drone parameters, basic functions, joystick, basic functions]
---

> **NOTE** This article is **Machine-Translated**. If you have any questions about this article, please send an <a href="mailto:dev@dji.com">E-mail </a>to DJI, we will correct it in time. DJI appreciates your support and attention.     

## Overview
Using drone flight control function of OSDK, you can set and obtain various basic parameters of the drone, control the drone to perform basic flight actions, and complex flight actions through the Joystick function.

## Concepts
### Basic Parameters
OSDK has opened interfaces for setting basic parameters of drones:
* Turn on or off the RTK function and obstacle avoidance function (horizontal obstacle avoidance and top obstacle avoidance)
* Set the home point and back altitude of the drone

The application with [Message Subscription](./massage-manager.html) could help users to obtain information about the basic parameters of the drone：
* Get the status of RTK and obstacle avoidance (horizontal and top obstacle avoidance)
* Back home point and altitude

### Basic Action
The basic flying actions of drones include three types: lock, takeoff and landing, and back to home. Developers can use the interface provided by OSDK to control the drone perform the specified flight action.

<div>
<div style="text-align: center"> <p> Table 1. Basic Action </div>
  <table>
    <thead>
      <tr>
      <th> Type </th>
      <th> Item </th>
      <th> Details</th>
      </tr>
    </thead>
<tbody>
      <tr>
         <td rowspan=2>Lock </td>
         <td> Unlock </td>
         <td> If the drone is unlocked, the drone ’s propeller will rotate at idle speed, but will not fly off the ground </td>
      </tr>
      <tr>
         <td> Lock </td>
         <td> If the drone is locked, the propeller of the drone changes from idle to static state </td>
      </tr>
      <tr>
         <td rowspan=5> Take off and Land </td>
         <td> Auto take off </td>
         <td> The drone will automatically take off 1.2 meters (the height cannot be adjusted) </td>
      </tr>
      <tr>
         <td> Automatic Landing </td>
         <td> The drone will land automatically </td>
      </tr>
      <tr>
         <td> Cancel Automatic Landing </td>
         <td> The drone will stop landing during the descent and hover </td>
      </tr>
      <tr>
         <td> Landing Confirmation </td>
         <td> When the drone has landed a certain distance from the ground, users can use this function to confirm that the drone has landed on the ground </td>
      </tr>
      <tr>
         <td> Forced Landing </td>
         <td> Ignore the status of the landing surface and force the drone to land (the landing speed is faster) </td>
      </tr>
      <tr>
         <td rowspan=2> Back To Home</td>
         <td> Return </td>
         <td> The drone will automatically return home </td>
      </tr>
      <tr>
         <td> Cancel </td>
         <td> The drone will hover </td>
      </tr>
</tbody>
</table>
</div>

> **NOTE**
> * Different drones may have different heights when taking off, landing and returning. Please refer to the User's manual of the drone for details.
> * After unlocked, if the takeoff command is not received, the drone will automatically lock and the propeller will stop rotating. If the drone fails to unlock, please query the reason for the unlock failure according to the error code.


### Joystick
Joystick is a comprehensive drone control function. When using the Joystick function, need **set the Coordinate System, Horizontal Mode, Vertical Mode, Yaw Angle Mode and Self-Stability Mode at same time**.

#### Coordinate System
* Body Coordinate System
The Body Coordinate System uses the center of gravity as the origin, the direction of the head is the X axis, and the right side of the head is the Y axis. The Z axis is perpendicular to the X axis and the Y axis(follow the "right-hand rule"). In the body coordinates, the flying action rotates around the X axis, Y axis and Z axis,it also can be called roll (the drone only rotates around the X axis), pitch (the drone only rotates around the Y axis) And yaw (the drone only rotates around the Z axis).

* Geodetic Coordinate System
The Geodetic Coordinate System is also called the Ground Coordinate System or the Local Horizontal Coordinate System. In this coordinate system, the direction of the drone pointing to the north of the earth is the X axis, and the direction of the east is the Y axis. The X axis and the Y axis are perpendicular to each other, The Z axis points vertically below the drone.(follow the "right-hand rule"), the Z axis will adjust the angle according to the actual situation of the drone, so this coordinate system is also called "North-East-Earth (NED) Coordinates System".

#### Horizontal Mode
* Attitude angle control mode: In this mode, the command in the horizontal direction is the attitude angle of the drone. (In the body coordinate system, the angle is roll and pitch)
* Speed ​​control mode: In this mode, the command in the horizontal direction is the speed of the drone
* Position control mode: In this mode, the command in the horizontal direction is the position of the drone
  > **NOTE** If the mode of the position command is not 0, the drone will fly forward at the specified speed, otherwise, the drone will hover at the specified position.
* Angular speed control: In this mode, the horizontal direction is the rotation angular speed of the drone

###### Hover mode
Only in the speed control mode in the **Horizontal mode**, the developer can set the hovering mode of the drone:
* Turn on the stable mode: After the stable mode is turned on, the drone will hover at the specified position
* Turn off the stable mode: After turning off the stable mode, the drone will fly according to the speed command. When the forward speed of the drone is 0, the drone may flutter with the wind

#### Vertical Mode
* Speed ​​control mode: Control the vertical speed of the drone
* Position control mode: Control the vertical position of the drone, which is an absolute position relative to the take-off point
* Accelerator control mode: Control the accelerator of the drone

#### Yaw Control Mode
* Angle control mode: In this mode, the command rotate the drone in the yaw direction is the yaw angle
* Angular rate control mode: In this mode, the command rotate the drone in the yaw direction is the angular rate of the yaw

### Drone Height
The basic height concept of DJI's drone during the flight is shown in Table 2.

<div>
<div style="text-align: center"> <p> Table 2. Concept Of The Height  </div>
<table>
<thead>
<th style="border-left: none;"> </th>
<th> Relative Takeoff Altitude </th>
<th> Fusion Height </th>
<th> GPS Altitude </th>
<th> RTK Height </th>
<th> Relative Altitude </th>
</thead>
<tbody>
<tr>
 <th style="border-left: none"> Basic Concept </th>
<td> Altitude change of drone relative to take-off point </td>
<td> The barometer value is used as the initial value, using the fusion algorithm and the altitude value output with the help of the data from all sensors on the drone </td>
<td> Real-time ellipsoid height based on GPS satellite output </td>
<td> Real-time ellipsoid height based on RTK technology output </td>
<td> The distance between the drone and the object below it by using the ranging sensor on the drone </td>
</tr>
<tr>
 <th style="border-left: none"> Source </th>
<td> IMU (which may include vision sensors, GPS, and RTK) and barometers </td>
<td> IMU (which may include vision sensors, GPS, and RTK) and barometers </td>
<td> GPS satellite </td>
<td> RTK satellite </td>
<td> TOF or ultrasound and IMU </td>
</tr>
<tr>
 <th style="border-left: none"> Height 0 Points </th>
<td> The point where the drone takes off from the ground </td>
<td> Standard pressure sea level </td>
<td> WGS84 coordinate system </td>
<td> RTK coordinate system (C2000, WGS84 or user specified coordinate system) </td>
<td> The surface of hard objects (such as the ground) directly below the drone </td>
</tr>
<tr>
 <th style="border-left: none"> Application Usage Scenarios </th>
<td> Used to get the current flying height of the drone </td>
<td> For more precise and stable control of drones to perform flight tasks </td>
<td> Used to analyze flight missions and flight status of drones </td>
<td> Used in missions such as precision mapping and waypoint flight </td>
<td> For the safe landing of drones (obstacle avoidance and speed reduction) </td>
</tr>
<tr>
 <th style="border-left: none"> Effective Range </th>
<td> Several kilometers </td>
<td> Several kilometers </td>
<td> Several kilometers </td>
<td> Several kilometers </td>
<td> Within 10 meters </td>
</tr>
<tr>
 <th style="border-left: none"> How to Get </th>
<td> Get this information through DJI Pilot </br> Mobile APP developed based on MSDK can subscribe to this information </td>
<td> Mobile APP developed based on MSDK can subscribe to this information </td>
<td> Mobile APP developed based on MSDK can subscribe to this information </td>
<td> Mobile APP developed based on MSDK can subscribe to this information </td>
<td> Get this information through DJI Pilot </br> Mobile APP developed based on MSDK can subscribe to this information </td>
</tr>
<tr>
 <th style="border-left: none"> Error </th>
<td> Yes, the altitude accuracy will be affected by the flying distance of the drone </td>
<td> Yes, the altitude accuracy will be affected by the flying distance of the drone </td>
<td> None </td>
<td> None </td>
<td> None </td>
</tr>
<tr>
 <th style="border-left: none"> Reliability </th>
<td> Unreliable </td>
<td> Unreliable </td>
<td> Basically reliable </td>
<td> Reliable </td>
<td> Reliable </td>
</tr>
<tr>
 <th style="border-left: none"> Noise Level </th>
<td> Low </td>
<td> Low </td>
<td> High </td>
<td> Low </td>
<td> Low </td>
</tr>
<tr>
 <th style="border-left: none"> Influencing Factors </th>
<td> Affected by temperature, humidity and air pressure </td>
<td> Affected by temperature, humidity and air pressure </td>
<td> Affected by the strength of GPS satellites, the short-term error is large and the long-term error is relatively small </td>
<td> Affected by the working status of the RTK satellite and the accuracy of the RTK base station, the overall error is small </td>
<td> The properties (such as texture and texture) of the surface of hard objects directly below the drone </td>
</tr>
</tbody>
</table>
<div>

## Developed With Flight Control
Developed with the Flight Control, developer need instantiate the object, then set the basic parameters of the drone, finally use the functions in Joystick.

#### 1. Instantiate
Please instantiate the objects of the drone before using OSDK to develop applications.

```c
FlightSample* flightSample = new FlightSample(vehicle);
```

#### 2. Set The Basic Parameters
Use the interfaces in `flightSample` and`flightController` to set the basic parameters of the drone.
> **NOTE** OSDK encapsulates the interface `flightController` in ` flightSample`, developer could using 
 `flightController` or` flightSample` to set the basic parameters of the drone.

```c
flightSample->monitoredTakeoff();
vehicle->flightController->setCollisionAvoidanceEnabledSync(
  FlightController::AvoidEnable::AVOID_ENABLE, 1);

/*! Move to higher altitude */
flightSample->moveByPositionOffset((FlightSample::Vector3f){0, 0, 30}, 0);

/*! Move a short distance*/
flightSample->moveByPositionOffset((FlightSample::Vector3f){10, 0, 0}, 0);

/*! Set aircraft current position as new home location */
flightSample->setNewHomeLocation();

/*! Set new go home altitude */
flightSample->setGoHomeAltitude(50);

/*! Move to another position */
flightSample->moveByPositionOffset((FlightSample::Vector3f){20, 0, 0}, 0);

vehicle->flightController->setCollisionAvoidanceEnabledSync(
FlightController::AvoidEnable::AVOID_DISABLE, 1);
/*! go home and confirm landing */
flightSample->goHomeAndConfirmLanding();

vehicle->flightController->setCollisionAvoidanceEnabledSync(
FlightController::AvoidEnable::AVOID_ENABLE, 1);
```

#### 3. Use The Joystick
To use the Joystick, developer need set the Joystick Mode and Corresponding Control commands first, and then execute the Joystick commands to control the drone. The following code use Joystick in `flightSample-> moveByPositionOffset ()` control the drone move to the specified position in the horizontal and vertical directions.

1. Set the Joystick mode
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

> **NOTE** If you do not change the settings in Joystick while the drone is flying, please set the Joystick mode only when the drone to perform the flight mission.

2. Set Joystick control instruction and execute Joystick function      
> **NOTE** The position of the z axis in the "joystickCommand" is the absolute height relative to the height of the take-off point.

```c
while (elapsedTimeInMs <timeoutInMilSec) {

Limited flying range
...

/* Set Joystick control instruction */
FlightController :: JoystickCommand joystickCommand = {
                    positionCommand.x, positionCommand.y,
                    offsetDesired.z + originHeightBaseHomepoint, yawDesiredInDeg};
vehicle-> flightController-> setJoystickCommand (joystickCommand);

/* Execute the Joystick function */
vehicle-> flightController-> joystickAction ();
...
Threshold for judging whether the drone has entered the set position
                                         }
```