---
create_date: 2022-11-18T11:28:19 (UTC +08:00)
tags: 
aliases: null
pagetitle: 四象限分析的 DAX 实现及高阶思维模式
source: https://mp.weixin.qq.com/s/ttkoTL9vgCAn9Ld5B1uqqg
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

## ![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMAjDwBTzXmuvpgoTPDeWwBsvDw2T2zGaJ8mVoDR1yHohBdnP6K41ibeYJsXvC79KHMBGkL4NCCibzA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

## 场景描述

在 Toboyoo 分析看板中，有一个专门的模块，通过 80/20 原理，建立起 “四象限分析” 模型。该模型从【组合象限】、【80/20 数字】和【年度变化】3 个主要子页面进行分析展示。如下所示：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOQlMBsOnLsSKbbUb2wUjtyZXmYegIz7K1m12uOAqCopDW9HqQ08ftkicocNqm264SdNKQL5EXbj8w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其中，最为基础的是：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOQlMBsOnLsSKbbUb2wUjtyU9PZGPemIn25HZpStibGeLricuIZ6Khpb9UJ6OjEVkKR3sIJKkXibesEw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里的 80s 和 20s 是一种标签，反映了从大到小排列后，累计贡献达到 80% 的群体和其他 20% 的群体。这里的 80% 和 20% 并不是群体个数占总群体个数的比例，而是上述所说的标签。因此，这里是不符合 20% 的东西创造 80% 的贡献的。

## 问题

现在的问题是，如何找出 80s 和 20s 的群体呢？如何通过 DAX 构建计算？当数据量很大的时候怎么处理呢？如何优化呢？

## 基础计算

通过逐次加列的方式建立这个结构，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOQlMBsOnLsSKbbUb2wUjtyEcYvy2CcXc0m0ibnQxeYHXStW8EhkAWLo6KYXfpbsN9ofjy6xTKnHfg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其中，店铺和利润很容易理解。

接着，构建一个排名，如下：

```
test2-rank = rankx(all('DIM-Stores'[StoreKey]),[Gross Profit])
```

使用 `RANKX` 函数完成这一任务。（对 RANKX 不清楚，可以参考：RANKX。）

接着，构建积累价值计算，如下：

```
test3-accumulated value = sumx(    topn([test2-rank],all('DIM-Stores'[StoreKey]),[Gross Profit]),    [Gross Profit])
```

这里的积累计算给出了一种与帕累托传统计算方法的另外模式。其中用到了 `TOPN` 函数和 `SUMX` 函数来实现累计。

接着，计算总数和帕累托积累占比，如下：

```
test1-ttl = CALCULATE([Gross Profit],all('DIM-Stores'[StoreKey]))test4-pareto% = divide([test3-accumulated value],[test1-ttl])
```

这样就得到了整个表。

也就实现了打标签。

## 预计算与静态化

DAX 引擎由于其动态计算能力，这是工业界的顶级自助 BI 引擎。其动态性体现在：需求不需要事先告知实现人员。例如在 RFM 分析中，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOQlMBsOnLsSKbbUb2wUjtyThLhp0PuiczjEjz171d19WLKciapkLl81l8VnFGs2vicn5s7KyKVrpOhg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其中，R，F，M 可以不预先给定，而是根据界面的选择，动态给定。这时候，对客户群体的打标签，就是动态打标签。这种能力在传统的 BI 工具中是不具备的，也是 DAX 的强大所在。

但由于一切都会拖延到运行时决定，导致实时计算会消耗大量时间。

因此，在实际中会考虑一种平衡的方案。同时满足设计模式思想的 OCP 原则，即：对修改封闭，对扩展开放。

在本案例中，作者将每年的 80s 和 20s 分别打标后导出到 Excel 再拼合起来。

再将拼合的数据与订单数据再在 PQ 中再拼合，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOQlMBsOnLsSKbbUb2wUjty2MpVy8EBUiciaKyJKFBSlRZibLq0wZiaravBagM1GKCOBLa8WVf8MsCVfw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样，整套数据内容就静态化了。这样对实时计算时候的性能会大幅度提升。

## 设计思想

第一步：对已有数据通过 DAX 计算进行打标签。利用了 DAX 的便利性。

第二步：导出数据静态化与现有数据拼接。实现了静态化和预计算，有利于大幅度性能改进。

