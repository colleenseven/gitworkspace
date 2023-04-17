---
create_date: 2021-07-10T19:43:04 (UTC +08:00)
tags:
aliases:
pagetitle: 分享一个更实用的Power BI日期表
source: https://mp.weixin.qq.com/s/4AD_AGKWs1-d6J17Ftwm3A
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

日期作为最常用的分析维度，几乎每个数据模型中都需要有个日期表，之前分享了几种日期表的制作方法：[日期表制作方式汇总](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067654&idx=1&sn=905c186a9cbd91159b6615924a2d5068&chksm=8e0c7791b97bfe87623904f7002cd6cb726f711c6e7a289a36c9a4973964d907493aa2397fe7&scene=21#wechat_redirect)。

那篇文章主要是介绍如何制作日期表，其中的日期表示例相对简单，和日期相关的维度也不够齐全，根据平时分析的需要，以及星友的反馈，这里再分享一个维度更多也更实用的日期表。  

本文不再分别用几种方式来制作，免得你纠结选择哪种方式，直接用DAX来建一个日期表，在PowerBI Desktop中，点击“新建表”，输入以下DAX公式：

```
日期表 = 
```

就可以得到一张下面的日期表：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOIhfia2tSgX1q9SubbFhMjZpicpNJdbc9ongUBUqLtUEmjdy3ldexgPVogoJ0aL0PNTVS6cHdGQqrw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

当你需要建日期表时，可以直接复制上面的DAX公式制作自己的日期表。

这个日期表有以下几个特点：

**1\. 可方便的修改日期参数**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJODdm2lYZ2vEJLBLuiatwpGcowvwuCybyuuQ3w21ibDv2L8nHNbpibuEtibcUJbRourKcjYVBN4GTr8Cg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

主要是根据需要修改日期表的起止年度，以及和周相关的参数，一般我们的使用习惯是从周一开始，正常情况下不需要修改周的参数。

**2\. 便于对月份等文本字段排序**

日期表中对月份、季度都添加有数字列，可以更方便的进行按列排序，比如对中文的月份字段进行按列排序：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJOIhfia2tSgX1q9SubbFhMjZEVgEWvTKQewN6pesNdr7nia40kGcdRsHKwnicjI7libTkg5vtKIJKAo2A/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

**3\. 添加有年月序号和年季序号字段**

在之前的文章中，曾使用过年度月份序号(比如：[无日期上下文如何计算同比环比？其实很简单](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074772&idx=1&sn=f13557e739a5b0304696c1b9213c09c2&chksm=8e0c53c3b97bdad5d606da03d4723cbdb822d3a5faa7d6b2b0d4fa4e8268bad5fe2d58ddfac8&scene=21#wechat_redirect))，在不适合使用时间智能函数的分析场合，利用这个连续的序号分析十分方便。

**4\. 提供了中英文的月份和星期字段、以及周相关的字段，满足更多的场景需求。**

制作一个顺手的日期表十分重要，根据分析的需要扩展日期表中的相关维度，可以更清晰快捷、以及用更简洁的DAX公式来实现日期相关的分析需求。

这个日期表中的维度不算是最齐全的，但非常实用，足够日常的分析场景使用。如果你还有更个性化的需求，可以在这个日期表的基础上添加相关的列。

___

**[新书上市：PowerBI商业数据分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)**

帮你从0到1，轻松上手PowerBI

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOojexubCy39PJZJic24XlI9IC8Fhx57SVYiciave3T7sAxeLXXZgrAzhAsUHXC3dxpU1fp72ChD8ibfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072351&idx=1&sn=fabb08c54790ac1225b470fd647c7a5e&chksm=8e0c4548b97bcc5e0450f1945a2c76039bbb42650bcb1edbc856820836d63d32af4c7780e31a&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 3k+ 学习者一起成长
