---
title: OSDK Hardware Introduction
date: 2017-06-06
keywords: [component, propellor, sensor, product comparison]
---

DJI produces small, highly capable, remotely controlled aircraft perfect for both consumer and commercial applications. The products are very accessible being easy to use and affordable, and have a quality and feature set unmatched in the industry.

### Aircraft

DJI has a range of multi-rotor aircraft that can be automated with the Onboard SDK including Matrice 600 Pro, Matrice 600, Matrice 100 as well as A3 and N3 Flight Controller Systems.

One of the key features of DJI aircraft is the camera's ability to stay horizontal no matter how the aircraft is flying. The camera is mounted on a gimbal, which actively compensates for any aircraft rotation, producing clear, beautiful images and videos.

There are many DJI aircraft to choose from that provide a range of features, performance, size and price. Specific metrics developers and users should be aware of when they consider an aircraft include:

* Flight time
* Size and weight
* Camera specifications (image quality and movement control)
* Swappable cameras
* Obstacle avoidance
* Customizable payloads
* Maximum service ceiling
* Available accessories
* Remote controller features

### Stand Alone Components

A3 and N3 flight controllers (along with LightBridge 2) are two components of the aircraft (flight controller, wireless link) that can be used on DJI or third party airframes. These components are fully supported in DJI Onboard SDK and offer limited support in DJI Mobile SDK.

### Accessories

DJI aircraft are compatible with a number of DJI accessories. Some of these accessories are also supported by the DJI Onboard SDK, meaning the onboard computer will be able to interact with the accessory to some degree.

## Components

Before doing a detailed product comparison it is useful to understand the components of a product and their function.

All products comprise component modules that provide an important feature or function. An introduction to typical components is below with more details in the [Component Guide](../guides/component-guide-flight-control.html).

![ComponentsAircraft](../images/common/hardware_introduction.png)

#### Propulsion

Motor mounted propellors provide vertical thrust. The vertical thrust can be adjusted at each motor to allow the aircraft to hover, rotate, ascend, descend or fly horizontally.

#### Sensors

DJI aircraft have a large number of sensors including accelerometers, gyroscopes, compasses, barometers, ultrasonic sensors, cameras and satellite positioning systems. These sensors are used to determine the current and predict the future state of the aircraft and the environment around it.

#### Flight Controller

The Flight Controller is an aircraft's main micro controller that couples control information from the pilot with sensor information to adjust the thrust at each propellor and fly the aircraft as desired.

#### Camera

The camera can record image and video data locally.

#### Gimbal

The gimbal holds the camera and can rotate it around three axes. The rotation can be used to both control the direction the camera points, and provide rotational stabilization when the aircraft is not horizontal. The gimbal is mounted on a damped plate for Matrice 100 and on a specialized gimbal mount for Matrice 600 and Matrice 600 Pro to stabilize lateral vibrations and rotational movement.

#### Smart Battery

Smart batteries provide the energy required to run the system. Together with the flight controller, the smart battery can estimate remaining flight time and provide warnings when low battery thresholds are crossed. Batteries are easily swapped between flights, extending product use considerably.

#### Remote Controller

The remote controller provides control sticks, buttons, and wheels that give control of the aircraft flight, camera and gimbal. The remote controller maintains a wireless link with the aircraft with some products having up to a 5km range in ideal environments. The **Flight Mode Switch** on the remote controller can be used to switch between manual and automated flight. See Precedence Control table below to learn about control precedence while using DJI Onboard SDK.

<html><table class="table-product-accessories">
  <thead>
    <tr>
      <th colspan="3">Precedence Control Table</th>
    </tr>
    <tr>
      <th>Product</th>
      <th>Flight Option</th>
      <th>Control Precedence</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Matrice 600 Pro</br>(Using A3 Pro Flight Controller)</td>
      <td>Movement Control</br>WayPoint Mission</br>HotPoint Mission</td>
      <td>DJI Onboard SDK</br>Remote Controller: speed, yaw, height</br>Remote Controller: speed, direction, radius, yaw</td>
    </tr>
    <tr>
      <td>Matrice 600</br>(Using A3 Flight Controller)</td>
      <td>Movement Control</br>WayPoint Mission</br>HotPoint Mission</td>
      <td>DJI Onboard SDK</br>Remote Controller: speed, yaw, height</br>Remote Controller: speed, direction, radius, yaw</td>
    </tr>
    <tr>
      <td>Matrice 100</br>(Using N1 Flight Controller)</td>
      <td>Movement Control</br>WayPoint Mission</br>HotPoint Mission</td>
      <td>DJI Onboard SDK</br>Remote Controller: speed, yaw, height</br>Remote Controller: speed, direction, radius, yaw</td>
    </tr>
    <tr>
      <td>N3 Flight Controller</td>
      <td>Movement Control</br>WayPoint Mission</br>HotPoint Mission</td>
      <td>DJI Onboard SDK</br>Remote Controller: speed, yaw, height</br>Remote Controller: speed, direction, radius, yaw</td>
    </tr>
  </tbody>
