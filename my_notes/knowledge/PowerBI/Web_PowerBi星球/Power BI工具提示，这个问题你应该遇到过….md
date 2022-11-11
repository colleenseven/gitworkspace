---
aliases: null
create_date: 2022-05-13T11:50:51 (UTC +08:00)
tags: 
pagetitle: Power BI工具提示，这个问题你应该遇到过…
source: https://mp.weixin.qq.com/s/n15CbZSY4dm0YDrGOATgrQ
author: 采悟
status: 未阅读
category: 
uid: 
---

本文来介绍一下在设计PowerBI报告的工具提示时，很多人可能都会遇到的一个问题。  

假如在报告中用柱形图展示了每个产品的某个月的数据，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPhdQBuaAxd442awqwibiaBIQPFN3Y1QF3uEqic14dutqXKdUPb2vGlz4OkQJlhouLCMoj7EpibToxINw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果想用工具提示的方式，来进一步展示产品的销售增长趋势，让展示鼠标悬停在某产品时，自动弹出该产品每月的变动趋势。

这种需求可以制作一个工具提示页，在这个页面上，将年度月份放到X轴，产品收入作为值，制作一个面积图，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPhdQBuaAxd442awqwibiaBIQpt9PjwsmMs9O9AvJBa77jiaeexMkXLBO4su2JSHicAkqJ4Dhu71CEd0A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后设置该页作为上面图形图的工具提示。

___

工具提示具体的设计步骤请参考：[深入了解PowerBI的工具提示功能](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067562&idx=1&sn=c3472d97c251abf52f38e2f7e31b23a6&chksm=8e0c763db97bff2bf8d514625a3fd037d274ea3014624766b7aa2822bc63a6e2c96006223ba7&scene=21#wechat_redirect)

___

不过这样做的结果很可能是这样显示的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPhdQBuaAxd442awqwibiaBIQppUwQH7YmVKjR2VYbicYKetKYycb0Gjrv0Pn3HBBRujGxrS4pTvW7Xg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

并没有弹出期望的该产品的趋势图，而只有一个点，为什么会是这种情况呢？  

这是因为柱形图的上下文是产品和年月，会自动筛选工具提示页的图表，面积图被筛选为只显示当月的数据，所以只显示一个数据点。

为了解决这个问题，你直接想到的可能是编辑交互，但是工具提示不在同一个页面上，无法通过编辑交互的方式来设置，那么如何让年月切片器上下文，不影响工具提示的图表呢？

可以利用DAX来实现这种需求，基本思路是建立一个独立的日期表来做工具提示页的趋势图，这样报告页的年月上下文就无法影响到它了。

具体步骤如下：

**1、建立独立日期表**

在数据视图下，点击新建表，输入：

独立日期表 = '日期表'

就建立了一个与模型中原日期表完全一样的日期表，相当于复制一个日期表。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPhdQBuaAxd442awqwibiaBIQLdKkoNoWHdteIZxgaNhbGbcmFvnx8ibXSt8HyvK5yZL6AbWAeicptmRg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个表不要与模型中的其他表建立关系。

**2、建立度量值**

因为独立日期表与模型没有建立关系，为了让它能够正常筛选订单表，并制作趋势图，需要写个度量值如下：

___

收入 工具提示 =

CALCULATE(

    \[收入\],

    TREATAS( VALUES('独立日期表'\[日期\]) , '日期表'\[日期\] )

)

___

该度量值的逻辑是利用TREATAS函数将独立日期表的日期列视同建立关系的日期表日期列，利用这个度量值，独立日期表即使没有建立关系，也能正常计算出某个时间的数据。

**3、制作趋势图**

在工具提示页中，用独立日期表的年月字段和上面建的度量值制作趋势图，然后将它设置为柱形图的工具提示，效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPhdQBuaAxd442awqwibiaBIQkMBIlN28vTdqVtDz9HCWCSgUwR5cib3mBA9I7JFN0xSdvXoV8FejgUQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

这样就实现了利用工具提示来展示趋势的需求。

在制作工具提示时，当出现类似的问题时，都可以运用这个思路，结合DAX来忽略图表上下文对工具提示的影响。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4500+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1AEySOiakLF2kY7eb1kUw2DtfKoVz2ctBDia5dtNsPX2GhV0ZOCDDWpgpaTQtnqfqJrRXt5PNia95g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
