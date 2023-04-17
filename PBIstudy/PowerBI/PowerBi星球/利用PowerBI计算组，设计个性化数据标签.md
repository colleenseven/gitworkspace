---
create_date: 2021-06-08T19:53:44 (UTC +08:00)
tags:
aliases:
pagetitle: 利用PowerBI计算组，设计个性化数据标签
source: https://mp.weixin.qq.com/s/74xRdSG2aIfDRCZ4KwPACg
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

之前曾经介绍过如何在折线图上标注出最大值和最小值，利用了几个度量值实现的：[PowerBI作图技巧：在走势图上标注最大值、最小值…](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068479&idx=1&sn=f96bf83e4f0705aecbd1960dac731ae9&chksm=8e0c4aa8b97bc3be08566dea69e91093e6383bc45c21a9a3cb149d83797c91f0f17a02e68aa8&scene=21#wechat_redirect)

其效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPCWuRtTZ5D49T8IznjSyNYPu31cWBQdfSShGjZIqZjcRpicYicUtS4uHLTDzSYvuGIDjiaibsbYnBWBA/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

**如****果在最低点和最高点上不仅显示数据标签，还想显示这个点的属性**，比如在某点的数据标签上不仅显示数据，并且用文本显示该点为“最高点”，能不能做到如下的效果呢？  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJP6g2CKCaFIHNPwj29EQJuXNM2m9NicBQ0sq4wAQkcr1PNDs3rve85U686GjicxIdqVHNkUsKcuryCw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

在PowerBI中，图表的数据标签，通过格式的设置，目前只能显示数据，无法显示文本，所以利用之前的技巧是无法做到的。

不过现在我们可以利用计算组，来实现这种个性化的数据标签，下面简单介绍一下步骤。

还以[之前介绍](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068479&idx=1&sn=f96bf83e4f0705aecbd1960dac731ae9&chksm=8e0c4aa8b97bc3be08566dea69e91093e6383bc45c21a9a3cb149d83797c91f0f17a02e68aa8&scene=21#wechat_redirect)使用的模型为例，利用一个基础度量值\[指标数据\]和日期表中的日期，图表类型可以选择折线图或者面积图，制作一个简单的趋势图，然后打开外部工具“Tabular Editor”，进行计算组的制作。

关于计算组的基础操作，这里不再详细介绍，你可以通过这篇文章来了解：

[PowerBI发布重磅更新，一文带你熟悉计算组怎么用](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072054&idx=1&sn=d403fdef264cbfb6fca46d33bd0083b9&chksm=8e0c44a1b97bcdb7fe466afe90d0f3d4b86738a0da7241f9125d4f36a1fcbd89c094b7ea42d8&scene=21#wechat_redirect)

**1\. 设置度量值的格式**

这里制作图表用到的是度量值\[指标数据\]，所以在Tabular Editor中找到这个度量值设置数据格式，可以根据自己的需要设置。

我这里对数据按千分位显示，并且保留两位小数，可以设置为"#,##0.00"

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP6g2CKCaFIHNPwj29EQJuXxEVlN9eXIXN8CNX4ubaXP8XQ6CTneWYejthM3QW2UI7ibMETVU3PYmg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**2. 建立计算组和计算项**

计算组可以命名为“数据标签”，因为这里要显示最高点和最低点，所以计算项可以命名为“最高最低点”，该计算项的表达式直接这样写就可以了：

SELECTEDMEASURE()

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP6g2CKCaFIHNPwj29EQJuXMjx4ibctatLcvszPtOBiaQyEExKQf4xHy5ia148spMIS4AaibMw5x8xDCg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**3\. 编辑计算项的格式表达式**

这是最重要的一步，先打开这个计算项的格式表达式编辑框：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP6g2CKCaFIHNPwj29EQJuX2DoxLia7oQePm7ib0oYiaRicvqeDM8PVJFIuic3bEXd6L7fzgWlML3GgbFw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后在编辑框中输入：

```
VAR dates_ =ALLSELECTED ( '日期表'[日期] ) VAR highest_ =MAXX ( dates_, SELECTEDMEASURE () )VAR lowest_ =MINX ( dates_, SELECTEDMEASURE () )RETURNSWITCH ( TRUE (),    SELECTEDMEASURE () = highest_, "最高：" & SELECTEDMEASUREFORMATSTRING (),    SELECTEDMEASURE () = lowest_, "最低：" & SELECTEDMEASUREFORMATSTRING () ,    UNICHAR(8203))
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP6g2CKCaFIHNPwj29EQJuXWdkur0Zn7eNticmpmMZLBuNejz6icbMxyMBH5XFVWNR9ZDOxgmZhgqjg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个表达式的逻辑与日常我们写的DAX逻辑是一样的，先通过变量计算出最高点和最低点，然后判断这两个点，来返回对应的数据。

**只不过在计算组中，度量值本身就可以作为上下文，使用** **SELECTEDMEASURE** **函数来表示目前上下文所使用的度量值，以及用函数** **SELECTEDMEASUREFORMATSTRING** **来获取当前度量值的数据以及格式。**  

这样设置好以后，点击保存，退出Tabular Editor，并在PowerBI界面刷新。

**4\. 利用计算组做个切片器，勾选“最高最低点”，就会在趋势图中出现带有文本的数据标签。**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP6g2CKCaFIHNPwj29EQJuXdIGPCAJxu59YJIibib6cYjmmIZJIm0J2sMpSSXq7ebcuqVSH714O4wbQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

为了让最高点和最低点显示不同的颜色，还可以通过度量值来进行配色：

> 配色 \=
> 
> VAR dates\_ =ALLSELECTED ( '日期表'\[日期\] )
> 
> VAR highest\_ = MAXX ( dates\_, \[指标数据\] )
> 
> VAR lowest\_ = MINX ( dates\_, \[指标数据\] )
> 
> RETURN
> 
> SWITCH( TRUE(),
> 
>     \[指标数据\] = highest\_, "lime",
> 
>     \[指标数据\] = lowest\_, "red"
> 
> )

然后就实现了本文开头的标签效果。

利用计算组，突破了图表数据标签默认不能个性化显示文本的限制，本文只是一个简单的应用示例，你也可以通过这种方式，对图表添加个性化的标注，来帮助用户快速理解数据。

___

**[新书上市](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)**

帮你从0到1，轻松上手PowerBI

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOojexubCy39PJZJic24XlI9IC8Fhx57SVYiciave3T7sAxeLXXZgrAzhAsUHXC3dxpU1fp72ChD8ibfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072351&idx=1&sn=fabb08c54790ac1225b470fd647c7a5e&chksm=8e0c4548b97bcc5e0450f1945a2c76039bbb42650bcb1edbc856820836d63d32af4c7780e31a&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 3k+ 学习者一起成长
