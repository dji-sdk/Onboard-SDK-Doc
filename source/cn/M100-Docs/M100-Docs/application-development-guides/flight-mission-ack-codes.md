---
title: Flight Mission ACK codes
version: v3.1.8
date: 2016-07-01
github: https://github.com/dji-sdk/Onboard-SDK
keywords: []
---

Onboard SDK implements functionality to wait for ACK frame from a flight controller. Developer is responsible to parse received ACK. DJI_Mission.cpp implements flight mission ACK map to allow you to map received ACK to a meaningful message (see "Flight Mission ACK Map" below with an example).

List of Flight Mission CMDs returning ACK:

Ground Station CMD Set : WayPoint
- Upload waypoint info
- Upload waypoint
- Start
- Stop
- Pause
- Resume

Ground Station CMD Set : Hotpoint
- Start
- Stop
- Pause
- Resume
- Set radius
- Reset yaw

Ground Station CMD Set : Follow Me
- Start
- Stop
- Pause
- Resume

Flight Mission ACK Map

<table>
<tr>
  <th>Mission Or Control Name</th>
  <th>ACK Code</th>
  <th>Description</th>
</tr>
<tr>
  <td>Control Call</td>
  <td>0x00</td>
  <td>Success</td>
</tr>
<tr>
  <td></td>
  <td>0x01</td>
  <td>Wrong WayPoint Index</td>
</tr>
<tr>
  <td></td>
  <td>0xD0</td>
  <td>Not At Mode F</td>
</tr>
<tr>
  <td></td>
  <td>0xD1</td>
  <td>Need obtain control</td>
</tr>
<tr>
  <td></td>
  <td>0xD2</td>
  <td>Need close IOC mode</td>
</tr>
<tr>
  <td></td>
  <td>0xD3</td>
  <td>Mission not initialized</td>
</tr>
<tr>
  <td></td>
  <td>0xD4</td>
  <td>Mission not running</td>
</tr>
<tr>
  <td></td>
  <td>0xD5</td>
  <td>Mission already running</td>
</tr>
<tr>
  <td></td>
  <td>0xD6</td>
  <td>Too consuming of time</td>
</tr>
<tr>
  <td></td>
  <td>0xD7</td>
  <td>Other mission running</td>
</tr>
<tr>
  <td></td>
  <td>0xD8</td>
  <td>Bad GPS</td>
</tr>
<tr>
  <td></td>
  <td>0xD9</td>
  <td>Low battery</td>
</tr>
<tr>
  <td></td>
  <td>0xDA</td>
  <td>UAV did not take off</td>
</tr>
<tr>
  <td></td>
  <td>0xDB</td>
  <td>Wrong patameters</td>
</tr>
<tr>
  <td></td>
  <td>0xDC</td>
  <td>Conditions not satisfied</td>
</tr>
<tr>
  <td></td>
  <td>0xDD</td>
  <td>Crossing No-Fly zone</td>
</tr>
<tr>
  <td></td>
  <td>0xDE</td>
  <td>Unrecorded Home</td>
</tr>
<tr>
  <td></td>
  <td>0xDF</td>
  <td>Already at No-Fly zone</td>
</tr>
<tr>
  <td></td>
  <td>0xC0</td>
  <td>Too High</td>
</tr>
<tr>
  <td></td>
  <td>0xC1</td>
  <td>Too Low</td>
</tr>
<tr>
  <td></td>
  <td>0xC7</td>
  <td>Too far from home</td>
</tr>
<tr>
  <td></td>
  <td>0xC8</td>
  <td>Mission not supported</td>
</tr>
<tr>
  <td></td>
  <td>0xC9</td>
  <td>Too far from current position</td>
</tr>
<tr>
  <td></td>
  <td>0xCA</td>
  <td>Beginner mode does not support missions</td>
</tr>
<tr>
  <td></td>
  <td>0xF0</td>
  <td>Taking off</td>
</tr>
<tr>
  <td></td>
  <td>0xF1</td>
  <td>Landing</td>
</tr>
<tr>
  <td></td>
  <td>0xF2</td>
  <td>Returning home</td>
