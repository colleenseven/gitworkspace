---
create_date: 2022-02-09T13:35:06 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI 中的十六大功能图标你都认识吗
source: https://mp.weixin.qq.com/s/2poPWiX0oIQTmOQDj6kc_A
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

Power BI 中有不少功能，很多特定的功能都有不同的图标，所以，可以看图标来识记功能。

你看看以下这 16 个图标以及功能你都玩过了吗？

准有一个你没用过，看你可以挺过几关。

## 数字字段图标

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPA2QibtJ8Mib0iaGlpp4ZJ8LPwoTWnMf1IaGxCqia61KvbcwvgFmdlGGdvhvFc36WKlzVibhyFh3o16vg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

例如，数值字段是可以求和或求平均值的聚合。聚合随数据一起导入，并在报表所基于的数据模型中定义。

## 计算列图标

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPA2QibtJ8Mib0iaGlpp4ZJ8LPTdJAa8UbN4A6EQK8B6S0s1l9LPU03R6078hAX4D2qnnqqqXvPbx2Yg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

非数值数据类型的计算列：使用数据分析表达式 (DAX) 公式创建的一个新的非数值列，该公式定义该列的值。

## 度量值

度量值：度量值有自己的硬编码公式。报表查看者不能更改此计算，例如，如果该计算是求和，则只能进行求和。值不会存储在列中。它们是动态计算的，具体取决于它们在视觉对象中的位置。

## 新文件夹图标

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPA2QibtJ8Mib0iaGlpp4ZJ8LPWiaNK3lbhVoOQ6sp8FuEicAOHX1qQsHPkmqFQjF60hqpuvRzIAwW4GicQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

“字段”列表中的文件夹。

在页面：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPA2QibtJ8Mib0iaGlpp4ZJ8LPkhZncZLkeJF6KdAIHh5ic2E28Z02FsD6x4hSOkiaDSibdliaXYHkrIFrIg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

对度量值进行设置，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPA2QibtJ8Mib0iaGlpp4ZJ8LPHLTfNp2ZqOgI2TIylibYYk9lxicD2SHYGnxaWAv1XHsc5ic3vSjkOEtUw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

## 数值计算列

数值计算列：使用数据分析表达式 (DAX) 公式创建新的列，该公式定义该列的值。

> 💡 注意
> 
> 与  不同，一个是数值类型，一个是非数值类型。

这关你过了吗？😊

## 度量值组

一个导入的表（不是计算表），除了度量值以外，全部是隐藏字段，就成为：度量值组。且位于数据模型所有表的首位。

所以，这个东东不是一个 BUG，是 Power BI 产品组内部存在的一个特性，且名字叫：度量值组。（与计算组不是一回事）

## KPI

它是一个视觉提示，用于传达针对可度量目标已完成的进度。

由于 Power BI Desktop 自身无法创建这个字段，很多人并没有用过。

> 💡 注意
> 
> 该字段没有实际独立存在的功能意义，因此，可以永远不用它。

## 字段的层次结构

字段的层次结构：选择箭头以查看构成层次结构的字段。

> 💡 注意
> 
> 这是一个非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常非常的字段。
> 
> 这么写，你懂了吧，很多人的确用过这个特性，但是大家并没有注意到它的真正价值。
> 
> 后面，我们已经有一个项目（代号：wxcj 无限层级生成器）完成，随后发布，将为您带来对这个特性的新认知。这个特性几乎是解决很多问题的根本技术，敬请期待。

## 地理数据

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPA2QibtJ8Mib0iaGlpp4ZJ8LPjEf8KAPqTnpT1uwXenictDTMQ1D5QkoyIiarBCUsLt7IHVXfQ1avIg7Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这些字段可用于创建地图可视化效果。

## 标识字段

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPA2QibtJ8Mib0iaGlpp4ZJ8LPGKhO8Nw4SpbibGIzQYsk5jFwO3l0JApd7MCOibKTkuWJv01V5oWZpLSA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

Power BI 文档对此的解释是：具有此图标的字段是“唯一字段”，将被设置为显示全部值，即使它们具有重复项也是如此。例如，数据中可能存在两个名为 Robin Smith 的不同人员记录，每一条都将被视为唯一。它们不会合成一条。

> 💡 注意
> 
> 经过测试，与 Power BI 文档的说法不同，具有重复项的字段拖拽到界面或者参与 DAX 计算，都会被当做同一个值，并不会因为设置了这个字段标识而有不同。

而真正的不同在于：

在使用 Power BI 的 QA（NLQ 自然语言问答）的时候，如果你问：显示用户表的用户，作为这个字段会被作为这个表的标识列而显示出来。

关于如何使用 NLQ，我们会再专门介绍。

## 参数

设置参数以使报表和数据模型的某些部分（例如查询筛选器、数据源引用、度量值定义等）依赖于一个或多个参数值。

## 内置日期表的日期字段

带有内置日期表的日历日期字段。

## 计算表

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPA2QibtJ8Mib0iaGlpp4ZJ8LPQUcL4uStomwgecFGclnA22EbpJymHbwiaWEswVw1XhVm5XtVhlgqPHw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

