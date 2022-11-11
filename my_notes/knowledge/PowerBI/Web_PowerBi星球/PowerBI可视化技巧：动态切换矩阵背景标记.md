---
aliases: null
create_date: 2022-02-09T12:27:39 (UTC +08:00)
tags: 
pagetitle: PowerBI可视化技巧：动态切换矩阵背景标记
source: https://mp.weixin.qq.com/s/jSSc_mqvA1wjU0pMWMP6Iw
author: 采悟
status: 未阅读
category: 
uid: 
---

[前面的文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078928&idx=1&sn=5c9ff579bfadeb840419a648949198c4&chksm=8e13a387b9642a91c5dc33098556d2c8984c7b236f4369789fcb31b54b8ed986576fcf79b0d4&scene=21#wechat_redirect)曾经介绍了如何为矩阵中的数据标记最大和最小值，分别按行标记、按列标记以及对整个矩阵来标记，掌握了这个思路以后，其实还可以动态的来选择按照哪种方式标记。  

就像下面这个效果，根据切片器，来动态切换不同的标记方式：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMTvFMwdibq0WqEJG6iaaYEM2tNHRuKZSbmkbSYjfIlt7atjpKeZ7iciaquJgro9mTJutfkDocJX8Gaow/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

下面简单介绍一下实现步骤。  

**1、建立辅助表**

辅助表如下：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMTvFMwdibq0WqEJG6iaaYEM2QibYVdDJ7QuS2MzLGgDTB1PQF0OEiaGJX7Ic1pAiajRcg2MpLOXjCaKMg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

关于如何建辅助表，请参考：[Power BI 辅助表制作方式汇总](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071809&idx=1&sn=9e8f4916082c32cc0291a2e4e565f1fd&chksm=8e0c4756b97bce4087ec53dfb6e5380e7cb0662e73fa070f831e4283095505a5aced233e59c8&scene=21#wechat_redirect)  

这个辅助表的作用是制作切片器，以便进行动态切换。

**2、建立度量值**

> 最大最小值标记 =
> 
> SWITCH(
> 
>     SELECTEDVALUE('辅助表'\[最大最小值标记\]),
> 
>     "按月",\[每月最大最小值标记\],
> 
>     "按产品",\[每个产品最大最小值标记\],
> 
>     "整体",\[全部 最大最小值标记\]
> 
> )

这个度量值判断切片器的选择，根据选项来返回对应的标记的度量值，关于这些度量值的写法，请参考之前的文章：[PowerBI可视化技巧：如何在矩阵中动态标记最大最小值？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078928&idx=1&sn=5c9ff579bfadeb840419a648949198c4&chksm=8e13a387b9642a91c5dc33098556d2c8984c7b236f4369789fcb31b54b8ed986576fcf79b0d4&scene=21#wechat_redirect)  

**3、可视化设计**

利用辅助表中的字段生成切片器。  

并将第二步建立的度量值，放入矩阵格式>单元格元素>背景色中，即可根据切片器的切换，来动态显示不同的标记，效果如本文开头的动图。

以上就是动态切换最大值最小值背景标记的思路，当然不仅仅对最大最小值，你可以根据需要写好标记逻辑的度量值，结合切片器进行动态展现，其实和很多动态设计技巧的整体思路都类似，比如下面这些：

[PowerBI技巧：动态切换数据单位](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068044&idx=1&sn=8383fd927b54d4746d6d92164b696939&chksm=8e0c741bb97bfd0d8e89ef808bccbf452fdff5c9c8f2ace13bdbd24c8b12266101849886aceb&scene=21#wechat_redirect)

[PowerBI作图技巧：创建度量值进行动态指标分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067957&idx=1&sn=93e3f3b54fd902e26ce98f8c4112abbb&chksm=8e0c74a2b97bfdb405f86c58998f8320ea8c26853b039edfd2c7f6d8cef0d97d28dacfe9d23f&scene=21#wechat_redirect)  

[**PowerBI星球的最新版****内容合辑****，值得你收藏学习：**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078675&idx=1&sn=07abf841815e43fb0a554081c82de72a&chksm=8e13a284b9642b92d07b518abe3e6e2e2ef5066c0941c1ced26a245a6990b4330830431789a9&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN8YOicNXzCaSLpQrKXOL0LsNeYw0fj3iaGFy7XSwwmibHicdtiaHEbhgmHSPXQlkg3WiaVA4hJ8PGDcdEQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078675&idx=1&sn=07abf841815e43fb0a554081c82de72a&chksm=8e13a284b9642b92d07b518abe3e6e2e2ef5066c0941c1ced26a245a6990b4330830431789a9&scene=21#wechat_redirect)

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
