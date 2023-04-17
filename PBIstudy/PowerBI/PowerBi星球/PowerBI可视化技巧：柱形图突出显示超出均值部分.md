---
create_date: 2021-01-11T20:22:16 (UTC +08:00)
tags:
aliases:
pagetitle: PowerBI可视化技巧：柱形图突出显示超出均值部分
source: https://mp.weixin.qq.com/s/bXyQrM8UXYvgIdnh2BNxoQ
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

之前介绍动态分组的时候，曾介绍如何利用度量值，对数据[进行动态分组和配色](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068189&idx=1&sn=8671add6ed386a011775851d8a922013&chksm=8e0c758ab97bfc9c1a2ae10f863a27ff6b7252a3288b1c0e706d03d5ce0b9fdb9689e505f3c5&scene=21#wechat_redirect)，按某个产品的销售额是否高出平均销售额的动态效果如下，

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNxWXQTa1Msptc4a6oSETTY3DkF90VZucfGZlrquyiboKmZEHNn3fkhzYJibRKqcslibibDSNibbfgq4Gw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

参考：[一个度量值，完成图表的动态分组和配色](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068189&idx=1&sn=8671add6ed386a011775851d8a922013&chksm=8e0c758ab97bfc9c1a2ae10f863a27ff6b7252a3288b1c0e706d03d5ce0b9fdb9689e505f3c5&scene=21#wechat_redirect)  

实际应用中还有一种需求是，对于每个产品的销售额，**如果高于平均值，就分为上下两部分，突出显示超出平均值的部分**，就是下面这个柱形图的效果：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJOsQXgZyeOXcribR47jbbTDLc478J61gyB072ePFLZVRxXxhqgiadwCvicX7wvNN1bBuGk3ERarszCfw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

是不是也挺有趣，不仅直观展现了哪些产品的销售额高于平均值，并且把超出均值的部分突出显示了出来。

其实就是用了一个折线和堆积柱形图，下面来看看实现步骤：

**1，建立度量值**

先计算出每种产品销售额的平均值：  

> 平均销售额 = 
> 
> AVERAGEX(ALL('产品'\[产品名称\]),\[销售金额\])

那么低于平均值的部分可以这样写：  

> 低于均值部分 = MIN(\[平均销售额\],\[销售金额\])

它的逻辑是，取产品销售额和平均销售额中的最小值，作为堆积柱形图的下柱，同理，高于均值的度量值：

> 高于均值部分 = MAX(\[销售金额\]-\[平均销售额\],0)

**2、绘制折线和堆积柱形图**

将第1步建立的度量值\[高于均值部分\]、\[低于均值部分\]和\[平均销售额\]分别放入到组合图的【列值】和【行值】中，  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOsQXgZyeOXcribR47jbbTDLOfqEfyGBQTEIKQeN7uhWGVhQv5VaWBVshYxU5yv2Xic2pvmlCy16iaHA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

就能实现前面的可视化效果，当然它也是可以动态交互的。  

通过这个简单的例子也可以看出，其实PowerBI作图与Excel作图类似，在Excel中一般是通过辅助列来灵活制作图表，而在PowerBI中，是通过度量值来实现的，关键是要掌握每个图表的内在展现逻辑，来构造对应的数据。

___

**PowerBI星球的**[**历史精华文章合辑**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)**，值得你收藏学习：**  

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNn5eia186067w5or6WoVmwdm210CYQfaibhdzFvJvR59sFUgk13iauEzR4oLzGvXiaziaX8VJcB2sCbzg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

___

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtVXYmWpicF9SVicdBBQYdaKG4icSfUTkS9dFIBW3NsL5ZrNpYH6icjgJaUA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 扫码加入，和 2k+ 学习者一起成长
