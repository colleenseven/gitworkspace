---
create_date: 2023-04-13T11:02:51 (UTC +08:00)
tags: wx/pbi/数据处理功能 
aliases: null
pagetitle: Power BI 2023年4月更新，你应该知道的一些变化
source: https://mp.weixin.qq.com/s/OYGQW6TnrvVdTQdR8UEdwQ
author: 采悟
status: 已完成
category: 浏览文章 
notes: False
ZK: Origin
uid: 
---

PowerBI2023年4月更新来了，这次更新带来了非常实用的==动态格式字符串和新的DAX函数==，关于本月的更新你可以在官方博客中浏览全面的介绍，点击最下方的阅读原文也可直接进入：

https://powerbi.microsoft.com/zh-cn/blog/power-bi-april-2023-feature-summary/

还可以在视频号中观看本月更新的微软官方视频讲解（已加中文字幕）:

这里我挑选几个你应该用到的更新带你浏览一下。

**1\. 度量值动态格式字符串**

这个功能期待了很多年，现在终于到来了，就是度量值可以动态的显示不同的格式，之前可以通过计算组来实现，字段参数也稍微解决了一部分这个需求，而动态格式字符串则把这个功能彻底实现了。

现在还是预览功能，先到文件>选项>预览功能 中勾选它。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMsNhzHiatNJDuHliaCbqpHBDxhKOvoicsYneXV57V09s6txkLR57G8w92xFCGlK0SxOemZHDrobwLIg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

然后当你选中一个度量值时，在格式下拉框中，就可以看到动态。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMsNhzHiatNJDuHliaCbqpHBD5a0EHtHmTklp8miaicLFDOrmGmsv9IoYiahg624yJ19SFcamVvooyWsJA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

点击进去，就会出现格式设置的编辑框。

仍以前面介绍的动态数据格式为例，之前计算组的解决方案：

[PowerBI设计技巧：动态数据格式](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074205&idx=1&sn=d8c9d1a3f80245e6e3b1f5bd2d14a053&chksm=8e0c5c0ab97bd51c1cdcc44737ff0967f5179b716c5f0bc90c87abcd977153b10cd11cdc3219&scene=21#wechat_redirect)  

虽然难度不高，但是需要依赖外部工具来实现，步骤比较繁琐，门槛也相对高一些，现在直接在PowerBI窗口通过动态格式来设置非常简单。  

选中指标数据这个度量值，然后在编辑框中写DAX，根据不同的情况来设置不同的格式：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMsNhzHiatNJDuHliaCbqpHBDUIibWqbpYIib2OiaRGrhZqiapu9eESPL1ib1YrKLzwOhQkyJPQaR1wiaVMoQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

然后用这个度量值作图，就可以动态的根据上下文，显示相应的格式了。

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMsNhzHiatNJDuHliaCbqpHBDPFEfnQgOLKITrn9w8S6RJQJS1Bmsvr454JNBVgtyK83bzfWM9tlHAw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

并且在DAX编辑框左侧增加了下拉选项，便于查看度量值本身的公式以及格式的公式，可以编辑修改：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMsNhzHiatNJDuHliaCbqpHBDC5pM4EdLha9u1JLYLics5zp5CeFjvnPibPqj1T2hVzDUrThJaeZOWZmw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

通过这个功能，设置图表的动态格式就方便、灵活多了，之前很多需要计算组的做法，现在都可以不再用了，之后会再单独介绍它的更多应用场景。  

**2\. 更新ORDERBY函数**

去年底新增了三个新的函数：

[Power BI本月正式推出的DAX新函数：OFFSET、INDEX、WINDOW](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484083291&idx=1&sn=18c13a35482f8e36820368e5afb095ce&chksm=8e13b08cb964399ab081b2a692fd7ee8f9084104dc756f254a2182798ae93ded282579a8b706&scene=21#wechat_redirect)  

不过其中的ORDERBY参数之前只支持列字段，现在终于支持度量值了，相当于为这几个函数解除了封印，功能和灵活性大大增强，应用场景更多，后面我会单独介绍它的用法。  

**3\. 新的DAX函数：RANK和ROWNUMBER**

又是两个非常震撼的新函数。

==RANK返回当前上下文的排名，看名字好像是RANKX的简化版，其实完全不是这样，它不像SUM与SUMX的关系，事实上，RANK比RANKX更加复杂，参数也完全不同，它更接近于WINDOW等窗口函数的用法==。  

==ROWNUMBER返回当前上下文的行号==，也是个非常刚需的函数，之前在可视化表格中添加的动态序号，非常困难，现在这个需求就会变得简单很多。

不过它们的用途绝对不止于表面的功能，这两个新函数，以及前几个月发布的OFFSET/INDEX/WINDOW，他们将会带来PowerBI的视图层计算时代。

大家先有个印象或者去动手摸索一下，后期我也会单独重点介绍。

本月的更新就简单介绍这几个，更全面的功能可以去看官方博客继续探索。
