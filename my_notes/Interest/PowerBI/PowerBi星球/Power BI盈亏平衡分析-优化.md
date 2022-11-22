---
create_date: 2021-08-19T22:47:17 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI盈亏平衡分析-优化
source: https://mp.weixin.qq.com/s/bOSuu4O3HliG4KlXiOKTsw
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

关于盈亏平衡分析，之前分享过PowerBI的做法（参考：[如何用 PowerBI 做盈亏平衡分析？原来这么简单！](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074680&idx=1&sn=a3607ef748c8fbdae96dbec508eb4444&chksm=8e0c526fb97bdb79703e4ac355c51cf3f5983ef09a093043ad21610550fe57f5aeb67de9a38b&scene=21#wechat_redirect)），其效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNysmaegt4ibdQN5ql5predfiaibTJRVlYCsZlZhlKoZ45Od53z8dic48VNZ48L3MjpjabBc0rRwgIc3Q/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

这个可视化是利用折线和簇状柱形图实现的，细节处理上相对较为繁琐，PowerBI 2021年8月更新后，可以更方便的添加X轴和Y轴辅助线，所以这里再对其中的可视化设计做一下优化。  

首先说明一下，本文关于盈亏平衡分析的整体逻辑不变，和之前是一样的，只是可视化效果，可以更简洁的制作，顺便也带你熟悉PowerBI中辅助线的做法。

前两个步骤，和[之前文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074680&idx=1&sn=a3607ef748c8fbdae96dbec508eb4444&chksm=8e0c526fb97bdb79703e4ac355c51cf3f5983ef09a093043ad21610550fe57f5aeb67de9a38b&scene=21#wechat_redirect)中的一样，这里不再重复，直接从第三个步骤，制作可视化开始。

**3、制作可视化**

这里直接用折线图来制作，只需要将收入、成本和利润的度量值，放入到折线图的【值】中，主体的效果即可完成：  

**为了突出显示盈亏平衡点和盈亏平衡对应的销量和收入值，需要在这个报表中添加一些辅助元素，下面才是本文的重点。**

为突出显示盈亏平衡点的位置，需要在收入和成本线的交叉处单独显示一个点，这个度量值[上篇文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074680&idx=1&sn=a3607ef748c8fbdae96dbec508eb4444&chksm=8e0c526fb97bdb79703e4ac355c51cf3f5983ef09a093043ad21610550fe57f5aeb67de9a38b&scene=21#wechat_redirect)也已经写好了：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMzJ7iaOplcBL1b0aMdtB9YV1TYp3DneHJY7TaMcnTvS5LChWFsKd0UIPWkp2nxPts6OoDLIdu8icfA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

将\[盈亏平衡点\]也放到折线图的值中，并通过自定义系列，调整平衡点的颜色和形状，效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMdLcDZj9oMDDzaIvqXibV2lSAY0xibxtn2dqkCxzjlLcCQFNlIcOQOiaAicV728HKZOO4GzT1SrsN2wA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后添加平衡点对应的销量和收入的辅助线，因为现在最新的版本已经支持在分析面板中，添加动态的辅助线，我们需要做的就是先写出平衡点对应的销量和收入的度量值：  

> 盈亏平衡点 销量 =
> 
> SUMX(
> 
>     ALL( '销量' ),
> 
>     IF(\[收入\] = \[盈亏平衡点\],\[销量\])
> 
> )
> 
> 盈亏平衡点 收入 =
> 
> SUMX(
> 
>     ALL( '销量' ) ,
> 
>     \[盈亏平衡点\]
> 
> )

这两个度量值不仅要返回盈亏平衡点的销量和收入，更关键的是，可以在任何销量的上下文中，都能返回同一个数据，只有这样，才能成为坐标轴的恒线。

然后打开分析面板，将上面两个度量值分别添加到X轴和Y轴的恒线中，并设置恒线的颜色和线型：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMdLcDZj9oMDDzaIvqXibV2lEkqwDg2DSG0VxJ1b7ybo0fzTwoU20bBvNBMUfpf0cjwxfzdGOumia6w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后就能实现这样的带X轴和Y轴辅助线的动态报表，并且辅助线的名称也可以自定义：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMdLcDZj9oMDDzaIvqXibV2lYASicpAOWiaepIA0uvx7H3zXFh1hS0SEDaF0Xos6tdcVuOs6sat8kcgg/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

对于盈亏平衡点，是不是有种聚光灯的效果呢。

至此就做出了一个动态的盈亏平衡分析报告，PowerBI制作步骤相对之前的非常简单，只是一个折线图以及两条辅助线。

关键的环节还是要梳理清楚这种分析的逻辑，根据具体业务，剥离出相关的变量进行动态的模拟计算，然后观察可视化的效果，找出不同变量组合的盈亏平衡点，为决策提供参考依据。  

___

****[PowerBI商业数据分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)****

帮你从0到1，轻松上手PowerBI

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPAkD9ib9iaV6nBEb29PicmWvyXnmLrt9jtBVgRU9CiahLiblaa5YnEN3DlTIXA31Iv1PhsTGcHvmzdGdw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOojexubCy39PJZJic24XlI9IC8Fhx57SVYiciave3T7sAxeLXXZgrAzhAsUHXC3dxpU1fp72ChD8ibfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072351&idx=1&sn=fabb08c54790ac1225b470fd647c7a5e&chksm=8e0c4548b97bcc5e0450f1945a2c76039bbb42650bcb1edbc856820836d63d32af4c7780e31a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

↑ 扫码加入，和 3k+ 学习者一起成长
