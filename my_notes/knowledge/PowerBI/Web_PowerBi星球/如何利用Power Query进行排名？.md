---
create_date: 2022-07-06T12:28:56 (UTC +08:00)
tags: 
pagetitle: 如何利用Power Query进行排名？
source: https://mp.weixin.qq.com/s/l3LaNDACvAQ-ir8jbGkljQ
author: 采悟
status: 未阅读
category: 
uid: 
---

以前介绍过利用RANKX函数来进行排名，在某些情况下，需要对PowerQuery中的数据直接进行排名，那么如何用PowerQuery来计算排名呢？  

DAX函数中有RANKX来计算排名(参考：[这几个示例，帮你深入理解RANKX排名](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068781&idx=1&sn=4f7d7abed75b6db6cae3b23a45e7dfbe&chksm=8e0c4b7ab97bc26c2303edcd22dad9261981486689833504f129603f5b20a7b8f8d3669517e6&scene=21#wechat_redirect)），其实PowerQuery中的也有一个M函数可以排名：Table.AddRankColumn。

这个M函数可以为表添加一个排名列，下面通过几个简单的例子，来熟悉这个函数的用法。

模拟数据如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNRcuyH6B6mAtg58nXdsAFDFiawkgic9qeAib0QC94WOZvg8neOU6fmZ56uPJ0Pn1edFCVF4HtYqqJRQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如要对这个表添加个排名列，对类别按照金额进行排名，先添加个步骤，来输入M公式。

___

关于PowerQuery中添加步骤，有两种方式：

1、点击编辑栏旁边的fx  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNRcuyH6B6mAtg58nXdsAFDS8YZuZ14gL3o9KfrHbLXEBT4Jq56QAIqtrzxBDxQEqxFz3Td3tUMNA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

2、点击上一个步骤，右键>插入步骤后  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNRcuyH6B6mAtg58nXdsAFDD1DLv2QytH6yZB3h2xFc6FRkjUCh5ic6niaDCg5sv6aGETk3T21xwibaQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

知道了如何插入步骤以后，就在插入的步骤中，在编辑栏中输入：  

> Table.AddRankColumn(
> 
>     更改的类型,
> 
>     **"排名",{"金额"}**
> 
> )

函数中第一个参数更改的类型，是上一个步骤的名称，第二个参数是新列的列名，第三个参数，是排名依据。

然后就自动添加了一列排名列。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNRcuyH6B6mAtg58nXdsAFDjocwTZw57MuR2j5vWSMq3V8rETJYSvoSwTPqic4WJibIkpw9WXw3sg2Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

通过这个M函数，我们就得到了一列排名，不过这个排名是按照金额升序排列的，也就是金额最小的排名第一。

如果想让金额最大的排名第一，可以这样改：

> Table.AddRankColumn(
> 
>     更改的类型,
> 
>     "排名",{"金额",**Order.Descending**}
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNRcuyH6B6mAtg58nXdsAFDTzpMTbgzg0HM1cuET0V9UknvmCNZdYcYwQSlqxWibS0ib16ELgQialj2Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就得到一列常见的排名，数据最大的排第一。

上面的排名数字是跳跃的，这个数据有两个类别并列第三，则下一个排名从5开始。  

如果想让下一个排名不跳跃，即使有并列的情况，也是连续的排名，还可以再添加个参数来调整排名。  

> Table.AddRankColumn(
> 
>     更改的类型,
> 
>     "排名",{"金额",Order.Descending},**\[RankKind=RankKind.Dense\]**
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNRcuyH6B6mAtg58nXdsAFDm5jiaCvh7l16GID9StBV3icU2Y8gJJy68MJFo0yP0SmQMSY0HKic56sng/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就得到了连续的排名。

这个函数不仅是对根据一列进行排名，还可以按照多个字段来排名，假如按照金额列和数量列来排名，如果金额相等，则按数量来排名，就可以这样来写：  

> Table.AddRankColumn(
> 
>     更改的类型,
> 
>    "排名",**{{"金额",Order.Descending},{"数量",Order.Descending}}**
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNRcuyH6B6mAtg58nXdsAFDgUjwa4RORxgd5II7kQV78IOrMk4urOxibYiajQvSVxSz4MIpM45YnjZg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就实现了按照两个字段来排名，如果按更多的字段排名，还可以继续添加字段。

通过以上几个示例，你应该了解了如何在PQ中计算排名，不过这里计算的排名都是静态的，如果你想在报告中实现动态的排名，还是应该用RANKX函数写度量值来实现。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4500+ 爱好者一起精进~**

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门Power BI》电子书，轻松入门。
