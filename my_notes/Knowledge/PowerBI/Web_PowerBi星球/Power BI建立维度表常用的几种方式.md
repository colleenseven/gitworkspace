---
create_date: 2022-11-01T12:41:13 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI建立维度表常用的几种方式
source: https://mp.weixin.qq.com/s/gyaXlvorqwUo_3z45QDFzA
author: 采悟
status: 未阅读
category: 
notes: False
uid: 
---

使用Power BI应摆脱单张表的思维，不建议在一张大宽表的基础上分析，最好先建立数据模型，而一个优秀的数据模型离不开合适的维度表。

维度也就是分析的角度，比如从日期的角度分析，模型中最好有个日期维度表；从产品角度分析，模型中应该有个产品维度表。建立维度表的好处是，可以对每个维度单独控制，按业务需求进行分组筛选，这样才可以更方便更灵活地实现各种动态分析。

如果源数据只有一个大而平的明细表，并没有各种维度表，那么在分析之前，最好先构造维度表，以下面这个简单的明细表为例：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPU9ElNbLCWdrkvvNTbiciby6YYU9IhfdUvPSFErD4Ll8807RuujW0CbYOGPyZYIklufXN70gm8x1Mg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个明细表中有日期、产品、部门和业务员字段，如果需要从这些角度对销售情况进行分析，就要建相应的维度表，下面来看看利用DAX生成维度表的几种方式。

**从表中提取一列作为维度表**

对于产品维度表，就可以利用VALUES函数从明细表中，提取产品名称的不重复列表来实现。  

> 产品表 = VALUES('明细表'\[产品名称\])

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOtic60cPmnUqdVlSHrolslXGib3Om86VvLPGPm0I8oH7gGeHoicusTPibso6IvUdic7MibkhiaCzGgH6DuA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**从表中提取多列作为维度表**

如果有部分维度之间是有对应关系的，那么就不要分开为多个独立的维度表，而应该整合为一个维度表。

比如上表中的部门和业务员字段，所属部门只算是业务员的一个属性，不用单独作为一张维度表，应把这两个字段整合到一个业务员维度表中。

从表中提取多列作为维度表可以用SUMMARIZE函数来实现。

> 业务员表 \=
> 
> SUMMARIZE(
> 
>     '明细表',
> 
>     '明细表'\[销售部门\],'明细表'\[业务员\]
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOtic60cPmnUqdVlSHrolslX3k7FRKIIP5n81g8YJkUCtvl4fj9dQodLShqHM3OFK9eheicsIEN5tUg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关于SUMMARIZE函数的用法可参考：[SUMMARIZE：值得你花30分钟来了解的函数！](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068502&idx=1&sn=4343d6bb0e9eef46b0d1dea97a5b45b3&chksm=8e0c4a41b97bc357e920d2b4d6b531d4f40c1edfb172a3cb1be83a3fd92f70d58cca2a5070a3&scene=21#wechat_redirect)  

**从多个表提取列作为维度表**

如果有两个明细表，除了上面的明细表，还有个明细表2，分别有一部分明细数据：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPU9ElNbLCWdrkvvNTbiciby690ScIpfWOXbEHAPqBWFWPeicbu9vSDoumRlut1RdOzoMC6m5UjRWxcA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

并且两个明细表中的产品并不是完全重叠，需要从这两个表中提取产品维度放在一起，才是一个完整的产品表，那么就可以这样建产品表：  

> 产品表 =
> 
> DISTINCT(
> 
>     UNION(
> 
>         VALUES('明细表'\[产品名称\]),
> 
>         VALUES('明细表2'\[产品名称\])
> 
>     )
> 
> )

这个公式的逻辑是，先用VALUES函数分别提取两个明细表的产品名称，然后用UNION函数将它们合并起来，最后利用DISTINCT函数进行去重，就得到了一个完整不重复的产品列表。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOtic60cPmnUqdVlSHrolslXmU3DlKicTfXD3FL7ohLq9Ju9kqCgibbbXic8miaWDv9olxt3wsDlplVmfA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其实对于这样的两个格式完全一样的明细表，建议在PowerQuery中追加合并为一张表，这样就可以按照上面第一种方式来提取维度表，合并以后的表对于之后的分析也会更加方便。

**从表中提取列并补充新列作为维度表**

对于上面的日期，可以像生成产品表一样，用VALUES函数提取日期的不重复列表，不过一般不会仅仅在日的粒度上分析，经常还需要按年、月等粒度进行分析，就需要在这个维度表中补充年、月相关的字段。

在表中添加列可以用ADDCOLUMNS函数，以上面明细数据为例，从里面提取日期并添加年月字段为例，可以这样来建表：  

> 日期表 =
> 
> ADDCOLUMNS(
> 
>     VALUES('明细表'\[日期\]),
> 
>     "年度",YEAR(\[日期\]),
> 
>     "月份",FORMAT(\[日期\],"OOOO","zh-cn")
> 
> )

这样就做好了一个带有年度和月份的日期表。

不过在实际分析时，对于日期表，不建议用这种方式建，数据表中的日期不能保证是全年连续并且无断点，为了让时间智能函数能正确计算，建议直接生成一个规范的日期表，而不是通过明细表来提取，你可以直接利用这篇文章中的DAX公式来生成日期表：

[分享一个更实用的Power BI日期表](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076559&idx=1&sn=e00814afa6a2013e3ba3a19cfb575f39&chksm=8e13aad8b96423ce61ca80169b35047204be5c7e4750491f84d7ff327eba9c093c9aa9a829f2&scene=21#wechat_redirect)

上面就是几种维度表的提取方式，主要灵活运用VALUES、SUMMARIZE、UNION、DISTINCT、ADDCOLUMNS等表函数，根据需要来生成各种维度的不重复列表。  

维度表建好以后，就可以建立模型了，关于建模你可以看看这篇文章：

[Power BI数据建模你可能遇到的一些问题](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484082318&idx=1&sn=e248fcdf3a865dfcac84fdc42a39436c&chksm=8e13bc59b964354fdc20d0eec79efc622799d43a509ad9d3c783a6e0d92ea86b04a73cf86c21&scene=21#wechat_redirect)  

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你想深入学习Power BI，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和5000+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMstwXX5zrKianmFXzyqbIVgh7byfo3V8JJPmhqicywbtYkM0j2ibngnT5XBZ2AwKvGZiby9ngoKfLvzg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门Power BI》电子书，轻松入门。
