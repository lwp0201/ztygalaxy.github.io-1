---
layout: post
title: Python经纬度计算
categories: Notes
description: 这篇文章解决了两个问题，两个GPS坐标之间的距离，距离指定点一定距离的GPS范围
keywords: 
---
​	处理地图数据时，经常会遇到计算两个地理位置之间的距离或者范围标定。

​	这篇文章解决了两个问题，两个GPS坐标之间的距离，距离指定点一定距离的GPS范围。

​	1.给定两个坐标，计算其在地球表面的实际距离。

~~~python
def calDistance(lon1, lat1, lon2, lat2):
    lon1, lat1, lon2, lat2 = map(radians, [lon1, lat1, lon2, lat2])
    # haversine
    dlon = lon2 - lon1
    dlat = lat2 - lat1
    a = sin(dlat / 2) ** 2 + cos(lat1) * cos(lat2) * sin(dlon / 2) ** 2
    c = 2 * asin(sqrt(a))
    r = 6371  # earth_radios
    return c * r * 1000
~~~

​	2.给定坐标和范围大小，确定地理围栏。

![demo](https://images2015.cnblogs.com/blog/1034021/201702/1034021-20170207133355432-51913608.png)

~~~python
def getArea(latitude, longitude, dis):
    r = 6371.137
    dlng = 2 * math.asin(math.sin(dis / (2 * r)) / math.cos(latitude * math.pi / 180))
    dlng = dlng * 180 / math.pi
    dlat = dis / r
    dlat = dlat * 180 / math.pi
    minlat = latitude - dlat
    maxlat = latitude + dlat
    minlng = longitude - dlng
    maxlng = longitude + dlng
    return minlat, maxlat, minlng, maxlng
~~~