</html>

#### Mobile Device

An Android or iOS device can be connected to the remote controller through USB link to give an augmented flight experience showing the live camera feed, and showing aircraft state information. Using the DJI Onboard SDK along with DJI Mobile SDK, the mobile device can also be used to control the aircraft.

## Supported Products

Drones and flight controller systems that support DJI Onboard SDK are: Matrice 600 Pro, Matrice 600, Matrice 100 as well as A3 Pro, A3, N3 flight controller systems.

### Matrice Series: Aircraft Description

* Industrial and developer platform
* Highly customizable, with up to 6 kg payloads supported
* Payloads can communicate with the flight controller directly through a serial port and the DJI Onboard SDK
* Mechanical mounting features
* Can use same cameras as Inspire series
* Additional accessories including

    * <a href="http://www.dji.com/product/matrice600" target="_blank"> DRTK </a> - cm precision positioning
    * <a href="http://www.dji.com/product/guidance" target="_blank"> Guidance </a> - 5 direction stereo camera and ultrasonic sensor module
    * <a href="http://www.dji.com/product/ronin-mx" target="_blank"> Ronin MX </a> - Gimbal that can support custom payloads up to 4.5 kg

Aircraft comparison can be difficult due to the large selection of products, features and functionality. Three summarized aircraft comparison tables are below to introduce the differences in aircraft and features.

<html><table class="table-aircraft-comparison">
<thead><tr><th colspan="9">Aircraft Comparison: <b>Aircraft</th></tr></thead>
<tbody>
<tr>
<th width = 20%><p>Product</p></th>
<th width = 10%><p>Max Flight Time</br><font color="#BBBBBB" size=1 style="font-weight:bold">min</p></th>
<th><p>Max Speed</br><font color="#BBBBBB" size=1 style="font-weight:bold">m/s</p></th>
<th><p>Max Ascent Speed</br><font color="#BBBBBB" size=1 style="font-weight:bold">m/s</p></th>
<th><p>Max Descent Speed</br><font color="#BBBBBB" size=1 style="font-weight:bold">m/s</p></th>
<th><p>Max Service Ceiling</br><font color="#BBBBBB" size=1 style="font-weight:bold">m</p></th>
<th><p>Propellors</p></th>
<th width = 10%><p>Mass</br><font color="#BBBBBB" size=1 style="font-weight:bold">g</p></th>
<th width = 15%><p>Max dimension</br><font color="#BBBBBB" size=1.7 style="font-weight:normal">Without propellors</br><font color="#BBBBBB" size=1 style="font-weight:bold">mm</p></th>
</tr>
<tr>
<td>Matrice 100</td><td>16-40*</td><td>18</td><td>5</td><td>4</td><td>4500</td><td>4</td><td>2355</br><p style="line-height:90%"><font color="#BBBBBB" size=1 style="font-weight:normal">With TB47 Battery</p></td><td>650</td></tr>
<tr>
<td>Matrice 200</td><td>13-38*</td><td>23</td><td>5</td><td>3</td><td>3000</td><td>4</td><td>3800</br><p style="line-height:90%"><font color="#BBBBBB" size=1 style="font-weight:normal">With 2x TB50 batteries</p></td><td>716</td></tr>
<tr>
<td>Matrice 600</td><td>18-40*</td><td>18</td><td>5</td><td>3</td><td>2500</td><td>6</td><td>9100</br><p style="line-height:90%"><font color="#BBBBBB" size=1 style="font-weight:normal">With 6x TB47 Batteries</p></td><td>1133</td></tr>
<tr>
<td>Matrice 600 Professional</td><td>18-40*</td><td>18</td><td>5</td><td>3</td><td>2500</td><td>6</td><td>9500</br><p style="line-height:90%"><font color="#BBBBBB" size=1 style="font-weight:normal">With 6x TB47S Batteries</p></td><td>1133</td></tr>
<tr>
</tbody></table></html>

