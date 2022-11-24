---
create_date: 2021-08-10T22:51:56 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI可视化设计：折线图高亮显示
source: https://mp.weixin.qq.com/s/F-def-K6lfKpSfSMwJzShA
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

平时制作可视化时，折线图会经常被用到，如果系列较多，折线图看起来就比较乱，比如每个产品的销售趋势图：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNNJia1fBccdeD4HTtvAuUibkibYoYtTPFXC03xb4TibLU3H7oxCFE1cWo4vDU6YmbsZkqLfFEKqm5BmA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

看起来信息密度好像很高，但是想看清楚是哪个产品都很困难，当然也就不能有效的传递信息了。

对于多系列折线图，可以换个思路，既然同时展示在一起太杂乱，不如只突出展示一条折线，并让其他折线作为背景，效果如下;  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNNJia1fBccdeD4HTtvAuUibkIgsjGlaU1jevEiaicNwiaCLtugefvpByibFf2xjVibtuOwuRffMXWFXtabw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

**这样设计既能快速获取特定产品的销售趋势，又不失去其他产品的上下文，依然能比较该产品相比与其他产品，处在什么位置。**

这是如何做到的呢？思路很简单，其实有**两个折线图，上下重合叠放到一起而已。**

对于下层的折线图，将所有的折线颜色都更改为浅色：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNNJia1fBccdeD4HTtvAuUibkqcgaEf9w7CTK6M83ibIkqgTtNErzggqc1xy3RicibELyMtmiaozk9oicORg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

而上层的折线图，只显示一个产品的数据，不过为了让切片器不影响下层的折线图，这里需要做一个独立的切片产品表，

> 切片产品表 = VALUES('产品表'\[产品名称\])

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNNJia1fBccdeD4HTtvAuUibk5vUNHGicfLng0EJibKL1ONxatqiblJJPvib229h6FTrV535YzBDTUwoySg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个表不要和模型中的其他表建立关系，并利用这个表做切片器。然后写个度量值，将切片器中的产品与模型中的收入关联起来：

> 产品收入 =
> 
> CALCULATE(
> 
>     \[收入\],
> 
>     TREATAS( '切片产品表' , '产品表'\[产品名称\] )
> 
> )

该度量值利用TREATAS函数，把未建立关系的切片产品表视同已建立关系的产品表来使用，这样切片器选择某个产品，该度量值就会返回该产品的数据，用这个度量值和月份生成单系列的折线图。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNNJia1fBccdeD4HTtvAuUibkT8icibY6N7ccRz5pvhZ8CC270e0GuFQQzxSibz8HhqS0iaicwcn6EoNbPKQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

折线图线条设置为亮色、显示数据标签、背景设置为透明，然后将两个折线图叠放到一起，突出显示的折线图置于顶层：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNNJia1fBccdeD4HTtvAuUibkuHM87V6ouPicdW6yaxTuSOclJBo25CIom1aD3lXdXgBiboicBbV8trw5w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

通过这样的组合叠放，就可以实现突出显示所选产品折线的效果。

  
这个技巧不难，不过上下叠放组合时，为了完全不漏痕迹，有些细节需要注意：  

**1、尺寸完全相同**

为了达到完全一致的效果，如果你先做好的是底层图，直接复制一个，替换字段，生成顶层的折线图，这样两个图表的尺寸就是完全一致的。  

**2、上下完全重合  
**

拖动顶层图表尽量与底层完全重合，虽然有自动对齐功能，但坐标轴字符并不一定会完全重合，为了不影响叠加效果，可以将底层的字符全部设置为与背景一致，这样稍微有一点偏差也不会显示出来。  

**3、Y轴刻度一致**

这个需要特别注意，如果不加控制，坐标轴刻度不一样，两个图表的折线几乎不可能重叠起来。

现在折线图的坐标轴已经支持在起止刻度上设置条件格式，利用度量值可以很方便的进行动态控制。

Y轴起始点可以都设置为0，结束点写个度量值：

> Y轴最大值控制 \=
> 
> MAXX(
> 
>     CROSSJOIN(
> 
>         ALL( '产品表'\[产品名称\] ),
> 
>         ALL( '日期表'\[月\] )
> 
>     ),
> 
>     \[收入\]
> 
> )\*1.1

这个度量值自动计算产品本年中的月度收入的最大值，并乘以1.1作为坐标轴的最大刻度，放置到结束点中。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNNJia1fBccdeD4HTtvAuUibk2BBDKFhSYrvfh8vqPwceVkCgkRcXTxBsoaVfCiaYhtz7CKG3CkPTODQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

上下两个折线图都按照这个来设置开始和结束点，Y轴的刻度就能同时一致性变换了：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNNJia1fBccdeD4HTtvAuUibk8iaURJBcYMC56MiayZUa4iae1pibfRGFKC7mQeleib9lZWB2HMSWwyYVibCg/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

上面就是突出显示折线图的技巧，在进行数据可视化时，不只是把图表做出来，还要看是否能清晰的表达，是否能快速高效传递信息，重视用户感受才能提升可视化的价值。

___

**[新书上市：PowerBI商业数据分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)**

帮你从0到1，轻松上手PowerBI

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOojexubCy39PJZJic24XlI9IC8Fhx57SVYiciave3T7sAxeLXXZgrAzhAsUHXC3dxpU1fp72ChD8ibfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNNJia1fBccdeD4HTtvAuUibkNI6YYicVJ3RPhufJhoh3lzY1e1dgUyxy6yGkk4UvZcuTfVGTc89iaI3Q/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074680&idx=1&sn=a3607ef748c8fbdae96dbec508eb4444&chksm=8e0c526fb97bdb79703e4ac355c51cf3f5983ef09a093043ad21610550fe57f5aeb67de9a38b&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072351&idx=1&sn=fabb08c54790ac1225b470fd647c7a5e&chksm=8e0c4548b97bcc5e0450f1945a2c76039bbb42650bcb1edbc856820836d63d32af4c7780e31a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

↑ 扫码加入，和 3k+ 学习者一起成长
