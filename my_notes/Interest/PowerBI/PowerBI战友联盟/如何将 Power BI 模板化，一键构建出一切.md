---
create_date: 2022-11-10T11:29:10 (UTC +08:00)
tags: 
aliases: null
pagetitle: 如何将 Power BI 模板化，一键构建出一切
source: https://mp.weixin.qq.com/s/Zd2kHT4mQErFE5eTedy9WQ
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

很多伙伴已经收录了四大精品案例。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOuibcypo62wx36KhJB4B9ClISdHUmTT2pYRRfytJorRXGnKQIQuEXr249F6FywUbeAiarCEJNfHic9g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

它的构建体验是：

用户小姐姐，完全不懂 Power BI 是啥，但她输入了数据路径，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOuibcypo62wx36KhJB4B9Clkm0oEicVWYHMTCicDvdSSJ8lMXnOpwUXgGrgFd9T88S1yXdInVJXVbXw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

输入路径，加载，如下：

几秒钟过后，一套高大上的 Power BI 报告体系，好了。如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOuibcypo62wx36KhJB4B9ClRMtMZtuY00GVkzSvWaIfib4R2JbwuiajytxkwGDK27rkl8bGMnTJMofw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

不懂 Power BI 的老板很震撼，她感觉一切就这样被构建完成了。

再来看一个更恐怖的案例吧。

对于拥有大量数据文件的 Power BI 报告一样可以模板化。即使数据量很大，很复杂，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOuibcypo62wx36KhJB4B9ClgOezMPv6yAy9NcOxjgqm29BK43m3NfC2ASaolkUPogRWS8z2jo5Byg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

打开 Power BI 模板，如下：

这次是要构建数百个文件构成复杂 Power BI 报告了。输入路径后，加载。如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOuibcypo62wx36KhJB4B9CliaPNfqzCIvVFHscKhYBHVB1zYk0cZ3aSkXmmElNEiaPolcAls6aic50icg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

一切完毕。

满满的拥有感，有没有。

怎么做到的呢？

## 第一步：路径参数化

必须设置一个数据源的参数，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOuibcypo62wx36KhJB4B9ClM14Bic0jex0t1M0GdK4JMDUjQGOQDPzbzzKvu8NJibWnWiavNTEgAq2icQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> 注意
> 
> 不能是多个参数，不然，小白用户驾驭不了。

这样，用户只需要未来输入参数即可。

## 第二步：模板化

很多小伙伴没有注意到一个问题：

Power BI 文件 .pbix = 数据模型（内容） + 数据模型（架构）+ Report（框架）

其中，数据模型（内容）的占到了总体量的 90% 大小。

我们有个需求：

1、实现数据和模板的彻底分离

2、用户拿到模板，而不是数据

当然，给用户数据的时候，用户可以现场构建整个含有数据的新鲜报告。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOuibcypo62wx36KhJB4B9ClvTh0Ydo0knoKvp8ibkAc5aiabOCcslhibELsCH2Zr8U6K9UuoNN1Vushw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

完成。

## 总结

Power BI 已经进入模板案例时代，有些经典案例是必须拥有的。

将 Power BI 模板化，让用户最轻松地感受 BI 小伙伴带来地价值是很愉快的。

[

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/09hv4Xua0LNicIFibczXDadHib5G2ibUS8xs59pEriaOzviafGWtR9hVS6yg3wfH5F70xjuQPF8v0wQYeFmOtMSzyZzQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

BI佐罗：四大 Power BI 作品，现已开放下载





](https://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650796560&idx=1&sn=9188517b8d17bba8466cfd39907de83d&chksm=f18cf201c6fb7b173b638c46fadf7752dd7160446c9b8fb1d6b9759de6cf24cadce5262f8112&scene=21#wechat_redirect)

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNhia5Pc4XC1Um7IYgQhGEoEC1yK05ibUFoPBYpcoAMvibuZh2BZaibMzULeDwNfSeQ0KHRcDUdX3FzVA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**Power BI 终极系列课程《BI真经》**

[

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/09hv4Xua0LNBM1lxlQYHJBicic4CvPoRGLqHgdTZOr8goNRh0asDXA48mRDzc9zxW4UMQiayHwgDmx7mlt4cQxtjg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

BI真经 - 让数据真正成为你的力量





](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650788512&idx=1&sn=76972ff4b0cf265fe9479c6457b04b47&chksm=f18cd2b1c6fb5ba7386eb0bb835280bd8a651bfe0481cc78f20fc30b80c60d2d4cb7eb5b1e3e&scene=21#wechat_redirect)

**BI佐罗严选推荐：[必学书籍](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650796095&idx=1&sn=16377fdcb6da7fc03a68b6e92d840a23&chksm=f18cf02ec6fb7938daa266bcf8ef723ddf54abe6050126f77391e0d6d95b204eaf825b2831fb&scene=21#wechat_redirect) [精英眼镜](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650796099&idx=1&sn=0e98a588f53c58b2ed3d890737b390dc&chksm=f18cf052c6fb7944fabc3564b8d5abc667348888a5384936c72b2710765d1ea8d22e6f6d5d8d&scene=21#wechat_redirect) [线下沙龙](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650796587&idx=1&sn=9cfcda5211b6bb82bbe4dd468079bd01&chksm=f18cf23ac6fb7b2c7d50a34ad68a775e464e6269d9c83e675ab4d8027c667d3d4dcf09b1578d&scene=21#wechat_redirect)**

扫码与精英一起讨论 Power BI，验证码：data2022

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNicIFibczXDadHib5G2ibUS8xsw1LOXrdwaibTQrZjA0via7FIILnS9zmkThSvUf1b7rMMD62ykxeica7Og/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击“阅读原文”进入学习中心

**↙**
