---
title: Flight Altitude
date: 2020-03-27
keywords: [flight altitude]
---

## Basic Concept
The basic concept of the altitude about OSDK and DJI's drone is as follows:
<div>
<table>
<thead>
<th style="border-left: none;"> </th>
<th> Relative Altitude </th>
<th> Fusion Altitude </th>
<th> GPS Altitude </th>
<th> RTK Altitude </th>
<th> Straight Altitude </th>
</thead>
<tbody>
<tr>
 <th style="border-left: none"> Concept </th>
<td> The vertical distance of the takeoff point and current point</td>
<td> Take the barometer value as the initial value, use the fusion algorithm and sensors to calculate the Altitude </td>
<td> Real-time earth ellipsoid height based on GPS </td>
<td> Real-time earth ellipsoid height based on RTK </td>
<td> Using the ultrasound to measure the distance between the drone and the below </td>
</tr>
<tr>
 <th style="border-left: none"> Get Method </th>
<td> Get this information from DJI Pilot </br> The Mobile App developed based on MSDK could subscribe this item </td>
<td> The Mobile App developed based on MSDK could subscribe this item </td>
<td> The Mobile App developed based on MSDK could subscribe this item </td>
<td> The Mobile App developed based on MSDK could subscribe this item </td>
<td> Get this information from DJI Pilot </br> The Mobile App developed based on MSDK could subscribe this item </td>
</tr>
<tr>
 <th style="border-left: none"> Application scenarios </th>
<td> To get the current altitude of the drone </td>
<td> For more accurate and stable control of the drone when flighting the missions </td>
<td> Analyze the flight mission and flight status of the drone </td>
<td> For missions such as accurate mapping and waypoint flight </td>
<td> For safe landing (obstacle avoidance and speed reduction)  </td>
</tr>
<tr>
 <th style="border-left: none"> Data source </th>
<td colspan=2> IMU (may includes vision sensors, GPS, and RTK) and barometers </td>
<td> GPS satellites </td>
<td> RTK satellites </td>
<td> TOF or ultrasound, and IMU </td>
</tr>
<tr>
 <th style="border-left: none"> 0 Point </th>
<td> The point where the drone takes off from the ground </td>
<td> Sea level at standard pressure </td>
<td> WGS84 Coordinate System </td>
<td> RTK Coordinate system (C2000, WGS84 or user-specified) </td>
<td> The surface of a hard object (such as the ground) below the drone </td>
</tr>
<tr>
 <th style="border-left: none"> Noise level </th>
<td> Low </td>
<td> Low </td>
<td> High </td>
<td> Low </td>
<td> Low </td>
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
 <th style="border-left: none"> Data Precision </th>
<td colspan="2"> The altitude accuracy will be affected by the flight distance of the drone </td>
<td> reliable </td>
<td> reliable </td>
<td> reliable </td>
</tr>
<tr>
 <th style="border-left: none"> Altitude Reliability </th>
<td> Unreliable </td>
<td> Unreliable </td>
<td> Neutral </td>
<td> Reliable </td>
<td> Reliable </td>
</tr>
<tr>
 <th style="border-left: none"> Influencing factors </th>
<td colspan=2> Affected by Temperature, Humidity, and Pressure </td>
<td> Affected by the strength of GPS signal, short-term deviation is large and long-term deviation is relatively small.
<td> Affected by the working status of RTK satellite and accuracy of RTK base station, overall it is very reliable  </td>
<td> Properties (such as texture) of the object belows the drone </td>
</tr>
</tbody>
</table>
<div>

## Compare
#### Relative and Fusion 
The difference between the relative takeoff altitude and the fusion altitude is starting point：
* The relative takeoff altitude is based on the aircraft's takeoff point.
* The fusion altitude uses standard atmospheric pressure (Sea level under the standard atmospheric pressure) as a starting point.

These two altitudes use MSL（Main Sealed Height) is 1013.25mBar at 15°C, and the per 1000m is -6.5°C). The environment of the aircraft is affected by temperature and humidity, the change doesn‘t fully conform to the standard model, so the absolute altitude obtained from these two altitudes is not reliable. And the fused altitude cannot be used for absolute measurement. In addition, the distance is far and the difference between the two points will have a large deviation.

#### GPS and RTK 
Both GPS altitude and RTK altitude can output the current earth ellipsoid height of the aircraft. The difference is as follows:
* RTK altitude depends on the user's coordinate system, like C2000, WGS84, or others. RTK is more accuracy in the case of ”fixed“, and is very reliable in the short and long term (fixed).
* GPS altitude is only in the WGS84. GPS is limited by positioning accuracy, and the short-term deviation of altitude is generally large, but it is reliable in the long-term. 

Regardless of the network RTK or the station RTK, when the station RTK is fixed, the relative positioning accuracy (relative to the station RTK) is accurate. For the handheld station RTK, the accuracy is affected by RTK station. If the RTK station calibrate automatically by itself, the deviation may reach to meter level, and the RTK will have the deviation at this time, but the relative position is reliable. For network RTK both relative position and absolute position are better.
