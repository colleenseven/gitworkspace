---
create_date: 2021-11-10T12:55:39 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI中的书签，你应该用过，但它的秘密却未必都知道
source: https://mp.weixin.qq.com/s/5vF8I5vLwZV1IRYQSHidcA
author: 采悟
status: 未阅读
category: 
notes: False
uid: 
---

设计一个丰富的Power BI交互报告，几乎都离不开书签，书签的用法并不复杂，点击几下鼠标就能建好一个书签，但在应用的过程中，你也许发现跳转后的效果并不是自己期望的？

以前的文章中，介绍过很多书签应用的技巧，为什么一个小小的书签，却能做出这么多效果呢？

上面这些问题的秘密就在书签的属性里，这里就汇总介绍一下，书签的属性如何影响报告的交互效果的？

书签的作用是记录页面上的信息，它的属性就是控制记录信息的范围、交互的特性，在视图中打开书签面板，右键某个书签，就能看到该书签的属性：**数据、显示、当前页、所有视觉对象和所选视觉对象。**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNMKL9pvp4XRLxln9h41T5NHAjqsiaa9HwjjviaHkytbhTnj8QLNdmItFBeFnFicEJXxAZ8AmMOia2g1w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

下面就来分别介绍这几个属性都是什么用途。

**数据**

数据属性表示该书签的筛选器是否被记录，如果勾选，各种筛选器的选项都将记录下来，当通过书签切换到这个页面时，筛选器将依然保持在最初创建书签的状态，也就是数据被锁定在最初状态。  

很多人应用书签时，遇到的最常见的问题，是跳转后发现数据没有正常的切换，就是因为勾选了数据的原因，所以当我在第一次介绍书签的功能时，就对"数据"属性做了说明：

[PowerBI中的书签，真的非常有用！](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068219&idx=1&sn=b74e0d16ac61413a90fb5f7837dea112&chksm=8e0c75acb97bfcba745fe9ba7eb4ca2aa83d0af34a17668284170b97c68b2d3dc909dc9eb936&scene=21#wechat_redirect)  

一般情况下，你应该去掉“数据”的勾选，以防止数据被锁定，不过，勾选也有勾选的用处，比如一键重置所有筛选器：

[PowerBI报告设计技巧：一键重置](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073105&idx=1&sn=630078447d92ab54c9c049fb8a656953&chksm=8e0c5846b97bd150bd23d3af28b62bf9813d17b339a2a4199096cdb076fd664b0e744d2808b8&scene=21#wechat_redirect)  

**所有视觉对象、所选视觉对象**

表示书签所记录视觉对象的范围，是记录页面的所有视觉对象还是所选择的视觉对象，这两个属性只能选择其一，勾选一个，另外一个就自动取消了。

如果把书签仅仅作为页面导航功能使用，可以默认勾选“所有数据对象”；而勾选“所选视觉对象”更加灵活，应用场景更多，比如一个常用的场景是部分重置：

[PowerBI报告设计技巧：一键部分重置](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076778&idx=1&sn=e2cb9d89996185c4cc5c6a9084c7c9ec&chksm=8e13aa3db964232bd26f4c5db84fa9081437627c850ec39a954cfeb175886dcdf851aad9b7c1&scene=21#wechat_redirect)  

**当前页**

表示该书签是否要跳转到当前页面，将书签应用于导航时，都应该勾选，才能实现点击跳转的效果。

如果不勾选，当操作该书签时，书签记录的信息会更新，但是并不跳转，也就是只记录信息，不记录页面位置。

比如上面的一键部分重置的效果，该书签就没有勾选“当前页”，在每个页面点击一键重置按钮，只是把部分切片器更新到初始状态，而页面并没有跳转。

取消勾选“当前页”，还有一个有趣的应用是：动态工具提示，只切换工具提示页的数据，而不需要跳转到工具提示页：

[Power BI报告设计技巧：动态工具提示](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076591&idx=1&sn=b58d43709fe14df092e63dd107c1d8cc&chksm=8e13aaf8b96423ee7bfbf3c9f9ef3643819c7f36970fb46e97bbf15fd23de54aa89380775772&scene=21#wechat_redirect)  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJO9gjBCKz2sSd5RY408697tGBcWtM9qIcDCDhKcH7yWPAGuIOVLXl0AAXZmV3PZYIdjGpKEZCU4pw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

**显示**

用来控制该书签记录的信息是否可见，正常情况下都应该选择勾选，如果取消勾选，这个书签记录的信息将不会显示。

在实际应用中，我没有遇到适合取消勾选“显示”的应用场景，如果你有关于它的实用场景，欢迎留言分享。  

___

以上就是关于书签属性的介绍，当你调整完书签的属性以后，要记得右键书签，点击更新，这个属性才生效哦。  

要想做出一个精细的PowerBI报告，上面介绍的每个属性都应该精确掌握，灵活运用这些属性，在特定的应用场景下将会发挥出巨大的作用。

关于书签，可以参考这些经典应用，打开报告设计思路：

[Power BI书签的十个经典应用，请务必收藏](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068940&idx=1&sn=723666f112f15b6d20fcd980d2268c97&chksm=8e0c489bb97bc18d87c357cd2ee31a363f2146dcfdac61a32e8708a6ecf5e502370210925251&scene=21#wechat_redirect)  

你还可以在「PowerBI星球」公众号对话框中发送“书签经典应用”，获取这十个经典报告的pbix源文件。

**PowerBI星球学习社群**  

**双11限时优惠活动进行中**

双11期间加入立减50，以后不再有的低价，数量有限，扫码抢先加入~

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPqMkIyUw4C2I47MgpY2Xy5vECkEIFgA1UK0GpDT8BySjzpfZP1sd5ev5amb6IsE0YVXia8NUHdR0Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 扫码加入，和4k 学习者一起成长
