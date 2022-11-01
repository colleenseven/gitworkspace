---
create_date: 2022-08-05T12:25:23 (UTC +08:00)
tags: 
pagetitle: Power BI业务分析：如何统计未完成的订单？
source: https://mp.weixin.qq.com/s/OG_X3u5aZsJG6_bX3okE4Q
author: 采悟
status: 未阅读
category: 
uid: 
---

对于有两列日期（订单日期和发货日期）的订单表，之前介绍过如何利用虚线关系和USERELATIONSHIP函数实现不同日期类型的销售额计算，参考：

[认识Power BI中的非活动关系](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071870&idx=1&sn=f110592b92b23dd7d7515c4cc342c101&chksm=8e0c4769b97bce7f97489d4f34ca603a0e12af4c5acd90101205c670709ecf07f3ee95830a1d&scene=21#wechat_redirect)  

还有一种需求经常被问到，**对于有订单日期和发货日期的订单表，如果发货后表示该笔订单完成，那么如何统计出尙未完成的订单呢？**

本文以统计当日未完成订单数量以及累计未完成订单数量来介绍这个问题。

首先，日期表与订单表同样只能有一列建立活动关系，这里还是只用订单表的订单日期与日期表建立关系，发货日期不建立关系。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMszibhYafHKeqouuiaDexgU2PsWEuTAYia4RcgSiakEUlBr7s16nvBwB4iaXtz7FkVvMnU4235icpIJfPA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后写一个度量值来计算每日的未发货订单数量：  

其中订单数是个基础度量值：  

> 订单量 \= COUNTROWS('订单表')

上图的度量值如果只看这个DAX本身，可能难以理解，只有结合外部上下文才更好理解它的含义。

在外部日期表上下文的筛选环境下，日期表的日期按订单日期筛选订单表，也就是查找出当日产生的订单，FILTER在当日订单的发货日期中，筛选发货日期晚于当前日期或者发货日期为空的订单，然后计算满足条件的订单数量，就得到了当日的未发货订单数量。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMszibhYafHKeqouuiaDexgU2fO6Anw6JZ06CZ93ao7FSo35xkuHjma0vopJ6QXaGiaDR20EY9XLd5pg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个度量值是在外部上下文的关系筛选，与DAX内部的筛选逻辑共同作用，来实现分析需求的。  

如果要进一步计算出截至当天累计的未发货订单，度量值可以这样来写：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMszibhYafHKeqouuiaDexgU25v4kbhNpiagWQDWgNf6V9nBsOM8hGicwoIcHYFMbFNHxA1N8Biatia1ibtQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

(点击查看大图)  

因为要计算累计未发货的订单，不是当日的，不能让关系自动筛选当前日期的订单，所以这里用了两个FILTER条件。

-   第一个FILTER条件，用ALL忽略当前上下文对日期表的筛选，在所有的日期中查找，小于等于当前日期的所有日期，满足条件的日期按订单日期来筛选订单表，就是订单日期小于等于当前日期的所有订单集合；
    
-   第二个FILTER条件，也是用ALL忽略当前上下文对订单表的筛选，从所有订单的发货日期中查找，发货日期大于当前日期或者发货日期为空的所有订单集合；
    

对两个FILTER条件筛选出的集合取交集，得到截至当前日期，所有未发货的订单，对这些订单计数，就得到了累计未发货订单数量。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMszibhYafHKeqouuiaDexgU2UojaBKTRFuHHBPJOGoax5MfU0uxWk3Izh3EnMG0gv6E99y17KJnyjw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

上面写法是统计未完成的订单数量，如果需要统计未完成的订单金额，同样是上面的思路，只需要把CALCULATE的第一个参数改成对销售额求和就可以了。

本文的这个分析需求不难实现，不过通过这个简单的例子，仔细理解这两个度量值的写法，可以帮助我们理解外部上下文、内部DAX条件的筛选逻辑，以及二者的共同作用，最终按业务逻辑完成计算实现了分析目的。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4500+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1AEySOiakLF2kY7eb1kUw2DtfKoVz2ctBDia5dtNsPX2GhV0ZOCDDWpgpaTQtnqfqJrRXt5PNia95g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门Power BI》电子书，轻松入门。
