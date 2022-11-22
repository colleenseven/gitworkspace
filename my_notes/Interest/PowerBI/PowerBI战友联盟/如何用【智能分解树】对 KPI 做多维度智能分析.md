---
create_date: 2022-05-13T13:16:00 (UTC +08:00)
tags: 
aliases: null
pagetitle: 如何用【智能分解树】对 KPI 做多维度智能分析
source: https://mp.weixin.qq.com/s/pTIBXThm-gm7KuyUnCbImg
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LN6PIKFT6n0awfPeLfKPmY39lVRk6dvP4T90iaPjawb7JOY27gEFjjdjWZgudXN1cXhrRToy8L0YFg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

很多小伙伴问：Power BI 不是有 AI 功能吗？比如分解树，可以没发现如何 AI 的啊。

Power BI 中集合一些 AI 功能，本文来讲其中重要特性：人工智能分解树。

## 效果展示

先来看看展示效果，如下：

盖图表明：

某 KPI 依次在多个维度逐层进行分解。其中重要考虑：

-   到底按怎样的维度顺序来分解？
    
-   如何显示某个维度对分解的绝对值和贡献度？
    
-   如何对分解着的维度元素呈现不同颜色？
    

如何可以分别解决以上问题，尤其是问题 1，则可以实现：智能分解。

## 解决方案

在 Power BI 中使用 AI 分解树，可以有两种模式：

-   静态分解
    
-   智能分解
    

其中，

静态分解，意思是按照既定意图依次对各个维度进行分解。

智能分解，意思是先通过 AI 特性判定分解顺序，再进行分解。

可以在 分解树 中进行智能探索，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LN6PIKFT6n0awfPeLfKPmY3ZIibKKufskF6KBkAQmSXdqqm9KqWhMiauqwicsByC63T0uBhKt7QU1M1g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

方法如下：

-   先选择一个度量值。
    
-   再选择要考虑的维度，如：
    

-   销售经理
    
-   产品类别
    
-   客户类型
    
-   客户行业
    

构成分解树如下：

形成结果如下：

已经完成分解。

问题来了，如何设置颜色呢？

可以对分解树通过度量值设置颜色，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LN6PIKFT6n0awfPeLfKPmY3S34QT89CtEWSuKqO4icOnaibicsr4WvmC2boe0QzN3kdibzrXAhceAcfvA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

于是颜色有了，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LN6PIKFT6n0awfPeLfKPmY3XVUI4CWMFKIp4ibib0oqaOZBcEbjHMNCicwJUB0QZz2QgzMdxt5ZxrYPQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

虽然一切都很好，但是还有一点，是否可以显示贡献度占比呢？

可以用计算组实现，在以前的文章中写过，这里不再重复，如下：

这样就实现了完美的分解树了。

## 总结

Power BI 提供了各种 AI 特性，，其中分解树，是一个非常重要的特性，在很多应用场景中，都有极大价值。

没有看懂？那快来预约直播吧

![](https://wx.qlogo.cn/finderhead/Q3auHgzwzM4Rz9mYvEFH2tuPTpv0svaghGlMxxNNbNjkwBJCRr1RFw/0)

**PowerBIMBA**

，

05月13日 20:00 直播

Power BI 智能分解树

视频号

在订阅了BI佐罗讲授的《BI真经》之《BI进行时》课程区，除了可以下载本文案例，还可以观看视频讲解。

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