</tr>
<tr>
  <td></td>
  <td>0xF3</td>
  <td>Starting motors</td>
</tr>
<tr>
  <td></td>
  <td>0xF4</td>
  <td>Invalid command</td>
</tr>
<tr>
  <td></td>
  <td>0xFF</td>
  <td>Unknown error</td>
</tr>
<tr>
  <td>Follow</td>
  <td>0xB0</td>
  <td>Too far from your position, lack of radio connection</td>
</tr>
<tr>
  <td></td>
  <td>0xB1</td>
  <td>Cutoff time overflow</td>
</tr>
<tr>
  <td></td>
  <td>0xB2</td>
  <td>Gimbal pitch angle too large</td>
</tr>
<tr>
  <td>HotPoint</td>
  <td>0xC2</td>
  <td>Invalid radius</td>
</tr>
<tr>
  <td></td>
  <td>0xC3</td>
  <td>yawRate too large</td>
</tr>
<tr>
  <td></td>
  <td>0xC4</td>
  <td>Invalid vision</td>
</tr>
<tr>
  <td></td>
  <td>0xC5</td>
  <td>Invalid yaw mode</td>
</tr>
<tr>
  <td></td>
  <td>0xC6</td>
  <td>Too far from HotPoint</td>
</tr>
<tr>
  <td></td>
  <td>0xC6</td>
  <td>Too far from HotPoint</td>
</tr>
<tr>
  <td></td>
  <td>0xC6</td>
  <td>Too far from HotPoint</td>
</tr>
<tr>
  <td></td>
  <td>0xA2</td>
  <td>Invalid HotPoint parameter</td>
</tr>
<tr>
  <td></td>
  <td>0xA3</td>
  <td>Invalid latitude or longtitude</td>
</tr>
<tr>
  <td></td>
  <td>0xA6</td>
  <td>Invalid direction</td>
</tr>
<tr>
  <td></td>
  <td>0xA9</td>
  <td>HotPoint paused</td>
</tr>
<tr>
  <td></td>
  <td>0xAA</td>
  <td>HotPoint failed to pause</td>
</tr>
<tr>
  <td>WayPoint</td>
  <td>0xE0</td>
  <td>Invalid waypoint mission data</td>
</tr>
<tr>
  <td></td>
  <td>0xE1</td>
  <td>Invalid waypoint point data</td>
</tr>
<tr>
  <td></td>
  <td>0xE2</td>
  <td>WayPoint distance out of range</td>
</tr>
<tr>
  <td></td>
  <td>0xE3</td>
  <td>WayPoint mission out of range</td>
</tr>
<tr>
  <td></td>
  <td>0xE4</td>
  <td>Too many points</td>
</tr>
<tr>
  <td></td>
  <td>0xE5</td>
  <td>Points too close</td>
</tr>
<tr>
  <td></td>
  <td>0xE6</td>
  <td>Points too far</td>
</tr>
<tr>
  <td></td>
  <td>0xE7</td>
  <td>Check failed</td>
</tr>
<tr>
  <td></td>
  <td>0xE8</td>
  <td>Invalid action</td>
</tr>
<tr>
  <td></td>
  <td>0xE9</td>
  <td>Point data not enough</td>
</tr>
<tr>
  <td></td>
  <td>0xEA</td>
  <td>WayPoint mission data not enough</td>
</tr>
<tr>
  <td></td>
  <td>0xEB</td>
  <td>WayPoints not enough</td>
</tr>
<tr>
  <td></td>
  <td>0xEC</td>
  <td>WayPoint mission already running</td>
</tr>
<tr>
  <td></td>
  <td>0xED</td>
  <td>WayPoint mission is not running</td>
</tr>
<tr>
  <td></td>
  <td>0xEE</td>
  <td>Invalid velocity</td>
</tr>
<tr>
  <td>IOC</td>
  <td>0xA0</td>
  <td>Too near to home</td>
</tr>
<tr>
  <td></td>
  <td>0xA1</td>
  <td>Too close to home, within 20 meters</td>
</tr>
</table>

Example:

Mission ack = api->task(<your task here>);
if (!api->decodeMissionStatus(ack))
  std::runtime_error("Mission ACK error");
