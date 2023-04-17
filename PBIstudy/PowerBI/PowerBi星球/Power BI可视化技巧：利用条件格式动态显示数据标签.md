---
create_date: 2023-02-01T23:33:56 (UTC +08:00)
tags: wx/pbi/DAX函数 
aliases: null
pagetitle: Power BI可视化技巧：利用条件格式动态显示数据标签
source: https://mp.weixin.qq.com/s/0xY9IqKvIv07fdu6zpwKgQ
author: 采悟
status: 已完成
category: 精读文章
notes: False
ZK: Origin
uid: 
---

DAX ::  IF,MAXX,ALLSELECTED,SWITCH

在走势图上进行特殊标记，只显示某些点的数据标签，之前介绍过利用多个系列来实现的方法，参考：  

[PowerBI作图技巧：在走势图上标注最大值、最小值…](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068479&idx=1&sn=f96bf83e4f0705aecbd1960dac731ae9&chksm=8e0c4aa8b97bc3be08566dea69e91093e6383bc45c21a9a3cb149d83797c91f0f17a02e68aa8&scene=21#wechat_redirect)  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPCWuRtTZ5D49T8IznjSyNYXxFoxG6cQp3k5pTU2z3nibEWpuicUicib3cxEia64wm0Ox5N7Ljd4ib5kQ8A/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

还有个更简单的方法，就是==利用数据标签的颜色条件格式，让标记的点的数据标签显示出颜色，其他点设置为透明色==，就可以实现了。

还以上面文章为例，写个度量值让折线图只显示最大值和最小值的数据标签：

> 最大最小标记 =
> 
> IF(
> 
>     \[指标数据\]=MAXX(ALLSELECTED('日期表'\[日期\]),\[指标数据\])||
> 
>      \[指标数据\]=MINX(ALLSELECTED('日期表'\[日期\]),\[指标数据\]),
> 
>      **"#000000",**
> 
>      **"#00000000"**
> 
> )

其中"#000000"表示黑色，   "#00000000"表示透明色（参考：[Power BI公式中表达颜色的3种方式](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484083399&idx=1&sn=7f6901c85eb1243517c3888a6eb51dc7&chksm=8e13b010b96439062501809eb1fa6ecdfc2980a52df1ee41c86a23be089101323b40268b72c9&scene=21#wechat_redirect)）。

然后点击数据标签颜色的条件格式：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNok2EZZXFTicYUibsDrbeyHYibLl3uKxmIAuNjYc5jjtAnjqW9seJLRWO3XklhDkcGpI4e0UQrl0Vvg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

设置为字段值，选择上面建好的度量值：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNok2EZZXFTicYUibsDrbeyHYiadwWUoVmf6Y4ntSGue00axR67tvaVrYmr0VaBvx8qcdRAyhtBxmGOg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

就实现了只显示最大值和最小值标签的效果：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNok2EZZXFTicYUibsDrbeyHYVDTNUB4icHDv1B6luiakbTpbWeuRTJ0jeIVq8hicPTPuSZzJAficjl3yuQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

如果想让最大值和最小值显示不同的颜色，只需要对最大值和最小值分别判断，来返回不同的颜色代码就可以了，比如最大值显示为绿色，最小值显示为红色：

> 最大最小标记 =
> 
> SWITCH(
> 
>     \[指标数据\],
> 
>     MAXX(ALLSELECTED('日期表'\[日期\]),\[指标数据\]),**"green",**
> 
>     MINX(ALLSELECTED('日期表'\[日期\]),\[指标数据\]),**"red",**
> 
>     **"#00000000"**
> 
> )

效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNok2EZZXFTicYUibsDrbeyHYBj6cGhicckMZEib1jyOtAc7r9VKray2iboIxLnxcq9RcHiaVRxuWsaIQicw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

不过通过条件格式的方法只能设置数据标签的颜色，无法单独设置数据标记，如果需要突出显示最大值和最小值的标记点，可以选择前面介绍的方法。

如果不仅仅只显示数字，还想直接显示出“最高”、“最低”的文本，就需要利用计算组才能实现了：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP6g2CKCaFIHNPwj29EQJuXdIGPCAJxu59YJIibib6cYjmmIZJIm0J2sMpSSXq7ebcuqVSH714O4wbQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这种方式之前也介绍过，你可以参考这篇文章来回顾一下：  

[利用PowerBI计算组，设计个性化数据标签](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076121&idx=1&sn=505f2d704bb46b641d21900a1fa9c3f6&chksm=8e0c548eb97bdd985786642ae697183cda036d6418757981aea2a380921a78b2af3d59b6cc7a&scene=21#wechat_redirect)
