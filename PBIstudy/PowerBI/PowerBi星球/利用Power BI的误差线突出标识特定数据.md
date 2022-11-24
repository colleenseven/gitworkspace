---
ZK: Origin
notes: True
aliases: null
create_date: 2022-06-19T12:31:26 (UTC +08:00)
tags: wx/pbi/可视化方法
pagetitle: 利用Power BI的误差线突出标识特定数据
source: https://mp.weixin.qq.com/s/-j8YpWielSYcLv5q7sXyug
author: 采悟
status: 已完成
category: 精读文章
uid: 
---

DAX:: IF, SELECTEDVALUE,MAXX,ALLSELECTED

---

之前曾介绍过一个可视化技巧，在折线图中添加垂直的阴影区域来突出标识特定数据：  

[PowerBI作图技巧：折线图突出标识特定数据](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068536&idx=1&sn=ada48acc8cfa143660fb749c68caa808&chksm=8e0c4a6fb97bc379ac2dc0552fa46326c6d8cd94124b7303f2532b2ed9e4beb3c4c9fe1baec1&scene=21#wechat_redirect)  

其效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMC9ReMPszcD1F27Yn46TQKYKsOM5JaC1NswWeuEQyd0yv5ibP2ljI2cGLvdxdq2shibGkibbu8uyyBw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这是利用折线和柱形组合图来实现的，这些阴影其实就是组合图中的柱子。

最近有伙伴在用这种方式的来设计时，发现无论怎么调整格式都做不到上图的效果，而是下面这样的，两个相邻的柱子无法完全贴合到一起，中间会有个缝隙。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPtJqPCmPPTn0EC7W4Oz6kZ2lFib36qJf6ibNHSXU5xxlHqZib7p5f27ev3GOHIQTjia0yqBH8oYs04Rg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这是由于新版本中组合图调整柱子间距的功能缺失了，导致无法完全重现之前的效果，也就导致这个方法不再适用。

不过现在我们还可以利用折线图的误差线功能，更方便的实现这种效果，关于误差线，它是在3月份刚发布的，之前专门介绍过，你可以先看看这篇文章了解它的用法：

[**PowerBI 2022年3月更新，折线图支持添加误差线了**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484079538&idx=1&sn=db3d9ce423d4c771891cd86e586fb9c6&chksm=8e13a165b9642873e5162a3b25f7ad2bd1b0e04e0f572cc77fc7195642806869e545cfd74e7e&scene=21#wechat_redirect)  

下面还以[之前的文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068536&idx=1&sn=ada48acc8cfa143660fb749c68caa808&chksm=8e0c4a6fb97bc379ac2dc0552fa46326c6d8cd94124b7303f2532b2ed9e4beb3c4c9fe1baec1&scene=21#wechat_redirect)，突出标记折线图中周末的数据为例，来看看是如何用误差线来设计阴影的效果。

先写两个度量值作为误差线的上限和下限：  

> 下限 = IF( SELECTEDVALUE('日期表'\[周末\]) ="Y",0)
> 
> 上限 =
> 
> IF(
> 
>    SELECTEDVALUE('日期表'\[周末\])="Y",
> 
>    MAXX(ALLSELECTED('日期表'\[日期\]),\[销售金额\])
> 
> )

<mark style="background: #FF5582A6;">下限度量值的逻辑是，如果当前上下文日期是周末，则返回0</mark>；<mark style="background: #FF5582A6;">上限度量值的逻辑是，如果当前上下文日期是周末，返回当前所选时间段的最大值</mark>，<mark style="background: #FF5582A6;">其他情况上限和下限都返回空值</mark>。

用日期和销售金额先做一个折线图，然后打开折线图的分析面板，找到误差线功能，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPtJqPCmPPTn0EC7W4Oz6kZ0tzKJDaEPblibTia5ymMulogDicWrOEy3RE8aby2rk4LYyYyyV56CTxYQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

展开误差线选项，将上面写的度量值放进去，并进行如下的设置：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPtJqPCmPPTn0EC7W4Oz6kZfOVric7SfMpib5GjXcGNibcqc1mdbV0w8Upg4xnSUdRFUWKQvtYmsoH8w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

注意上下限与度量值的关系要选“绝对"，然后就可以实现同样的阴影标记效果了：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPtJqPCmPPTn0EC7W4Oz6kZeVISzFgPPHrt6DAJapt5G1hRqtAk2NoEV3lMvkQ07wqadbCyzxqVUA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

利用误差线的方法，是真正的在折线图中添加阴影标记，更加实用。

以上的例子是<mark style="background: #FF5582A6;">为周末添加阴影</mark>，其他各种特定的区间添加阴影都可以参考这种思路，关键是灵活掌握误差线的用法。
