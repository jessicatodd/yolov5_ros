# YOLOv5 ROS
This is a ROS interface for using YOLOv5 for real time object detection on a ROS image topic. It supports inference on multiple deep learning frameworks used in the [official YOLOv5 repository](https://github.com/ultralytics/yolov5).

This ROS interface has been modified to be compatible with WARPLab's CUREE (WARPAUV) robots. 

## Installation

### Dependencies
This package is built and tested on Ubuntu 20.04 LTS and ROS Noetic with Python 3.8.

* Clone the packages to ROS workspace and install requirement for YOLOv5 submodule:
```bash
cd warp_ws/src/drivers/yolo-ros-drivers
git clone https://github.com/mats-robotics/detection_msgs.git
git clone --recurse-submodules git@github.com:jessicatodd/yolov5_ros.git 
```
* Check and install the requirements for yolov5
```bash
cd yolov5_ros
pip install -r requirements.txt  # install the requirements for yolov5_ros
```
* Yolov5 also requires OpenCV and Torch. The following package versions should be checked manually and only updated in consultation with Levi Cai. Note that OpenCV has been built from the source, not installed via `pip`. 
```
opencv2-python>=4.1.1
torch>=1.7.0
torchvision>=0.8.1
```
* Build the ROS package:
```bash
cd warp_ws
catkin build yolov5_ros # build the ROS package
```
* Make the Python script executable 
```bash
cd warp_ws/src/dreivers/yolo_ros_driver/yolov5_ros/src
chmod +x detect.py
```

## Basic usage
Change the parameter for `input_image_topic` in launch/yolov5.launch to any ROS topic with message type of `sensor_msgs/Image` or `sensor_msgs/CompressedImage`. Other parameters can be modified or used as is.

* Launch the node:
```bash
roslaunch yolov5_ros yolov5.launch
```

## Using custom weights and dataset (Working)
* Put your weights into `yolov5_ros/src/yolov5`
* Put the yaml file for your dataset classes into `yolov5_ros/src/yolov5/data`
* Change related ROS parameters in yolov5.launch: `weights`,  `data` to the directory where your weights and yaml file are stored

## Reference
* YOLOv5 official repository: https://github.com/ultralytics/yolov5
* YOLOv3 ROS PyTorch: https://github.com/eriklindernoren/PyTorch-YOLOv3
* Darknet ROS: https://github.com/leggedrobotics/darknet_ros
