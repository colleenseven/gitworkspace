---
create_date: 2021-03-21T20:13:56 (UTC +08:00)
tags:
aliases:
pagetitle: PowerBI 2021年3月更新，你应该知道的几个变化
source: https://mp.weixin.qq.com/s/FuybeA--QH9I5zwiZLYJBQ
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

PowerBI 2021年3月的更新如约而至，关于更新具体内容官方博客的介绍非常详尽，大家可以在博客中浏览，或者在我的视频号中观看本月更新的视频介绍:

这里依旧挑选几个大家可能都会遇到的变化简单介绍一下。

**1，折线图支持添加X轴恒线**

折线图之前只能添加一条Y轴的辅助线，现在终于可以添加X轴的恒线了，依然是在分析面板中，打开就可以看到该功能：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJON35qfrP6kibnyYduYHtPc02Vr24zHT11AGPhpzCeVYGgiczasrEia0D3pYz4kibNqWCYn11myygnFyg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

按上图的设置效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJON35qfrP6kibnyYduYHtPc0jElmzcYvZGyMCN3NKYO2M3ZOeajpIyBsiaAe1ECwrwSmVK0M13cnRRg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

不过现在只是恒定的线条，只能设置常量，无法动态变动，如果想做动态X轴辅助线，依然需要借助折线和柱形组合图来实现，比如这篇文章的效果：

[如何用 PowerBI 做盈亏平衡分析？原来这么简单！](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074680&idx=1&sn=a3607ef748c8fbdae96dbec508eb4444&chksm=8e0c526fb97bdb79703e4ac355c51cf3f5983ef09a093043ad21610550fe57f5aeb67de9a38b&scene=21#wechat_redirect)

**2，模型视图界面变动**

这是上个月刚更新的功能，这个月算是又改回来了，基数显示在关系的端点，关系的方向显示在中心。 

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJON35qfrP6kibnyYduYHtPc05EnbNicHica4nkwBuGicCC6GiayLmBsHfS6cqj3afPtGIDIgJdUwPZHYYg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在这个小细节上有必要这么来回折腾么……

**3、新的DAX函数：IF.EAGER**

功能以及使用方式和IF一样，但在特定的场景下，性能可能更优，如果你觉得用IF时性能较差，可以尝试改为IF.EAGER。  

关于该函数的介绍可以参考官方文档：https://docs.microsoft.com/zh-cn/dax/if-eager-function-dax

**4、CALCULATE优化**

这是DAX非常友好的改动，大多数人刚开始写度量值时，应该都遇到过这种报错：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJON35qfrP6kibnyYduYHtPc0tO7noia29iaibgjparXQzDH4yOUye7L16xGxaY7dwbaxyVqRddSt6PgIg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

是不是很抓狂？

期望是计算产品零售价大于50的手机配件的销售额是多少，从逻辑上来看，上述写法没有问题，但以前PowerBI就是不允许这样写，不同列的多个过滤条件，必须用FILTER作为一个显式过滤器来完成，也就是要改成下面这样才能不报错：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJON35qfrP6kibnyYduYHtPc0Ricdlv8icoHYRgNjLMsoEdzCWiciauicRJZZFQuTrhVphMjuEZ0xafvibz1g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

从2021年3月开始，新的版本支持上述简易写法，不用FILTER也不会报错了，和FILTER的写法完全等价：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJON35qfrP6kibnyYduYHtPc0rChos4ibNpDnxE5HaQGxaicvF6f2eNXzHz1AaSQIzdicEInOA558IcWRQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

它降低了初学者遭遇DAX报错的概率，使CALCULATE更易于使用，但是建议大家仍必须清楚这种简易写法的FILTER等价写法，才能更精确的理解上下文筛选与计算逻辑。

**5、Windows 7不再支持**

前几天还有人问我，为什么电脑安装PowerBI Desktop总是报错安装不了，细问才知道电脑是Win7的操作系统，PowerBI官方已明确宣布，Power BI Desktop于2021年1月31日停止支持Windows7，Power BI Desktop现在仅在Windows 8.1或更高版本的Windows上受支持。

所以如果你用的电脑还是win7系统，还是赶快换吧，PowerBI本身对电脑的要求就比一般办公软件更高，在一个老旧电脑上，再高级再智能的东西也难以玩出什么花样。一个好的电脑，既能提升工作效率又能提升自身技能，对自己的这点投资还是不要节省了。

关于3月的更新，就简单介绍这么多，关于更多更详细的功能介绍请参考官方博客。

PowerBI每月更新后，如果不能自动更新或者不方便下载，可以在公众号后台回复"软件下载",获取最新的安装包。

[我的新书已上市](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)，感兴趣可以扫描下方二维码购买：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOvxZXDgz6hr3eDTavmiaxEtNHCkjlDMMOTe1joF93T0Oj3NDawRbq207dVqq0OHPaZGIN14G55d0w/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOojexubCy39PJZJic24XlI9IC8Fhx57SVYiciave3T7sAxeLXXZgrAzhAsUHXC3dxpU1fp72ChD8ibfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072351&idx=1&sn=fabb08c54790ac1225b470fd647c7a5e&chksm=8e0c4548b97bcc5e0450f1945a2c76039bbb42650bcb1edbc856820836d63d32af4c7780e31a&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 3k+ 学习者一起成长
