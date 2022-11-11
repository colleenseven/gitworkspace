---
aliases: null
create_date: 2022-01-26T12:29:05 (UTC +08:00)
tags: 
pagetitle: PowerBI可视化技巧：如何在矩阵中动态标记最大最小值？
source: https://mp.weixin.qq.com/s/xJQ302Dw95VS7N9BvjqRPQ
author: 采悟
status: 未阅读
category: 
uid: 
---

遇到星友的提问，如何在矩阵中动态标记出哪个数据是最大值、哪个是最小值呢？  

这个问题比较普遍，因为矩阵作为最常用的视觉对象之一，它展现的信息量最为密集，如果不做任何标记，很难快速找到关键的信息，这篇文章就来介绍如下，如果在矩阵中标记关键性的最大值和最小值。

以下面这个矩阵为例，行字段为产品名称、列字段是年度月份，展现的是每个月每个产品的收入：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMdI24iaex1UOnS5AEosyORleGtjgDW0jRIYu8GoTNBRF8q4vUyNNsZmtCfGVGDYp3cicf5E6aLiadOg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

只靠眼睛观察，是不是很难看出哪个是最大值，哪个是最小值？

矩阵中的最大最小值有几种标记方式，按照每行、每列还是对整个矩阵进行标记？假如最大值标记为绿色背景，最小值标记为红色背景。  

**1、标记每列的最大最小值**

对于上面的矩阵，标记每列的最大最小值，就是找出所有产品在每个月份的最大最小值，可以用下面度量值来实现。

> 每月最大最小值标记 =
> 
> VAR t=CALCULATETABLE(VALUES('产品表'\[产品名称\]),ALLSELECTED())
> 
> RETURN
> 
> SWITCH(
> 
>     \[收入\],
> 
>     MAXX( t ,\[收入\] ),"limegreen",
> 
>     MINX( t ,\[收入\] ),"red"
> 
> )

这个度量值的主要逻辑是，先利用变量构造出每个产品的虚拟表，并对这个虚拟表，计算出其对应的收入的最大值和最小值；并判断当前单元格的收入，如果等于最大值返回绿色，如果等于最小值，返回红色。

打开矩阵的格式面板，在“单元格元素”中（之前的版本是条件格式），打开“背景色”，点击fx按钮：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMdI24iaex1UOnS5AEosyORlNJmDoehH6praBMrQySoT8fhVb8Ck2mKRHNerw4hR6KgdSSHQEwPg3A/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

然后在弹出的窗口中，格式样式选择“字段值”，下面的字段选择上面建的度量值，如下图。  

这么设置以后，矩阵的效果如下：

这样清晰标记出了每一列的最大值和最小值，通过颜色就可以直观看出，每个月贡献收入最高的大都是VR眼镜，而数据线的收入贡献一直都是最低的。  

并且上面的度量值中，VAR定义的虚拟表t，用了ALLSELECTED，返回的产品名称列表就是动态的，计算出的最大最小标记也是动态的，比如放置个产品类别切片器，选择“手机配件”，矩阵只显示属于手机配件的产品收入，最大最小标记也在这个范围内进行每列标记：  

手机配件中，收入贡献最高的产品位置被充电宝和耳机占据。

**2、标记每行的最大最小值**

每一行的数据，是一个产品在各个月份的收入，标记每一行的最大最小值，可以先构造出每个月份的虚拟表，上面的度量值修改成下面这样：

> 每个产品最大最小值标记 =
> 
> VAR t=CALCULATETABLE(VALUES('日期表'\[年度月份\]),ALLSELECTED())
> 
> RETURN
> 
> SWITCH(
> 
>     \[收入\],
> 
>     MAXX(t,\[收入\]),"limegreen",
> 
>     MINX(t,\[收入\]),"red"
> 
> )

同样按照上面的方式，设置背景色，效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMdI24iaex1UOnS5AEosyORl6T2elibmZ7mckD0ZF4y4xxrJk1LjK5Ma8wtLdvSvv10CpYoJIvLrCKg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这样标记，也可以很清晰的看出，一般是在3月收入最低，而年底的2个月收入通常是最高的。

**3、标记整个矩阵的最大最小值**

找出整个矩阵的最大值和最小值，和上面的思路一样，构造行字段和列字段组合的列表，对这个列表所对应的每个收入，计算出最大最小值，度量值写法如下：

> 全部 最大最小值标记 =
> 
> VAR t=CALCULATETABLE(SUMMARIZE('订单表','产品表'\[产品名称\],'日期表'\[年度月份\]),ALLSELECTED())
> 
> RETURN
> 
> SWITCH(
> 
>     \[收入\],
> 
>     MAXX(t,\[收入\]),"limegreen",
> 
>     MINX(t,\[收入\]),"red"
> 
> )

设置背景色以后，效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMdI24iaex1UOnS5AEosyORl57llEKWU7n9JWeWC46vwib5IyN3pRv5icNJIe34woiaib2JouCqHvuKAuA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

单月收入贡献最高的是2021年11月VR眼镜、最低的是2021年3月数据线。  

以上就是对矩阵的最大最小值不同的标记方式，关键是根据需要，针对矩阵每一行、每一列以及全部数据的逻辑，构造出对应的虚拟表，并对这个表计算最大值和最小值，如果单元格的收入等于最大值或者最小值，利用矩阵的背景色字段值规则，标记相应的颜色。

[**PowerBI星球的最新版****内容合辑****，值得你收藏学习：**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078675&idx=1&sn=07abf841815e43fb0a554081c82de72a&chksm=8e13a284b9642b92d07b518abe3e6e2e2ef5066c0941c1ced26a245a6990b4330830431789a9&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN8YOicNXzCaSLpQrKXOL0LsNeYw0fj3iaGFy7XSwwmibHicdtiaHEbhgmHSPXQlkg3WiaVA4hJ8PGDcdEQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078675&idx=1&sn=07abf841815e43fb0a554081c82de72a&chksm=8e13a284b9642b92d07b518abe3e6e2e2ef5066c0941c1ced26a245a6990b4330830431789a9&scene=21#wechat_redirect)

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
