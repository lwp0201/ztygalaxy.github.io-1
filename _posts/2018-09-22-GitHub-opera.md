---
layout: post
title: 'Github基本操作入门'
date: 2018-09-22
author: 张天宇
cover: 'http://on2171g4d.bkt.clouddn.com/jekyll-banner.png'
tags: Notes
---

>  一些常用基本操作

#### 创建空目录

```java
mkdir Test
cd Test
pwd //显示当前目录
```

#### 将目录变成git仓库

```java
git init
```

#### 添加文件到仓库并提交

```java
git add readme.txt / git add .
git commit -m "first commit"
git remote add origin https://gitee.com/ztygalaxy/Test.git
git push -u origin master
git add .
git commit -m "second"
git push origin master
```

#### 克隆远程仓库

```java
git clone git@gitee.com:ztygalaxy/DidiPython
cd DidiPython
ls
git add .
git commit -m "first commit"
git push origin master
```

### 分支管理

#### 创建dev分支

```java
git branch dev
```

#### 切换到dev分支

```java
git checkout dev
```

```
git checkout -b dev
```

#### 查看所有分支

```java
git branch
```

#### 提交改动

```java
git add readme.txt 
git commit -m "branch test"
```

#### 切换回master分支

```java
git checkout master
```

#### 将dev分支合并到master分支

```java
git merge dev
```

 readme.txt | 1 +
 1 file changed, 1 insertion(+)