---
create_date: 2021-06-22T19:51:33 (UTC +08:00)
tags:
aliases:
pagetitle: Power BI如何对度量值分组统计？
source: https://mp.weixin.qq.com/s/Fgbev8GauKLhvUuHUbtBWg
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

经常碰到有同学问，如何对度量值进行分组统计，比如有一个环比度量值，怎么将环比划分为几个档次，然后统计数量分别是多少？  

其实度量值只是一个值，并不存在对它分组的问题，**真正的问题应该是，如何对某个维度分组统计，只是统计的依据恰好是一个度量值而已**。  

以常用的订单数据模型为例，已经写好了一个环比的度量值，计算出了每个产品的环比：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNuzWM0glkrnYrMHqd0HeZwicpm2BUH0wp2zeicPOaWibIN02g1ib1J9veqso8hibAyhWme9HZeVHk9QGA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

很多人提的问题就是如何对环比进行分组统计，环比负增长的有几个，增长20%以内的有几个，超过20%的有几个？

如果只是想到怎么对这个度量值进行分组统计，你很可能就不知道怎么下手了，毕竟度量值是一个动态的虚拟数值，怎么分组呢？

**而实际的问题呢，其实是对产品分组统计，负增长的产品有几个，增长率在20%以内的产品有几个，增长超过20%的有几个？而分组统计的依据，就是这个环比度量值。**

这个思路转变过来以后，再进行分组统计就很简单了，以上面的问题为例，下面简要介绍一下。

**1\. 制作分组辅助表**

为了进行分组，先制作一个这样的辅助表：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNuzWM0glkrnYrMHqd0HeZwKHDNZLibchGjLknExiaWib0I6xrTcJxmMqSYIib2JYUZ1PmCCYXHG9FsJw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关于如何制作辅助表，可以参考这篇文章：[Power BI 辅助表制作方式汇总](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071809&idx=1&sn=9e8f4916082c32cc0291a2e4e565f1fd&chksm=8e0c4756b97bce4087ec53dfb6e5380e7cb0662e73fa070f831e4283095505a5aced233e59c8&scene=21#wechat_redirect)

**2\. 建立度量值**

根据分组建立一个度量值来统计产品数量：

```
产品数量 = 
```

这个度量值的逻辑是，获取当前分组的最大值和最小值，然后迭代产品名称，筛选出环比在这个区间的产品，然后统计数量。

关于这个分组的逻辑，之前也已经写过，还可以参考：[Power BI 数据分析应用：客户购买频次分布](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070056&idx=1&sn=f03cc79148b1c420d25800be8c0380b9&chksm=8e0c4c7fb97bc56943e3552d9403aaf07e1bb12b24f8f248aab2891af38614f1065e289697e7&scene=21#wechat_redirect)

这个度量值写好以后，就可以统计出每个分组的产品数量了：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNuzWM0glkrnYrMHqd0HeZwG98l0WJ8w2G5fGMbjGTMJxVhNPxgR9f4ulSAuUozZ9yCIzg2TsUN6A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

环比负增长的产品有2个，增长率在20%以内的产品有4个，环比超过20%的产品有7个。

当然这个数据是可以随着数据的更新或者时间的选择动态计算的。  

还可以做个矩阵，来看看每个类别中，不同增长水平的产品分别是多少：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNuzWM0glkrnYrMHqd0HeZwapBd0frZOO2hQ4hUZVAsceUt6gOIX1b3hQSB10meC3psyJMXhybtNw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这就是依据度量值对产品分组统计的思路，其他类似的分组问题，都可以按这个思路解决。  

___

**618限时优惠活动进行中**

扫码立减50元，PowerBI星球社群最后一次这么低价，感兴趣的星友不要错过了哦~  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNKwl8qibtr4ZxJ7WPtps7CJMHA1vEqTmWWpyDWxfbMJPiamUDJiaJHCKugTdIyLfpUmhWLofHFS3tBw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**▼****点击****阅读原文****，也可立享优惠~**
