---
create_date: 2021-09-13T22:42:21 (UTC +08:00)
tags: 
aliases: null
pagetitle: PowerBI可视化技巧：突出显示特定期间数据
source: https://mp.weixin.qq.com/s/trY14l8M7KsM9T0qo5jHrw
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

数据可视化时，为了突出显示特定的数据，之前的文章中分享了如何突出显示多折线图的某一条线（参考：[Power BI可视化设计：折线图高亮显示](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076932&idx=1&sn=3cad8e68d76597590f60aeb9d067f4be&chksm=8e13ab53b9642245fee0ffb53095aaebe19b9729447cdc7209530b1ab993195f0956baba026d&scene=21#wechat_redirect)），效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNNJia1fBccdeD4HTtvAuUibkIgsjGlaU1jevEiaicNwiaCLtugefvpByibFf2xjVibtuOwuRffMXWFXtabw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

如果说上面效果是折线图的纵向突出显示，其实我们还可以进行横向的突出显示，高亮显示某一区间的数据，效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNVwQ5v1HFlE7tAqETZfQqPOckbokBH5b3fibbbDWwBL4EThuz1AQ3Asjo6FfWaejBpugmxndH63Sw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

这种效果是怎么实现呢？  

看起来类似，其实实现方式是完全不同，上面高亮显示某一段时间的折线，只是用了上月刚更新的功能：X轴恒线。  

下面来看看实现步骤。  

**1、建立一个独立日期表**

可以用CALENDARAUTO函数来生成。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNVwQ5v1HFlE7tAqETZfQqPFgatTw5BiaxBzWcAYoFicKpvYHfzbrPc96EqCVia2a87kmyFPVzssTZ8Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

建立这个日期表目的，是为了让这个日期与模型中原有的数据不发生筛选作用，所以这个新的日期表不必与其他表建立关系。  

**2、制作折线图**

这里用独立日期表的日期作为轴，为了让每个日期能正确的显示销售额，再写个度量值：

> 销售额 折线图 \= 
> 
> CALCULATE(
> 
>     \[销售额\],
> 
>     TREATAS('独立日期表','日期表'\[日期\])
> 
> )

通过TREATAS将未建立关系的独立日期表，视同日期表使用，来计算每日的销售额，将这个度量值作为折线图的值。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNVwQ5v1HFlE7tAqETZfQqPVGd5d3DbVLY2jpruZx1cZzwHlMR7ywq6ZE86JSt8zTvfawlMrVXXOQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**3、为折线图添加X轴恒线**

先写两个度量值，来确定切片器的开始点和结束点：  

> 起始点 = MIN('日期表'\[日期\])
> 
> 结束点 = MAX('日期表'\[日期\])

然后打开分析面板，添加X轴恒线，点击fx即可使用度量值来确定恒线的位置：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNVwQ5v1HFlE7tAqETZfQqP2QJCKs4YgKKnCNt3p9oB5ZLCIIWz3bId3p3KcibeQxuibWhEU4wAKPVQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

分别用上面两个度量值值添加两条恒线，**其中起始点设置阴影区域设置为"之前"，并设置透明度**。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNVwQ5v1HFlE7tAqETZfQqPeicAng6M5xzZlHEOnGD325yDEeWpFT22e9nbONCK5VP6fibIfYSL1ia5g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

同样，**设置结束点恒线的阴影为"之后"**。

然后利用模型中的正常日期表中的日期，制作切片器，就可以实现突出显示特定区间的效果。

柱形图也可以用这种方式突出显示：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNVwQ5v1HFlE7tAqETZfQqPqEzIgMmEZG6FXicgpU6QAFeSbcQEERqWhnDNxsvjm5x1I6iaygq31JhQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

通过以上的步骤，你应该看出来了，其实原理并不是让某个区间的数据高亮显示，恰恰相反，而是利用X轴恒线的阴影功能，让其他期间的数据变得暗淡而已。

___

**[PowerBI商业数据分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)**

帮你从0到1，轻松上手PowerBI

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNuVIqc0mzbKDNPmI0mwcTkvUibMVjf4z1bY0MYFh7lAkqrcHiaEHE4UicvjJjibpmkxJjc4TDlVO04qg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPUabZXugXKNdmeUzxwJM4OyUpTibBJjoq1jk8CzVZJz6s4nJRW1ViammT4ecqAJ7iapDccKNNrwtLYQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077212&idx=1&sn=bb3dac9becf80b5d929e5dc8405158dd&chksm=8e13a84bb964215d6362f78768cdefa18def4dfc8cd5c14f075442431604ed9c9729e4051a4b&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNNJia1fBccdeD4HTtvAuUibkNI6YYicVJ3RPhufJhoh3lzY1e1dgUyxy6yGkk4UvZcuTfVGTc89iaI3Q/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077048&idx=1&sn=b3da0a4079ed8366c67982912e795d59&chksm=8e13ab2fb964223978c16d5647e4a28eaeb50bc7338c4e82f4e14f2cddc8bb844b956f09beb6&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

↑ 扫码加入，和 3k+ 学习者一起成长