<html><table class="table-aircraft-comparison">
<thead><tr><th colspan="9">Flight Controller Comparison: <b>Flight Controller System</th></tr></thead>
<tbody>
<tr>
<th width = 20%><p>Product</p></th>
<th><p>Supported Multi-rotor</p></th>
<th><p>DJI Products Supported</p></th>
<th><p>Battery</p></th>
<th><p>Supported ESC</p></th>
<th><p>Supported SDK</p></th>
<th><p>SDK Port</p></th>
<th><p>Components</p></th>
</tr>
<tr>
<td>A3 Pro</td><td>Quadcopter: I4，X4</br>Hexacopter: I6，X6，Y6，IY6</br>Octocopter: X8，I8，V8 Ronin-MX</br></td>
<td>Z15</br>Ronin-MX</br>S900</br>S1000</br>S1000+</br>iOSD</br>D-RTK</br>DATALINK PRO</td>
<td>3S to 12S LiPo</td><td>400Hz Frequency</td><td>Mobile SDK</br>Onboard SDK</td><td>API/CAN2</td>
<td>Main controller unit</br>(integrated with IMU)</br>IMU PRO module x 2 PMU</br>GPS-Compass PRO module</br>X3 RGB LED</td></tr>
<tr>
<td>A3</td><td>Quadcopter: I4，X4</br>Hexacopter: I6，X6，Y6，IY6</br>Octocopter: X8，I8，V8</br></td>
<td>Z15</br>Ronin-MX</br>S900</br>S1000</br>S1000+</br>iOSD</br>D-RTK</br>DATALINK PRO</td>
<td>3S to 12S LiPo</td><td>400Hz Frequency</td><td>Mobile SDK</br>Onboard SDK</td><td>API/CAN2</td>
<td>Main controller unit</br>integrated with IMU PMU</br>GPS-Compass PRO moduleRGB LED</td></tr>
<tr>
<td>N3</td><td>Quadcopter: I4，X4</br>Hexacopter: I6，X6，Y6，IY6</br>Octocopter: X8，I8，V8</td>
<td>DJI GO</br>iOSD</br>Zenmuse Z15-A7</br>5D III</br>GH4</br>BMPCC</br>Ronin-MX</br>X3</br>X5</br>X5R</br>Z15</br>DJI propulsion systems</br>S900</br>S1000</br>S1000+</td>
<td>3S to 12S LiPo</td><td>400Hz Frequency,</br>DJI Intelligent ESC</td><td>Mobile SDK</br>Onboard SDK</td><td>API/CAN2</td><td>With A3 upgrade kit (IMU Pro and GPS-Compass Pro modules)</td></tr>
<tr>
</tbody></table></html>

<html><table class="table-aircraft-comparison">
<thead><tr><th colspan="9">Aircraft Comparison: <b>Features</th></tr></thead>
<tbody>
<tr>
<th width = 20%><p>Product</p></th>
<th><p>Camera And Gimbal</p></th>
<th><p>FPV Camera</p></th>
<th><p>Wireless Range</br><font color="#BBBBBB" size=1.7 style="font-weight:normal">US / EU</br><font color="#BBBBBB" size=1 style="font-weight:bold">km</p></th>
<th><p>Batteries</p></th>
<th><p>Landing Gear</p></th>
<th><p>Custom Payload</br><font color="#BBBBBB" size=1 style="font-weight:bold">g</p></th>
<th><p>Compatible Accessories</p></th>
</tr>
<tr>
<td>Matrice 100</td><td>X3, Z3, X5, X5R, XT, Z30</td><td>-</td><td>5 / 3.1</td><td>1-2</td><td>Fixed</td><td>1000</td><td>Guidance, Manifold, Focus</td></tr>
<tr>
<td>Matrice 200</td><td>X4S, X5S, Z30, XT</td><td>Yes</td><td>7 / 3.5</td><td>2</td><td>Fixed</td><td>1601-2340</br><p style="line-height:90%"><font color="#BBBBBB" size=1 style="font-weight:normal">Battery Dependant</p></td><td>Focus</td></tr>
<tr>
<td>Matrice 600</td><td>X3, Z3, X5, X5R, XT, Custom with Ronin MX, Z15-A7, Z15-BMPCC, Z15-5D III, Z15-GH4</td><td>-</td><td>5 / 3.1</td><td>6</td><td>Moveable</td><td>6000</td><td>Guidance, Manifold, DRTK, Ronin MX, Focus</td></tr>
<tr>
<td>Matrice 600 Professional</td><td>X3, Z3, X5, X5R, XT, Custom with Ronin MX, Z30, Z15-A7, Z15-BMPCC, Z15-5D III, Z15-GH4</td><td>-</td><td>5 / 3.1</td><td>6</td><td>Moveable</td><td>6000</td><td>Guidance, Manifold, DRTK, Ronin MX, Focus</td></tr>
</tbody></table></html>


