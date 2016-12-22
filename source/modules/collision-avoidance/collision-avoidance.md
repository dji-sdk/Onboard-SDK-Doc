---
title: LiDAR-based Collision Avoidance
version: 3.2
date: 2016-12-24

---

## Introduction

The objective of the LiDAR-based collision avoidance package (beta) is to help enhance the safety during both precision mission and manual flying. Previously we have used LiDAR as a sensor for data collection. This module uses LiDAR as a sensor for perception.


## Hardware and Software Setup

### Hardware setup
![fully-assembled-system](../../images/modules/collision-avoidance/fully-assembled-system.jpg)

The system for collision avoidance consists of the following components:
1. Velodyne Puck LITE or VLP-16 LiDAR
2. Onboard embedded system (OES): Intel NUC with i5 processer, 256G SSD and 8G ram
3. Power adapters to power the LiDAR and the OES from the drones main power source
4. Customized rack for the LiDAR and the OES

The overall weight of the above system is around 1.77 kg, so we choose the DJI Matrice 600 as the platform. The rack is designed such that the field of view (FOV) of the VLP-16 is not blocked by the body of the M600. The VLP-16 is mounted upside down, with the power cable pointing to the right side of the M600.

The VLP-16 needs to be configured from its network interface
Configure the VLP-16 from its network interface. 
![VLP16-webconfig](../../images/modules/collision-avoidance/VLP16-webconfig.png)


### Software setup

The collision avoidance software is developed and tested on the following software environment:

1. Ubuntu 16.04
2. ROS Kinetic full installation
3. Velodyne driver for ROS
3. DJI onboard sdk
4. DJI onboard sdk ros package
5. DJI collision avoidance package (binary)

Depending on if the user needs the collision avoidance module in the precision mission or in the manual fly, the software setup procedure are differen.

First follow software setup instructions in [Precision Mission](../../modules/missionplan/README.html#setup) and [ROS](../../github-platform-docs/ROS/README.html#setup) to build the linux sample with precision mission support and the `DJI_OnboardSDK_ROS` package. 

Next, build the `velodyne` ROS package:

       1. cd path-to-catkin-workspace/src
       2. git clone https://github.com/dji-sdk/velodyne.git
       3. cd ..
       4. catkin_make -DCOLLISION_AVOIDANCE=ON
       5. source devel/setup.bash
       6. source dji_ros_package/dji_collision_avoidance/setup.bash


In step 4, the `-DCOLLISION_AVOIDANCE=ON` flag downloads the `dji_collision_avoidance` binary and put it under `path-to-catkin-workspace`, which is why the `setup.bash` needs to be sourced.


## Workflow

### Use with precision mission

The collision avoidance module can be started automatically with the precision trajectory following mission. To execute a precision mission with collision avoidance support, run the linux sample executable in mobile mode (`-mobile`). Then from the `advanced` tab in the mobile app, hit the `Go` button under the `Precision Trajectory` section with the 'Collision Avoidance` switch on, as shown below. After the M600 takes off, the collision avoidance module will be started and the drone will pause if there are unexpected obstacles in the flying direction. The precision mission will resume when the obstacle is cleared. If the obstacle cannot be removed, the user will have to abort the mission and re-plan.

![mission-collision-avoidance](../../images/modules/collision-avoidance/mission-collision-avoidance.png)

### Use with manual fly

The collision avoidance module can also be started to assist the pilot during manual flying. To start the collision avoidance in manual fly, first start the ROS nodes `dji_sdk` and `dji_sdk_client` following the instructions in [ROS documentation](../../github-platform-docs/ROS/README.html#examples), and enter the mobile mode. Then, take off manually or using the mobile command. After the drone is in the air, hit the `Go` button under section `Collision Avoidance` in the `Advanced` tab, and the drone will enter collision avoidance manual fly mode. 

In collision avoidance manual fly mode, the user stick inputs are be remapped to velocity commands. To ensure safety, we scaled the maximum velocities such that the maximum `X` and `Y` velocities are scaled to `3 m/s`, the maximum `Z` velocity is scaled to `2 m/s`, and the maximum yaw rate is scaled to `45 deg/s`.


![manual-fly-collision-avoidance](../../images/modules/collision-avoidance/manual-fly-collision-avoidance.png)

## Under the hood

The collision avoidance module is developed as a ROS package named `dji_collision_avoidance`. This package consists of the following ROS nodes

### `dji_occupancy_grid_node`
This node creates occupancy grid from the LiDAR point cloud.
- Subscribed topics:
  1. `/velodyne_points`: published by the `velodyne_pointcloud` package
  2. `/tf`

- Published topics:
  1. `/dji_collision_avoidance/octomap_binary`: the occupancy grid for collision checking
  2. `/dji_collision_avoidance/occupied_cells_vis_array`: markers of the occupancy grid for visualization by `rviz`

### `dji_collision_detection_node`
When the drone is moving, this node checks if there is collision in the current flying direction to determine if the drone needs to pause. When the drone is paused, it checks if the commanded moving direction leads to collision to determine if the drone can proceed.

- Subscribed topics:
  1. `/dji_sdk/velocity`
  2. `/dji_sdk/rc_channels`
  3. `/dji_collision_avoidance/octomap_binary`

- Published topics:
  1. `/collision_info_msg`

### `drone_tf`
- Subscribed topics:
  1. `/dji_sdk/attitude_quaternion`

- Published topics:
  1. `/tf`

### `manual_fly`
- Subscribed topics:
  1. `/dji_sdk/velocity`
  2. `/dji_sdk/rc_channels`
  3. `/dji_sdk/global_position`
  4. `/collision_info_msg`

Advanced developers can look at `from_Linux_sample.launch` and `from_DJI_ros_client.launch` located in `install/lib/dji_collision_avoidance/launch`, which are the launch files used by the precision mission and the manual fly, respectively. The launch files contain the nodes that needed in each case.

### Limitations

- Currently the collision avoidance module only stop and hover when moving towards obstacles. It will not move away from an approaching dynamic obstacle.

- It is not a simultaneous localization and mapping (SLAM) solution. It only usese the instantaneous point cloud information from the LiDAR to build an occupancy grid and tries to avoid the collision in that short term grid.

- It requires good velocity information to work. In the M600 setup, this means that good GPS reception is required.

- Plan the mission with conservative velocity, e.g., `5 m/s` and be prepared to switch to `P` mode to take over.

