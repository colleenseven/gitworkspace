---
notes: False
aliases: null
create_date: 2022-10-04T17:44:57 (UTC +08:00)
tags: wx/pbi/可视化图表
pagetitle: Power BI如何制作漂亮的玫瑰图？
source: https://mp.weixin.qq.com/s/sYL7FCpJdRwwPAg__Cyz8w
author: 采悟
status: 已完成 
category: 浏览文章 
uid: 
---

有星友看到网易数读上的这个图表很有特色，问我这是什么图，以及在PowerBI能不能制作这样的图表？

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNZpt24h2co1tspSIIsW7vjEkWiaYOXEVYqEDjsHKZGCALlvsw7yBZHcQKvMuAibs4Pz43APQewBvLw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

网址：https://www.163.com/data/article/HFN186H3000181IU.html

这个图表是玫瑰图，也称作<mark style="background: #FF5582A6;">南丁格尔玫瑰图</mark>，最早是由弗罗伦斯·南丁格尔绘制，因此该图用她的名字来命名，来纪念这位伟大的护士和统计学家。

玫瑰图类似一种<mark style="background: #FF5582A6;">圆形的柱状图，以扇形的半径来表示数据的大小</mark>， 那么如何用PowerBI来制作玫瑰图呢？

以上面图表中，各地区生均校舍面积的数据为例，来看看如何制作玫瑰图。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPg0QEjBw7THnrW5jp1F0H6v1cvcGLdMV4Sic0ibwxh7WZq9mw9libp38bnkniatWlu8oV5lZOfVURpWQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

内置的可视化对象里没有这种图表，在自定义图表中有两个视觉对象可以制作玫瑰图。

**1. Aster Plot**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNZpt24h2co1tspSIIsW7vjoMb3VQmj3cTGWF6VKLUOaibNURUEToE3jRL9iaqudiad8gMMlKYqWibFBw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

Aster Plot使用起来很简单，只需要将两个数据字段放入到图表中即可：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNZpt24h2co1tspSIIsW7vjpHhcbfFvyYzW3JZ5slqpSgZQwxgSC5dAP7XwDRhu5yDzzsZc6ySVhQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就可以很简单的实现玫瑰图的效果，不过Aster Plot的格式设置十分简陋，连最基本的的类别标签也无法显示，这就让该视觉对象的应用场景十分有限。

**2. Charticulator**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNZpt24h2co1tspSIIsW7vjJ7X4KTfb3K26e4Gl9hDEsib9h3ET2SWLmyvElcKficsw1axc9px61VwQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

Charticulator不是一个图表类型，而是一个十分强大的可视化工具，关于它的用法，之前专门介绍过：

[在Power BI中轻松使用可视化神器Charticulator](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484075663&idx=1&sn=0e005a834d40ec83e13432eac3791af3&chksm=8e0c5658b97bdf4e6c27a3fd5998b9a45e6d54cd578da2efa35181ea6ce35767aec268075dd2&scene=21#wechat_redirect)  

在Charticulator的模板库中，有一个玫瑰图，我们可以直接导入这个模板文件制作。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPg0QEjBw7THnrW5jp1F0H6KKzRhpCm0zmHJUK7MAicGDN7J5AWjyiaNtsHXQZMEEx2S6XXbJDjueibA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关于模板如何应用在上面[charticulator的文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484075663&idx=1&sn=0e005a834d40ec83e13432eac3791af3&chksm=8e0c5658b97bdf4e6c27a3fd5998b9a45e6d54cd578da2efa35181ea6ce35767aec268075dd2&scene=21#wechat_redirect)中也有介绍，点击几下鼠标就可以获得如下的玫瑰图效果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPg0QEjBw7THnrW5jp1F0H6Yu7u6ndGTbQtiaqudJpgAw8HNPutksmPtfEBF6iajaQPicKhlD7QO5TUQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

并且图表的各种元素都可以进行自定义调整，在上图的基础上继续调整格式，比如调整颜色：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPg0QEjBw7THnrW5jp1F0H6wcML6el0HibHjewNgdxXol6nAFm5fj84ETGxrxVHTticRhmGGPmMYgWw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

添加数据标签：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPg0QEjBw7THnrW5jp1F0H686xAbqoYqTl2ECqBY0kYibJh7VMjcHvF1BeptoSXJvcXG5dG5ic1q9icg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

简单调整后的效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPg0QEjBw7THnrW5jp1F0H6jvKgEf794HSlKDE9eicT2wAibMBPNZPxIZWKdibLWian58OicCO213e1DEQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

虽然没有做到网易数读的效果完全一致，但也很不错了。  

关于玫瑰图的制作，建议使用上面第二种方式。其实不仅仅是玫瑰图，如果你有个性化的图表展现需求，而PowerBI中没有合适的图表可以用，那么就可以尝试使用Charticulator，熟悉它的操作和用法后，它就是一个灵活、免费、无代码实现各种可视化效果的好帮手。

本文示例文件可以在公众号对话框发送"PowerBI玫瑰图"获取。
