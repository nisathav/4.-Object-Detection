# 4.-Object-Detection-ROS2

We have the following detection in the systems, 
1. YOLO detection system - https://pjreddie.com/darknet/yolo/
   This is a real time object detection system.
   The available YOLO detection algorithms are darknet, yolov3 or yolov4
   
3. Object detection with RVIZ - https://www.stereolabs.com/docs/ros/object-detection/
   This is a 3D visualization tool used in the ROS. It visualize sensor data, robot states and other information in 3D environment. 

Remark: combining the above two will provide real-time visualization of detected objects in a 3D environment.

2D Detection
---------------
start the simulation,
`roslaunch pr2_tc_gazebo main_elephant_person.launch`

create the package and the launch file,
`cd ~/catkin_ws/src
 catkin_create_pkg my_object_recognition_pkg rospy
 roscd my_object_recognition_pkg
 touch launch/yolo_v2_tiny.launch`

yolo_v2_tiny.launch,
`<?xml version="1.0" encoding="utf-8"?>

<launch>
  
  <!-- Use YOLOv3 -->
  <arg name="network_param_file"         default="$(find darknet_ros)/config/yolov2-tiny.yaml"/>
  <arg name="image" default="/camera/rgb/image_raw" />


  <!-- Include main launch file -->
  <include file="$(find darknet_ros)/launch/darknet_ros.launch">
    <arg name="network_param_file"    value="$(arg network_param_file)"/>
    <arg name="image" value="$(arg image)" />
  </include>

</launch>`

run the above launch file,
`roslaunch my_object_recognition_pkg yolo_v2_tiny.launch`


