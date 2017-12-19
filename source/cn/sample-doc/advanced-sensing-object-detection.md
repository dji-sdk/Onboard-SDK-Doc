---
title: Advanced Sensing - Object Detection Sample
date: 2017-12-19
version: 3.5
keywords: [Object detection, main camera, fpv camera, image, tiny-yolo, CNN]
---

With the capability to access the camera streams of M210 and reasonable onboard computing power, we can run convolutional neural network (CNN) based object detection algorithms. In this sample, we will demonstrate how to run a very powerful real-time object detection package named [YOLO V2](https://pjreddie.com/darknet/yolo/) and one of its ROS wrappers [darknet_ros](https://github.com/leggedrobotics/darknet_ros) in ROS environment.

We have tested this setup on Ubuntu 16.04 and ROS kinect, on both a laptop computer with NVIDIA GTX 970M graphics card and the [NVIDIA Jetson TX2](https://www.nvidia.com/en-us/autonomous-machines/embedded-systems-dev-kits-modules/) with the [Orbitty Carrier board](http://connecttech.com/product/orbitty-carrier-for-nvidia-jetson-tx2-tx1/).

## Object Detection in Camera Stream Using Yolo2 on ROS

#### 1. Setup the Onboard SDK ROS environment

Follow the `ROS Onboard Computer` section of the [sample-setup](./sample-setup.html) to build and install the onboard sdk core library to your system, and to download the onboard sdk ros package to your catkin workspace.

#### 2. Download darknet and darknet-ROS package for target tracking

```
cd /path/to/catkin_ws/src
git clone --recursive https://github.com/leggedrobotics/darknet_ros.git
cd ../
catkin_make
```
During the build stage, it will download the `tiny-yolo-voc.weights` and the `yolo-voc.weights`. However, from our tests, we found that the `tiny-yolo.weights` works better. So please download it with the following command
```
wget http://pjreddie.com/media/files/tiny-yolo.weights -P /path/to/catkin_ws/src/darknet_ros/darknet_ros/yolo_network_config/weights
```


Next, you'll need to edit some config files to tell `darknet_ros` to use the `tiny-yolo.weights` and use the image source from `/dji_sdk/fpv_camera_images` (or `/dji_sdk/main_camera_images`).

1. In `darknet_ros/darknet_ros/launch/darknet_ros.launch`, change `yolo_voc.yaml` to `tiny_yolo.yaml`
2. In `darknet_ros/darknet_ros/config/ros.yaml`, change `/camera/rgb/image_raw` to `/dji_sdk/fpv_camera_images` (or `/dji_sdk/main_camera_images`)
3. In `darknet_ros/darknet_ros/config/tiny_yolo.yaml`, change the threshold value from 0.3 to 0.6 to reduce some false positive

#### 3. Start the dji_sdk node

Make sure you have run `source /path/to/catkin_ws/devel/setup.bash`, and have properly edit the entries in `/path/to/catkin_ws/src/OnboardSDK-ROS/dji_sdk/launch/sdk.launch` such as the `app_id`, `enc_key` and `baud_rate`. Then you can start the `dji_sdk` node with
```
roslaunch dji_sdk sdk.launch
```

#### 4. Start the FPV camera stream using ROS service

In a separate terminal, run
```
rosservice call /dji_sdk/setup_camera_stream "cameraType: 0 start: 0"
```
In the `dji_sdk` node terminal, you will initially see some error messages since it takes some time to decode the first image.

#### 5. Start the object detection node

With all the modifications we made to `darknet_ros` in step 3, you can start it with 
```
roslaunch darknet_ros darknet_ros.launch
```
Now you should see bounding boxes around detected objects.
