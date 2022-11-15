---
notes: True
aliases: null
create_date: 2022-06-23T12:30:55 (UTC +08:00)
tags: wx/pbi/建模技巧
pagetitle: Power BI可视化设计：用文字展示切片器的筛选情况
source: https://mp.weixin.qq.com/s/rlUeB6WYoOfxZO_Yfr_y8g
author: 采悟
status: 已完成
category: 精读文章
uid: 
---

DAX:: SELECTEDVALUE, MAX,CONCATENATEX,VALUES,IF, COUNTROWS,ALL,ISFILTERED,NOT

---

最近遇到有星友问这样的问题，**如何在报表页面中用文字将切片器的筛选情况展示出来？**因为当报告中切片器比较多、或者切片器折叠起来时，是很难直观看出来到底都是哪些切片器被选中，以及选择了哪些项目的。

虽然PowerBI的图表标头中有个显示筛选的功能，鼠标放上去可以自动显示该图表的筛选情况：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMuv84Ae1sR3bYYb7cnOIhSHZfYnIvGellibGyIroEuRyeG4sk0twNviaB1TNql7ImYRvMJweOiciavSQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

但这个功能本身很隐蔽，用户可能找不到它，并且这一块在外观上也比较难看，影响整体的可视化效果，一般是建议隐藏图表的标头（隐藏方法参考：[PowerBI可视化报告美化的12个技巧](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484079925&idx=1&sn=32669d2ea59d10d480c386f4f2306d56&chksm=8e13a7e2b9642ef4a327fa1cb8cf7a3b33f4a371b23888b407c4824ab9bf9354b2f629f3584a&scene=21#wechat_redirect)）。

图表的标头隐藏以后，报表看起来是清爽多了，但如果想快速查看报表的筛选情况，应该怎么办呢？

本文就来介绍一个方法，<mark style="background: #FF5582A6;">利用DAX将切片器的筛选情况直观展示出来</mark>。以产品切片器为例，根据切片器的几种筛选情况，先来分别看看DAX是如何获取切片器状态的。  

___

**切片器单选**

单选的情况很简单，<mark style="background: #FF5582A6;">利用SELECTEDVALUE函数或者MAX函数都可以直接获取切片器当前的选项</mark>，度量值如下：

> 产品切片器 单选 \= SELECTEDVALUE('产品表'\[产品名称\])

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMuv84Ae1sR3bYYb7cnOIhSjbIIOsWxE4Kd5kJlnVRRPiaMJvz4qQmWriaFduhia53pMVnRnesmCzeMQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

**切片器多选**

由于度量值只能返回一个值，并不能返回列表，所以<mark style="background: #FF5582A6;">对于多选的情况，可以将多个选项利用CONCATENATEX函数合并成一个字符串来返回</mark>，度量值可以这样写：

> 产品切片器 多选\=
> 
> CONCATENATEX(
> 
>    VALUES('产品表'\[产品名称\]),
> 
>    \[产品名称\],
> 
>    "、"
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMuv84Ae1sR3bYYb7cnOIhSJnX9QluBD9LxHIgd7CwY3Z2Zfzhn3wmc01iaCS5ecqTsdP0BfdBeKzQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其实切片器多选的度量值也适用于单选，是更通用的写法，所以正常情况下，直接使用多选的度量值就可以了。  

___

**切片器全选**

如果<mark style="background: #FF5582A6;">切片器全选，并不需要将所有的选项都列出来，可以直接返回“全选”来表示</mark>，利用如下的度量值来判断是否全选：  

> 产品切片器 全选 =
> 
> IF(
> 
>    COUNTROWS(VALUES('产品表'\[产品名称\]))=
> 
>    COUNTROWS(ALL('产品表'\[产品名称\])),
> 
>    "全选"
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMuv84Ae1sR3bYYb7cnOIhSGtkY0Au61mxx5oT9RcatHWmzsXkGqAicdFQ6ric7onaGCvKUvkoIvQUw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

**切片器不选**

可以<mark style="background: #FF5582A6;">利用ISFILTERED函数来判断切片器是否筛选</mark>：

> 产品切片器 不选 \=
> 
> IF(
> 
>    NOT ISFILTERED('产品表'\[产品名称\]),
> 
>    "未筛选"
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMuv84Ae1sR3bYYb7cnOIhSIY7HAiaL9poOX8h0wQ7RIAq06GLDbPTYbl3vicb43XqwGGcSbLhrbX8Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

___

其实切片器不选，默认和全选的效果是一样的，都会显示全部数据，如果你想让切片器在不选的情况下，数据也不显示，可以参考这篇文章：

[PowerBI切片器，原来还可以这样交互？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074281&idx=1&sn=ea825a10f8bb56815772997dcccfff08&chksm=8e0c5dfeb97bd4e8b6bf810457b5c579cf6633545260ce2097d21bc48e187bd88f49f3c528bf&scene=21#wechat_redirect)

___

理解了上面几个度量值的逻辑，就可以轻松判断切片器的筛选情况了，单选和多选可以直接用多选的写法；全选和不选，一般情况下也可以只判断不选就可以，这样判断产品切片器的各种筛选情况直接写一个度量值：  

> 产品维度 =
> 
> IF(
> 
>    ISFILTERED('产品表'\[产品名称\]),
> 
>    CONCATENATEX(
> 
>         VALUES('产品表'\[产品名称\]),\[产品名称\],"、"
> 
>     ),
> 
>    "未筛选"
> 
> )

逻辑就是<mark style="background: #FF5582A6;">如果切片器被选中，则返回选中的项目（多个项目时，用“、”分隔），否则返回“未筛选”</mark>。

如果报表中有多个切片器，比如还有年份、城市维度的切片，也与产品维度一样，分别写度量值：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMuv84Ae1sR3bYYb7cnOIhSLBexFoaeBJvGA91nLIriarjOz7LU5LwT2ddza3JNYQqv0ACyibJhX4BA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMuv84Ae1sR3bYYb7cnOIhS9a637JQDFydvGvZibFCH297uPR5WF5SKp5TibzO6pHToicqSHEDwUyEtQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后在画布上添加个文本框，写入必要的文字并将上面的度量值放进去，就可以展示切片器的结果了，具体操作方法可参考：[利用Power BI智能叙述，生成动态报告摘要](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073801&idx=1&sn=3a6dcd73ed52e77a4159612fe49af3e7&chksm=8e0c5f9eb97bd68889ce7e6ae0af81e62b7ed6b7ea7827deb5ca1ba097c14e4965889736baa4&scene=21#wechat_redirect)

在文本框中，可以对不同的字符设置不同的颜色，稍作调整就可以获得这样的效果。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMuv84Ae1sR3bYYb7cnOIhSrMnXJiccln4RwxqAf6I777UMB5t5Th2yKRcGW3B2mne0bd9ZGS9yEJA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样看起来是不是非常直观呢，并且随着切片器的切换，文本也会动态调整，最终通过一个文本框就可以将报告中的筛选情况一目了然的展现出来。

你还可以在页面上设计个重置切片器的按钮，一键将所有的筛选切换回初始状态，参考：

[PowerBI报告设计技巧：一键重置](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073105&idx=1&sn=630078447d92ab54c9c049fb8a656953&chksm=8e0c5846b97bd150bd23d3af28b62bf9813d17b339a2a4199096cdb076fd664b0e744d2808b8&scene=21#wechat_redirect)

