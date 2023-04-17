---
create_date: 2021-07-02T19:44:55 (UTC +08:00)
tags:
aliases:
pagetitle: Power BI条件格式规则，你知道怎么设置吗？
source: https://mp.weixin.qq.com/s/OcpsF_TKV9EduXPdv_JrJA
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

本文介绍一个好用但也非常容易设置错的功能：条件格式规则。

当我们需要按不同的规则来设置图表元素的颜色时，就会用到这个功能，以下面这个简单的表格可视化为例：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNGZPkLT5R0IubKzBibzYVK1zkxe2Licib6BBatCBZaW6xicaFCIj7rauaIeKPBmMURnjQ1f73IbvTqLQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**如果想让同比数据大于等于20%的数据背景显示为绿色，小于20%的数据背景显示为红色**，就可以利用条件格式>背景色：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNGZPkLT5R0IubKzBibzYVK1ybMuKciaFgFojGXzd00PaIz251nHiakTavfKe5AYPO66tkFsnHGHznDA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后点击“高级控件”，在弹出的窗口中，格式模式选择为“规则”：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNGZPkLT5R0IubKzBibzYVK1cXRCL6fqr1KIP9ERXmqDIZ6HcVx9VdV6DN4NPneWXelFfFbtxuESIg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

根据上面的需求，以同比数据20%为分界点显示红绿色背景，很多人是这样设置的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNGZPkLT5R0IubKzBibzYVK1YP7l9v6h1OHe6o5ufkoYkDu6MR6qFfa0aMgOKrDxAdhtiaicRThohNCQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

看起来好像没有问题，但这样设置的结果是这样的：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNGZPkLT5R0IubKzBibzYVK1OFhr6mpZwR9P5LOdlIUUSg8JxPecPruaslXGO2epT6dfJIb5SCic4BQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

是不是比较困惑，明明是设置的高于20%的数据背景显示为绿色，为什么19%、5%甚至-1%也都显示为绿色了呢？  

这是因为条件格式的规则，**"百分比"并不是指实际数据本身，而是数据在该字段中所处的相对位置，100%代表该字段的最大值，0%代表该字段的最小值**，而设置低于20%显示红色，是指在这一列数据中，根据最高和最低值，位于最低的20%的数据显示为红色。

以上面的同比数据为例，最高数据为35%，最低数据为-11%，那么20%的分界点可以这样计算出来：

> （-11%）+（ 35%-（-11%））\*20% = -1.8%

所以只要同比数据大于等于-1.8%，背景就会显示为绿色，这就是上面19%、5%和-1%背景显示为绿色的原因。  

那么如果想让同比数据大于等于20%的才显示为绿色，应该怎么做呢？

直接按下图这样设置就可以了：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNGZPkLT5R0IubKzBibzYVK1ZicUFrVS8T5cZ6kicyKHAib59sTo9cwmSjicXW37YzHvQR2DYvJp33lxNg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

表格显示的结果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNGZPkLT5R0IubKzBibzYVK1INMgzWVibZqrXyPep6xnvzoRS8L7HEibEkpq2QAEzaOyJTQy0kCRJe9Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

正是期望的结果。

这里关键是要理解"数字"和"百分比"，"数字"就是数据本身，"百分比"是指数据所处的相对位置。

这个规则设置的是，大于等于数字0.2，并且小于等于百分比为100%（表示最大值）的数据，显示为绿色；而大于等于百分比0%（表示最小值），小于数字0.2的数据，显示为红色。

所以不要看到同比数据格式是百分比，就把规则全部设置为百分比，其实同比数据本身就是一个正常的数字而已。  

这样设置也解决了很多人提到的，规则无法设置小于某个值的问题，比如对上面的表格中的数据列，设置大于等于600的显示为绿色，小于600的显示为红色，你会发现，规则中第一项只有大于、等于或者大于等于，并没有"小于等于"这个选项。  

那应该怎么做呢，有些人会设置为大于等于一个非常大的负数，小于等于非常大的正数，如下图：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNGZPkLT5R0IubKzBibzYVK18xvYnwWCVg1YVhUXg6ZTFayYaX3fbkt3RicRyoOQLibUicrPP4GlTbBkA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

一般情况下，这样设置可以满足需要，但并不能绝对保证没有例外的数据，并且这样设置也不是这个规则的初衷，正确的设置方法应该是这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNGZPkLT5R0IubKzBibzYVK1SyFYpoiaNbdmMRhMvglmnTFjhPf76gukyHv4ib9W9lE8kQAib0XGfUY3g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

不用写一个非常大的负数或正数，只要设置大于等于最小值（百分比：0%），小于等于最大值（百分比：100%），就能实现这样的需求了：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNGZPkLT5R0IubKzBibzYVK1cH1DLicAs398cewRJibfMYopRmpEZROwkLJBlOiaia81FAqRtFx4Sib04mQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

上面的介绍是以表格可视化为例，其他可视化图表的颜色设置中，如果支持条件格式，也都可以按这种方式来设置规则。

___

**[新书上市：PowerBI商业数据分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)**

帮你从0到1，轻松上手PowerBI

___

\-精彩推荐-

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072351&idx=1&sn=fabb08c54790ac1225b470fd647c7a5e&chksm=8e0c4548b97bcc5e0450f1945a2c76039bbb42650bcb1edbc856820836d63d32af4c7780e31a&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 3k+ 学习者一起成长