> Note: DJI Focus is only compatible with DJI cameras.

Detailed specifications are listed on each product's webpage **specs** section at <a href="http://www.dji.com" target="_blank">www.dji.com</a>.


<html><table class="table-aircraft-comparison">
<thead><tr><th colspan="9">Aircraft Comparison: <b>Vision System and Missions</th></tr></thead>
<tbody>
<tr>
<th width = 20%><p>Product</p></th>
<th><p>Obstacle Avoidance</p></th>
<th><p>Infrared Sensing</p></th>
<th><p>Vision Positioning</p></th>
<th><p>Waypoint</p></th>
<th><p>Hotpoint</p></th>
<th><p>Follow Me</p></th>
<th><p>ActiveTrack</p></th>
<th><p>Tap Fly</p></th>
</tr>
<tr>
<td>Matrice 100</td><td>With Guidance</td><td>-</td><td>With Guidance</td><td>Yes</td><td>Yes</td><td>Yes</td><td>-</td><td>-</td></tr>
<tr>
<td>Matrice 200</td><td>Front</br><p style="line-height:90%"><font color="#BBBBBB" size=1 style="font-weight:normal">0.7-30m</p></td><td>Top</br><p style="line-height:90%"><font color="#BBBBBB" size=1 style="font-weight:normal">0-5m</p></td><td>Yes</td><td>Yes</td><td>Yes</td><td>Yes</td><td>Yes</td><td>Yes</td></tr>
<tr>
<td>Matrice 600</td><td>-</td><td>-</td><td>-</td><td>Yes</td><td>Yes</td><td>Yes</td><td>-</td><td>-</td></tr>
<tr>
<td>Matrice 600 Professional</td><td>-</td><td>-</td><td>-</td><td>Yes</td><td>Yes</td><td>Yes</td><td>-</td><td>-</td></tr>
</tbody></table></html>


> Note: For mission descriptions, see [Missions](./component-guide-missions.html) in **Guides**.
> 


### Flight Time

Product flight time is determined by total aircraft mass and the available stored (battery) energy on the aircraft. The available energy is determined by the number of batteries, the battery energy density and the maximum mass the propulsion system can support.

#### Battery Energy Density

DJI provides two series of batteries for the Inspire and Matrice product lines. The TB47 series is the default 99 Wh battery that comes with all aircraft. The TB48 series is a 130 Wh battery. While the TB48 battery has a 10-15% higher energy density, it is less practical as batteries >100 Wh often have transport restrictions.

Using a battery with a higher energy density will always translate to longer flight time if all else is kept constant. However, as the TB48 battery is a little heavier than the TB47 battery, it is important to remember that its use will restrict the maximum custom payload. This is particularly noticeable on the Matrice series of products when using more than one battery.

#### Using More Batteries

Increasing the number of batteries on a product will:

* Increase the available energy for flight (increasing flight time)
* Increase the aircraft mass and therefore:
     * Decrease flight time
     * Decrease the allowable additional payload

#### Flight Time Comparison

To help understand the potential functionality and flight time of different aircraft configurations, a detailed summary of payload and flight times is below:

