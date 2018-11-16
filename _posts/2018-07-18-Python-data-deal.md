---
layout: post
title: Python数据处理初
categories: Notes
description: 最近实验室数据处理，一个Didi的数据文件要四千万条数据左右，了解了一下python。本着拿来主义的学习原则，用到什么学什么，记录之。
keywords: 
---
>  最近实验室数据处理，一个Didi的数据文件要四千万条数据左右，了解了一下python。本着拿来主义的学习原则，用到什么学什么，记录之。

### 一、数据读入与输出

~~~ python
#1.按照指定列名读入数据
names = ['ID1','ID2','time','Longitude','Latitude']
f = open('F:/迅雷下载/已上传/g.csv')
df = pd.read_csv(f,names = names)

#2.逐行读入数据
with open("F:/迅雷下载/已上传/order.csv") as f:
    for line in f:
        #do something with data
        
#文件写入
f_average = open('G:/DidiPython/driverData.txt')
fw.write('Hello World!')
fw.close
~~~

### 二、数据处理

~~~python
#查找两个DataFrame对应属性元素
df_order['ID2'].isin(dd_gps['ID2'])

#使用pandas和numpy求某项平均值与方差
import pandas as pd
import numpy as np
names = ['ID1','average','var']
df_average = pd.read_csv(f_average,names = names)
a_list=df_average['average'].values.tolist()
al_array=np.array(a_list)
print((al_array.sum()/al_array.size))
print ('方差：%0.2f' % r_array.std())

#数据按列去重
d_driver=df_gps.drop_duplicates(['ID1'])

#Dataframe遍历
for row_gps in d_driver.itertuples(index=True, name='Pandas'):
    print(getattr(row_gps, "ID1"))
    
#数据基本格式化，格式：（11.22222，33.44444）
print ('(%.05f' % getattr(row, "Longitude"),end='')
print (',%.05f),' % getattr(row, "Latitude"))
print(df.loc[indexs].values[0:2])
~~~

### 三、地图数据轨迹还原

​	这里采用了GitHub上的开源库gmplot，[具体使用方法](https://github.com/vgm64/gmplot)。




**使用方法、项目代码及其他未尽事宜，详情请见 [GAIARead](https://github.com/ztygalaxy/GAIARead)。**