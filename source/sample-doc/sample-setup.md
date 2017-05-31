---
title: Setting up Samples
date: 2017-06-01
version: 3.3
keywords: [write apps, development, SDK, samples, DJI, OSDK, setup]
---

## Linux OES

1. Clone (or download as zip) the DJI OSDK from Github [here](https://www.github.com/dji-sdk/Onboard-SDK).
2. Open a terminal inside the onboardsdk folder and follow these steps to build the OSDK:
```
mkdir build
cd build
cmake ..
make
```
3. The above step builds the `osdk-core` library, as well as the Linux samples. Executables are located inside the `build/bin` folder.
4. Still inside the `build` folder, copy the default user config file to your executable location:
```
cp ../sample/linux/common/UserConfig.txt bin/
```
5. Open the UserConfig.txt file in a text editor and fill in your App ID, Key, Baudrate and Port name in the designated places.
6. Run your desired Linux sample (e.g. flight control sample) with the following command:
```
cd bin
./djiosdk-flightcontrol-sample UserConfig.txt
```
7. Follow the interactive prompt to execute actions available in the sample.

## ROS OES

1. Clone (or download as zip) the DJI OSDK from Github [here](https://www.github.com/dji-sdk/Onboard-SDK).
2. Open a terminal inside the onboardsdk folder and follow these steps to build the core OSDK library:
```
mkdir build
cd build
cmake ..
make djiosdk-core
```
3. Now, install the osdk-core library to your system so that the `dji_sdk` ROS node may find it and link against it:
```
sudo make install djiosdk-core
```
4. If you don't have a catkin workspace, create one as follows:
```
mkdir catkin_ws
cd catkin_ws
mkdir src
cd src
catkin_init_workspace
```
5. Clone (or download as zip) the DJI OSDK-ROS from Github [here](https://www.github.com/dji-sdk/Onboard-SDK-ROS) in the `src` folder.
6. Build the `dji_sdk` ROS package and the `dji_sdk_demo` ROS package.
```
cd ..
catkin_make
```
7. Remember to source your `setup.bash`:
```
source devel/setup.bash
```
8. Edit the launch file and enter your App ID, Key, Baudrate and Port name in the designated places:
```
rosed dji_sdk sdk.launch
```
9. Start up the `dji_sdk` ROS node:
```
roslaunch dji_sdk sdk.launch
```
10. Open up another terminal and `cd` to your catkin_ws location, and start up a sample (e.g. flight control sample):
```
source devel/setup.bash
rosrun dji_sdk_demo demo_flight_control
```
11. Follow the prompt on screen to choose an action for the drone to do.
