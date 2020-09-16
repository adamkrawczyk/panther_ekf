## Installation

First, you need to install robot localization pkg to use the `panther_ekf` package:

```
$ sudo apt-get install ros-noetic-robot-localization
```

After that, clone the `panther_ekf` repo to your `ros_ws/src` directory and compile with `catkin_make`.

## Installing camera drivers 

At the time of writing this was working. Let me know by creating an issue when it stops working. 

1. Add intel realsense repo for ubuntu18 (there is no version for ubuntu 20 yet)

```bash
sudo apt-key adv --keyserver keys.gnupg.net --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE || sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-key
sudo add-apt-repository "deb http://realsense-hw-public.s3.amazonaws.com/Debian/apt-repo bionic main" -u
```

2. Install libraries 

```bash
sudo apt-get install -y librealsense2-dkms
sudo apt-get install -y librealsense2-utils
sudo apt-get install -y librealsense2-dev
sudo apt-get install -y librealsense2-dbg
```

3. Install ROS wrapper

Go to your `ros_ws/src` and clone repository

```bash
git clone https://github.com/IntelRealSense/realsense-ros.git
cd realsense-ros
git checkout 2.2.17
cd ../..
catkin_make clean
catkin_make -DCATKIN_ENABLE_TESTING=False -DCMAKE_BUILD_TYPE=Release
```

INFO: I have used branch development tag 2.2.17 

Documentation taken from [librealsense](https://github.com/IntelRealSense/librealsense/blob/master/doc/distribution_linux.md#installing-the-packages) and from [realsense-ros](https://github.com/IntelRealSense/realsense-ros)

## Using `panther_ekf` package

To start the Intel Realsense cameras (T265 and D435i) and EKF run:
```bash
$ roslaunch panther_ekf panther_ekf_rs.launch
```

For version without cameras use:

```bash
$ roslaunch panther_ekf panther_ekf.launch
```

You can also include this launch in your custom launch files using:

```xml
<include file="$(find panther_ekf)/launch/panther_ekf.launch"/>
```


## Author

* **Adam Krawczyk**  - [adamkrawczyk](https://github.com/adamkrawczyk)

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details