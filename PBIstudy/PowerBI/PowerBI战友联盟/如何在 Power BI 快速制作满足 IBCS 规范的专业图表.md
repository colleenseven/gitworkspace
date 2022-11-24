---
create_date: 2022-01-20T13:36:23 (UTC +08:00)
tags: 
aliases: null
pagetitle: 如何在 Power BI 快速制作满足 IBCS 规范的专业图表
source: https://mp.weixin.qq.com/s/TrjBey5M5Ks6YesVIougqg
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

使用 Power BI 一月内 的小伙伴在思考的是：如何做出一个图表。

使用 Power BI 三月内 的小伙伴在思考的是：如何做出一个酷酷的图表。

使用 Power BI 一年内 的小伙伴在思考的是：都有哪些酷酷的图表可以用。

使用 Power BI 一年后 的小伙伴在思考的是：如何做出一个有业务价值的分析型图表。

Power BI 的图表叫：视觉对象。它从设计的时候就没有考虑要实现特定于业务本身的分析。

我曾在这个方面做过大量研究和尝试，结论就是：

在原生图表和分析型图表之间有一个鸿沟。

目前来看，Power BI 产品组是不准备填上的，因为不够通用。

这就导致在这个领域沉浸多年的一家小公司的分析型图表借助 Power BI 平台快速成长并发挥价值：Zebra BI。

在如何选择图表方面，他们按照分析型的需要，塑造了更适用于分析的图表。

在近日，为了方便大家选图，Zebra BI 用 Power BI 做了一个图表选择器。我们对此进行了中文化（纠正了原来的某些错误，可能是他们团队非资深人士做的），现在给到大家使用。另外，后续我们还会发布独立的图表选择器，来帮助大家快速实现图表的构建。

需要的伙伴可以加入我们的微信群。

## 如何选择一个图表

打开图表选择器，根据你的需要，你可以直接选择到你需要的效果。如下：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/09hv4Xua0LMnOmGmfGacNT99YPnrw7Jyfiaq5Q8aF9u6ibhiaO34OC0yfzH2oJS0euZDSWibNu1OuXRwkGOESnVG8g/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

通过这个图表选择器可以快速实现对图表的选择了。

## 选择器

这里实现了一个选择器：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMnOmGmfGacNT99YPnrw7Jy5HmgcEOR9R489sdxFIFtibZKIRAXzPugJ99ib2fa2oP35HfnDibw32aYA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果想要选择某个图表并查看下介绍，可以点击某个图标跳转到对应页面。

## 水平对比图

使用水平对比图，可以快速定位到所要关注的数据（如：上月销售额），在不同数值之间进行对比，并观察数据所呈现的趋势（如：甚至某些数据呈现线性增长或季节性规律）。水平类型图常常用于表示时间维度（如：年，季，月）。时间维度应该从左向右。

如下：

## 垂直对比图

使用一个度量值在多个元素之间进行对比，排名，标识特定值以发现数据的规律。若要对离散元素（如：产品，客户，科目）进行分析，应该使用垂直方向的图表。垂直方向图表可以方便的显示元素标签或集成到表中更直观的显示数据。

如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMnOmGmfGacNT99YPnrw7Jy7V7ibwShAOknCNHRxQY4lcQZlic67XaK4Ttx1RGQ6jsBpXvIPuGGPUFA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

## 堆叠图

堆叠图可以帮助分析某个值的内部构成关系（如：对总销售额来说的每类产品的销售额）。这种分析可以快速看出每一部分相对整体的关系。

如下：

## 系列对比图

由于系列对比分析可以允许同时呈现更多数据，所以它是对单个指标对比分享的增强。一种典型的案例就是将本期实际与目标，去年同期几个系列一起看。既可以随着水平轴放置时间维度（年，季，月，周）来看趋势；也可以随着垂直方向放置离散元素构成的维度（如：产品，客户，科目）等来进行对比。

如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMnOmGmfGacNT99YPnrw7Jy7kibJ169DhHicR54C1uVicaXpn4LBvQbHGtmjJJL3Wm2BETic6ohFuyaJg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

## 水平差异图

差异图用于对比两个系列并计算每个元素对应度量值的差异。这是商业报表成功的关键构件所在。这同时还需要一种很简单的可被直观理解的方式构建。其中，绝对差异表示按绝对数值反映两者的差异；而相对差异则按照百分比反映两者的差异。水平差异图，更适合时间序列上产生的差异问题。

