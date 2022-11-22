---
create_date: 2021-09-22T22:41:23 (UTC +08:00)
tags: 
aliases: null
pagetitle: PowerBI 2021年9月更新，你应该知道的几个变化
source: https://mp.weixin.qq.com/s/SYjGQ-sHR5fEOpCyDt6O5Q
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

PowerBI 2021年9月的更新来了，关于更新的完整内容官方博客的介绍非常详尽，你可以在博客中浏览（使用Chrome浏览器可自动翻译），点击阅读原文”也可直接进入：

https://powerbi.microsoft.com/zh-cn/blog/power-bi-september-2021-feature-summary/

也可以在我的视频号中观看本月更新的官方视频讲解（已加中文字幕）:

这里我主要挑选几个你很可能会用到的功能简要介绍一下。

**1\. 折线图支持系列标签**

## 这算是本月最实用的一个功能更新，折线图终于可以在折线上直接显示系列标签了，在格式中打开“系列标签”，就可以添加标签，并可以自定义设置标签的位置、文本和背景：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOSR5KDAwS17PCsRsKQ80gHPwCZTbNiblibS2sLcrBaRLibadbWvr7qWKa2tlpd7JLbWwp5QIKIIIQMw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后就可以折线图上可以直接显示标签，比如显示在折线图的右端：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOSR5KDAwS17PCsRsKQ80gHVuReemiaWtia5lO7b2x8DQaP9Dib70MFGsiaPzf5JxDyScYdIdNq3ic2htg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样看起来是不是非常自然，可是以前只能利用计算组来变相实现（[PowerBI可视化技巧：折线图上直接显示类别](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076437&idx=1&sn=8f9e3f84e7894246cf05fa8ca7166c81&chksm=8e0c5542b97bdc54f9ed24dbeb304d55e3bf9891b9271a87b1e309bfc84ad9b4d325c8e2426c&scene=21#wechat_redirect)），现在终于可以直接设置了。

**2\. 内置瀑布图支持关掉"总计"**

之前内置的瀑布图被吐槽最多的地方，就是必须显示个总计项，无法去掉：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOSR5KDAwS17PCsRsKQ80gHfYy9tMRvgkLJ8WoCeuTXwjyk18hwsl7GWiczQbCZASQCmjA5S1u48Bg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

而本月更新后，可以在Y轴中，关掉“显示总计”：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOSR5KDAwS17PCsRsKQ80gHEQlt3dYSq1MeS0KKKfmFUtnoCKor5ueoTmWHFEnBicRhGd50aBBrR7A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

有了这个设置以后，内置的瀑布图就可以有更多应用场景，而不必总是使用自定义图表中的瀑布图了。  

**3\. CALCULATE语法改进**

之前当我们这样写度量值：  

> 高价产品销售额 =
> 
> CALCULATE(
> 
>     \[销售额合计\],
> 
>     **'产品表'\[零售价\]>AVERAGE('产品表'\[零售价\])**
> 
> )

使用时会报错：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOSR5KDAwS17PCsRsKQ80gHeiciaEdlichDLVnjsKq9ENS0ZcKDSlVFiacAqVXpejbp4TYPRbFyRSsbPg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

而现在更新后，这个 写法就不会报错，可以正常计算了。

因为CALCULATE 和 CALCULATETABLE 函数过滤器中布尔 (True/False) 表达式，现在可以直接使用聚合函数。与之前必须用FILTER函数相比，代码更加简洁，新支持的语法提高了 DAX 表达式的可读性，并且不会影响性能。

**4\. 新的按钮选项**

PowerBI中的按钮十分常用，现在它支持更多格式选项，包括新的形状、

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOSR5KDAwS17PCsRsKQ80gHsjBaicf2eHHwOaQITMXfngSyk6ibZXUpsx8hRAxZLhStgTs402zrhvKg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

自定义图标的样式和位置：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOSR5KDAwS17PCsRsKQ80gHrn5H3S1s8RXRkGZmJY5RyYF66MvDFGQNiaSlgbr7kLV2v4HNvPiceUEg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这些可以帮助我们设计更丰富、更精致、更细腻的可视化效果。

关于9月的更新就简单介绍这些，更全面的可以去看官方博客或者我的视频号中观看中文字幕的视频讲解。

___

PowerBI每月更新后，如果不能自动更新或者不方便下载，可以在公众号后台发送"**软件下载**",获取最新的PowerBI Desktop安装包；

如果要下载历史安装包，也可以发送**6位年月编号**获取，比如发送“202102”获取2021年2月的安装包（2021年2月是支持win7的最后一个安装包）。

___

**[PowerBI商业数据分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)**

帮你从0到1，轻松上手PowerBI

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNuVIqc0mzbKDNPmI0mwcTkvUibMVjf4z1bY0MYFh7lAkqrcHiaEHE4UicvjJjibpmkxJjc4TDlVO04qg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPUabZXugXKNdmeUzxwJM4OyUpTibBJjoq1jk8CzVZJz6s4nJRW1ViammT4ecqAJ7iapDccKNNrwtLYQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077212&idx=1&sn=bb3dac9becf80b5d929e5dc8405158dd&chksm=8e13a84bb964215d6362f78768cdefa18def4dfc8cd5c14f075442431604ed9c9729e4051a4b&scene=21#wechat_redirect)

[](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077048&idx=1&sn=b3da0a4079ed8366c67982912e795d59&chksm=8e13ab2fb964223978c16d5647e4a28eaeb50bc7338c4e82f4e14f2cddc8bb844b956f09beb6&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

↑ 扫码加入，和 3k+ 学习者一起成长
