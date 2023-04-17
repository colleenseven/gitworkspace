---
create_date: 2021-02-27T20:16:09 (UTC +08:00)
tags:
aliases:
pagetitle: 原来PowerBI里还有这个精美图表，你一定还不知道
source: https://mp.weixin.qq.com/s/XXOIaGZMKQ_cnn4_Ipzniw
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

最近PowerBI可视化库中新上架了一个自定义图表：Dynamic Radial Bar Chart，直译过来是动态径向条形图，其实它还有个古朴典雅的中文名：玉玦图。

先来看看这个图表是什么样的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNtI6s47Aib9gaG7WuVsxN67OKFGF5d5icDAsN3OWY2xe3CLcgNicl3GCxYOomSkIHoLuYR41CTuyJyg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

是不是看起来很像环形图，只是没有连成完整的圆环。

根据汉字的释义，圆形中间有孔的玉称为环，环形有缺口的玉称为玦，所谓满者为环，缺者为玦：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNtI6s47Aib9gaG7WuVsxN67b5iasoazyicFchoacWia1gQSUFhNVp7n8EyCGibVuWFP7IXLpqRAIRKDWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

古代精美玉玦

径向条形图特别像中国的玉玦，因此该图也被称为玉玦图。

它是环形图和条形图的变种，外观像环形图，但环形图主要是用来展示数据的相对比例，而玉玦图一般用来比较数据的绝对大小，但也不同于条形图根据长短来比较，而是根据极坐标下的角度来表示多少。

以展示2008年北京奥运会前10个国家的奖牌数据为例，简单介绍一下PowerBI玉玦图的做法：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNtI6s47Aib9gaG7WuVsxN67MZHQL6tAN9crxP0tQR8frGP2ia1Ok8yAscdiamnaMkda8RibkvUMZ7zmg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

首先从AppSource中将这个图表加载进来：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNtI6s47Aib9gaG7WuVsxN67Wbqg8RubMtweDdXQZbEJKeq8NoZ2GuiaguicmHrL54npbno0KKcLBuvg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

只需要两个字段就可以生成个简单的玉玦图：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNtI6s47Aib9gaG7WuVsxN679lI2HBAI8Hnus06uvvKngPly9DAcbNFwgEV15UBYWbbsqabEUl8y4g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以添加类别字段来细化数据，比如将奖牌类别添加进来，并调整一下颜色，就变成了下面的效果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNtI6s47Aib9gaG7WuVsxN67OuVqZxIFNuZJcPszsHPgfdztkuEeM4mS2GI1R1XEUhQtOBXuJFARJQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

不仅可以添加类别，还可以在图表中添加目标值，并且它的格式设置十分丰富，标签的格式、径向条曲线、背景、参考线、配色方案等，都可以自定义设置：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNtI6s47Aib9gaG7WuVsxN67H1h7pyZecmqXvOaJVsN6pN0HrLAKjFwAXnTBfWWmO5Rkic3AOg1O8Eg/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

PowerBI中玉玦图还有个前缀，Dynamic Radial Bar Chart，也就是动态玉玦图，来看看它的动态效果：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNtI6s47Aib9gaG7WuVsxN67l4F1rRtSAKMrWDKRzia0vK57jhK3s1L1bGriaMsN6pCOiaYNZDskj9d0A/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

通过单击可以下钻到下一层级，然后左上角自动出现一个返回的箭头图标，点击可以返回到上一层级，动画效果非常顺滑，动画的持续时间也可以在格式中调整。

玉玦图的好处是节省空间，美观，更多功能和设置技巧你可以自行探索。

### 需要注意的是视觉上半径越大的玦环会看起来更大，半径小的则小。**但玉玦图比较数据时，并不是根据面积大小或者长短，而是根据角度，所以很容易误认为外侧的数值会大于内侧。**

仅从实用性来看，它不如柱形图或者条形图直观，更多的是一种审美上的需求，把报告做的赏心悦目何尝不是信息传递的高效方式呢。

本文练习玉玦图的示例数据，可以在「PowerBI星球」公众号后台回复“奖牌数据”获取。

___

\-精彩推荐-

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 3k+ 学习者一起成长
