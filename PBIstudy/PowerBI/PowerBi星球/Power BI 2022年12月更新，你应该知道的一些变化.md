---
create_date: 2022-12-15T23:48:43 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI 2022年12月更新，你应该知道的一些变化
source: https://mp.weixin.qq.com/s/nEQ3JX27kWHI9l-pxdT0ug
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

PowerBI2022年的最后一次更新如期而至，这次更新主要是带来了几个新的DAX函数和一些新的图表，关于本月的更新你可以在官方博客中浏览全面的介绍，点击最下方的阅读原文也可直接进入：

https://powerbi.microsoft.com/zh-cn/blog/power-bi-december-2022-feature-summary/

还可以在视频号中观看本月更新的微软官方视频讲解（已加中文字幕）:

这里我挑选几个你应该用到的更新带你浏览一下。

**1.** **切片器类型设置移动到格式窗格**

之前更改切片器的类型是通过鼠标悬停在标头上，点击向下的小箭头来设置的，如下图。

本月更新后，这个设置移动到格式窗格中，在切片器设置>选项>样式中进行设置。

**2\. 新增DAX函数**

本月正式发布了三个DAX函数：INDEX、OFFSET 和 WINDOW。

-   INDEX使用绝对定位检索结果；
    
-   OFFSET使用相对定位检索结果；
    
-   WINDOW使用绝对或相对定位检索结果片段。
    

这些函数还带有两个辅助函数， ORDERBY 和 PARTITIONBY，将使执行计算变得更加容易，例如：

-   比较值与基线或查找另一个特定条目（使用 INDEX）；
    
-   将值与先前值进行比较（使用 OFFSET）；
    
-   添加运行总计、移动平均值或依赖于选择一系列值的类似计算（使用 WINDOW）。
    

这里可以先有个印象，后面会结合具体场景来详细介绍这几个DAX函数的用法。

**3、新增自定义图表**

本月新增一大波自定义视觉对象，官方公布的列表如下：  

-   kpi emoji
    
-   GANTT by Lingaro
    
-   Aimplan Planning and Reporting Visual
    
-   Excalibur
    
-   3DBI
    
-   verticalText by sio2Graphs
    
-   Definitive Logic Advanced Gantt Chart高级甘特图
    
-   swColorMap\_twoLevels
    
-   100% Clustered Stacked Bar Chart (Standard) 簇状堆积条形图
    
-   100% Clustered Stacked Column Chart (Standard)簇状堆积柱形图
    
-   Advanced Line Chart (Standard)高级折线图
    
-   Bubble Chart with Categorical Data (Standard)
    
-   Dual X-axis Bar Chart (Standard)双X轴条形图
    
-   Dual Y-Axis Column Chart (Standard)双Y轴柱形图
    
-   Likert Scale (Standard)
    
-   Lollipop Bar Chart (Standard)
    
-   Overlapping Column (Standard)
    
-   Pie Chart with Full Legend Label (Standard)
    
-   Lollipop Column Chart (Standard)棒棒糖柱形图
    
-   Population Pyramid (Standard)人口金字塔图
    
-   Dual X-Axis Combo Chart (Standard)双X轴组合图
    
-   Dual Y-Axis Combo Chart (Standard)双Y轴组合图
    
-   Horizontal Bullet Chart (Standard)水平子弹图
    
-   Merged Bar Chart (Standard)合并条形图
    
-   Overlapping Bar (Standard)重叠图
    
-   Vertical Bullet Chart (Standard)垂直子弹图
    
-   Multiple Vertical Line Chart (Standard)多条垂直折线图
    
-   OneTax-PowerBIvisual
    

你可以在AppSource中加载使用，我之后也会挑选一些好用的视觉对象作更详细的介绍。

本月的更新就简单介绍这几个，更全面的功能可以去看官方博客继续探索，或者视频号中观看中文字幕的官方视频讲解。

___

PowerBI每月更新后，如果不能自动更新或者不方便下载，可以在公众号后台发送"**软件下载**",获取最新的PowerBI Desktop安装包；

如果要下载历史安装包，也可以发送**6位年月编号**获取，比如发送“202109”获取2021年9月的安装包。

更多安装说明请参考：[关于Power BI的下载和安装，你想知道的都在这里了](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078648&idx=1&sn=7e53496bd78498ed962696055a500474&chksm=8e13a2efb9642bf98bb73de730c5141d61eb2dfd22e1781c2603745137302ea56ba2ae4dd6ba&scene=21#wechat_redirect)

___

**如果你想深入学习Power BI，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和5000+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMstwXX5zrKianmFXzyqbIVgh7byfo3V8JJPmhqicywbtYkM0j2ibngnT5XBZ2AwKvGZiby9ngoKfLvzg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门Power BI》电子书，轻松入门。
