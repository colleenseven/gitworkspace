---
aliases: null
create_date: 2022-05-22T11:42:36 (UTC +08:00)
tags: wx/pbi/可视化图表
pagetitle: 认识3个新的Power BI可视化控件
source: https://mp.weixin.qq.com/s/EQN6yAMDe_fCjo7E6EKG5w
author: 采悟
status: 已完成
category: 浏览文章
uid: 
---

今天周末，带你认识3个最近增加的Power BI 自定义可视化控件。  

___

## **Mass Filter**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPdps8BZLtoJusqBlFlG4L3vOt7xIicz446o4hfkCb34icYqquXfJlHKIticAuAw0T1Ar7b38Wtx2ibGw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

Mass Filter 优点是用户可以<mark style="background: #FF5582A6;">从任何外部源复制筛选的列表，并将其粘贴到输入框中，然后单击过滤器按钮时，所有值都会立即用于过滤报告</mark>，不需要中间步骤，如下图。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPdps8BZLtoJusqBlFlG4L3palc8xj335N1JHE9w54Zjq9t3sGZfkkxuzMTZiaWXZjkq0fibAhicePFQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

用户还可以通过单击下面框柱的这个按钮，来切换关键字列表是筛选还是排除，比如排除的效果是这样的，除了这个列表中的不显示，而只显示其他数据。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPdps8BZLtoJusqBlFlG4L3wj17BHWjH7h4ppZuZBvss5e40Ct5aONIAly9VkKY4PEpQ9zI1Bibm3A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

当<mark style="background: #FF5582A6;">某个维度的选项特别多时，切片器一项项找会比较麻烦，而利用这个控件操作更简单一些</mark>。

___

## **Preselected Slicer(预选切片器)**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPdps8BZLtoJusqBlFlG4L3X8d13POCXibsAAibicppyYibdHbzknAYx1BSwpZJxyHFoQPS2cKgFNNB4Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个切片器最大的优点就是可以<mark style="background: #FF5582A6;">设定切片器的默认值，利用DAX来表达默认的逻辑</mark>。

它不太方便的地方，是必须建个这样的辅助表才能正常使用，  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMOPxX0f8Qxh465ByIP1NdLfZBibM2xsU4mGhaDA01RbjC1DzM79aw8ibkK6ZZUDq4zuRyhPP9nSSwg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个表就是True和False的笛卡尔积组合列表，需要把其中一列，放到该切片器的【Dirty Status】中；如果一个页面上放置两个该切片器，最好使用不同的辅助列。

比如设定切片器默认选择当前月份（之前的做法参考：[Power BI设计技巧：切片器的动态筛选](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074134&idx=1&sn=351c14436442ed68b0249ee1e4f5de72&chksm=8e0c5c41b97bd557d4347f0b6d9dc33ea87166d5de716c34cf68dd9ddece57d2ee2195847b1a&scene=21#wechat_redirect)），可以这样来写个度量值:

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMOPxX0f8Qxh465ByIP1NdL8u3GsObfB23LoBFdDdQSZrFm1IeRuibnKZDjQM0Zu45kZVlpx9OB3xA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

将相关字段放到这个切片器的字段框中：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMOPxX0f8Qxh465ByIP1NdLMYaPqSLvPql1yxWSMPnkyCOFO9qZ84Zaxw5Iml0Ctx0byTr0Ad5ZWw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后任何时候打开报告，这个切片器都会默认显示在当前月份：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMOPxX0f8Qxh465ByIP1NdLhaa3YEib3e69LXic0fiagwN3rBib2SgibJFUgs6gIv3WYhhZBicJhV9KicAjg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个切片器看起来和内置切片器差不多，依然也还可以选择其他月份，并且右上角有个红色的按钮，无论切片器当前选择什么，点击这个按钮可以一键重置到默认状态。

该切片器的配置中还有个功能也很有用，让选中的项目自动置顶：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMOPxX0f8Qxh465ByIP1NdLvPCMAN7WpzNloK7UqAG7aCiajqKDGLyHfU8mKTMRUuWEqu0hOpoGjzQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

打开这个选项后，然后无论选择哪些项目，选中的项目默认出现在最上方。

___

## **Data Refresher(数据刷新器)**

## ![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPdps8BZLtoJusqBlFlG4L38tJeHH4o3eoq4PwuibUFs4llTuuicSdhnfwmMVicib4t3S4RGbXF0tyBjA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在报表上添加这个控件，可以重复更新数据和其他视觉对象。当您在没有输入设备的电视屏幕上显示报告并且想要查看最新数据时，它特别有用。

它在报告中默认的效果是这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMOPxX0f8Qxh465ByIP1NdLK8AUiby9mziav428QrVtaNg5KPSkzWFDoKrIM28s8m9JicCdK0WYUC7mg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击左侧的按钮即可启动/暂停，在格式中可以配置刷新频率，最高可以设置每秒更新一次：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMOPxX0f8Qxh465ByIP1NdLwVmoK4dVYsAqVMfEe59I3Hxia5hiamTk0MlG862GvR7H6PSHVR3agm7A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

相对于数据刷新，我觉得它更适合做的是可视化报告上的数据轮播，添加需要轮播的维度字段放到这个控件的字段框中，就可以对该维度按照设置的频率轮播。

比如将产品类别列放到这个控件中，设置每秒播放一次，效果就是这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMOPxX0f8Qxh465ByIP1NdL17G5U97fYLHJpMI8vAaibBWxn3J98TxWWp8STDWesxITOI467iaEuPLQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

这样就可以实现循环重复展示每个产品类别的数据了，作用和[之前介绍](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484075525&idx=1&sn=3a9a9b94ef22b9e041570bfb3403a06a&chksm=8e0c56d2b97bdfc4defc0c193efd1d0dd90d5549901cb581dd254c7b451d9eaebbf269438909&scene=21#wechat_redirect)的Play Axis功能类似。

关于上面这3个控件的更多用法，你可以自行摸索。当然每个图表或者控件都有自己的局限性，不可能满足所有的需求，特别是自定义视觉对象，应用场景比较窄，不过多了解一些，在特定场景下多一个选择也没坏处。
