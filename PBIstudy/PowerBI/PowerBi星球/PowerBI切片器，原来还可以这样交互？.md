---
create_date: 2021-01-06T20:22:35 (UTC +08:00)
tags:
aliases:
pagetitle: PowerBI切片器，原来还可以这样交互？
source: https://mp.weixin.qq.com/s/mudoBxue3-omQ5kKJXRGmw
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

切片器是最常用的PowerBI控件，正常情况下，是选择某个项目就显示该项目的数据，如果不选时，显示全部的数据，就像下面这样：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPCJlp1D6Kibt9mGDlkENsicy2f3KHv8oKQqwFaXGT3Jf7A6eiaCpicbUtiaBibYg1mXuqsvvBlhwMuKdFw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

然后就有星友提问，切片器选择时正常显示选择的数据行，**但切片器不选择任何一个项目时，如何不显示数据呢？**

因为切片器不选时，就是不能起到筛选作用，所以正常情况下会显示全部的数据，那如何实现不选时也不显示数据呢？其实我们依然可以利用DAX来实现。

以上图中的数据为例，**首先切片器的字段不要用数据表中的字段，应该有个独立的类别维度表，用这个维度表中的字段来生成切片器。**

至于维度表是否与数据表建立关系，对本文来说无所谓，是否建立关系不影响下面要实现的结果。

**1、建立度量值**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPCJlp1D6Kibt9mGDlkENsicy8r51JkUBAic6wR3CwNPLdAjcba9zMjZSibLPMdY3tOVsDbjwoorJx6KA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个度量值的含义是，如果切片器被筛选且当前上下文在切片器的选择范围内，返回1，否者返回BLANK。

**2、将该度量值作为可视化表格的筛选器，只显示度量值结果为1的数据**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPCJlp1D6Kibt9mGDlkENsicyicgCYATVicokgXYiaxtWD1Yzoibia3zkF3HFz9YAekhBuVYBeXSpEAqkMkw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样两个简单的步骤设置好以后，就可以实现期望的结果了：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPCJlp1D6Kibt9mGDlkENsicyCf9GbicU2fhrz8E8Pef1O06pAm8nYg3xiaOba8I0eiaU8XOgicq7ibPA0oQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

用PowerBI中的文本搜索控件TextFilter来代替切片器效果也是类似的：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPCJlp1D6Kibt9mGDlkENsicyj6I1c8qmibOIMic121Huw5ib7lHDznNYcHkJOeIGnta7coviaHY9lOQ10w/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

从TextFilter的效果可以看出，输入关键字后，会返回包括该关键字的所有数据，这一点和切片器并不相同，不过当清除关键字，不选择任何项目时，结果和切片器一样，不显示任何数据。  

以上就是切片器非正常交互的一种实现方式，关于切片器其他类型的个性化交互，可以参考之间分享的一篇文章：

[利用DAX，突破切片器的默认交互方式](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072463&idx=1&sn=95c684b48ff2e2779ca90f734688b3e1&chksm=8e0c5ad8b97bd3ce897a72e1255398769c1a0da914a553dab6f39d34f9cf4e8169bb1a97f96a&scene=21#wechat_redirect)  

___

**PowerBI星球的**[**历史精华文章合辑**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)**，值得你收藏：**  

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNn5eia186067w5or6WoVmwdm210CYQfaibhdzFvJvR59sFUgk13iauEzR4oLzGvXiaziaX8VJcB2sCbzg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

___

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 2k+ 学习者一起成长
