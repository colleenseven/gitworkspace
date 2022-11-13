---
create_date: 2021-12-26T12:47:30 (UTC +08:00)
tags: 
aliases: null
pagetitle: PowerBI中的这个AI功能，你可能还没有用过
source: https://mp.weixin.qq.com/s/LnRjqdB9Fvr6ykgw89PfMg
author: 采悟
status: 未阅读
category: 
notes: False
uid: 
---

PowerBI中不仅有普通的可视化图表，还有不少AI智能应用，之前曾介绍过几个，比如：

[尝鲜Power BI的AI黑科技图表：关键影响因素](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068371&idx=1&sn=497a7574a9d1a8a69d7d5e90f3ac6d64&chksm=8e0c4ac4b97bc3d2bbde4d08927abf4a1f25ae5dcf0c8cf01ed9e45b63a21fe1d3ad7db3b2f7&scene=21#wechat_redirect)  

[体验PowerBI新的AI黑科技图表:分解树](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070285&idx=1&sn=00ec89edc4e0157b6d60670ab4c232ef&chksm=8e0c4d5ab97bc44c1a8c22d6385a58e755331499a80def5ea6f7019181c29b120047b8f2fb8f&scene=21#wechat_redirect)  

[利用Power BI智能叙述，生成动态报告摘要](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073801&idx=1&sn=3a6dcd73ed52e77a4159612fe49af3e7&chksm=8e0c5f9eb97bd68889ce7e6ae0af81e62b7ed6b7ea7827deb5ca1ba097c14e4965889736baa4&scene=21#wechat_redirect)  

今天再介绍另外一个AI功能：异常检测。这个功能已经推出有一段时间了，可能很多人并没有注意到，最近正好被人问起，这里就再专门对该功能做个介绍。  

首先说明一下，这个功能目前只适用于折线图，并且只针对坐标轴为日期、单条折线并且没有启用预测的情况下，才能使用异常检测功能。

以一个收入趋势的折线图为例，选中折线图，然后在“分析”面板中打开"查找异常"，折线图周围自动就会出现期望的范围，不在范围内的数据点就会标记为异常的数据点：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPnlBZuYvQ2UKCxWJ81RPJKFy4yTcyq3KVhLRJ4ibib5y0lR4yd3wuYblniclV5uhQ2K6fOhjMFdkTfA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

展开“查找异常”功能，可以看到它的各项设置，可以调整异常点的形状、大小和颜色，还可以设置预期范围的颜色、样式和透明度，以及配置检测算法的敏感度参数。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPnlBZuYvQ2UKCxWJ81RPJKCq7MibNbfrfJNh0iazfWVtumEYNVghICscHA0aohc7RiasPng8KOInM6w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果提高敏感度，算法对数据的更改会更敏感。 在这种情况下，即使微小的偏差也会标记为异常。 如果降低敏感度，算法对异常的判断会更宽容，更少甚至没有异常点。

点击某个异常点，就会弹出异常面板，介绍关于异常点的说明：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPnlBZuYvQ2UKCxWJ81RPJKxJfH1j8451LcjRiaGXHibvlqcVyc2XGleEgqM9TYicMf6lWWRLqTKZbLg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

  
并在下方对该异常出现的原因进行可能的解释，并且影响最大的因素还会自动以图表的形式对比展示出来。在上图的示例中，显示是由于VR眼镜的销量提升，拉高了整体的收入。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPnlBZuYvQ2UKCxWJ81RPJKOkrBPnFLn71XiaGrqa52cPYzvjpYY52C1PKfVgWsMkTMsnrsafQgoog/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个解释的可视化图表还可以直接添加到报表中，放大进行更详细的观察和分析：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPnlBZuYvQ2UKCxWJ81RPJKaIxv5uspiaic9waY0fSR0rEEDzaEvibvgkJqZsWLvzqa0kQylqpWP7rnw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个解释的折线图的次坐标轴所用的数据，模型中并没有这个度量值，完全是系统智能生成的，并且自动添加一条异常点的X轴恒线。

关于这个解释，你可以自定义解释的字段，将你觉得会对结果产生重大影响的因素放到异常的设置里面，它就会自动计算出这些因素对结果的影响程度。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPnlBZuYvQ2UKCxWJ81RPJKltibiaHJCz8OIOy9Xj7a8CxcDibuww1OuzZaYussrXg6CslA0LDwTDmZw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这就是异常检测智能的地方，无需提供计算逻辑，只需要设置好参数，并将可能的因素放进去，它自动、快速的识别出哪个因素影响最大，以及具体的影响数据是多少。我们无需知道背后的算法是什么，它输出的结果也是可以复核、验证的。

你也可以尝试使用该功能，找出你的异常数据以及可能的原因。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
