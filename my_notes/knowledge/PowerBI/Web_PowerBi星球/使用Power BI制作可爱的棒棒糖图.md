---
notes: Fa'l'se
aliases: null
create_date: 2022-01-23T12:29:39 (UTC +08:00)
tags: 
pagetitle: 使用Power BI制作可爱的棒棒糖图
source: https://mp.weixin.qq.com/s/zDwcIjcDzkAFzekwSxosdg
author: 采悟
status: 未阅读
category: 
uid: 
---

棒棒糖图，Lollipop chart，也叫大头针图，是传统的柱形图/条形图的一种变体，在柱形的顶端凸显一个大圆点，来突出数据之间的相对位置，相比柱形图/条形图更加简洁、更具吸引力，因其形似棒棒糖、大头针而得名。  

很多工具都可以制作这个图表，有星友问用Power BI如何制作棒棒糖图，这里简单介绍几种制作的方式。  

内置可视化对象没有这个图表类型，在PowerBI的自定义视觉对象库中，搜索"Lollipop",就可以找到下面几个图表：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMHdfFMzopM2xoABVqaD8Yu4X3iaswlwXLQ6kevl4C9Qw7qbSicQYRZdVXEeZBZvUbp1IFtwgrAiaF7Q/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

下面来看看这几个图表的效果，并介绍其他几种制作方式。

以显示每个产品的销售额为例，这个图表具体制作步骤非常简单，和制作柱形图类似，不再着重介绍，主要来看看这几种方式的效果和特点。  

## **1、Lolipop Bar Chart**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMHdfFMzopM2xoABVqaD8Yu821qQmo5EYOeFGZ38BxGmJnoqRKXhChQLI1p3clfhzXzA0SOiccqV7A/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这是一种条形的棒棒糖图。

## **2、Lolipop Column Chart**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMHdfFMzopM2xoABVqaD8Yuy2WaDYSsZ5TiaslfaibcfDYMbT8t0DibhvPrRLq7iade35saicXicRgMJViaw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这是柱形的棒棒糖图。  

以上两个图表为同一个公司发布的，在PowerBI Desktop中可以随意使用，但是发布后，如果未付费购买，将无法使用，所以如果不打算购买的话，上面两个就不建议使用了。

**3、Lollipop Column Visual**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMHdfFMzopM2xoABVqaD8YuYHP0SkSPnojlVN9WqZDItUeurGZukUY5Lfk6RiblsMKxUqfua4VIgicg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这算是中规中矩的一个棒棒糖图，虽然自定义设置上比较简陋，但是完全免费，需要的时候可以尝试使用。  

在自定义图表库中，还有一个图表Lolipop Chart by Visualizeit，这个图表对中文支持不友好，不推荐使用，这里就不介绍了。

除了上面的自定义图表，在PowerBI中还有下面三种制作方式。

**4、利用Charticulator制作**

Charticulator是非常强大的无代码图表设计工具，可以直接在PowerBI中使用，对于棒棒糖图，有现成的模板，可以在官网下载：https://charticulator.com/templates.html

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMHdfFMzopM2xoABVqaD8YuQlesAColJJ5kBoAta3TtrK5m7mKwFcCgHOaXvDyZC2Zia9dg2QibNNhw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

具体使用方法参考：[在Power BI中轻松使用可视化神器Charticulator](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484075663&idx=1&sn=0e005a834d40ec83e13432eac3791af3&chksm=8e0c5658b97bdf4e6c27a3fd5998b9a45e6d54cd578da2efa35181ea6ce35767aec268075dd2&scene=21#wechat_redirect)  

其效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMHdfFMzopM2xoABVqaD8YuSjciaqxiahUKT987jdGnGP05r0wncAGnJQAnDAA7balZegAich5ghQNibg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

掌握Charticulator图表设计的基本操作以后，你还可以对这个图表做各种细节的调整。  

**5、利用矩阵的迷你图制作**

这是迷你图功能的一个巧妙应用，具体制作方法可参考佐罗老师的文章：[如何在 PowerBI 中实现矩阵行中迷你图棒棒糖](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650791575&idx=1&sn=ea43a07b2f631ea4cad0ff8d69d2ba7c&chksm=f18cde86c6fb5790d0738e91c28c4573cff078c8d8027f5fff3350aabe73e8c5e1789ee3a7ed&scene=21#wechat_redirect)

**6、利用DAX+SVG制作**

这种方式也非常灵活，利用DAX就可以制作出各种效果，包括棒棒糖图，如果感兴趣可以参考武俊敏老师的文章：[使用公式花式制作条形图](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247487240&idx=1&sn=b4e076eb10214fe2e05dc99734b0c101&chksm=97db3658a0acbf4e51e6beac9664a76c3929a02e001e351f4fd787ba15ca8ba482e7ee1771fd&scene=21#wechat_redirect)

上面就是PowerBI中制作棒棒糖图的几种方式，其灵活度、难易程度各不相同，如果你的报告中想用该图表展现，可以动手尝试，选择一个最适合你的方式。  

[**PowerBI星球的最新版****内容合辑****，值得你收藏学习：**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078675&idx=1&sn=07abf841815e43fb0a554081c82de72a&chksm=8e13a284b9642b92d07b518abe3e6e2e2ef5066c0941c1ced26a245a6990b4330830431789a9&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN8YOicNXzCaSLpQrKXOL0LsNeYw0fj3iaGFy7XSwwmibHicdtiaHEbhgmHSPXQlkg3WiaVA4hJ8PGDcdEQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078675&idx=1&sn=07abf841815e43fb0a554081c82de72a&chksm=8e13a284b9642b92d07b518abe3e6e2e2ef5066c0941c1ced26a245a6990b4330830431789a9&scene=21#wechat_redirect)

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
