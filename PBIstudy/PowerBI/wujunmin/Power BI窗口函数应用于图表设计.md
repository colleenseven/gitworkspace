---
create_date: 2022-12-22T00:09:46 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI窗口函数应用于图表设计
source: https://mp.weixin.qq.com/s/GYUJRjut29I2guq70CrkLw
author: wujunmin
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

Power BI于2022年12月推出的窗口函数极大简化了使用[SVG矢量图自定义图表的](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491267&idx=1&sn=9f8011a4c2a7f38f17b6ef4168625c63&chksm=97db2793a0acae853c07277e58d55c0b8db67e953b44228508b7282f4e907af330cf64efbf51&scene=21#wechat_redirect)过程。OFFSET、INDEX和WINDOW函数对设计连续型图表有重大意义。（不了解窗口函数参考采总此文：[Power BI本月正式推出的DAX新函数：OFFSET、INDEX、WINDOW](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484083291&idx=1&sn=18c13a35482f8e36820368e5afb095ce&chksm=8e13b08cb964399ab081b2a692fd7ee8f9084104dc756f254a2182798ae93ded282579a8b706&scene=21#wechat_redirect)）

什么是连续型图表？连续性图表是指当前维度图表的内容和上一维度或下一维度存在关联。条形图柱形图是非连续型图表，因为每个柱子是独立分布的。折线图属于连续型图表，例如下图的纵向折线图，本行的折线走向受上一行和下一行影响。

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6SqcrZdMBhoMn0MWaj42maxSDBbheCtH4aeiaZjpPqqdd9ghhNmRnrRcjk146vRyiayRM1o8mJtTZ5w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

瀑布图当前柱子的位置受上一个柱子的位置的影响。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6SqcrZdMBhoMn0MWaj42maxmWB6CkHtrDQY4dLc6bEibYpe7XVZfvxHF3XqgvIAhEWarI5lLiauv7Kw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

OFFSET、INDEX、WINDOW分别实现了单行相对定位、单行绝对定位和任意范围的相对定位及绝对定位。**以下以纵向折线图为例进行讲解。**

纵向折线图每一行的折线形状由上一行数据、本行数据和下一行数据共同决定。比如，上一行数据50，本行数据20，下一行数据80，我们大体可以判断本行的折线走向大致如下图所示：

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6Ro5z9o7jVFn9TibTjRqNgrWCoZVO21icT3ibRbaibztjT39SgXnUFEn0ZXiaqtRG6J9hA3Ps2xHqv6pwg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如何在计算本行折线的时候，让图表度量值知道上一行数据和下一行数据分别是多少？这就需要使用OFFSET函数进行上下偏移。如下是上一行和下一行的计算结果：

```
上一行 = CALCULATE([Value],OFFSET(-1,ALLSELECTED('日期表'[Date]),ORDERBY('日期表'[Date])))
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6Ro5z9o7jVFn9TibTjRqNgrWZR06A4gbRLGL8mK4MYvBApiaq3RdOdgEdu3uDx5GXGphd3S5wGwRh7g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

以下是纵向折线的完整度量值，新建好度量值后，标记为图像URL，拖入表格。

```
纵向折线图 = 
```

此时你大概率得不到正确的结果，很可能显示如下图的断裂效果。这是因为水平网格线的存在切断了连线。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6Ro5z9o7jVFn9TibTjRqNgrWzNwWIeMMc53CKmG0J4uW8l7Jb5qe3QEk80CIa8icr7pEnU4gL1WtCbg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

将网格线的宽度调整为0之后，即可得到一条连贯的折线。另外图像高度的设置与度量值中的高度保持一致（此处为50）。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6Ro5z9o7jVFn9TibTjRqNgrWZnw5KcU4iaLPySFp6k6bjDDHIeTW1MVqo3ZdaSicFh6Sfj5MUBzqsS1w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这条折线还有第二种用法，放入条件格式的图标，下图右侧是条件格式模式：

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6Ro5z9o7jVFn9TibTjRqNgrWpOEtZkgbreqb8Fvjjg2GAqo83sNTVZiaEmkqFZib4lXdPKGjsvuIX7Xw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

有读者可能会有疑问，日期具有连续的特性，非连续的维度是否也可以同样操作？答案是可以的。下图的店铺业绩增长率是个示例：

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6Ro5z9o7jVFn9TibTjRqNgrWS5CSmHFibKeotRo2yZLwZu13oiakrMc2uz5ickE5hiavDL3voExUAY1ZNw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这条折线的圆点设置了按条件变化颜色，在这基础上还可以进行深加工，比如加上数据标签：

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6Ro5z9o7jVFn9TibTjRqNgrWFZRsxAf95xwP5AN2wjSUZ0OPiaQ0XaHKK4meZId0Nmaygs5hK8GAddg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

目前（截止2022年12月）推出的窗口函数最神通广大的是WINDOW，一定程度上，可以只用WINDOW，而不使用OFFSET和INDEX。比如上方度量值在定义上一行和下一行的值时使用了OFFSET，现在替换为WINDOW如下所示。WINDOW需要指明定位范围，例如上一行（度量值中的offsetlast）定位的起点和终点都是-1，REL表示相对偏移。

```
VAR OffsetNext=CALCULATE([Value],WINDOW(1,REL,1,REL,ALLSELECTED('日期表'[Date]),ORDERBY('日期表'[Date])))
```

度量值同样可以放于表格矩阵列显示，也可设置为条件格式图标，以下是条件格式效果。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6SqcrZdMBhoMn0MWaj42maxaG0ic1nwX1jH1QGsOvMZV3YX0G1g9esibuibo8NzWmV2NavcNIFrYy4zA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

本文INDEX函数还没有用到，且听后文分解。前期介绍的若干自定义图表都可以基于窗口函数进行优化。  

本文PBIX源文件在下方知识星球下载。直达链接（左下角阅读原文也可访问）：https://t.zsxq.com/09PlAsPkz

___

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/JHQQIBqYy6SrFOpSISmqT2k74QM76UrbIBKw9vBMzBUmBfibKCas2iccpABJdicQ4UNYGL2QCMLGaesXVyJ601kvw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

[详情](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491267&idx=1&sn=9f8011a4c2a7f38f17b6ef4168625c63&chksm=97db2793a0acae853c07277e58d55c0b8db67e953b44228508b7282f4e907af330cf64efbf51&scene=21#wechat_redirect)
