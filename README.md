# iris_with_camera_gazebo

#### Ubuntu 18.04, ROS-melodic, PX4 v1.8.1

* * *

### MAVROS install
https://dev.px4.io/v1.8.0/kr/ros/mavros_installation.html



### gazebo_ros_pkgs install
http://gazebosim.org/tutorials?tut=ros_installing&cat=connect_ros



### Install px4
```
$ sudo apt update
$ sudo usermod -a -G dialout $USER

log out and log in ( or reboot )

$ wget https://raw.githubusercontent.com/PX4/Devguide/master/build_scripts/ubuntu_sim_nuttx.sh 
$ source ubuntu_sim_nuttx.sh

reboot

$ sudo apt install ros-melodic-geographic-msgs

$ wget https://raw.githubusercontent.com/PX4/Devguide/master/build_scripts/ubuntu_sim_ros_gazebo.sh

edit ubuntu_sim_ros gazebo.sh : kinetic -> melodic

$ source ubuntu_sim_ros_gazebo.sh
```
reference : https://dev.px4.io/v1.8.0/en/setup/dev_env_linux.html


```
$ git clone https://github.com/PX4/Firmware.git
$ cd Firmware
$ git checkout v1.8.1
```
reference : https://dev.px4.io/v1.8.0/en/setup/building_px4.html


##### you can skip the following step
```
$ git submodule sync --recursive
$ git submodule update --init --recursive
```


##### (if your PX4 doesn't work well,) do the following step (recommended)
```
$ mkdir build
$ cd build
$ cmake ..
$ make
( $ sudo make install )
```

```
$ cd ~/catkin_ws/src/Firmware/Tools/sitl_gazebo
$ mkdir Build
$ cd Build
$ cmake ..
$ make
```


### change Gazebo Path
```
$ vi ~/.bashrc

add the followings

export GAZEBO_PLUGIN_PATH=${GAZEBO_PLUGIN_PATH}:~/catkin_ws/src/Firmware/Tools/sitl_gazebo/Build
export GAZEBO_MODEL_PATH=${GAZEBO_MODEL_PATH}:~/catkin_ws/src/Firmware/Tools/sitl_gazebo/models
```


### Execute Gazebo by ROS
```
$ roscore

$ cd <Firmware>
$ no_sim=1 make posix_sitl_default gazebo

$ roslaunch gazebo_ros empty_world.launch world_name:=$(pwd)/Tools/sitl_gazebo/worlds/iris.world

you can change launch file or world_name
```


### get camera data by image
```
check rostopic and run
$ rostopic list
$ rosrun image_view image_view image:={topic name}
```
or using rviz
```
$ rviz

Change 'Fixed Frame' option to camera_link

Add PointCloud2 or Topic
```
reference : http://gazebosim.org/tutorials?tut=ros_depth_camera&cat=connect_ros 
