---
create_date: 2022-04-04T13:20:51 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI 实现局部走向预测 - 效果篇
source: https://mp.weixin.qq.com/s/6lCvh-X3zwxhvIE_Qy2TGw
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

在已经完成的根据拐点的模型中，有这样的图：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM9NWl1Xa4Ke3iafMYnrOWslsLsdaniczEbMh7GQVeZCeXvjv2BakD08Kw6iaDmxkZaG870DLDwWo9TQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

由于长尾数据的存在，对此进行趋势线，则得：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM9NWl1Xa4Ke3iafMYnrOWsls87Eths7Tz3bKolYPID6ltoW7XibwLuJA7WSbtgYMUzGyEttutm9ibrg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

很显然，这不是我们向看到的趋势线。

因此，经过研究，我们需要一种动态的局部区域趋势线。效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM9NWl1Xa4Ke3iafMYnrOWsl6dAGsbnibUQInWs9wib3GS7eic1BzbCSrCFuiaiauCxcKxzpLlfsjgKSWvw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

此种实现非常强大，具体表现为该模型由四个参数调控：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM9NWl1Xa4Ke3iafMYnrOWsldejTTDXq97zOicKSITRicADqBOrNuIC8zXALnrG4b2Y8cjXo2H62qj5w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

功能如下：

-   绿色实线，表示实际的数字，最后一个数字有终结点给出。
    
-   绿色虚线，表示全局趋势线，由全部日期范围选定下数据共同计算出该趋势线。
    
-   蓝色虚线，表示局部趋势线，由局部趋势范围选定下数据部分计算出该趋势线。
    
-   蓝色区域，表示局部趋势可能的上下幅度。
    
-   红色端点，表示拐点，且通过参数判断只有当拐点的幅度大于一定程度时才标记出来。
    

这个模型具有非常广泛的通用性。

以目前的疫情数据为例，由于疫情管理措施的实时进行，那么全局数字对看局部效应就显得没有意义了。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM9NWl1Xa4Ke3iafMYnrOWslmHicrpYf0kOtBgu4jPhHdFKlrSAxuELFpTZkQM0WPjbnZB7iaPNYS8gg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

并基于此，给出高级的调节工具，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM9NWl1Xa4Ke3iafMYnrOWsliaq7Wib2kPUnvYiccIu0GRibZPITeXwW2OO8wericsMv2M8XSvQ8A8iaOYVQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果你想自己体验以下，可以试试看。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM9NWl1Xa4Ke3iafMYnrOWslHszLZ1ibUlSnp0PHo6SmMsFQUfDqGs2U631M0YMYtq5iccwTCobMlvkg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

至此，我们进一步来守候这个拐点。

在订阅了BI佐罗讲授的《BI真经》之《BI进行时》课程区，4月会加入本套内容的更新讲解。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNhia5Pc4XC1Um7IYgQhGEoEC1yK05ibUFoPBYpcoAMvibuZh2BZaibMzULeDwNfSeQ0KHRcDUdX3FzVA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**Power BI 终极系列课程《BI真经》**

[

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/09hv4Xua0LNBM1lxlQYHJBicic4CvPoRGLqHgdTZOr8goNRh0asDXA48mRDzc9zxW4UMQiayHwgDmx7mlt4cQxtjg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

BI真经 - 让数据真正成为你的力量





](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650788512&idx=1&sn=76972ff4b0cf265fe9479c6457b04b47&chksm=f18cd2b1c6fb5ba7386eb0bb835280bd8a651bfe0481cc78f20fc30b80c60d2d4cb7eb5b1e3e&scene=21#wechat_redirect)

扫码与精英一起讨论 Power BI，验证码：data2022

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOiad5BOrdQTKpB733esKiaxZa53LXWIPlQicMjxntaRr3a2hnMmuibTib8QacXeiakucDr7lSNGkuV2MXw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击“阅读原文”进入学习中心

**↙**
