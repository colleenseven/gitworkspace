---
create_date: 2022-09-26T11:35:40 (UTC +08:00)
tags: 
aliases: null
pagetitle: PowerBI 抖动图，快速标记众多数值的分布
source: https://mp.weixin.qq.com/s/kCQUNVZccys7IQCWR1KFQw
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

对于一堆元素，如：员工和其年龄，SKU 和销售额等，任何符合只需要研究一个指标的情况。

但立刻就会遭遇这样的效果，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LP9iaKhPjBde2DGPEiaO6nhFe3JaagolT6jrUKQfibZIrDxA2HWCX1aMnqPokrT7S0MnAktyQRAXIbmw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其问题在于：

-   由于元素过多，会造成彼此遮盖，不知道分布的紧密程度。
    
-   由于元素过多，会造成彼此遮盖，也无法知道在稀松处的元素。
    

进行优化后，可以得到：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/09hv4Xua0LP9iaKhPjBde2DGPEiaO6nhFeOA9wyWeSV7qqHHvDWQI5gIHzDMAuUibosJoPX31XYgLwnVdib7pCfXyA/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

该问题很巧妙地得以化解。

其方法是：

在水平方向给每个点一个随机的 X 值，来拉开距离即可。这里通过一个滑竿来控制拉开的幅度。

具体的 DAX 公式如下：

```
Point.X = VAR xX = [X.Value] // 抖动幅度VAR xMin = MINX( ALL( Point ) , [Point.Y] )VAR xMax = MAXX( ALL( Point ) , [Point.Y] )VAR xDistance = xMax - xMinVAR xNumber = COUNTROWS( ALL( Point ) )VAR xPosition = RANDBETWEEN( 0 , xDistance ) / xDistance * 100 - 50 // 归一化RETURN     xX / 100 * xPosition // 按照抖动幅度偏移
```

这个公式非常简单，大家可以自己试试咯。

## 总结

很多可视化，结合创意和 DAX 以及 Power BI 的基本图表可以做出很多定制化的效果。所以，创意很重要哦。

在订阅了BI佐罗讲授的《BI真经》之《BI进行时》课程区，除了可以下载本文案例。

**Power BI 终极系列课程《BI真经》**

[

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/09hv4Xua0LNBM1lxlQYHJBicic4CvPoRGLqHgdTZOr8goNRh0asDXA48mRDzc9zxW4UMQiayHwgDmx7mlt4cQxtjg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

BI真经 - 让数据真正成为你的力量





](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650788512&idx=1&sn=76972ff4b0cf265fe9479c6457b04b47&chksm=f18cd2b1c6fb5ba7386eb0bb835280bd8a651bfe0481cc78f20fc30b80c60d2d4cb7eb5b1e3e&scene=21#wechat_redirect)

扫码与精英一起讨论 Power BI，验证码：data2022

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOiad5BOrdQTKpB733esKiaxZa53LXWIPlQicMjxntaRr3a2hnMmuibTib8QacXeiakucDr7lSNGkuV2MXw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击“阅读原文”进入学习中心

**↙**
