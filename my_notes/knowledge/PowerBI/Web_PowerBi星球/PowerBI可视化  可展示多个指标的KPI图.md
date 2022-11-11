---
aliases: null
create_date: 2022-07-26T12:27:12 (UTC +08:00)
tags: wx/pbi/可视化图表
pagetitle: PowerBI可视化 | 可展示多个指标的KPI图
source: https://mp.weixin.qq.com/s/WlsQ0SsnAFd9HoF2h3_NaQ
author: 采悟
status: 已完成
category: 浏览文字
uid: 
---

我们经常有<mark style="background: #FF5582A6;">展现多个指标的需求</mark>，在PowerBI中有多种方式可以实现，今天推荐一个非常好用且免费的视觉对象，帮你轻松的实现这种需求。  

这个视觉对象就是近期刚上架的Multi targetKPI:

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOuIuSxDjVKtPIjibMQ4RUbJLzclZXQsMBul7f6OqyF2ZKDE3CdKRMy6Bib5k1tUgWywPfia5UJVicXUw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

它使用起来很简单，可<mark style="background: #FF5582A6;">展示一个主要的指标，和不超过3个的附加指标</mark>，只需要将相应的列字段或者度量值放进去就可以了，下面我放入了几个度量值。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOuIuSxDjVKtPIjibMQ4RUbJJeTe5G84nZHLpQViasb4xQGDN3GjvJsU5mW7NoVfaFWTic41oibgbxyaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果发现数据不能正确显示（如上图），可以在格式中找到每个指标的显示单位，改成"无"，以主指标为例，调整方式如下图。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOuIuSxDjVKtPIjibMQ4RUbJUEGeyXgmtjUaUVAJH7DGXIFa5fBNnmyxnNPdj9hr1iabSNUWPFgSEsQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

把相关指标的单位调整好以后，就可以得到一个显示多个指标的卡片图：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOuIuSxDjVKtPIjibMQ4RUbJWNXfBq7ZFEqgbjNFaWPibmxO1oWPFNnVADWudG9G2y9OlyPpuYHX59Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

除了可以展示多个指标，这个视觉对象的格式设置也十分丰富，可以对主指标、附加指标、类别和卡片图等元素进行自定义调整。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOuIuSxDjVKtPIjibMQ4RUbJCr87nDpG0uuAc2Cd2HJuV8GMSIFZz2JgSm1BPCeac06DlJBYaoVuvw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

下面介绍几个主要的格式调整和外观展示样式。

**<mark style="background: #FF5582A6;">附加指标调整为水平显示</mark>**

附加指标设置中找到“Layout type”，调整为“Horizontal”：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOuIuSxDjVKtPIjibMQ4RUbJP1331KaurxIb3hzEPmX4c8scxToDaNhGHD76rMJrt0HQTYpsjTP6zQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOuIuSxDjVKtPIjibMQ4RUbJdEZmSeia4drql7ic1cJAYrn35UvWAWrQiaZEISicic5dPlrUl70b6pqNWpQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**空白拦截**

使用内置的卡片图时，如果没有数据，会显示为“空白”，需要用度量值去修正，但在这个视觉对象中，可以<mark style="background: #FF5582A6;">在设置中阻止“空白”，而不需要额外的方式</mark>，非常方便。

在格式中找到这个选项，打开，并设置无数据时显示为“-”。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOuIuSxDjVKtPIjibMQ4RUbJGPyg4Pc84iazSbM6UpvBk6XPV020tEBU2jgCYOGdHXZtTG0PSdoqe4A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

当某个指标无数据时，就会显示为"-",而不是“空白”。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOuIuSxDjVKtPIjibMQ4RUbJUY4kQT55wQSqotXL9rksbWnk73BYauIzZoibYduOR9dMEOjctibGbcdg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**<mark style="background: #FF5582A6;">按条件设置颜色</mark>**

支持对每个指标按照一定的条件来显示不同的颜色，比如对于上面的目标完成率，完成目标显示为绿色，未完成目标显示为红色，可以这样设置：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOuIuSxDjVKtPIjibMQ4RUbJ45OwncqreNPu8o0jXWbgEOxYdvcicwSBSpozuY9ZWYf9ibazF8YLMlWg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOuIuSxDjVKtPIjibMQ4RUbJy12m3R1N6hvCWKmGT6vAylbsuofz2dEccgLoQhRWnH3UPjUADC3luQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**<mark style="background: #FF5582A6;">批量显示多个卡片图</mark>**

还可以在这个图表中类别中加入字段，就可以批量生成多个卡片图，比如将产品类别放到里面。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOuIuSxDjVKtPIjibMQ4RUbJySicqHBHiakblv1Hb7Gr1TRlR72yqWgjAia5Iy9VXiaiatiabVHZW8RIrvAQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个图表就会一次显示每个类别的卡片图：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOuIuSxDjVKtPIjibMQ4RUbJcAKfPQkaPibfYjRLWXf5NibNkRGO0eoVqwj9pcVo8MxHjCHV5iaCFdtiaw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

是不是非常便捷，并且这个图表还完全免费，直接在市场中加载即可使用，当需要同时展示多个指标时，可以试试该图表，你也可以摸索该图表的更多用法。  
