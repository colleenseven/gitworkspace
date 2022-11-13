---
create_date: 2022-11-10T12:37:21 (UTC +08:00)
tags: 
aliases: null
pagetitle: 如何在Power BI报告中添加个搜索框？
source: https://mp.weixin.qq.com/s/20SBj5IkplcDlnF-X1GCJQ
author: 采悟
status: 未阅读
category: 
notes: False
uid: 
---

在PowerBI报告中最常用的筛选方式是切片器，不过有些场景下，比如类别很多时，靠切片器一项项找就太麻烦了，而有个搜索框就会更加方便，本文就来介绍几个可以搜索的控件。

**1\. 利用切片器搜索**

内置切片器有个搜索功能，点击切片器右上角三点进入，勾选"搜索"，即可打开切片器的搜索功能：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNEon7dlL6fcjP1z8O9gNd3icgksss6sZcNqMC0JicTlxnO7NpUSq4bnPDFXOtVGwuicvuPm08ktukow/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

或者选中切片器，然后快捷键Ctrl+F，也可以调出搜索框。

需要注意的是，文本型字段的切片器才有搜索功能，数值或者日期切片器无搜索功能。

关于更多切片器的用法参考：[玩转PowerBI的切片器，看这篇就够了](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074560&idx=1&sn=7050c2194d5e0a5587ec6282ff17b4ad&chksm=8e0c5297b97bdb81d70e9a7ece3d0d557a1fe58fe7102ceedec734222a89777e8724f784acfe&scene=21#wechat_redirect)

对于切片器的搜索结果，并不会立即产生筛选作用，必须选中筛选的结果，才能筛选，由于这个特性，切片器并不是太适合作为搜索框。

**2\. 利用Text Filter搜索**

Text Filter是个自定义视觉对象，你可以在AppSource中加载。  

它使用起来非常简单，可以对包含在总字符串中的部分文本过滤，只要包含搜索词的数据都会显示出来，比如这个报表左上角的搜索框就是用TextFilter制作的。

这个效果与平时我们使用搜索的体验类似，小巧而实用，不过它的各项设置也很简陋，基本不支持自定义调整。

## **3.利用Text search slicer搜索**

Text search slicer是近期新发布的一个自定义控件：

## 

它的效果与Text Filter类似，不过设置更加灵活，可以调整文本、填充、边框、颜色等各种可视化元素的格式，做成一个更加个性化的搜索框。

比如这个报告的左侧的两个搜索框用的就是Text search slicer，可以在搜索框中设置提示信息：

此外，该视觉对象还支持放入多个字段，这时会在下方显示字段按钮，然后根据突出显示的字段进行搜索。

上面三种方式，推荐使用最后一个，Text search slicer足够简单，设置灵活，当你需要在报告中放置搜索框时，它应该是当前的最佳选择。

___

**PowerBI星球学习社群**  

**双11限时优惠活动进行中**

双11期间加入立减50，以后不再有的低价，数量有限，扫码抢先加入~
