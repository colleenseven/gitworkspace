---
create_date: 2020-11-15T23:47:12 (UTC +08:00)
tags: 
aliases: null
pagetitle: PowerBI 2020年11月更新，这两个功能很好用
source: https://mp.weixin.qq.com/s/RKXTnAKzsV9eQwM2EwsBFA
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

PowerBI 2020年11月的更新如约而至，发布的一长串功能虽然没有重大更新，但在外观、操作、功能、工具提示等方面有很多优化，这些细节在使用时更方便，你可能感觉不到，以为本来就是这样。正是这些长期的、细微的改进，使PowerBI越来越贴心，越来越友好。

官方博客的介绍非常详尽，我不再赘述，如果想看官方的视频介绍，可以在我的视频号上观看，已加上中文翻译字幕。

这里挑选两个大家可能都会用到的功能简单介绍一下。

**1，可视缩放滑块**

现在可以将缩放滑块添加图表中，缩放滑块为报表创建者和使用者提供了一种简便的方法，无需使用过滤器即可检查图表中特定范围的数据。

内置的可视化对象中，XY坐标系的图表几乎都支持该功能，比如折线图、柱形图、组合图、散点图等，首先在格式窗格中启用缩放滑块。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP6ia63Kz7seibVJxiaZddcrqNKN6eqfaMNjO01b8hAhDLMV8VKpYyXA3VgRSI2LV0pPABNUhvLaOZVw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以根据需要打开X轴、Y轴的滑块，打开后，就会在图表坐标轴旁边看到滑竿，单击并拖动它们之间的栏即可查看某个范围，效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJP6ia63Kz7seibVJxiaZddcrqNYVUIXYBTtibRxD8OA8w0enfftLaKicONtzHvMn0D1icbGp09wiacWNFiaiaQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

保存和发布报告时，视觉效果的缩放状态也将被保存。最终用户打开报表时，缩放滑块的端点将默认为您保存的端点，从而可以突出显示特定的数据窗口，同时保持其上下文可立即访问。

**2、异常检测**

异常检测可通过自动检测时间序列数据中的异常来帮助您增强折线图。它还提供了异常的解释，以帮助进行根本原因分析。只需单击几下，您就可以轻松找到见解，而无需对数据进行切片和切块。

这个功能目前还是预览，首先在选项>预览功能中勾选：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP6ia63Kz7seibVJxiaZddcrqNxyPkO5e2nJlnQNjz1OowRBahqnWjLHibZm8XRIM3QPDTPYSFbKJhTHg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在单系列折线图的“分析”面板中，可以看到"查找异常"：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP6ia63Kz7seibVJxiaZddcrqNecPZjB9ft6QYw7PkwR9ymh71SP2PVAofP47v6bNS8J1maUnbSEib31Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

添加后折线图会自动丰富，显示预测的范围，如果在预测范围之外，就会标记为异常值。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP6ia63Kz7seibVJxiaZddcrqN6GBcOYMqOIAyxj6ibp8c38NRvKO9ricXjlgUzPoe0tlac9ESxq9PbpKQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

异常值的标记算法主要取决于敏感度的设置，如果提升这个参数，算法将变得更加敏感，即使是变动比较微小的数据，也被标记为异常值。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP6ia63Kz7seibVJxiaZddcrqNIdicodic9RGzSJ9b3QtSsErWzpD1uRUWbDUpsfMwb6etwR6UkY4A6s8g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以在解释依据中自定义添加分析字段：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP6ia63Kz7seibVJxiaZddcrqNQgYsYg2m9dNDXGLnOjmkJr1p048ZSJjvbBicquDXdcSJoQ9O6pWvKFQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

单击折线图中的异常标记，即会运行分析算法，弹出分析面板，系统将解释异常的影响因素，这和关键影响因素的效果（[尝鲜Power BI的AI黑科技图表：关键影响因素](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068371&idx=1&sn=497a7574a9d1a8a69d7d5e90f3ac6d64&chksm=8e0c4ac4b97bc3d2bbde4d08927abf4a1f25ae5dcf0c8cf01ed9e45b63a21fe1d3ad7db3b2f7&scene=21#wechat_redirect)）很类似。 

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJP6ia63Kz7seibVJxiaZddcrqNZk2vic3kV1DPhzPwYw5JYDaAibfrUKY5ztd9Sg1EOE9DjNr4UuRFgh4Q/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

打开下方的某个影响因素，即可看到该因素的影响情况，还可以将解释的结果添加到报告上。

异常检测的格式设置也非常丰富，可以调整预测的背景颜色和透明度、以及标记的颜色和样式。

以上就是这两个功能的简单介绍，你可以尝试使用，更多介绍请参考官方博客，或者关注我的视频号，观看官方介绍视频自行探索。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP6ia63Kz7seibVJxiaZddcrqNBaIOvSjwFXrCicvtibIdxZYpibMlibx0ytFFFF0CHxhQ3K1A2YCtdvosicg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

PowerBI每月更新后，如果不能自动更新或者不方便下载，可以在公众号后台回复"软件下载",获取最新的安装包。
