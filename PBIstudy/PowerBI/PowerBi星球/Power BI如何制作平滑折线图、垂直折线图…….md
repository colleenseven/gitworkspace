---
create_date: 2022-12-25T23:47:06 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI如何制作平滑折线图、垂直折线图……
source: https://mp.weixin.qq.com/s/cV_qLEYqS4-fLCluqjqe5Q
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

Power BI可视化很丰富，但也有很多不够灵活的地方，比如内置的折线图，被吐槽最多的痛点是无法通过简单的设置来实现平滑效果，到现在依然没有改观。

本月新增了很多自定义可视化对象，其中有一个可以实现平滑折线图的效果，它就是Advanced Line Chart。

这个图表称为高级折线图，可以进行很多细节上的调整，其中一个非常好用的功能是可设置折线效果为平滑，比如用它制作折线图，正常是这样的：

在格式中设置Line shape为“Smooth”：

然后折线图就变成了平滑的效果。  

这样的折线图看起来舒服多了。

**需要说明的是，这个可视化对象在Power BI Desktop中可以免费使用****(右上角的图标，如果觉得碍眼，可以放个文本框遮挡)****，但是发布报告在线分享时需要付费购买License，请斟情使用（下面提到的图表同样如此）。**  

这个视觉对象是PBIVizEdit发布的，除了平滑折线图，本月他们还发布了其他一些视觉对象也很有趣，下面列举几个。

**垂直折线图**

通过视觉对象Multiple Vertical Line Chart可实现。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNYXHL1D3vNhqXsmnr224axM0tOS436bqicBic0oYySGBnNGRKhdqK6FxEEBVvd1KFtIuWAkOWwD1tg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNYXHL1D3vNhqXsmnr224axygakibia0HCJPVwJqshkw4PgY32qNjIXPnf5hfLUsCVvT5LWKZQNrUTw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**垂直组合图**

通过视觉对象Dual X-Axis Combo Chart来实现。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNYXHL1D3vNhqXsmnr224axRxORicaAhfSicR6hdQibVgAibRSSLJX7Gzr2Kej5X00Gs8RaEibhf8CLbLg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

效果如下：

**百分比堆积和簇状柱形图**

通过视觉对象100% Clustered Stacked Column Chart可实现。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNYXHL1D3vNhqXsmnr224axo2M4pErhkWqBfsFRlUVR1DqibrclAwK2hrsich3Dibgamw5y3dCHkyRsA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNYXHL1D3vNhqXsmnr224axaIqiawMlQfv0HUPzibJMLRWiaYLHTjo0B9CWcfmf8zrwTEaia495fEHZxg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**重叠柱形图**

通过视觉对象Overlapping Column实现。

效果如下：

看到上面的这些效果是不是耳目一新，这些都是靠内置的图表无法做到的，当然这些图表的设置非常丰富，效果并不止于此，更多的细节你可以去深入探索一下。

并且PBIVizEdit发布的视觉对象非常丰富，你可以在Appsource中搜索找到它制作的更多图表：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNYXHL1D3vNhqXsmnr224axaLiaicCex3KmFqhvicFTtLLD3NG6I2prFAUk4Pch6jSwtCicxOU1RrvlfA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

当你有类似的需求时，可以尝试使用上述图表，PBIVizEdit其实也是一个开发PowerBI自定义视觉对象的工具，上面的这些视觉对象就是用该工具制作的，如果你有开发个性化图表的需求，可访问pbivizedit.com详细了解。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你想深入学习Power BI，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和5000+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMstwXX5zrKianmFXzyqbIVgh7byfo3V8JJPmhqicywbtYkM0j2ibngnT5XBZ2AwKvGZiby9ngoKfLvzg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门Power BI》电子书，轻松入门。
