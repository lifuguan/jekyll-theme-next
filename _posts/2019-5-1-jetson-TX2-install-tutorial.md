---
title:  jetson TX2(JetPack 4.2)安装和配置指南
date: 2019-5-2 16:00:00
categories:
- TX2
- ROS
tags:
---
# Jetson TX2（Jetpack 4.2）刷机完全教程

## 在主机安装SDKManager并刷机

![SDKManager](https://img-blog.csdnimg.cn/20190403191419432.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1lhbl9Kb3k=,size_16,color_FFFFFF,t_70)

- 参考教程
https://blog.csdn.net/Yan_Joy/article/details/88998578

### 要注意的地方

1. 选择手动（manual）模式
2. 安装完Jetson OS时，需要在TX2上进行最后的设置操作，然后才可以安装jetson SDK
3. 等待，鬼知道要等多久

## Jetson TX2换源

- 在换源的时候，注意添加`-ports`（ https://blog.csdn.net/Yan_Joy/article/details/88998578 文章最后部分）。否则会出现`apt update 404`的情况。
- 千万别信是什么arm64架构的问题

## 在TX2上安装ROS

- 由于JetPack对应的是Ubuntu 18.04，所以不能使用网上流行的方法，比如：运行`installROSTX2`。 但是我们可以使用Xavier的方法。

- 更重要的是，在查看这个sh文件后，我们发现其实可以直接采用最正常的方法进行安装（出错概率低且可以使用`国内源`）

- 安装步骤
https://blog.csdn.net/zhangrelay/article/details/80241758

## 开发环境：pycharm 和 QT creator 

### 1. Pycharm安装
1. 安装JDK环境。使用`wget http://download.oracle.com/otn-pub/java/jdk/8u111-b14/jdk-8u111-linux-x64.tar.gz` 安装包在你执行这个命令时所在的文件夹位置
2. 解压
3. 设置环境变量：
    修改全局配置文件，作用于所有用户：
    打开配置文件`gedit ~/.bashrc`
    ```bash
    export JAVA_HOME=/usr/lib/jdk/jdk1.8
    export JRE_HOME=${JAVA_HOME}/jre
    export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
    export PATH=.:${JAVA_HOME}/bin:$PATH
    ```
    激活`source ~/.bashrc`
4. 下载pycharm社区版。 https://www.jetbrains.com/pycharm/download/#section=linux 
5. 
6. 解压。 ubuntu可以直接使用右键解压，当然可以`cd`切换到目标所在目录使用`tar -avxf`来进行解压。
7. cd到bin文件夹，运行./pycharm.sh
8. 完成

- 参考文档：https://cloud.tencent.com/developer/article/1327218

### 2. QT creator安装

## 事先声明：我看到一篇贼牛逼的文档 https://doc.qt.io/QtForDeviceCreation/qtee-preparing-hardware-jetsontx1.html 不过还没试过，有兴趣可以看看

1. 安装命令 `sudo apt-get install qt5-default qtcreator -y`
2. 下面就开始进行gcc的配置，首先定位到Tools->Options->Build & Run->Compilers ，然后点击Add并选择GCC，在compiler path一栏，输入gcc地址：/usr/bin/gcc 。接下来修改ABI选项，将其依次修改为custom – arm – linux – generic – elf – 64 bit，完成后点击apply生效。

![](https://img-blog.csdn.net/20170815122235610?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMzg4ODAzODA=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)