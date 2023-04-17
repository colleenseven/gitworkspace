---
create_date: 2022-12-24T00:09:19 (UTC +08:00)
tags: wx/pbi/可视化图表 
aliases: null
pagetitle: Power BI表格矩阵实现大头针图的极简方案
source: https://mp.weixin.qq.com/s/-Q2xmcKFC-IOvt3dX-z4MA
author: wujunmin
status: 已完成 
category: 浏览文章 
notes: False
ZK: Origin
uid: 
---

大头针图，属于一种异形条形图。使用==REPT函数与UNICODE结合==，可以很简便的在Power BI表格、矩阵实现各种大头针效果。下图是两个基础版本，头部分别为实心和空心。

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6QRDwu1icQibw6r9TiajXkRYOg8YRZ245BqvcrQuD8XY1vFPYZjhicIB81fdY6iaascvBVDnmbHyQz2nwA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图表需要的素材是横线和圆圈，在https://unicode-table.com/cn/blocks/搜索对应关键字可以方便找到。如下度量值9472代表横线，9679代表实心圆。度量值放入表格即可正常显示。  

```
Unicode大头针图实心 = 
VAR MaxValue =
    MAXX ( ALLSELECTED ( '店铺信息'[店铺名称] ), '店铺信息'[业绩_今年] )
RETURN
    REPT ( UNICHAR ( 9472 ), 25 * [业绩_今年] / MaxValue )
        & UNICHAR ( 9679 )
```

横线使用REPT按照指定次数重复，从而达到长短不一的效果。这里最长的横线重复显示了25次。读者可以修改为其他数值，需要注意的是这个数值不宜过大也不宜过小，过小使得精确性不足，过大使得展示需要空间更大。  

因UNICODE是一种文本，此处可以使用条件格式中的字体颜色增加效果，上图排名前三显示为绿色，否则红色：

```
Color = IF([本期排名]<=3,"Green","Red")
```

UNICODE的线条样式和图标样式非常丰富，比如线条可以替换为虚线，头部的图标也可任意更换：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6QRDwu1icQibw6r9TiajXkRYOgQHE3icNCcicv5SAduyjICxFA7NPnL5VibP1L3jD36ykMGT7rCOny1nM4Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以使用链接文本的形式增加数据标签：

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6QRDwu1icQibw6r9TiajXkRYOgzHqdeWJk6adzQ4MqzvEN2VV7pvPlmJ3sl9wUIX4H0DIsoVUNAkGAEQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

上图的度量值如下：  

```
Unicode大头针图实心数据标签右 = 
VAR MaxValue =
    MAXX ( ALLSELECTED ( '店铺信息'[店铺名称] ), '店铺信息'[业绩_今年] )
RETURN
    REPT ( UNICHAR ( 9472 ), 25 * [业绩_今年] / MaxValue )
        & UNICHAR ( 9679 ) 
        & UNICHAR ( 8194 )
        & FORMAT([业绩_今年],"#,#")
```

度量值中的8194代表一个空格。数据标签的位置也可以换行显示UNICHAR(10)产生了这种效果。

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6QRDwu1icQibw6r9TiajXkRYOgwtRxV0HkmW15OAhtQ08upl9icgoicXRy9PYZPSgYOUtAcc9vWPcSJHwA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

文中的示例均为正数，如读者的数据涉及负数，需注意度量值调整图表的显示顺序。  

本文PBIX源文件在下方知识星球下载。直达链接（左下角阅读原文也可访问）：

_https://t.zsxq.com/098EsuUYu_
