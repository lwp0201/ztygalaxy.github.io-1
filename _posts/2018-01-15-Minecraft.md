---
layout: post
title: '树莓派搭建低功耗Minecraft服务器'
date: 2018-01-15
author: 张天宇
tags: 一跪一路
---

> 搭建你自己的Minecraft服务器，以及在树莓派上搭建Minecraft服务器。

为什么要折腾这个？
为什么要自己搭Minecraft服务器呢？限制于经费，在自己的服务器上玩Minecraft，不是随便谁都可以做的。搭建在服务器上，你可以让服务器一直运行，当你不玩的时候，你的朋友和家人还可以加入到游戏中，继续建造你的世界。你可以尝试修改游戏参数，制作mod，而且还能让你体验一把GM的感觉，这在公共服务器里可是做不到的，而且也不用花很多钱去租远程主机来做服务器。对于Minecraft狂热粉丝而言，搭建Minecraft服务器已经很有吸引力了。但是在树莓派上搭则会更有吸引力。小小的树莓派耗电非常少，你可以不间断地开着服务器，一年的电费也不过几块钱而已。只要一个树莓派，一张SD卡，花上一点时间设置一下，就能有一台全天候的Minecraft服务器，月运行费用只不过一条口香糖的价格。


## 0.需要的东西

​	一个已经烧录好系统的树莓派，一台能够联网的PC。

## 1.针对Minecraft优化树莓派

​	将系统分区拓展至整个SD卡分区，选择高级操作选项，拓展分区，重启。

​	![拓展分区](../../../assets/img/es0.png)

![拓展分区](../../../assets/img/es1.png)

## 2.安装Java环境

​	如果你的树莓派不是官方镜像或者没有安装Java环境，请先配置。

​	检查方法：

~~~shell
java -version
~~~

## 3.配置服务器

​	首先，用下面的命令下载一份代码(建议mkdir新建一个文件夹放置)：

~~~shell
sudo wget http://ci.md-5.net/job/Spigot/lastSuccessfulBuild/artifact/Spigot-Server/target/spigot.jar
# 这个链接可以一直用，因为它指向的是Spigot最新的稳定版
# 如果有任何问题，可以参考SpigotMC[http://ci.md-5.net/job/Spigot/]的下载页
~~~

​	下载完成后，输入下面的命令：

~~~shell
sudo java -Xms256M -Xmx900M -jar /home/pi/mc/spigot.jar nogui
# 参数说明：内存将从256M开始分配,最大900M
# 这里将代码放置在了mc文件夹中
~~~

​	接下来服务器启动，屏幕上会出现各种进度百分比。

​	等上大概几分钟，程序会搭建服务器，生成地图，之后的启动会快很多，大概20-30秒。在命令行用“stop”就可以优雅地关掉服务器，然后你就可以重启服务器，找出问题在哪里。

​	在上面的流程完成后，你就可以坐在电脑旁普通地玩Minecraft，启动程序，选择多人游戏。你会看到自己建的服务器，这是属于你自己的服务器。

###  	祝大家玩的开心！







PS：目录下server.properties参数说明，可按需修改

~~~properties
# 以下是Minecraft服务器设置文件，true代表执行，false代表不执行。

#Sun Mar 11 18:24:34 CST 2012 此为文件生成时间
# 是否开启地狱，不开启话地狱门将无效
	allow-nether=true
# 地图文件夹名称，下界与末路之地将会自动以nether,ender加上并用下划线隔开
　　level-name=world
# 是否开启GameSpy4协议服务器监听器，用于获取服务器信息，国内应该用不上。
　　enable-query=false
# 是否允许飞行
　　allow-flight=false
# 远程访问服务器的密码，此项可以留空或删除
　　rcon.password=
# 服务器端口(25565为默认端口，联机时无需输入)
　　server-port=25565
# 第5行对应功能的端口
　　query.port=25565
# 地图类型，Default=默认，FLAT=超平坦，LARGEBIOMES=巨型生物群系
　　level-type=DEFAULT
# 是否开启远程访问服务器控制台。技术人员可选。
　　enable-rcon=false
# 地图种子，在生成地图文件夹之前填入此项，可生成特定的地图
　　level-seed=
# 服务器IP，不输入则为默认IP，内网用户的话请填内网IP
　　server-ip=
# 最大建筑高度，上限是256，因为Chunk的高度最大值是256
　　max-build-height=256
# 是否生成NPC
　　spawn-npcs=true
# 是否开启白名单，没有白名单的玩家尝试进入服务器会被自动拒绝
　　white-list=false
# 是否生成动物
　　spawn-animals=true
# 此处填写服务器默认材质下载链接，链接必须以.zip结尾
　　texture-pack=
# 用于给http://snoop.minecraft.net网站发送服务器数据，这样玩家可以从客户端上获取服务器信息，推荐关闭
　　snooper-enabled=false
# 是否开启极限模式，玩家死亡将自动被ban
　　hardcore=false
# 是否开启联网模式(正版专用，盗版必须改成false)
　　online-mode=false
# 是否开启PVP，不是战争服就不要开了
　　pvp=false
# 游戏难度，与单机相同
　　difficulty=1
# 玩家第一次进入游戏时的游戏模式
　　gamemode=0
# 同时在线的最大玩家数
　　max-players=20
# 远程访问服务器的端口号，此项可以留空或删除
　　rcon.port=25575
# 是否生成怪物
　　spawn-monsters=true
# 是否生成建筑物(包括村庄和地牢)
　　generate-structures=true
# 可见距离，最大值为10
	view-distance=10
# 服务器欢迎信息(显示在玩家联机页面)，中文需中文补丁支持和转码，推荐EmEditor文本编辑器，自带转码功能。
　　motd=A Minecraft Server
~~~

