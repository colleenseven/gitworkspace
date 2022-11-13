---
create_date: 2021-11-04T12:57:08 (UTC +08:00)
tags: 
aliases: null
pagetitle: 通过一个案例，掌握Power BI可视化的制作技巧
source: https://mp.weixin.qq.com/s/PeKMmRhmDbCETvafRZYLXw
author: 采悟
status: 未阅读
category: 
notes: False
uid: 
---

前一段在知识星球中，星友Gavin提出了一个关于个性化的瀑布图制作问题，最近也被其他人问过类似的做法，我觉得挺典型，值得写篇文章介绍一下。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMdUTSzSDdAQ2lt6tyV6gQYDSoygdq5eEk6iajNsSJwo5rUkwALDzGz9PZ2rL7WXSPcXY2GzVjAVaQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

[瀑布图](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067368&idx=1&sn=99c421b2e7fd1e18e495612c5bfd15a2&chksm=8e0c76ffb97bffe9bb4af1fefc09c5afa7d6f49be14f8a2b2960b3ce2aaeb7edaf0a97b6571a&scene=21#wechat_redirect)我们并不陌生，它以悬空柱形图的方式，展示数据变动的过程，我之前曾介绍过，这里我就以个性化瀑布图的制作为例，来介绍PowerBI可视化设计的一般思路。

我先简单描述一下这个问题（数据为模拟）：

假如有两个表，每个业务员的指标数据和实际达成数据：

对这两个表，分别做瀑布图很简单，以下是指标和实际达成两张瀑布图：  

**现在的需求是，如何将这两个瀑布图整合为一个瀑布图，直观展现出每个业务员的指标达成情况，以及从总指标到实际达成的变化过程。**

如果你还不是很理解该需求，我这里直接把最终的效果放出来：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMdUTSzSDdAQ2lt6tyV6gQYSJIf3cngf0ibUQvnJ8W6cRgkYdTA4oN9s42ZHoaLibD1412PtC15cYYg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个瀑布图的效果看起来是不是清晰多了，每个人以及整体的指标达成情况一目了然。  

那么这种瀑布图是怎么做的呢？只需要下面几个简单的步骤。

**1、构造辅助表，建立模型**

使用PowerBI作图，首先一定要清楚，**位于上下文(坐标轴)的字段，必须来自模型中的某一个表。**但是现有模型中，只有上面两个表，其中没有任何一个字段既包含所有的业务员，也包含“总指标”、“总达成”，所以需要先构造出一个包含所有这些类别的辅助表。  

关于如何制作辅助表这里不再单独介绍（可参考：[Power BI 辅助表制作方式汇总](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071809&idx=1&sn=9e8f4916082c32cc0291a2e4e565f1fd&chksm=8e0c4756b97bce4087ec53dfb6e5380e7cb0662e73fa070f831e4283095505a5aced233e59c8&scene=21#wechat_redirect)），最终构造的表是这样的：  

然后将这个辅助表与上面两个表建立关系：

**2、新建度量值，计算每个类别的数据**

上一步建立的辅助表，是为了作为瀑布图的类别的，现在需要计算每个类别对应的数据，新建度量值如下：

```
指标完成数据 = 
```

这个度量值的逻辑，已经在DAX中做了注释。  

**3、制作瀑布图**

完成上面两个步骤以后，制作可视化就是很简单的事情了，不过这里我没有用内置的瀑布图，因为内置瀑布图，对总计的处理不够灵活，我选用的是一个十分好用的自定义图表：Simple Waterfall。  

将结构表中的类别，与度量值\[指标完成情况\]分别放到该图表的字段框中，  

并打开这个图表的格式面板，关掉“Define Pillars”中的累计总计，然后将"总达成"设置为总计，就能实现本文开头的瀑布图效果。  

通过以上3个步骤的设计，我们就可以突破现有表结构的限制，制作各种个性化的瀑布图，关键是根据需求构造数据结构、利用DAX实现自定义的类别计算，并熟练掌握瀑布图的各项格式设置。

其实也不仅仅是瀑布图，其他图表的制作步骤也都类似，简单的可视化需求可以直接拖拽现有模型中的字段来制作，**复杂的需求就需要构造数据结构并利用DAX来实现，只有掌握了这个思路，才能突破PowerBI默认可视化的限制，设计更丰富的可视化效果。**  

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和3900+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMqicSUp5EfHiae4ibtEjIZsDCy5RUEz1Yp2hsG1ExlG3XiaqfWPqspJ1oiaEcKjuJCKPStBaWQXO6SOew/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
