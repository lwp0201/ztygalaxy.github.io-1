---
layout: post
title: 次元画社(一)，带有渐变动画的启动Activity
feature-img: "assets/img/pexels/book-coffee.jpeg"
thumbnail: "assets/img/pexels/motherboard.jpg"
tags: [Android, 次元画社]
---

## 一、概述

​	次元画社：基于Android的二次元图片分享社区，用户通过实时绘画或本地上传与其他用户共同分享图片，其中图片以瀑布流显示并配以高斯模糊背景等美化效果，独立开发，持续完善中。

​	目的：练手，对一些基础部件进行一些应用，拆分讲解。

​	开发工具：Android Studio

## 二、基础准备

### 1.创建一个新的空Activity，StartActivity。

### 2.设计布局文件，activity_start.xml.

​	布局规划及效果图如下：

![效果图](https://raw.githubusercontent.com/ztygalaxy/ztygalaxy.github.io/master/assets/img/thumbnails/start.jpg)

~~~xml
<!-- 采用常规摆放方式，logo左上，AppName、Slogan和声明放在下方.
	 工程全部采用string.xml引用字符串编写.
-->
<?xml version="1.0" encoding="utf-8"?>
<!--相对布局兜底-->
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:tools="http://schemas.android.com/tools"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_centerVertical="true"
                android:background="@mipmap/spll"
                android:orientation="vertical"
                tools:context="com.android.zty.ssssss.StartActivity">
 	<!--logo放置左上角-->
    <ImageView
        android:layout_width="50dp"
        android:layout_height="50dp"
        android:layout_margin="20dp"
        android:src="@mipmap/logo"/>
  	<!--线性布局，包裹AppName、Slogan-->
    <LinearLayout
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_above="@id/tv_group"
        android:layout_centerHorizontal="true"
        android:layout_marginBottom="10dp"
        android:gravity="center_horizontal"
        android:orientation="vertical">
        <ImageView
            android:layout_width="wrap_content"
            android:layout_height="50sp"
            android:layout_marginBottom="10dp"
            android:src="@mipmap/appname"/>
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_centerHorizontal="true"
            android:layout_gravity="center_horizontal"
            android:text="@string/slogan"
            android:textColor="#000"
            android:textSize="15sp"/>
    </LinearLayout>
  	<!--作者信息-->
    <TextView
        android:id="@+id/tv_group"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:layout_centerHorizontal="true"
        android:layout_marginBottom="8dp"
        android:text="@string/author"
        android:textColor="#6b6b6b"
        android:textSize="10sp"/>
</RelativeLayout>
~~~

配合自动生成的StartActivity代码，此时一个启动页面就做好了，但它还没有自动跳转功能，一般而言我们所见到的APP启动后都会简单展示自动跳转到主页面。

下面，我们来实现这个功能。

## 三、渐变的加入

加入一个动作较短的渐变动画是一个很好的主意。

### 1.动画设计

![动画文件位置](https://raw.githubusercontent.com/ztygalaxy/ztygalaxy.github.io/master/assets/img/thumbnails/alpha.png)

​	在资源文件夹res下新建anim文件夹用于存放渐变动画xml文件，这里新建了一个alpha.xml用于执行启动页面的渐变动画，代码如下：

~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<!--
    alpha 渐变动画
    duration 设置动画播放时长
    fromAlpha 动画开始时的透明度
    toAlpha 动画结束时的透明度
      （0 完全透明 1 完全不透明）
 -->
<alpha xmlns:android="http://schemas.android.com/apk/res/android"
       android:duration="1700"
       android:fromAlpha="0.2"
       android:toAlpha="1.0"/>
~~~

### 2.动画装入

#### 1.基本设置

~~~java
//全屏显示
getWindow().setFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN,
                WindowManager.LayoutParams.FLAG_FULLSCREEN);
//去除标题栏
this.requestWindowFeature(Window.FEATURE_NO_TITLE);
//装入流布局
View rootView = LayoutInflater.from(this).inflate(R.layout.activity_start, null);
setContentView(rootView);
~~~

#### 2.设置渐变动画

~~~java
Animation animation = AnimationUtils.loadAnimation(this, R.anim.alpha);
//设置动画监听器
animation.setAnimationListener(new Animation.AnimationListener() {
    @Override
    public void onAnimationStart(Animation animation) {
       // TODO Auto-generated method stub
    }
    @Override
    public void onAnimationRepeat(Animation animation) {
       // TODO Auto-generated method stub
    }
    //动画结束后跳转到下一个Activity(TestActivity)
    @Override
    public void onAnimationEnd(Animation animation) {
        Intent i = new Intent(StartActivity.this, TestActivity.class);
        startActivity(i);
        // finish();
    }
 });
//开始播放动画
rootView.startAnimation(animation);
~~~

​	在这里发现因为下一个布局加载延迟，直接finish掉StartActivity可能会出现黑屏空隙，因此想到这么一个思路，增加了一个新变量指向自己，在下一个活动加载完成后finish。

~~~java
public static StartActivity mActivity = null;
mActivity = this;
//在下一个活动中调用
StartActivity.mActivity.finish();
~~~

​	**这样，一个带有一定动画效果的启动页面就做好了。**

![效果图](https://raw.githubusercontent.com/ztygalaxy/ztygalaxy.github.io/master/assets/img/thumbnails/start_demo.gif)