基于已加载到模型中的数据使用数据分析表达式 (DAX) 公式创建的表。这类表最适合用于中间计算，且最好将其存储为模型的一部分。

## 警告

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPA2QibtJ8Mib0iaGlpp4ZJ8LP4xuKKcGfEFXj3v4wDKo2YKIOH96cBuGbDJHibb2clu2esGSWbiaL6bFQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

带有错误的计算字段。例如，DAX 表达式的语法可能不正确。

## 组

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPA2QibtJ8Mib0iaGlpp4ZJ8LPgiaw8nG3KH5yNxVxZk4CUia4ib4CCn7Njv3icTVYK6MC5QrzJ95zM1CLcA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

此列中的值基于：使用组和箱功能对其他列中的值进行分组。

## 检测度量值

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPA2QibtJ8Mib0iaGlpp4ZJ8LPxrZhewAcQlFT3sm7Eh1KZ3AsGvmEL5BoJCiaHl0GNCENT7LAmVLlEtg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

当你配置页面以进行自动页面刷新时，可以配置更改检测度量值，通过查询该度量值可确定是否应更新页面的其余视觉对象。

这个字段在实时报表中很有用，此前介绍过，后续会进一步来说明。

## 总结

十六个功能图标你用过了几个呢？

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNhia5Pc4XC1Um7IYgQhGEoEC1yK05ibUFoPBYpcoAMvibuZh2BZaibMzULeDwNfSeQ0KHRcDUdX3FzVA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

你可能感兴趣：  

[

新春献礼：微软官方 Power BI 技术最佳学习去处 全免费

2022-02-07

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/09hv4Xua0LORflVMyAMJ6DZq1vLdQcZHJXZIWkicia6iclkvkJH3IdZSZILWQbFGYEQspzU23a8ib0BbZz2otvNHtQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

](https://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650791776&idx=1&sn=c5d068895692b70ab9ed65a43d36df64&chksm=f18cdf71c6fb566709c970393a8bd09bb4b23ca543cf7a41e6b6fb92a3a983f019bc1fd83e9f&scene=21#wechat_redirect)

[

Power BI 内网穿透精灵 正式发布

2022-01-26

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/09hv4Xua0LMM8pfz8zG2jur7bbtqggT3EWT4TqEOXsdibDccNFaXttvK0cW1z5TPjPmpxLZ82RM9fc3vAQj6DrA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

](https://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650791754&idx=1&sn=363b9edbb16bb7923e7338175a0f23a9&chksm=f18cdf5bc6fb564d995b451e08b2caba2f9dbd64add1f8b0734892f9d899eade4fbbc500fa39&scene=21#wechat_redirect)

[

Power BI 可视化大全，可直接下载 383 案例

2022-01-21

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/09hv4Xua0LPYHHFZjI13iaJRq4vk1wdd7HkzAkE4bwgmZLtF2KRnuhIibibJHyW7qATG5b1YIMLTu8hxXECibUkUiaA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

](https://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650791732&idx=1&sn=3b2b313e46d43745b83a091a1c390037&chksm=f18cdf25c6fb563383f0995956a5bb05c93f02307876d58e6b2c1be0764d7e05ebf9782dc708&scene=21#wechat_redirect)

[如何在 Power BI 快速制作满足 IBCS 规范的专业图表](https://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650791720&idx=1&sn=f69de52e600ad7609327e03e7ea5c19a&chksm=f18cdf39c6fb562f38be4e703a0583ea9473a06e2e97ad6e58188e942fd8588f4b44e46ff76e&scene=21#wechat_redirect)

[2022-01-20](https://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650791720&idx=1&sn=f69de52e600ad7609327e03e7ea5c19a&chksm=f18cdf39c6fb562f38be4e703a0583ea9473a06e2e97ad6e58188e942fd8588f4b44e46ff76e&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/09hv4Xua0LMnOmGmfGacNT99YPnrw7JyIqKOxAFWuVlBXiaYVKuvQicGBFxFvyyaU7yjibCkHiaKtk5bpwjez1mfqg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](https://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650791720&idx=1&sn=f69de52e600ad7609327e03e7ea5c19a&chksm=f18cdf39c6fb562f38be4e703a0583ea9473a06e2e97ad6e58188e942fd8588f4b44e46ff76e&scene=21#wechat_redirect)

**Power BI 终极系列课程《BI真经》**

[

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/09hv4Xua0LNBM1lxlQYHJBicic4CvPoRGLqHgdTZOr8goNRh0asDXA48mRDzc9zxW4UMQiayHwgDmx7mlt4cQxtjg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

BI真经 - 让数据真正成为你的力量





](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650788512&idx=1&sn=76972ff4b0cf265fe9479c6457b04b47&chksm=f18cd2b1c6fb5ba7386eb0bb835280bd8a651bfe0481cc78f20fc30b80c60d2d4cb7eb5b1e3e&scene=21#wechat_redirect)

扫码与精英一起讨论 Power BI，验证码：data2022

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOiad5BOrdQTKpB733esKiaxZa53LXWIPlQicMjxntaRr3a2hnMmuibTib8QacXeiakucDr7lSNGkuV2MXw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击“阅读原文”进入学习中心

**↙**
