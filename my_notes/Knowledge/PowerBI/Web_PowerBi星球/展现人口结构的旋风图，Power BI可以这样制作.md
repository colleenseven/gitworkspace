---
create_date: 2021-11-21T12:53:31 (UTC +08:00)
tags: 
aliases: null
pagetitle: 展现人口结构的旋风图，Power BI可以这样制作
source: https://mp.weixin.qq.com/s/Zsv13Q3pZ2zHaxH1-uNm7g
author: 采悟
status: 未阅读
category: 
notes: False
uid: 
---

在进行人口年龄结构的可视化展示时，经常会用到旋风图，就是下面这样的，  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOjoPeG5kDSA7JTfnJF5jZKI4sibA6wkVYxJjMtpUvsTib6yoDgWapkdIPxzICTztJMfh0M9rfXCYfw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

你肯定也见过这样的图表，但可能不知道它的名字。之前也有不少人问过我这个图怎么做，其实上图就是Power BI制作的，利用了一个自定义图表：Tornado Chart。

Tornado Chart，旋风图，它是一种左右结构的条形图，用于比较两个维度的指标，比如上图，不仅可以纵向对比同性别的不同年龄段人口分布，还可以与异性对比，整体上也可以体现出人口的年龄分布情况。

这个图制作很简单，只需要将相应的字段放进去就可以了：  

其中【组】和【值】是必须的，如果只用这两个字段，就是个普通的条形图，在【图例】里放入字段以后，才会出现左右结构的条形图。

它的格式设置也很简单，这也意味着无法满足个性化的要求，如果你觉得这个图表格式太简陋了，还可以试试下面这种方法。  

旋风图本质上是一个左右结构的条形图，因此就可以换个思路，将两个条形图组合起来实现。

首先制作两个条形图，一个男性的条形图，一个女性的条形图：

然后将左侧的女性条形图的X轴反转，并关闭Y轴：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOjoPeG5kDSA7JTfnJF5jZKJptOEogjkjwBOic0FepCPLu5x51w5Ft62yic0HZicRMPKMjiaYc7emVjKQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

就可以得到将分类放到中间显示的旋风图效果：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOjoPeG5kDSA7JTfnJF5jZK4jDicwZprvPVibAaR1Zv5YEmdoXRVwkRcvvuVBc8xyflXWoB5LrQakaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

内置的条形图要比自定义图表灵活的多，你可以调整X轴、Y轴、数据标签的格式，也可以自定义条形图的颜色，比如调整为渐变色：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOjoPeG5kDSA7JTfnJF5jZKqp1WxYZXoZ7icPk9CkJFq6oicJzj64XFpXWNC8lQxRicKJPvfNL8cOerQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

以上就是PowerBI制作旋风图的两种方法，当你有类似的可视化需求时，可以尝试应用。  

本文制作旋风图的数据可以在「PowerBI星球」公众号后台发送"旋风图示例数据"获取。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
