---
ZK: Origin
create_date: 2021-12-23T12:48:02 (UTC +08:00)
tags: 
aliases: null
pagetitle: PowerQuery数据处理技巧：时分秒文本转换为数字
source: https://mp.weixin.qq.com/s/vnlH6gqb3GhO4z9wXcDe3g
author: 采悟
status: 未阅读
category: 
notes: False
uid: 
---

今天分享一个数据处理的小技巧。  

最近被星友问到文本格式的时间如何转换为数字时间的问题，本文就来介绍一种简易的转换方式，如果你恰好碰到这种问题，应该会有帮助。

模拟示例数据如下图：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM6wuLntBIhbJp16zRQxB7ibVGPX2xicNOcOycbHXk5qHTuJfbJTAKwbgDtUfe3eN1ISJNqFV0zyvqQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在这些时间字符串中，有的是完整的时分秒，而有的只有小时或者分钟，对于这样的字符串显然不能直接转换为标准的时间或者数值数据，如果想把这样的文本转换为数字的秒数，应该怎么做呢？

基本思路是将文本的小时、分钟和秒根据单位，替换为相应的计算表达式，然后运行计算即可，下面就来看看PowerQuery的具体转换方式。

导入PowerQuery以后，选中这一列，右键>替换值：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM6wuLntBIhbJp16zRQxB7ibiaEye8zpZsnibvuJcF6ptIdpKIuLETqiaglQrOSXdrEox6RPic37mh0Wlw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

将"小时"替换为"\*3600+":  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM6wuLntBIhbJp16zRQxB7ibPzlyOknwHkw3zXgYu2wUdHopM6MgJTgrrcF7wPogMMXlDFjhbRqXbA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

同样的方式，再做两次替换，将"分钟"替换为"\*60+"、将"秒"替换为空，就可以将以上的时间字符串转换为这样的数学表达式：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM6wuLntBIhbJp16zRQxB7ibpZE0R9F9TNVWMp1SVYGr5XNOAEJBMJOTbkpH9PFdfBsqGh16wzMCzw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后利用M函数Expression.Evaluate来计算这个表达式，添加自定义列：  

> Expression.Evaluate(
> 
>      Text.TrimEnd(\[时间\],"+")
> 
>  )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM6wuLntBIhbJp16zRQxB7ibf6ADQuzSOsbW3t8IzrC0Dokm1OvmeRiac6eU2IRpefNE6BkhtBHOskQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

因为数据中有些时间的秒是不全的，导致上面的替换操作后，有的值最后带有“+”，所以这里用了Text.TrimEnd先将尾部的字符"+"清除掉，然后再计算这个表达式，结果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM6wuLntBIhbJp16zRQxB7ibQ2JsyIPnZlySNrXwicHaQAEK7jJ7xzkOunJpLVxTic1EuDyL3I6ld4Pw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就轻松从时间文本得到了具体的数字，如果想要的是小时数，在这个基础上再除以3600即可。

解决这种需求的方法，当然不止这一种，但应该是最简单、最易于理解的做法，很多数据的处理，不要把它想的太复杂，大部分需求都可以灵活使用PowerQuery中的界面操作来完成。

**/推荐阅读/**

01 [](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068904&idx=1&sn=5e82ba6bd4e39067c423ce1d9c7c8e9e&chksm=8e0c48ffb97bc1e96f333480a099f16220edf1b4515030e776f8815607a560e726b13dd50b66&scene=21#wechat_redirect)[PowerQuery](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070803&idx=1&sn=826d571e4133872ff3bedb4ad4d524f9&chksm=8e0c4344b97bca5281787e9a0cf1a3f2571227316537b1ba7069c5bf5f600d4a4249cfc18932&scene=21#wechat_redirect)[批量合并Excel技巧](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070803&idx=1&sn=826d571e4133872ff3bedb4ad4d524f9&chksm=8e0c4344b97bca5281787e9a0cf1a3f2571227316537b1ba7069c5bf5f600d4a4249cfc18932&scene=21#wechat_redirect)

02 [](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068461&idx=1&sn=7d0cc28760d0afd4f7c1e53e3c319437&chksm=8e0c4abab97bc3acca7a5e9b89d85ac48a5484d9bc2fc3709519db7d955adc2b3e838c51995e&scene=21#wechat_redirect)[利用 API 获取地点经纬度信息](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068753&idx=1&sn=e58728447ebaf22c8099e7b798386b0f&chksm=8e0c4b46b97bc250bf35546391eaa9e1ad168fe1918ed130bbd7be0dbd89c5c4991112dda884&scene=21#wechat_redirect)

03 [](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068163&idx=1&sn=41bc68e5c89950443ec13ee13b58c60c&chksm=8e0c7594b97bfc82aa620942036c2f30fee832c601a600e5e4eda1582a46f96b809bddda40ab&scene=21#wechat_redirect)[PDF 转 Excel 技巧](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068151&idx=1&sn=41509c2109d2d0cc851d57a051159ddc&chksm=8e0c75e0b97bfcf6682a72fe714a5eef7194ce9124d4510bc1b2bc89ac01c4933429ba305f68&scene=21#wechat_redirect)

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