第三步：注意静态化时候的平衡选择。

整套流程下来，不仅仅利用了 DAX 的计算能力，还继续使用手工方法复制粘贴，再利用 Power Query 做数据拼接，同时蕴含了预计算以及平衡的设计思维。

## 总结

当小伙伴们拿到作品案例的时候，很多人只是因为作者在 Power BI 外部计算了店铺和产品的标签，而根本不知道这里有这样的深层次考量，这就是普通用户和资深用户之间思维模式带来的差异。请大家注意，这里的技巧根本不是技巧，而是一种思维模式，这种思维模式的精华在于：优势整合。

没有完美的，只有有优势的，厉害的人绝不会抱怨什么东西不完美，因为他们深知你无法改变你无法改变的东西，他们反而会通过智慧去找到平衡，利用不同部分的优势去平衡构建。这里有一部分工作是通过手工复制粘贴完成的。这甚至告诉我们，不管工具多么先进和自动化，复制粘贴这个最初等的动作一样是要用的。

这里表面是在说四象限分析，实际在说的是一种思想模式；这是表面在讲 Power BI，实际在讲的是可以用于任何领域的通用思维模式。如果你还在学习某个函数，那么，还是在一维空间。这里是抽象的四维空间了，因此有点难度，需要反复体会。

**作品欣赏**

该作品案例可直接参考：

excel120.com/go/case/toboyoo

建议在PC端欣赏整个案例  

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMAjDwBTzXmuvpgoTPDeWwB2JLtcFgEvRZhqdcHtmgQvv54NicToA86zTdoD9ouruTsdBTbKEQIlPg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)  
另外还可以在  
最强大的 Power BI 案例体验学习中心  
体验众多案例  
获得设计灵感

![图片](https://mmbiz.qpic.cn/mmbiz_gif/MfTd6rd9CyvNRMW8I9cvI1CK5gKiaYqg2veTn9t9dAe1GxYic7pAvgvRIKNFickConFyX8AvW2reAq8GchJI6aBpA/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

**excel120.com/pro**  
（从免费到企业级顶级专家PowerBI智库）

**直播预约**

预约下一次不容错过的直播分享  
主题：关键因素分析

![](https://wx.qlogo.cn/finderhead/Q3auHgzwzM4Rz9mYvEFH2tuPTpv0svaghGlMxxNNbNjkwBJCRr1RFw/0)

**PowerBIMBA**

，

将在11月22日 20:00 直播

关键因素分析

视频号

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNhia5Pc4XC1Um7IYgQhGEoEC1yK05ibUFoPBYpcoAMvibuZh2BZaibMzULeDwNfSeQ0KHRcDUdX3FzVA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**Power BI 终极系列课程《BI真经》**

[

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/09hv4Xua0LNBM1lxlQYHJBicic4CvPoRGLqHgdTZOr8goNRh0asDXA48mRDzc9zxW4UMQiayHwgDmx7mlt4cQxtjg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

BI真经 - 让数据真正成为你的力量





](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650788512&idx=1&sn=76972ff4b0cf265fe9479c6457b04b47&chksm=f18cd2b1c6fb5ba7386eb0bb835280bd8a651bfe0481cc78f20fc30b80c60d2d4cb7eb5b1e3e&scene=21#wechat_redirect)

**BI佐罗严选推荐：[必学书籍](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650796095&idx=1&sn=16377fdcb6da7fc03a68b6e92d840a23&chksm=f18cf02ec6fb7938daa266bcf8ef723ddf54abe6050126f77391e0d6d95b204eaf825b2831fb&scene=21#wechat_redirect) [精英眼镜](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650796099&idx=1&sn=0e98a588f53c58b2ed3d890737b390dc&chksm=f18cf052c6fb7944fabc3564b8d5abc667348888a5384936c72b2710765d1ea8d22e6f6d5d8d&scene=21#wechat_redirect) [线下沙龙](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650796587&idx=1&sn=9cfcda5211b6bb82bbe4dd468079bd01&chksm=f18cf23ac6fb7b2c7d50a34ad68a775e464e6269d9c83e675ab4d8027c667d3d4dcf09b1578d&scene=21#wechat_redirect)**

扫码与精英一起讨论 Power BI，验证码：data2022

点击“阅读原文”  
立刻拥有此案例

**↙**
