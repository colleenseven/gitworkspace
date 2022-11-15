---
notes: False
aliases: null
create_date: 2022-09-16T23:28:19 (UTC +08:00)
tags: wx/pbi/数据处理功能
pagetitle: Power BI 2022年9月更新，你应该知道的几个变化
source: https://mp.weixin.qq.com/s/FTn7Hy9cbn8Hn-5uIz2GaA
author: 采悟
status: 已完成
category: 浏览文章
uid: 
---

Power BI 2022年9月的更新如期而至，首先修补了上个月版本中的[几个bug](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484081741&idx=1&sn=598ab271338bc77087bd181c03665e30&chksm=8e13be9ab964378cebaa62f897fff96f3b852d9332533bb0e984ca202647824eed40cd38cbe4&scene=21#wechat_redirect)，本月更新主要是优化了层级坐标轴的显示方式，你可以在官方博客中浏览全部的介绍，点击最下方的阅读原文也可直接进入：

https://powerbi.microsoft.com/zh-cn/blog/power-bi-september-2022-feature-summary/

还可以在视频号中观看本月更新的微软官方视频讲解（已加中文字幕）:

本月的更新依然没有大的变动，这里我挑选几个可能会对你有用的细节简单介绍一下。

### **1\. 层级坐标轴优化**

当图表的X轴放多个字段时，比如把年、季度、月份都放到柱形图的X轴中，之前默认是这样的效果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOQ4Ig8TCcEiaebBbx92FC879kC2c3bT0tXcPvLFTicibdYyAnIW5b1qgcC13ewaqdC2sPdcicX5QWf0A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

看起来非常拥挤，而现在新的版本下，默认可以实现如下的效果：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOQ4Ig8TCcEiaebBbx92FC87Dt3gQsh1VxP8gyzOlaceLQwic2iaias9fleSVjnrwaqRf96jJIOe3yLCA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

<mark style="background: #FF5582A6;">重复的维度自动分组显示</mark>，这样的坐标轴是不是简洁多了。  

### **2\. 增加了是否显示聚合类型的选项**

将列字段放到表格中时，之前是自动不显示默认聚合的类型，比如下面这个表格中，列字段\[零售价\]的默认聚合方式是“平均值”，直接拖拽到表格里是不显示聚合类型的：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOQ4Ig8TCcEiaebBbx92FC870yMBWhbEfV9AGfNWuBa5v8eIU2xaAWUNfU0sje6Qu9M0bK2FBvI6kw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样可能会让用户误解，每个产品类别有多个产品，零售价是怎么聚合的，代表的是什么含义？所以新的版本中新增了一个选项：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOQ4Ig8TCcEiaebBbx92FC878bg4IY8icZ8IaIia1lcbLe21KDJicmSPiaicT3ibAODsJtBUicP2PF7AWkLDA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

上图的设置勾选后，则无论是否为默认的聚合类型，都会显示出来，这样就能看出来，这个数据是每个产品的平均售价。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOQ4Ig8TCcEiaebBbx92FC87bFuDBuu6GbjTwmqJbbW5zEcrAZQr6y4rJKIicXQiafm2jPUicMLYz9a8w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其实建议直接用显示度量值来聚合，对度量值规范命名，并不会引起歧义，所以这个功能意义不大。  

### **3\. 移动布局单独调整格式功能普遍可用**

[移动布局单独调整格式功能](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484079146&idx=1&sn=9107a5be99c1ea63fbb1da3209aa3785&chksm=8e13a0fdb96429ebf572ac6b2b9c7d3cf739de85f3490af96e18fff8e161d25e6f2ced19f2db&scene=21#wechat_redirect)最早在今年2月推出，现在该功能普遍可用！

移动格式选项允许您在移动优化布局中设置视觉效果的样式和格式，而不会影响其在桌面布局中的格式。这为您提供了极大的灵活性，并为创建真正针对手机查看优化的精美报告开辟了设计可能性的世界。

本月的更新就简单介绍这几个，更全面的功能可以去看官方博客继续探索，或者视频号中观看中文字幕的视频讲解。
