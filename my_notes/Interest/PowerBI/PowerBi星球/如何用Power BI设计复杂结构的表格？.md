---
create_date: 2021-10-08T22:39:52 (UTC +08:00)
tags: 
aliases: null
pagetitle: 如何用Power BI设计复杂结构的表格？
source: https://mp.weixin.qq.com/s/HtR1LuSDbs4CJq7JezvyjA
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

复杂结构的表格，一般是指多行表头、特殊维度的表格，也被称为中国式报表，其实不论国内国外，都会有这种需求，这篇文章就来看看如何在PowerBI中，制作这样的表格。

如果只是现有维度结构的多行表头，那很简单，矩阵自身就支持，不需要特别处理，比如这样的结构：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN6oGnIQSa3kx3M0QQESdrYgZg2VQHqKibVwYw2CNBDOMrxAuicbHibOfylbVOsdTyGlHwvPPq5DxfkQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个表格，行有两个表头，产品类别和产品名称；列也有两个表头，年度和季度，不过这里的表头都是现有维度表就有的字段，只需要将这些字段拖到【行】和【列】中就可以了：

但是如果表头不是维度表中的字段，比如想在一个表中查看每个产品的收入和利润指标，每一个指标又划分为本月、上月和环比，结构如下：

对于这样的结构，就无法直接拖动字段得到，因为模型中就没有这样的字段，并且本月和上月的收入、利润，也需要分别写不同的度量值，那应该怎么做呢？

本文就以上面的表头结构为例，来看看PowerBI如何制作这样的表格，其实只需要2个步骤。

**1\. 创建辅助表，构造表头结构**

其实任何表头结构，都需要在模型中有对应的字段，既然现有模型中没有，那就先构造一个这样的结构表，作为表头。

指标结构表如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN6oGnIQSa3kx3M0QQESdrY5Bicdl03YGWIvuOxlpVFO3x227AwKXmQqY8dsO2YbfC5SwYd5icnvvwQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关于如何制作这样的表，有多种方式，请参考下面这篇文章，这里不再介绍：  

[Power BI 辅助表制作方式汇总](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071809&idx=1&sn=9e8f4916082c32cc0291a2e4e565f1fd&chksm=8e0c4756b97bce4087ec53dfb6e5380e7cb0662e73fa070f831e4283095505a5aced233e59c8&scene=21#wechat_redirect)  

上面的表中添加有两列序号，是为了对指标分类和指标名称[按列排序](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068059&idx=1&sn=28dff6992fe6d167f4a2fbd6a0c40460&chksm=8e0c740cb97bfd1a55d7789987c7c1ed2ac94a07529cc0428b1cdf48216671f468fa7820c420&scene=21#wechat_redirect)，以便表头的结构可以按照我们期望的顺序来展现。  

**2\. 根据表头，构造数据**

既然要展现收入和利润的本月、上月和环比指标，就需要先把这些数据用度量值写出来。

对于本月和上月的计算，可以参考这篇文章：

按该文章介绍的逻辑，分别写出以下6个度量值：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN6oGnIQSa3kx3M0QQESdrYNiahcZeIicL77OnNny2S2ZvicablQfFHGuU9JrD9owNIoh1A6PJlFqXog/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后根据表头的逻辑，将这些度量值整合到一个度量值里面，可以利用SWITCH函数来判断：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN6oGnIQSa3kx3M0QQESdrYurZIIGqEf2Wvjn4A3X5HsLqvicM4IIDgWLzEBQJj4KvbyC9QcSX4hibw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

看着公式很长，其实逻辑非常简单，就是判断当前上下文，也就是每一列的表头，来返回对应的数据，对应的数据就是上面我们已经写好的度量值：

如果是"收入"、"本月",返回 \[本月收入\] ；  

如果是"收入"、"上月",返回 \[上月收入\] ；

如果是"收入"、"环比",返回 \[收入环比\] ；

……

因为比率一般习惯用百分比来表示，所以在返回环比数据时，用了FORMAT函数，来让这个度量值的格式变为百分比。  

上面两个步骤完成之后，就可以构造矩阵了，将结构表的字段放到【列】中，\[指标数据\] 放到【值】中，  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN6oGnIQSa3kx3M0QQESdrYibTezIja4fiaAqiaosAgCjGqZwWtz5SvRKgQbYcPuUzxmGwts2kiciaKaTg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

就可以得到如下结构的表格：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN6oGnIQSa3kx3M0QQESdrYJ2bxu3Dh6e1R226ePndKLFvibIXf0LnR4q3LvcUlsusjXyUb5LkEYog/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果想设置条件格式，比如让环比大于0的显示为绿色，否则显示为红色，可以写一个度量值：

同样是判断当前表头上下文，如果是环比，就判断环比是否大于0，对应返回不同的颜色。

然后将这个度量值放到条件格式的字体颜色中，就得到了如下的矩阵：

这就是一个简易的中国式报表，更复杂的结构也同样是上面两个步骤，难度不高，但是相对较为繁琐，尤其是表头结构特别复杂的时候，可能要写很长的度量值，判断每个单元格的上下文来返回对应的数据，关键是要弄明白其中的构造逻辑，然后根据你的需要来一步步实现。

并且想做出表头结构复杂、外形赏心悦目的表格，你还应该看看这篇文章，熟练掌握矩阵的各项格式设置：

[Power BI矩阵格式设置13招](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071983&idx=1&sn=3fd379f7bf88141747ac9a09dc4273b7&chksm=8e0c44f8b97bcdee4cb068fd1e47e033629cf0734dd29c8341746d449372068dbb4e6d298cba&scene=21#wechat_redirect)

___

**[PowerBI商业数据分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)**  

帮你从0到1，轻松上手PowerBI

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN6oGnIQSa3kx3M0QQESdrYCTV9SBx5LXD4kp3icA9LouW3YN2z2njBWWQzM1zia9Fbeky0fdIpNakw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPUabZXugXKNdmeUzxwJM4OyUpTibBJjoq1jk8CzVZJz6s4nJRW1ViammT4ecqAJ7iapDccKNNrwtLYQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077212&idx=1&sn=bb3dac9becf80b5d929e5dc8405158dd&chksm=8e13a84bb964215d6362f78768cdefa18def4dfc8cd5c14f075442431604ed9c9729e4051a4b&scene=21#wechat_redirect)

[](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077048&idx=1&sn=b3da0a4079ed8366c67982912e795d59&chksm=8e13ab2fb964223978c16d5647e4a28eaeb50bc7338c4e82f4e14f2cddc8bb844b956f09beb6&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

↑ 扫码加入，和 3k+ 学习者一起成长
