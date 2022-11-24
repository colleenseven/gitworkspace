---
create_date: 2021-09-26T22:40:59 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI自定义排序，你应该知道的技巧
source: https://mp.weixin.qq.com/s/tx96eLF-gNyA5uxKaLUZDA
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

本文分享一个PowerBI中自定义排序可能会遇到的问题以及解决的办法。

以这样一个应收明细为例，模拟的每个客户不同账龄的应收余额：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO89rRuUYtbWlBibyaf9X2g59YRjFI3YPXzBGibtciaUOibib8dHwkYnclN4nG5BVrYshO3sWZ8mahXKlg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果想要展示各账龄应收余额占该客户总应收余额的占比，你可能会这样写个度量值：

> 应收 占比 =
> 
> DIVIDE(
> 
>     SUM('应收明细表'\[应收余额\]),
> 
>     CALCULATE( 
> 
>         SUM('应收明细表'\[应收余额\]) , 
> 
>         **ALL( '应收明细表'\[账龄\] )**
> 
>     )
> 
> )

用PowerBI做一个矩阵，是这样的效果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO89rRuUYtbWlBibyaf9X2g5CxEyCM4xRysVWxKxMotNuUBOv31GVm1Kl0k9CKqPAvIkspDgFX25yQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

看起来计算的结果是正确的，但是列标题上账龄显示的顺序却是错乱的，不是我们想要的按照账期长短的顺序。

这样的问题是不是都遇到过？应该怎么调整为期望的顺序结构呢。  

其实只要熟练掌握之前分享过的按列排序技巧就可以解决，参考：

[这个小功能可以快速搞定文本排序，很多人却没注意到！](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068059&idx=1&sn=28dff6992fe6d167f4a2fbd6a0c40460&chksm=8e0c740cb97bfd1a55d7789987c7c1ed2ac94a07529cc0428b1cdf48216671f468fa7820c420&scene=21#wechat_redirect)  

根据按列排序的规则，首先需要为这些账龄添加一个序号列，以方便排序。在不破坏原表结构的情况下，可以新建一个单独的账龄分组表:

关于辅助表的制作，可以参考：[Power BI 辅助表制作方式汇总](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071809&idx=1&sn=9e8f4916082c32cc0291a2e4e565f1fd&chksm=8e0c4756b97bce4087ec53dfb6e5380e7cb0662e73fa070f831e4283095505a5aced233e59c8&scene=21#wechat_redirect)  

对这个表的账龄列，按照序号列排序，操作方式如下：  

然后将这个表与应收余额表建立关系：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO89rRuUYtbWlBibyaf9X2g5I7UdPl8oNj31befwdL9h7VttsY8ADiaPNgluAfF3KNicfjBmwX5xZF0Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**并将矩阵的列标题替换为账龄分组表中的账龄，度量值也调整为账龄分组表的字段**：

> 应收 占比 =
> 
> DIVIDE(
> 
>     SUM('应收明细表'\[应收余额\]),
> 
>     CALCULATE( 
> 
>         SUM('应收明细表'\[应收余额\]) , 
> 
>         **ALL( '账龄分组表'\[账龄\] )**
> 
>     )
> 
> )

做完这样的操作以后，发现矩阵变成了这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO89rRuUYtbWlBibyaf9X2g5IiaPkJIAwwOO4KrxQpg1WGYeDuZwwMRtjYlQjozXIuLtQia4yeFXAsjg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

虽然列标题的顺序对了，但是值却全部变成了100%，这是什么原因呢？

**因为对账龄列做按列排序以后，再用这个字段做可视化，上下文就不仅仅是这个字段本身，实际上还隐含了序号列，所以才能将文本按照一定的顺序展示。**

既然上下文中隐含的有序号列，在度量值中将序号列也ALL掉就可以了：

> 应收 占比 =
> 
> DIVIDE(
> 
>     SUM('应收明细表'\[应收余额\]),
> 
>     CALCULATE( 
> 
>         SUM('应收明细表'\[应收余额\]) , 
> 
>         **ALL( '账龄分组表'\[账龄\] , '账龄分组表'\[序号\] )**
> 
>     )
> 
> )

更省心的做法，为了避免出错，这里也可以直接ALL整个分组表：

> 应收 占比 \=
> 
> DIVIDE(
> 
>     SUM('应收明细表'\[应收余额\]),
> 
>     CALCULATE( 
> 
>         SUM('应收明细表'\[应收余额\]) , 
> 
>         **ALL( '账龄分组表' )**
> 
>     )
> 
> )

度量值这样修改以后，就可以按照正确的顺序准确显示了：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO89rRuUYtbWlBibyaf9X2g5cX5kPZq4xTvShftVlhdseUoewfvfU97N0k9cbka3eue5heHcKiapykw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

以上就是在不改动原数据的情况下，对文本字段进行自定义排序的技巧，关键是正确的操作按列排序，以及排序后根据上下文的变化调整度量值的写法。  

如果你再遇到类似的问题，套用上面的解决思路就行了。  

___

**[PowerBI商业数据分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)**

帮你从0到1，轻松上手PowerBI

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPUabZXugXKNdmeUzxwJM4OyUpTibBJjoq1jk8CzVZJz6s4nJRW1ViammT4ecqAJ7iapDccKNNrwtLYQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077212&idx=1&sn=bb3dac9becf80b5d929e5dc8405158dd&chksm=8e13a84bb964215d6362f78768cdefa18def4dfc8cd5c14f075442431604ed9c9729e4051a4b&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNNJia1fBccdeD4HTtvAuUibkNI6YYicVJ3RPhufJhoh3lzY1e1dgUyxy6yGkk4UvZcuTfVGTc89iaI3Q/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077048&idx=1&sn=b3da0a4079ed8366c67982912e795d59&chksm=8e13ab2fb964223978c16d5647e4a28eaeb50bc7338c4e82f4e14f2cddc8bb844b956f09beb6&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072351&idx=1&sn=fabb08c54790ac1225b470fd647c7a5e&chksm=8e0c4548b97bcc5e0450f1945a2c76039bbb42650bcb1edbc856820836d63d32af4c7780e31a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtVXYmWpicF9SVicdBBQYdaKG4icSfUTkS9dFIBW3NsL5ZrNpYH6icjgJaUA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 扫码加入，和 3k+ 学习者一起成长