如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMnOmGmfGacNT99YPnrw7JyOoqe7asdEic9qYSf9cv9SFLHSMPosLsgqYvRiaEowpbibZ5YnXBYUN2hA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

## 垂直差异图

差异图用于对比两个系列并计算每个元素对应度量值的差异。这是商业报表成功的关键构件所在。这同时还需要一种很简单的可被直观理解的方式构建。其中，绝对差异表示按绝对数值反映两者的差异；而相对差异则按照百分比反映两者的差异。垂直差异图，更适合分析结构上产生的差异问题。

如下：

## 集成差异图

集成差异图用于同时显示值以及差异。因为将值和差异同时显示，就可以直观地看出差异及其占据实际值的大小。这是管理报表中最重要的图表之一。

如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMnOmGmfGacNT99YPnrw7JyibSU9csRUzJvHnQOmV6EnFicvzeTVWocUsLZK0VyRP4F7ZpWAKbGQkeQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

## 差异构成图 - 瀑布图

构成分析（又称：贡献度分析），是用来反映构成整体的各个部分对总体的构成贡献度的。这是基于柱形图（条形图）已经有了表示整体的度量值后，在其内部构成元素已经用条形图表示的进一步优化。常常形成：瀑布的形态。故又称：瀑布图。它常常用于直观地解释总体为什么发生了变化。典型场景包括：利润分析，构成分析等。

如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMnOmGmfGacNT99YPnrw7JyYIVxwSARxnwEoqEiaUkdn7Q3CicwzkHnzUITgy8m0Dib4rxzmRLXwHN1g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

## 扩展图表

扩展的图表是将多个图表合并的强大模式。在一个视觉对象中，可以将不同主题的图表进行合并，其好处在于共享一个单位尺度标准，这为数据的可视化分析提供了更多信息密度。

如下：

## 组合图

组合图是专门为了显示有两套坐标体系的图表的。如：同时在一个图中按百万单位来显示销售额，且按百分比显示利润率。

如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMnOmGmfGacNT99YPnrw7Jy29C5PY0ttOKT1PR9ibh4W1vV2ZfrqRYConAAmBs3F4b3Z3xXZt4vWdQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

## 小多图

小多图（又称：格架图 Trellis chart）是一种用于在同一报表页同时显示对比图表的非常强大的方法。与使用各种零散的图表相比，小多图具有的明显优势是：它让所有的图表使用了同一的坐标尺度以及同样的外观，这可以实现对多个部分对比的快速可视化。

如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMnOmGmfGacNT99YPnrw7Jyk627LhMWApKRUsAwRFpsanRibbJUjnbTicib7vWtLBATAPQR6w4NHXMAQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

## 总结

虽然说 Power BI 除了原生图表以外还有 300 多种可视化图表可以在 Power BI 的图表库中进行选择，但我们并不希望真的去研究这么大的范畴，从业务分析本身而言，我们更希望将精力集中在具有规律的图表，保持业务驱动。

Zebra BI，在这方面无疑做得非常好。如果你还没有用过 Zebra BI，可以试试了，如果你还不知道 Zebra BI 怎么用，我们会推出相关专业课程，不用着急。

最后，这个图表选择器工具已经发布，如果需要使用，可以点击【阅读原文】即可。

另外，我们也会在群里交流使用这个工具的方法，如果你感兴趣，也可以加入。

就在

**excel120.com/find-chart.html**  

扫码加入交流群  

建议阅读：

[PowerBI 被吊打，如何从数据中获得切实可行的商业见解](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650791478&idx=1&sn=9872b8db3253949a08d81385d4f753c7&chksm=f18cde27c6fb5731d1b0d6e24c4dde2d925c8e2183ddc33d5930cdc82b54bbcfbaaa69a66286&scene=21#wechat_redirect)  

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNhia5Pc4XC1Um7IYgQhGEoEC1yK05ibUFoPBYpcoAMvibuZh2BZaibMzULeDwNfSeQ0KHRcDUdX3FzVA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

与精英一起讨论 Power BI，验证码：data2022  

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOiad5BOrdQTKpB733esKiaxZa53LXWIPlQicMjxntaRr3a2hnMmuibTib8QacXeiakucDr7lSNGkuV2MXw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击“阅读原文”在线使用选择器

**↙**
