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
`cd ~/catkin_ws/src`
`catkin_create_pkg my_object_recognition_pkg rospy`
`roscd my_object_recognition_pkg`
`touch launch/yolo_v2_tiny.launch`

refer yolo_v2_tiny.launch file

run the above launch file,
`roslaunch my_object_recognition_pkg yolo_v2_tiny.launch`

3D Detection
-------------
create the following files in the following directory,
`roscd my_object_recognition_pkg`
`touch config/darknet_3d.yaml`
`touch launch/darknet_ros_3d.launch`

refer darknet_ros_3d.launch and darknet_3d.yaml files.

launch the file,
`roslaunch my_object_recognition_pkg darknet_ros_3d.launch`

start the visualizing tool,
`rviz`

and setup the following in the rviz, adding a RobotModel, Pointcloud2 and MarkerArray. within Pointcloud2 under topic select /camera/depth_registered/points. In MarkerArray under marker topic select /darknet_ros_3dmarkers. This enables us to visualize the 3D object within a box. 

To get the postion and other parameters related to the detected object do the following,
`rostopic grep | darknet`
`rostopic echo /darknet_ros_3d/markers`

we can utilize the above node to make decisions with the robot. 