<html><table class="table-flight-time" id="t03">
 <thead>
  <tr>
    <th colspan="9">Payload & Flight Time</th>
  </tr>
  <tr>
    <td width=20%>Product</td>
    <td width=10%>Camera</td>
    <td width=10%>Battery Configuration</td>
    <td width=10%>Aircraft Mass</td>
    <td width=10%>Battery Mass</td>
    <td width=10%>Camera Mass</td>
    <td width=10%>Payload</td>
    <td width=10%>Take-off Mass</td>
    <td width=10%>Max Flight Time (Approx.)</td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td></td>
    <td><p><font size=1 color="#BBBBBB">grams</p></td>
    <td><p><font size=1 color="#BBBBBB">grams</p></td>
    <td><p><font size=1 color="#BBBBBB">grams</p></td>
    <td><p><font size=1 color="#BBBBBB">grams</p></td>
    <td><p><font size=1 color="#BBBBBB">grams</p></td>
    <td><p><font size=1 color="#BBBBBB">min</p></td>
  </tr>
 </thead>
 <tbody>
  <tr>
    <td rowspan="11">
    Matrice 100
    <p><font size="1">Max Take-off Mass: 3600g</br>Compatible with XT, X3, X5, X5R, Guidance, Manifold</p>
    </td>
    <td align= "center">-</td>
    <td>TB47D</td>        
    <td>1755</td>        
    <td>600</td>        
    <td>0</td>        
    <td>0</td>        
    <td>2355</td>        
    <td>22</td>        
  </tr>
  <tr>
    <td align= "center">-</td>
    <td>TB47D</td>        
    <td>1755</td>        
    <td>600</td>        
    <td>0</td>        
    <td>500</td>        
    <td>2855</td>        
    <td>17</td>
  </tr>
    <tr>
    <td align= "center">-</td>
    <td>TB47D</td>        
    <td>1755</td>        
    <td>600</td>        
    <td>0</td>        
    <td>1000</td>        
    <td>3355</td>        
    <td>13</td>
  </tr>
    <tr>
    <td align= "center">-</td>
    <td>TB48D</td>        
    <td>1755</td>        
    <td>676</td>        
    <td>0</td>        
    <td>0</td>        
    <td>2431</td>        
    <td>28</td>
  </tr>
    <tr>
    <td align= "center">-</td>
    <td>TB48D</td>        
    <td>1755</td>        
    <td>676</td>        
    <td>0</td>        
    <td>500</td>        
    <td>2931</td>        
    <td>20</td>
  </tr>
    <tr>
    <td align= "center">-</td>
    <td>TB48D</td>        
    <td>1755</td>        
    <td>676</td>        
    <td>0</td>        
    <td>1000</td>        
    <td>3431</td>        
    <td>16</td>
  </tr>
    <tr>
    <td align= "center">-</td>
    <td>2x TB47D</td>        
    <td>1915</td>        
    <td>1200</td>        
    <td>0</td>        
    <td>0</td>        
    <td>3115</td>        
    <td>33</td>
  </tr>
    <tr>
    <td align= "center">-</td>
    <td>2x TB48D</td>        
    <td>1915</td>        
    <td>1352</td>        
    <td>0</td>        
    <td>0</td>        
    <td>3267</td>        
    <td>40</td>
  </tr>
    <tr>
    <td>X3</td>
    <td>TB47D</td>        
    <td>1755</td>        
    <td>600</td>        
    <td>247</td>        
    <td>0</td>        
    <td>2602</td>        
    <td>19</td>
  </tr>
    <tr>
    <td>X3</td>
    <td>TB48D</td>        
    <td>1755</td>        
    <td>676</td>        
    <td>247</td>        
    <td>0</td>        
    <td>2678</td>        
    <td>23</td>
  </tr>
    <tr>
    <td>X3</td>
    <td>2x TB48D</td>        
    <td>1915</td>        
    <td>1352</td>        
    <td>247</td>        
    <td>0</td>        
    <td>3514</td>        
    <td>33</td>
  </tr>
  <tr>
    <td rowspan="4">
    Matrice 200
    <p><font size="1">Max Take-off Mass: 6140g</br>Compatible with XT, X4S, X5S, Z3</p>
    </td>
    <td align= "center">-</td>
    <td>2x TB50</td>        
    <td>2760</td>        
    <td>1040</td>        
    <td>0</td>        
    <td>0</td>        
    <td>3800</td>        
    <td>27</td>        
  </tr>
    <tr>
    <td align= "center">-</td>
    <td>2x TB50</td>        
    <td>2760</td>        
    <td>2040</td>        
    <td>0</td>        
    <td>2340</td>        
    <td>6140</td>        
    <td>13</td>
  </tr>
    <tr>
    <td align= "center">-</td>
    <td>2x TB55</td>        
    <td>2760</td>        
    <td>1770</td>        
    <td>0</td>        
    <td>0</td>        
    <td>4530</td>        
    <td>38</td>
  </tr>
    <tr>
    <td align= "center">-</td>
    <td>2x TB55</td>        
    <td>2760</td>        
    <td>1770</td>        
    <td>0</td>        
    <td>1610</td>        
    <td>6140</td>        
    <td>24</td>
  </tr>

  <tr>
    <td rowspan="4">
    Matrice 600
    <p><font size="1">Max Take-off Mass: 15100g</br>Compatible with XT, X3, X5, X5R, Guidance, Ronin MX, DRTK, Manifold</p>
    </td>
    <td align= "center">-</td>
    <td>6x TB47S</td>        
    <td>5530</td>        
    <td>3570</td>        
    <td>0</td>        
    <td>0</td>        
    <td>9100</td>        
    <td>35</td>        
  </tr>
    <tr>
    <td align= "center">-</td>
    <td>6x TB47S</td>        
    <td>5530</td>        
    <td>3570</td>        
    <td>0</td>        
    <td>6000</td>        
    <td>15100</td>        
    <td>16</td>
  </tr>
    <tr>
    <td align= "center">-</td>
    <td>6x TB48S</td>        
    <td>5530</td>        
    <td>4080</td>        
    <td>0</td>        
    <td>0</td>        
    <td>9610</td>        
    <td>40</td>
  </tr>
    <tr>
    <td align= "center">-</td>
    <td>6x TB48S</td>        
    <td>5530</td>        
    <td>4080</td>        
    <td>0</td>        
    <td>5500</td>        
    <td>15110</td>        
    <td>18</td>
  </tr>
 </tbody>
