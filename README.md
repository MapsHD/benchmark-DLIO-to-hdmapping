# dlo-converter

## Intended use 

This small toolset allows to integrate SLAM solution provided by [dlo](https://github.com/vectr-ucla/direct_lidar_odometry) with [HDMapping](https://github.com/MapsHD/HDMapping).
This repository contains ROS 1 workspace that :
  - submodule to tested revision of dlo
  - a converter that listens to topics advertised from odometry node and save data in format compatible with HDMapping.


## Building

Clone the repo
```shell
mkdir -p /test_ws/src
cd /test_ws/src
git clone https://github.com/marcinmatecki/DLO-to-hdmapping.git --recursive
cd ..
catkin_make
```

## Usage - data SLAM:

Prepare recorded bag with estimated odometry:

In first terminal record bag:
```shell
rosbag record /robot/dlo/odom_node/odom /robot/dlo/odom_node/pointcloud/keyframe
```

and start odometry:
```shell 
cd /test_ws/
source ./devel/setup.sh # adjust to used shell
roslaunch direct_lidar_odometry dlo.launch pointcloud_topic:=<pc_topic_name> imu_topic:=<imu_topic_name>
rosbag play <path_to_rosbag>
```

## Usage - conversion:

```shell
cd /test_ws/
source ./devel/setup.sh # adjust to used shell
rosrun dlo-to-hdmapping listener <recorded_bag> <output_dir>
```
