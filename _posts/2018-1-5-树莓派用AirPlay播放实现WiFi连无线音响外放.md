---
layout: post
title: 树莓派用AirPlay播放实现WiFi连无线音响外放
feature-img: "assets/img/pexels/circuit.jpeg"
thumbnail: "assets/img/thumbnails/pi.jpeg"
tags: [RaspberryPi]
---

​    之前[有一篇文章](http://wangye.org/blog/archives/921/)介绍了如何使用蓝牙实现手机连接无线音箱外放，在网上搜索相关资料的过程中，我发现了树莓派另外一个强大的功能，那就是可以实现苹果(Apple)的AirPlay播放技术，简单的介绍一下，AirPlay类似于蓝牙音响播放，但是其是建立在WiFi局域网基础上的，在接入有AirPlay播放技术的局域网上，苹果的设备就会显示支持AirPlay。综合AirPlay的优势，我开始在Raspberry Pi（树莓派）上实现相关功能。

  同样的，关于树莓派一些好玩的功能国外资料较为丰富，经过查阅后[《Raspberry Pi Airplay Tutorial》](http://www.raywenderlich.com/44918/raspberry-pi-airplay-tutorial)（原文超级详细）这一篇文章对我帮助较大，具体步骤如下。

1. 升级Raspberry Pi系统的软件

   ~~~shell
   sudo apt-get update
   sudo apt-get upgrade
   ~~~

2. 将音频输出变更为默认的音频输出口

   通常情况下树莓派的音频输出使用的是HDMI接口，我们需要下面的命令将其变更为普通音频输出口：

   ~~~shell
   sudo amixer cset numid=3 1
   ~~~

3. 安装系统所必需的软件包

   ~~~shell
   sudo apt-get install git libao-dev libssl-dev
   sudo apt-get install libcrypt-openssl-rsa-perl libio-socket-inet6-perl
   sudo apt-get install libwww-perl avahi-utils libmodule-build-perl
   ~~~

4. 安装Perl Net-SDP协议软件

   ~~~shell
   cd ~
   git clone https://github.com/njh/perl-net-sdp.git perl-net-sdp
   cd perl-net-sdp
   perl Build.PL
   sudo ./Build
   sudo ./Build test
   sudo ./Build install
   cd ..
   ~~~

5. 使用Shairport将树莓派设置为AirPlay接收器

   ~~~shell
   cd ~
   git clone https://github.com/hendrikw82/shairport.git
   cd shairport
   make
   ~~~

6. 启动Shairport以支持AirPlay

   ~~~shell
   ./shairport.pl -a ZhangPi
   ~~~

   这里我们指定了一个名字叫做ZhangPi，大家可以根据实际进行修改，自此，你可以使用苹果设备来访问AirPlay了，当然每次使用这个命令略显不便，下面介绍如何将其变成系统服务。

7. 将Shairport设置为系统服务

   ~~~shell
   cd shairport
   sudo make install
   sudo cp shairport.init.sample /etc/init.d/shairport
    
   cd /etc/init.d
   sudo chmod a+x shairport
   sudo update-rc.d shairport defaults
   ~~~

   好了，上面的步骤将移植Shairport到系统路径下，同时创建名称为shairport的服务，你可以使用`sudo service`控制这个服务。

   接下来编辑这个启动文件：

   ~~~shell
   sudo nano /etc/init.d/shairport
   ~~~

   找到`DAEMON_ARGS="-w $PIDFILE"`这行，并且修改成`DAEMON_ARGS="-w $PIDFILE -a ZhangPi"`，同样的这里WangyePi为你的AirPlay名字。

   ~~~shell
   sudo service shairport start
   ~~~

启动AirPlay看看效果吧：