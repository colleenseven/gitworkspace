---
create_date: 2021-06-20T19:51:59 (UTC +08:00)
tags:
aliases:
pagetitle: 图表太多不知道用哪个？让PowerBI可视化辞典来帮你
source: https://mp.weixin.qq.com/s/T4aLk1bLs5TZiarXoRvWhQ
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

PowerBI可视化图表类型众多，内置的加上自定义图表库中，现在已经超过300个各式各样的图表，它们为报告设计提供了更多可能性，但同样因为数量太多，也给人带来了困扰，作图时总是拿不准该用哪个？

今天分享一个PowerBI可视化辞典，帮你更轻松的选择合适的图表来展现数据。

___

  

几年前金融时报的视觉团队曾做了一个可视化辞典，以帮助大家更快更佳的选择图表类型，如下图：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOpGrbBXPUYTJkdLpy6ucEFkYHduiaZmyOshqj6ZuqMfl6c8jRibU9RseibIRblabOAfhvuWBNnYoMIw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

根据展现的需要将可视化分成9大类别，72个主要的图表类型，并对每种图表的使用场景做了说明，微软工程师Jason Thomas在此基础上，复现了一个PowerBI版的可视化辞典。

PowerBI版的可视化辞典制作相当精良，可以说是PowerBI可视化的集大成，每类分析一个页面，每个页面是该类分析推荐使用的图表，每个图表标注了主要使用场景。一个报告融合了几十种视觉对象，不仅可以帮你选择合适的图表，还可以了解这些图表的用法，下面让我们浏览一下。  

**离差**

Deviation

强调相对于一个固定参考值的变化（正╱负值）。通常参考值为零，但也可能是一个目标数值或是长期平均值。也能用来展现态度倾向（正向╱中立╱负面）。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOpGrbBXPUYTJkdLpy6ucEF41fiaHWKiabZTAvGibeTCaJe1VotOhSpC5LfsXJt7PjXRL1HibUj8x507g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**相关性**

Correlation

展示两个或多个变量之间的关系。要注意的是，除非你特别说明，许多读者会认为你所展示的两个变量之间存在因果关系。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOpGrbBXPUYTJkdLpy6ucEFfzI7gY47YIvbicGUKFsEvbhLfrbaRcZckwhDmDqRRbhuyDuFrSHnhFw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**排序**

Ranking

当某个项目在排序列表中的位置比其绝对数值或相对数值的大小更重要时，使用这种图表。不要害怕强调出需要关注的重点。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOpGrbBXPUYTJkdLpy6ucEFoLQwC1AHlChD6dbVZQ8RZJoWzJqJPXbpnJPWnibJMLqM03xQr6rgRRw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**分布**

Distribution

显示数据集中的数值及其出现的频率。分布的形状（或偏离程度）是突出数据的不一致或不平均的方便记忆的方式。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOpGrbBXPUYTJkdLpy6ucEFMO8OuKaWICeUnUtgHOto4icwdoz6IqA4T4vZEyvIEicHicTic4jrFAXAZQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**随时间的变化**

Change over Time

强调趋势的变化。有可能是短期（一日内）波动或长到数十年或数百年的改变。为了向读者提供适当的背景信息，选择正确的时间段很重要。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOpGrbBXPUYTJkdLpy6ucEFickZCoIE5FM0ohadIxAoobP9wIHNqs5hicg7TOLoibg7ia2Mdibj48ayVgg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**规模**

Magnitude

用来比较数据的规模。有可能是比较相对规模（显示出哪一个比较大），有可能是比较绝对规模（需要显示出精确的差异）。通常用来比较数量（例如桶、人、美元），而不是经过计算后的比率或百分比。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOpGrbBXPUYTJkdLpy6ucEFIj9hXD9AJDsc0PzbSn4F4VHzkaWliamCyvc4ktibVnn76kN3MPq5EytA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**部分和整体**

Part-to-whole

能显示出一个整体如何被拆解成不同组成。如果读者只是想了解个别组成部分的大小，不妨改用规模类的图表。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOpGrbBXPUYTJkdLpy6ucEFVrUKy7wnvub54t6ibLbNxQguH7MJaNIoVQHWialZ3NdkMGs6QQgicKUrw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**地理空间**

Spatial

当数据中的精确位置和地理分布规律比其他信息对读者来说更重要时，可使用这类图表。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOpGrbBXPUYTJkdLpy6ucEFlqF6Fqlwn9H8QzctxqAKN1YjYED95WbWCjK4GS8EynVnckGBMwuLgg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**流向**

Flow

向读者展示两个或两个以上的状态、情境之间的流动量或流动强度。这里的状态、情境可能是逻辑关系或地理位置。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOpGrbBXPUYTJkdLpy6ucEFJOlVIEWu1UHZeoq38es30iaYNEuDO59kOaeSA4Ca5JSrprxcI4fmSFQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个报告基本涵盖了平时可能会用到了各种图表，每个图表的格式和配色处理的非常细腻，虽然有些是天天在用的图表，看到这个也让人眼前一亮。

其中有少数图表，利用PowerBI现有的内置或者自定义图表是无法完成的，作者采用了Charticulator 定制可视化图表，以及利用了R和Python来作图。

如果使用了R/Python视觉对象，但是你的电脑中没有安装软件或者缺少对应的程序包，打开时会出错，作者非常贴心的用一张做好的可视化图片覆盖到视觉对象上，这样无论任何情况下，打开看到的第一眼都是完整的可视化报告。

并在报告顶部放置了一个勾选框来让用户选择，如果想查看R/Python可视化代码，去掉勾选即可。

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJOpGrbBXPUYTJkdLpy6ucEFdeLNfJEEyrFqRShQevjTHUo2aIStibfT5CpYQ6Rodsyr9lOayic0X7LQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

如果你对PowerBI比较熟悉，应该能想到这种操作其实是用书签实现的，技术并不难，但思路非常巧妙。所以这个可视化辞典不仅仅是指导你如何选择图表，里面涉及到的报表设计思路，同样值得借鉴。

关于该报告的更多细节，这里不再详细介绍，在「PowerBI星球」公众号后台发送"PowerBI可视化辞典"获取pbix源文件，大家可自行探索，学习借鉴。

___

  

**618限时优惠活动进行中**

扫码立减50元，PowerBI星球社群最后一次这么低价，感兴趣的星友不要错过了哦~  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNKwl8qibtr4ZxJ7WPtps7CJMHA1vEqTmWWpyDWxfbMJPiamUDJiaJHCKugTdIyLfpUmhWLofHFS3tBw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**▼****点击****阅读原文****，也可立享优惠~**
