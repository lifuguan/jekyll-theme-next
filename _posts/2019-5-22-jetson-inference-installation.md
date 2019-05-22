---
title:  Jetson TX2中的jetson-inference框架安装的问题
date: 2019-5-22 20:00:00
categories:
- ROS
- TX2
tags:
- jetson-inference
---

## 官方安装文档 
- https://github.com/dusty-nv/jetson-inference/blob/master/docs/building-repo-2.md


## 提醒
- 使用前要完全安装tensorrt,opencv,tensorflow工具

## 步骤

1. 跟着文档跑
2. 跑到`Configuring with CMake`中的`cmake ../`时暂停
3. `cmake ../`会执行位于`jetson-inference/CMakePreBuild.sh`，其中有大量的`wget`命令，在国内会很慢以至于失败
4. 这时候可以先自己把那些文件下载下来（文件下载链接 https://pan.baidu.com/s/13iXKyN4R28yasFlbJ-7Vjg）
5. 并放入规定的文件夹`/jetson-inference/data/networks/`
6. 然后注释掉`CMakePreBuild.sh`中的`wget`命令，再执行`cmake ../`命令
7. 最后再执行`make`命令
8. 完成