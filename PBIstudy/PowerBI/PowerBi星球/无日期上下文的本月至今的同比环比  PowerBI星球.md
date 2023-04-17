---
create_date: 2021-03-24T20:13:26 (UTC +08:00)
tags:
aliases:
pagetitle: 无日期上下文的本月至今的同比环比 | PowerBI星球
source: https://mp.weixin.qq.com/s/oqkm-fGfR9Y5Lw23VHYPCw
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

[前面的文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074772&idx=1&sn=f13557e739a5b0304696c1b9213c09c2&chksm=8e0c53c3b97bdad5d606da03d4723cbdb822d3a5faa7d6b2b0d4fa4e8268bad5fe2d58ddfac8&scene=21#wechat_redirect)曾介绍了无日期上下文的同比环比，不过数据是整月的累计，如果想计算本月至今的数据，以及相对应的上月、去年同期对比，应该怎么做呢？

其逻辑依然是不利用外部上下文，仅利用今天的日期TODAY，构造一个从本月1号到今天的日期列表，然后再执行汇总计算，度量值可以这样写：

> 收入 MTD =
> 
> CALCULATE(
> 
>     \[收入\],
> 
>     FILTER(
> 
>         ALL('日期表'),
> 
>         '日期表'\[日期\]>=EOMONTH(TODAY(),-1)+1
> 
>         &&'日期表'\[日期\]<=TODAY()
> 
>     )
> 
> )

这里用到了EOMONTH函数，它的用法如下：

> EOMONTH是一个日期函数，返回移动指定月份后的当月的最后一天日期，比如EOMONTH("2021-3-15",-1)将返回2021年2月的最后一天日期:2021-2-28。

EOMONTH可以返回移动后的月份的最后一天的日期，所以通过这个函数构造出EOMONTH(TODAY(),-1)+1，将返回本月第一天的日期，利用这个逻辑，顺利计算出本月至今的数据。

同样的方式，计算上个月的本月至今，可以这样写：

> 收入 MTD PM =
> 
> CALCULATE(
> 
>     \[收入\],
> 
>     FILTER(
> 
>         ALL('日期表'),
> 
>         '日期表'\[日期\]>=EOMONTH(TODAY(),-2)+1
> 
>         &&'日期表'\[日期\]<=EDATE(TODAY(),-1)
> 
>     )
> 
> )

EOMONTH(TODAY(),-2)+1返回上个月的第一天，然后上个月的今日，利用了另外一个日期函数EDATE，EDATE(TODAY(),-1)返回上月的今日。

  
EDATE的用法如下：

> EDATE也是一个日期函数，返回移动指定月份后的对应日期，比如EDATE("2021-3-15",1)将返回"2021-4-15",如果移动后的日期在对应的月份中不存在，晚于当月最后一天，则自动返回该月的最后一天，比如EDATE("2021-3-30",-1)，2月是没有30号的，则自动返回为最后一天2021-2-28。

这里用到了两个常用的日期函数，它们功能非常容易理解，只和提供的参数有关，和其他上下文没有关系，也不需要日期表，比时间智能函数的逻辑简单多了，在某些场景下很好用。

当然TODAY本身也是个日期函数。  

同理，可以很容易的计算出本月至今的上年同期数据：

> 收入 MTD PY =
> 
> CALCULATE(
> 
>     \[收入\],
> 
>     FILTER(
> 
>         ALL('日期表'),
> 
>         '日期表'\[日期\]>=EOMONTH(TODAY(),-13)+1
> 
>         &&'日期表'\[日期\]<=EDATE(TODAY(),-12)
> 
>     )
> 
> )

用矩阵显示如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNjvL42eEMiaH0rib46gLqjtUFIdBib8ygPPxCLmyEUoVfkBaiaRQOZ7TlictibM8gNbmhnTylnVwl11NFw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

计算上月同期数据时候，还有个小问题是，如果本月的天数比上个月少，比如2021年2月份，2月28号是最后一天，本月至今就是2月整月累计的数据，但上期是1月1号到28号的数据，如果想让1月也显示出整月的累计数，可以加个判断逻辑，这样来写本月至今的上月的度量值：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNjvL42eEMiaH0rib46gLqjtUrKfOHAYuiakibxBLuACDhgvRwP5fcQzodWw5YPpdcvjIma8XWsQVHIvg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

上面利用了日期函数，很方便了计算出了本月至今和环比、同比的数据，那么能不能利用时间智能函数来完成这些运算呢，也是可以的。

下面看看利用时间智能函数的写法：

> 收入 MTD1 =
> 
> CALCULATE(
> 
>     \[收入\],
> 
>     DATESMTD(
> 
>         TREATAS({TODAY()},'日期表'\[日期\]))
> 
> )

因为没有外部日期上下文，这里利用了TREATAS将TODAY视同为日期表里的日期，作为DATESMTD的上下文，这样就会返回从月初至今的日期列表，然后执行汇总计算。

TREATAS的第一个参数必须是个表，而日期函数返回一个值，所以在外面套个大括号{ }，就可以将值变成表。

同理本月至今的上月以及上年同期，时间智能函数的写法是这样的：

> 收入 MTD PM1 =
> 
> CALCULATE(
> 
>     \[收入\],
> 
>     DATESMTD(
> 
>         TREATAS({EDATE(TODAY(),-1)},'日期表'\[日期\]))
> 
> )
> 
> 收入 MTD PY1 \=
> 
> CALCULATE(
> 
>     \[收入\],
> 
>     DATESMTD(
> 
>         TREATAS({EDATE(TODAY(),-12)},'日期表'\[日期\]))
> 
> )

其结果和前面的写法完全一样：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNjvL42eEMiaH0rib46gLqjtU3ITtYqmzic8LB76doiafQXTlPUYibBcibJh8tTClqO3z0PQSXcyRoViapow/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里就灵活运用了日期函数和时间智能函数，实现了无外部上下文的各种计算。

本文用到的这几个度量值，值得你去细细理解了其中的逻辑，将加深你对日期函数和时间智能函数的理解，掌握这个思路以后，以后碰到类似的分析时都可以利用这类函数轻松计算。

___

[我的新书已上市](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)，帮你从0到1，轻松上手PowerBI

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOoBOqb2ddx32yTWcia8shjuj6zhsEQA5tc6ze1tv7E6QVprfOjKC9CIRrfibRFrX1AXNSibiajcl398g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

  

感兴趣的同学可以扫描下方二维码在京东购买：

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

喜欢当当购物的朋友也可以点击链接直接下单：  
  

\-精彩推荐-

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072351&idx=1&sn=fabb08c54790ac1225b470fd647c7a5e&chksm=8e0c4548b97bcc5e0450f1945a2c76039bbb42650bcb1edbc856820836d63d32af4c7780e31a&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 3k+ 学习者一起成长