</table></html>

### Camera

DJI provides several camera configurations. For the Phantom and Mavic lines of products, the cameras are fixed to the product. For the Inspire and Matrice lines of products, cameras can be interchanged (Zenmuse X3, X5, X5R, Z3, XT, Z30, X4S, X5S) however not all cameras are compatible with all Inspire and Matrice aircraft. The [Products and Accessories](#supported-products) table at the top of the page details the combinations of camera and aircraft compatibility.

The Zenmuse XT is a thermal camera. It's specifications are difficult to compare directly to other cameras, however it is included in the comparison for it's mass for payload calculation. More details on the specifications of the Zenmuse XT can be found <a href="http://www.dji.com/product/zenmuse-xt/info#specs" target="_blank"> here </a>.

<html><table class="table-aircraft-comparison">
<thead><tr><th colspan="9">Camera Comparison: <b>Sensor</th></tr></thead>
<tbody>
<tr>
<th width = 20%><p>Product</p></th>
<th><p>Sensor Size</p></th>
<th><p>Image Pixels</br><font color="#BBBBBB" size=1 style="font-weight:bold">Megapixels</p></th>
<th><p>Max Video Resolution</p></th>
<th><p>ISO</p></th>
<th><p>Mechanical Shutter</p></th>
<th><p>Shutter Speed</br><font color="#BBBBBB" size=1 style="font-weight:bold">s</p></th>
</tr>
<tr>
<td>Zenmuse X3</td><td>1/2.3"</td><td>12</td><td>4K</td><td>100-1600</td><td>-</td><td>8-1/8000</td></tr>
<tr>
<td>Zenmuse X4S</td><td>1"</td><td>20</td><td>4K</td><td>100-12800</td><td>Yes</td><td>Mechanical 8-1/2000<br>Electronic 1/2000-1/8000</td></tr>
<tr>
<td>Zenmuse X5</td><td>4/3"</td><td>16</td><td>4K</td><td>100-25600</td><td>-</td><td>8-1/8000</td></tr>
<tr>
<td>Zenmuse X5R</td><td>4/3"</td><td>16</td><td>4K</td><td>100-25600</td><td>-</td><td>8-1/8000</td></tr>
<tr>
<td>Zenmuse X5S</td><td>4/3"</td><td>20.8</td><td>5.2K</td><td>100-25600</td><td>-</td><td>8-1/8000</td></tr>
<tr>
<td>Zenmuse XT</td><td>NA</td><td>0.32</br><p style="line-height:90%"><font color="#BBBBBB" size=1 style="font-weight:normal">Depending on Model</p></td><td>640 x 512</br><p style="line-height:90%"><font color="#BBBBBB" size=1 style="font-weight:normal">Depending on Model</p></td><td>NA</td><td>-</td><td>NA</td></tr>
<tr>
<td>Zenmuse Z3</td><td>1/2.3"</td><td>12</td><td>4K</td><td>100-1600</td><td>-</td><td>8-1/8000</td></tr>
<tr>
<td>Zenmuse Z30</td><td>1/2.3"</td><td>2.13</td><td>1080p</td><td>1600</td><td>-</td><td>1-1/6000</td></tr>
</tbody></table></html>


<html><table class="table-aircraft-comparison">
<thead><tr><th colspan="9">Camera Comparison: <b>Lens</th></tr></thead>
<tbody>
<tr>
<th width = 20%><p>Product</p></th>
<th><p>Swappable Lens</p></th>
<th><p>FOV</br><font color="#BBBBBB" size=1 style="font-weight:bold">degrees</p></th>
<th><p>Focal Length</p></th>
<th><p>Aperture</p></th>
<th><p>Focus</br><font color="#BBBBBB" size=1 style="font-weight:bold">m</p></th>
</tr>
<tr>
<td>Zenmuse X3</td><td>-</td><td>94</td><td>20</td><td>f/2.8</td><td>&#8734</td></tr>
<tr>
<td>Zenmuse X4S</td><td>-</td><td>84</td><td>24</td><td>f/2.8-f/11</td><td>1-&#8734</td></tr>
<tr>
<td>Zenmuse X5</td><td>Yes</td><td>72</br><p style="line-height:90%"><font color="#BBBBBB" size=1 style="font-weight:normal">Standard Lens</p></td><td>30</br><p style="line-height:90%"><font color="#BBBBBB" size=1 style="font-weight:normal">Standard Lens</p></td><td>f/1.7 - f/16</br><p style="line-height:90%"><font color="#BBBBBB" size=1 style="font-weight:normal">Standard Lens</p></td><td>0.2 - &#8734</td></tr>
<tr>
<td>Zenmuse X5R</td><td>Yes</td><td>72</br><p style="line-height:90%"><font color="#BBBBBB" size=1 style="font-weight:normal">Standard Lens</p></td><td>30</br><p style="line-height:90%"><font color="#BBBBBB" size=1 style="font-weight:normal">Standard Lens</p></td><td>f/1.7 - f/16</br><p style="line-height:90%"><font color="#BBBBBB" size=1 style="font-weight:normal">Standard Lens</p></td><td>0.2 - &#8734</td></tr>
<tr>
<td>Zenmuse X5S</td><td>Yes</td><td>72</br><p style="line-height:90%"><font color="#BBBBBB" size=1 style="font-weight:normal">Standard Lens</p></td><td>30</br><p style="line-height:90%"><font color="#BBBBBB" size=1 style="font-weight:normal">Standard Lens</p></td><td>f/1.7 - f/16</br><p style="line-height:90%"><font color="#BBBBBB" size=1 style="font-weight:normal">Standard Lens</p></td><td>0.2 - &#8734</td></tr>
<tr>
<td>Zenmuse XT</td><td>-</td><td>13-90</br><p style="line-height:90%"><font color="#BBBBBB" size=1 style="font-weight:normal">Depending on Lens</p></td><td>NA</td><td>f/1.25 - f/1.4</br><p style="line-height:90%"><font color="#BBBBBB" size=1 style="font-weight:normal">Fixed - Value Depends on Lens</p></td><td>NA</td></tr>
<tr>
<td>Zenmuse Z3</td><td>-</td><td>92-35</td><td>22-77</td><td>f/2.8 - f/5.2</td><td>0.5 - &#8734</td></tr>
<tr>
<td>Zenmuse Z30</td><td>-</td><td>63.7-2.3</td><td>22-77</td><td>f/1.6 (Wide) - f/4.7 (Tele)</td><td>0.1 - &#8734 (Wide)<br>1.2 to &#8734 (Tele)</td></tr>
</tbody></table></html>


<html><table class="table-aircraft-comparison">
<thead><tr><th colspan="9">Camera Comparison: <b>Gimbal, Media and Mass</th></tr></thead>
<tbody>
<tr>
<th width = 20%><p>Product</p></th>
<th><p>Controllable Gimbal Pan</br><font color="#BBBBBB" size=1 style="font-weight:bold">degrees</p></th>
<th><p>Stabilization</p></th>
<th><p>Controllable Gimbal Tilt</br><font color="#BBBBBB" size=1 style="font-weight:bold">degrees</p></th>
<th><p>Storage Media</p></th>
<th><p>Mass</br><font color="#BBBBBB" size=1.7 style="font-weight:normal">With Gimbal</br><font color="#BBBBBB" size=1 style="font-weight:bold">g</p></th>
</tr>
<tr>
<td>Zenmuse X3</td><td>+/- 320</td><td>roll, pitch, yaw</td><td>-90 to 30</td><td>Micro SD</td><td>247</td></tr>
<tr>
<td>Zenmuse X4S</td><td>+/- 320</td><td>roll, pitch, yaw</td><td>-90 to 30</td><td>CineSSD and SD on aircraft</td><td>253</td></tr>
<tr>
<td>Zenmuse X5</td><td>+/- 320</td><td>roll, pitch, yaw</td><td>-90 to 30</td><td>Micro SD</td><td>526</td></tr>
<tr>
<td>Zenmuse X5R</td><td>+/- 320</td><td>roll, pitch, yaw</td><td>-90 to 30</td><td>Micro SD, SSD</td><td>583</td></tr>
<tr>
<td>Zenmuse X5S</td><td>+/- 320</td><td>roll, pitch, yaw</td><td>-90 to 30</td><td>CineSSD and SD on aircraft</td><td>461</td></tr>
<tr>
<td>Zenmuse XT</td><td>+/- 320</td><td>roll, pitch, yaw</td><td>-90 to 30</td><td>Micro SD</td><td>270</td></tr>
<tr>
<td>Zenmuse Z3</td><td>+/- 320</td><td>roll, pitch, yaw</td><td>-90 to 30</td><td>Micro SD</td><td>262</td></tr>
<tr>
<td>Zenmuse Z30</td><td>+/- 320</td><td>roll, pitch, yaw</td><td>-90 to 30</td><td>Micro SD</td><td>556</td></tr>
</tbody></table></html>



### Remote Controller

Remote controllers will differ in:

* How they connect to a mobile device
* What wireless technology they use to connect with the aircraft
* Whether they have GPS built-in
* If they can output secondary video
* If they can be used in a dual configuration (one flys the aircraft while the other controls the gimbal and camera)

<html><table class="table-aircraft-comparison">
<thead><tr><th colspan="9"><b>Remote Controller Comparison</th></tr></thead>
<tbody>
<tr>
<th width = 20%><p>Product</p></th>
<th><p>Remote Controller</p></th>
<th><p>Connectivity to Mobile Device</p></th>
<th><p>Connectivity to Aircraft</p></th>
<th><p>Supports Dual RC</p></th>
<th><p>Built-in GPS</p></th>
<th><p>Secondary Video Output</p></th>
<th><p>Flight Mode Switch</br><font color="#BBBBBB" size=1.7 style="font-weight:normal">To use SDK</p></th>
</tr>
<tr>
<td>Matrice 100</td><td>Required</td><td>USB</td><td>Lightbridge</td><td>Yes</td><td>-</td><td>Mini HDMI</td><td>F</td></tr>
<tr>
<td>Matrice 200</td><td>Required</td><td>USB</td><td>Lightbridge</td><td>Yes</td><td>-</td><td>Mini HDMI</td><td>P</td></tr>
<tr>
<td>Matrice 600</td><td>Required</td><td>USB</td><td>Lightbridge</td><td>Yes</td><td>-</td><td>Mini HDMI, SDI</td><td>P</td></tr>
<tr>
<td>Matrice 600 Professional</td><td>Required</td><td>USB</td><td>Lightbridge</td><td>Yes</td><td>-</td><td>Mini HDMI, SDI</td><td>P</td></tr>
<tr>
<td>A3 Professional</td><td>Optional</td><td>USB</td><td>Lightbridge</td><td>Yes</td><td>-</td><td>Mini HDMI, SDI</td><td>P</td></tr>
<tr>
<td>A3</td><td>Optional</td><td>USB</td><td>Lightbridge</td><td>Yes</td><td>-</td><td>Mini HDMI, SDI</td><td>P</td></tr>
<tr>
<td>N3</td><td>Optional</td><td>USB</td><td>Lightbridge</td><td>Yes</td><td>-</td><td>Mini HDMI, SDI</td><td>P</td></tr>
</tbody></table></html>

