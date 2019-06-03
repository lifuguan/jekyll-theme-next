---
title: ROS melodic kernel 4.18 安装 realsense D435i
date: 2019-5-28 23:00:00
categories:
- D435i
- ROS
tags:
---


# 安装环境
系统：ubuntu 18.04 内核 4.118-generic
ROS： melodic
传感器：intel realsense d435i
环境上已经成功搭建并使用ROS完成demo

# 安装Realsense SDK
github：https://github.com/IntelRealSense/librealsense
安装可以参考文档：https://github.com/IntelRealSense/librealsense/blob/master/doc/installation.md


1. 下载source
```
git clone https://github.com/IntelRealSense/librealsense
cd librealsense
```
2. 安装依赖项
```
sudo apt-get install libudev-dev pkg-config libgtk-3-dev
sudo apt-get install libusb-1.0-0-dev pkg-config
sudo apt-get install libglfw3-dev
sudo apt-get install libssl-dev
```
3. Install Intel Realsense permission scripts located in librealsense source directory:
```
sudo cp config/99-realsense-libusb.rules /etc/udev/rules.d/
sudo udevadm control --reload-rules && udevadm trigger 
```
4. **重点** ： 我发现如果和官网一样运行`patch-realsense-ubuntu-lts.sh`编译内核，好像会报错， **但是**直接忽略掉并不会有什么影响，所以直接运行编译
```
mkdir build
cd build
cmake ../ -DBUILD_EXAMPLES=true
make
sudo make install
```
5. 进入/librealsense/build/examples/capture，试一下效果
```
./rs-capture 
```

# 安装realsense-ros
#### 不要不要不要安装intel-ros上的，intel-ros上缺少`DDynamic_reconfigure`（被intel悄咪咪删掉了）
#### 详情 ： https://github.com/ros/rosdistro/pull/20651 和 https://github.com/IntelRealSense/realsense-ros/pull/665

1. 直接下载  https://github.com/IntelRealSense/realsense-ros.git
2. 下载缺少包 https://github.com/pal-robotics/ddynamic_reconfigure
3. 直接运行`catkin_make`，绝对成功！


# 完
---

