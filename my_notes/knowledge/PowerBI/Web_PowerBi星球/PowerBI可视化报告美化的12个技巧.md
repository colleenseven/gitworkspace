---
aliases: null
create_date: 2022-04-26T11:52:57 (UTC +08:00)
tags: 
pagetitle: PowerBI可视化报告美化的12个技巧
source: https://mp.weixin.qq.com/s/YPIrftFDKyWhl8X7flQ6Lg
author: 采悟
status: 未阅读
category: 
uid: 
---

上周的文章介绍了参加PowerBI可视化大赛时[如何进行数据脱敏](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484079875&idx=1&sn=597bad738cd8be8cc19e43e4ab5620c4&chksm=8e13a7d4b9642ec2afc378f86f46551085aefea39b96f87f2bcfcd5783a64379ba605b3be102&scene=21#wechat_redirect)，而对于可视化大赛，更重要的是可视化效果，因此有不少参赛的同学问有没有一些可视化的技巧分享呢？  

下面我就分享一些提升可视化效果的技巧，希望对你有帮助。

这里并不介绍具体图表的制作和美化，主要从可视化的细节设计，以及报告的整体效果上，比如布局、导航、背景、封面、颜色的设计等方面，来介绍一些技巧和思路，你也可以做好报告以后，检查在这些方面还能不能做的更好。

**1、隐藏视觉对象标头**

在一个深色背景的报告上制作好图表，会发现右上角白色的视觉对象标头非常扎眼，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNnvIqQHgS8ljhgBkW34mXuxJic6FXtichJwIVfewcYkmMWnmXyCz8NB40QgGn5TwaQLoW0y9hFepiaw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以通过在选项>报表设置，勾选“在阅读视图中隐藏视觉对象标头”：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNnvIqQHgS8ljhgBkW34mXuj3piafcpWLWT9dBxgcJob0T65DyCnxgsQr5qFAjH5c4ibZDKeH5p2EyA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样的设置只在阅读视图中有效，也就是发布以后，不会出现白色的标头。

但是在PowerBI desktop编辑状态下，它是去不掉的，如果你实在觉得难看，也可以通过变通的方式来隐藏它。

在格式面板中，常规>标头图标，将它的透明度设置为100%，颜色设置为与背景色一致：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNnvIqQHgS8ljhgBkW34mXuafTrs9SznvnTh5frhX6CB7SgtsmFdEQkvP6rarZibydoAyrfrOb4GJw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后，即使在PowerBI desktop里面，右上角也不会再显示白色的图标了。

**2、对齐和分组**

对齐是可视化设计的一个基本要求，你可以通过鼠标框选住需要对齐的对象，然后点击上面的格式，对齐，来快速实现各种对齐和分布效果。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNnvIqQHgS8ljhgBkW34mXu9C8VNk5BBNGpk9FyYxdDJun1PmJOrle85HY2Ap8GCYa6D9f6ib7xywg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

对齐以后，你还可以点击上图中的分组，将对齐以后的对象组合到一起，这样就不会错乱了。

**3、锁定对象**

报告做好以后，页面上不仅有各种图表，还有会切片器、按钮等控件，可能鼠标一不小心就会移动某个对象，这个时候，可以点击锁定对象，将每个对象的位置固定下来。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNnvIqQHgS8ljhgBkW34mXuEmr7lMSRcN5mdT0ukMoEOIBeay3xEG5Vf4b4ghkwly0deDTibTTagRw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**4、切片器**

在一个报告中，切片器几乎肯定会用到，并且还会有专门放置切片器的地方，虽然每个人都会制作，但想要设计的美观以及与整体页面协调，还是要花点心思的。

关于切片器的设计你可以参考这两篇文章：

[玩转PowerBI的切片器，看这篇就够了](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074560&idx=1&sn=7050c2194d5e0a5587ec6282ff17b4ad&chksm=8e0c5297b97bdb81d70e9a7ece3d0d557a1fe58fe7102ceedec734222a89777e8724f784acfe&scene=21#wechat_redirect)  

[利用PowerBI的这个控件，美化你的切片器](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073642&idx=1&sn=d4e57071dc6421b4bb2f0bc9fc1e51b2&chksm=8e0c5e7db97bd76b1e9de73326a5676b2b5aeca519c036bbc9a30ee7a15075145783e09c55b8&scene=21#wechat_redirect)  

**5、标题**

每一页报告都应该有个标题，这个虽然简单，但是不要忽略它的作用，标题可以是本页面的分析重点、可以是报告的名称，也可以组织的名称。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNnvIqQHgS8ljhgBkW34mXubsbMZMAtgJVtiatn28gr1iabwn5Bgic8xPUbrVCicDPbnlEgbFI7hY3iaicQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**6、页面尺寸**

这是以前可视化大赛的一个作品，很多人问怎么能做成这么长的页面：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPu3qgz7pfVFLSWSOyGp0t6lCz5F8wONdsnDTng1Cq96VRy1Es6DCoToUw44sD59T5brYBLgqhic8g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其实只需要设置页面的尺寸和比例就可以了。

PowerBI默认的页面比例是16:9，正常情况下不需要更改，如果你想设计成竖长型的报告，还可以自定义尺寸：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPu3qgz7pfVFLSWSOyGp0t6305pPP1ibPfle4r4QgEiaIAlQL5fW1ftmjHmnTQwbtpvuWoNyxHLrBTA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

尺寸设计好以后，还要结合页面视图中的这几个选项才能看到效果，一般设置为“适应宽度”，你也可以每个都尝试一下，体会一下他们的效果。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPu3qgz7pfVFLSWSOyGp0t61Ta7q3rIlSNJ0icSBZrAPicalqSDubsHgXWpVmEJG0kJqGSBzBVByDxA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**7、布局**

合理布局是可视化呈现的关键，可以做一页图表，看看怎么摆放更美观，或者先在纸上简单画出来你的报告效果，有了整体的布局思路以后，建议直接使用背景图片来固定布局，然后报告上的元素只需要摆放到对应的位置上就可以了，见下面关于背景图片的介绍。  

**8、导航**

一个多页的报告，不要点击下方的页码跳转，使用按钮制作导航交互起来更加平滑和自然。

现在PowerBI中有自动的页面导航器，不过不够灵活，个性化设置也很简陋，建议自己用按钮来设计。

**报告发送之前，一定要测试导航的效果，保证能够流畅地进入任意一个页面，也能从任意一个页面返回到初始页面。**  

**9、页面背景**

页面背景或者叫画布背景，承载着主要的可视化呈现效果，你平时看到的惊艳的PowerBI可视化报告，背后几乎都是靠背景图片加持的。

所以一定要重视页面背景图片的应用和设计。

并且PowerBI并不能灵活的设置字体、也没有太多的设计素材，你想做的很多设计元素、细节点缀，都可以在背景图片上完成，只需在PPT中设计好这张图片就行了。

比如上面提到的标题、布局和导航的背景，都可以在背景图表的设计中完成，下面就是用PPT制作的一张图片。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNnvIqQHgS8ljhgBkW34mXuicvqUkvrf27M8Y1UwWFbpsibFxyaShsD5I7icrpkA0HNiaicRI2G3eiaAnOg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后将其插入到PowerBI页面的背景中：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM2V42z6Z0yfB5UwSQUUxgPcl2OhIgPIxUsZia5LeNODiaGs07jibUn4Xs1CKBqowzIG1RhXMFZE2W6Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后只需要将图表、切片器摆放到相应的位置就可以了。

**10、壁纸**

壁纸与页面背景的设置类似，都是在页面视图中设置：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPu3qgz7pfVFLSWSOyGp0t6KK5mOYk4HbEvCH8TwNWl2D2ItAThMAyARLE2gY1tpibL2HMevDZA05Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

壁纸与画布背景不同的是，它会铺满整个屏幕，包括画布外围，比如这个报告背后的图片就是一张壁纸。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPu3qgz7pfVFLSWSOyGp0t6vU5ibBTOia9xSz4cjo7YCW0ZkQtRC4yRtD3ZLejwF8gYjpAYlJ4m6uJw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

一张合适的壁纸可以让报告的整体效果看起来更大气。  

**11、封面**

首先并不存在一个封面页的功能，它也是一个普通的页面，只是我们可以把它打造成报告封面的效果。

封面是用户打开报告后第一眼看到的页面，所以必须要设置的美观一些，你可以选用一张合适的图片，并添加必要的信息，比如报告的名称、组织的名称和logo等，作为该页面的壁纸。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPu3qgz7pfVFLSWSOyGp0t60GQuXZia2hHA3S1GibYxNsbHypkfdYhhS1thcO1jMvH12mzBkWojbb2Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

除了美观，它也是进入具体分析页面的入口，所以封面上的导航设计非常重要。  

除了用静态的图片作为封面，你甚至可以用动画效果来设计：  

关于PowerBI中动画的设计，你可以参考：[Power BI报告中的动画效果，利用这三种方式轻松实现](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484079628&idx=1&sn=adf62bc59f2690799929803cf6ca0f27&chksm=8e13a6dbb9642fcdf86e9e5f74f80e7b317cb7c7f94e603a895ae3a3c38a909ee14edf9e043a&scene=21#wechat_redirect)

**封面页设计好之后，记得将其他页面全部隐藏，只显示封面页。**

**12、颜****色主题**

色彩的重要性不言而喻，通过设置主题可以快速调整整个报告的颜色：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPu3qgz7pfVFLSWSOyGp0t6xnr5QRDO6Hqnhl1NvfxwxppIZJ7HFGHNRk34zFYxdlomwJAQ8Kibbmg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关于主题的设置和技巧，你可以参考：

[如何在Power BI中随心所欲的搭配色彩？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068978&idx=1&sn=33c435da5b89e10b7ba3a2a908746aec&chksm=8e0c48a5b97bc1b3d5be5769b95d148813985a7c13ab3f3f5b294abc4e8a5829dec2719deb90&scene=21#wechat_redirect)  

[如何把PowerBI文件中的图片和主题导出来？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068491&idx=1&sn=68fcac7d1713f271e189d00d20385ce6&chksm=8e0c4a5cb97bc34ac4f3cd671fb7840ab22c7c64ae23aa79294f2c7f40494e2e17548c7c07f4&scene=21#wechat_redirect)  

上面的介绍的技巧，有些操作性的功能，通过动手摸索一下就可以快速学会，但是有关设计性的东西，比如配色、布局等，都不是短期能快速提升的，但有个捷径就是模仿优秀的可视化报告，你可以参考往届PowerBI可视化大赛的作品，链接如下：

http://www.chinapowerbi.com/Activity.html

不过里面作品的效果也是参差不齐，重点看一下前面获奖的作品就好。

你还可以学习一下我们新出的财务报表分析课程，以上的可视化技巧也都有涉及：[PowerBI财务报表分析课程上线，知识星球涨价倒计时！](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484079883&idx=1&sn=98a790aecadbbec8ee7359021d615e8d&chksm=8e13a7dcb9642ecad60e4e1729ac9936ec982facac65025f44719503fb402da0ecf1d06bce8b&scene=21#wechat_redirect)

**新增财务报表分析视频课程，2022年4月28日起，社群价格将上涨至365元，现在加入，立省66，感兴趣的伙伴不要错过。**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNnvIqQHgS8ljhgBkW34mXulvCwbxbgNXyibIgqSY6kibz7kcibANFv3Hia09S7GCZaZibohQ7oFU5E0Fg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
