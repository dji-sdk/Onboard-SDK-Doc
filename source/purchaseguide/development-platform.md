---
title: Development Platform
date: 2020-05-08
version: 4.0.0
keywords: [development kit, linux, freertos]
---
> **NOTE** This article is **Machine-Translated**. If you have any questions about this article, please send an <a href="mailto:dev@dji.com">E-mail </a>to DJI, we will correct it in time. DJI appreciates your support and attention.

According to the features、resource usage and toolchain to choose the OS and the development platform for the application.

## Platform and Toolchain
* Linux
   * OS: Ubuntu 16.04
   * Toolchain : gcc / g ++ 5.4.0
   * Onboard Computer: Manifold 2-C / 2-G

* Choose ROS
   * OS: kinetic
   * Toolchain: gcc / g ++ 5.4.0
   * Onboard Computer: Manifold 2-C / 2-G

* Choose FreeRTOS
   * OS: FreeRTOS v10.2.1
   * Toolchain: armcc
   * Onboard Computer: STM32F4 Series

## Feature

<div>
<div style="text-align: center"><p>Table1. Features Suppport </p></div>
<div>
<table>
<thead>
   <th>Class</th>
   <th> Name </th>
   <th width=200> Description </th>
   <th> Linux </th>
   <th> RTOS </th>
   <th> ROS </th>
   <th width=120> Drone </th>
   <th> NOTE </th>
</thead>
<tbody>
    <tr>
    <tr>
    <th rowspan="3"> Control </th>
     <td> Time Synchronization </td>
     <td> Get the timestamp of the drone flight controller, get hard synchronization signals such as NMEA data UTC time ,subscription PPS signal </td>
     <td> ✓ </td>
     <td> ✓ </td>
     <td> ✓ </td>
     <td> M300 RTK </br> M200 RTK V2 </br> M200 V2 </td>
     <td rowspan="6">-</td>
    </tr>
    <tr>
     <td> Basic Control </td>
     <td> Set and obtain the parameters of the flight controller to perform basic flight tasks</td>
     <td> ✓ </td>
     <td> ✓ </td>
     <td> ✓ </td>
     <td> M300 RTK </br> M200 RTK V2 </br> M200 V2 </td>
    </tr>
      <tr>
      <td> Motion Planning </td>
      <td> Waypoint mission and hotpoint mission </td>
      <td> ✓ </td>
      <td> ✓ </td>
      <td> ✓ </td>
      <td> M300 RTK </br> M200 RTK V2 </br> M200 V2 </td>
    </tr>
    <tr>
      <th rowspan="3"> Management </th>
      <td> Information Management </td>
      <td> Get drone's flight controller broadcast information and subscribe the data of the drone flight controller </​​td>
      <td> ✓ </td>
      <td> ✓ </td>
      <td> ✓ </td>
      <td> M300 RTK </br> M200 RTK V2 </br> M200 V2 </td>
    </tr>
    <tr>
     <td> Gimbal Management </td>
     <td> Rotation and reset the gimbal, set the basic parameters of the gimbal, get the current status and basic information of the gimbal </td>
     <td> ✓ </td>
     <td> ✓ </td>
     <td> ✓ </td>
     <td> M300 RTK </br> M200 RTK V2 </br> M200 V2 </td>
    </tr>
    <tr>
     <td> Camera Management </td>
     <td> Control the camera to perform basic actions such as taking pictures, recording and zooming, and set basic parameters such as camera shutter, aperture, and ISO
     <td> ✓ </td>
     <td> ✓ </td>
     <td> ✓ </td>
     <td> M300 RTK </br> M200 RTK V2 </br> </td>
    </tr>
    <tr>
      <th rowspan="3"> Expansion Category </th>
      <td> Advanced Visual </td>
      <td> Obtain camera image and stream (obtain original stream and H.264 stream) to achieve object recognition and other advanced functions </td>
      <td> ✓ </td>
      <td>-</td>
      <td> ✓ </td>
      <td> M300 RTK </br> M200 RTK V2 </br> M200 V2 </td>
      <td> M200 RTK V2 and M200 V2 only support obtaining the original camera stream and H.264 stream </td>
    </tr>
        <tr>
      <td> SDK Interconnection </td>
      <td> MSDK, PSDK and OSDK communication </td>
      <td> ✓ </td>
      <td> ✓ </td>
      <td> will support </td>
      <td> M300 RTK </br> M200 RTK V2 </br> M200 V2 </td>
      <td>-</td>
    </tr>
</tbody>
</table>
</div></div>