---
create_date: 2022-12-09T23:49:44 (UTC +08:00)
tags: 
aliases: null
pagetitle: 如何用Power BI制作四象限图？
source: https://mp.weixin.qq.com/s/YvkBisWL2Mr_G6Frlbz4yQ
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

四象限图是根据水平和垂直分割线将图表区域划分为四个象限，从而对落入每个象限的数据进行特定的管理。经常有人问如何制作四象限图，这里以之前介绍过的关联分析为例（参考：[如何用Power BI分析产品关联度？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068422&idx=1&sn=218b3a331f4ea648d4c3e2d0e05701e4&chksm=8e0c4a91b97bc387219523f5ae09fa32e60a8c04b3d02bbdc2763bd6e72ae09f32f1ee1b4e7d&scene=21#wechat_redirect)），其中最后就是个四象限图，这里再详细介绍一下实现方式。

先通过产品之间的关联销售金额和关联客户占比制作一个散点图：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMHX44XBicjxxae6egOtwicZA4pGLN7Bret6V97W5ic4f8HWuIicF0YHiavMd80lPBCFDfVa9qGkLZ0sLg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

将这个散点图划分为四个象限，可以在散点图中分别添加一条X轴恒线和Y轴恒线：

假如将x轴恒线设置为80、Y轴恒线设置为15%，就将这个散点图切割成了4个象限：  

不过上面添加的是静态的恒线，如果数据发生变化，还按照这两条线切割就很可能不合适了，对于动态的需求，可以写动态度量值放到X轴轴线和Y轴恒线中。

动态情况下，更常用的方式是利用x轴和y轴指标的平均值来作为四个象限的分界点，可以利用分析功能里面的平均值线来实现。  

然后，这两条线就会根据指标的范围进行动态分割，总是将这些数据合理划分到不同的象限。

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMHX44XBicjxxae6egOtwicZAicnRaj7Jrooib92U6SLsJoiadmrLb84TQLicHRL0ibtZ4pxPyDfopt58siaw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

为了让四个象限更加直观，还可以让每个象限的数据点显示不同的颜色，通过度量值进行动态配色。

```
四象限配色 = 
```

这个度量值的逻辑是根据四象限的分界点，判断每个点的所属象限来返回不同的颜色，将配色度量值放到散点图颜色设置中就可以实现四个象限的不同配色：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMHX44XBicjxxae6egOtwicZA2icoq1rCEibx3MsYc97bI2SWXUJWhKuRAf7aFb6lOC2jaXOicgyUXicI5g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

以上就是四象限图制作的简易方法，细节之处还可以继续优化，其中的关键是掌握在PowerBI中为图表添加辅助线的技巧，更多辅助线的添加方式请参考：  

[如何为Power BI图表添加辅助线？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484081759&idx=1&sn=544a5ba816946c932f74b13434f4326b&chksm=8e13be88b964379ec42109ca8c01c5bc4ce37aa29b8a0dfbbabc688d7acd31b231e7867f3d6f&scene=21#wechat_redirect)  

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你想深入学习Power BI，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和5000+ 爱好者一起精进~**

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门Power BI》电子书，轻松入门。
