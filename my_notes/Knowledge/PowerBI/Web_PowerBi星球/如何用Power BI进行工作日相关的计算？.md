---
create_date: 2022-11-11T13:00:37 (UTC +08:00)
tags: 
aliases: null
pagetitle: 如何用Power BI进行工作日相关的计算？
source: https://mp.weixin.qq.com/s/rjzlrVy3mUX58v-AW5dpJw
author: 采悟
status: 未阅读
category: 
notes: False
uid: 
---

我们平时应该都会碰到针对工作日的分析，在Power BI中，并没有与工作日相关的函数，很多人因此就无从下手，不知道该如何计算了，那么，如何用PowerBI处理工作日的分析呢？这篇文章给你提供个思路。

**考虑到非工作日，不仅有周末，还有法定节假日，并且涉及到调休等问题，很难有某个固定的函数，进行这些不规则的个性化计算**，即使Excel中有工作日函数，也并不方便，直接使用的计算结果也很可能与实际不符。

其实最简单的办法就是先做一个节假日的列表，你可以在网上找每年节假日的资料，即使是手工制作，也不麻烦，毕竟周末是很规律的，法定节假日和调休的处理每年也就是十几天而已，很快就可以做出来这张表。

这里我先做出一个2019年到2021年的中国节假日表：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNbtiatk6CdmYgNu9SjpqPtAkBaLOe6qYp5jDgliaBicYg8R7J2Nmd9phHPabQSuNDeVhCIjia4LW4CVw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后将这个假日表导入到PowerBI数据模型中，这里不将它与模型中的其他表建立关系，而是利用它，在模型原有的日期表中，添加关于工作日、节假日的字段。  

首先判断每个日期是否为工作日，添加一列工作日标记：

> 工作日标记 = 
> 
> IF(
> 
>     LOOKUPVALUE(
> 
>         '中国节假日表'\[日期\],
> 
>         '中国节假日表'\[日期\],
> 
>         \[日期\]
> 
>     ), 
> 
>     0 ,  1 
> 
> )

这里用了DAX函数LOOKUPVALUE，它不需要两个表建立关系即可查找，如果在假日表中找到日期，返回0，否则返回1，1代表是工作日。

___

  

关于LOOKUPVALUE的语法和用法，可以参考下图，这里不再介绍：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNbtiatk6CdmYgNu9SjpqPtAibAONmTRGjcsmiaTA3Kq9PQjibKEtvnmUibTps2WiaklxB6YiaemSjvAnlxw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

同样的方式，利用LOOKUPVALUE，将每个日期对应的节假日名称和节假日类别匹配过来，如果不是节假日，就返回空白：

> 节假日名称 = 
> 
> LOOKUPVALUE(
> 
>     '中国节假日表'\[节假日名称\],
> 
>     '中国节假日表'\[日期\],
> 
>     \[日期\]
> 
> )
> 
> 节假日类型 \= 
> 
> LOOKUPVALUE(
> 
>     '中国节假日表'\[节假日类型\],
> 
>     '中国节假日表'\[日期\],
> 
>     \[日期\]
> 
> )

在日期表中显示如下（节选）：

为了能够灵活进行工作日的计算，这里我再添加一个字段工作日编号，为每个工作日添加一个不重复的顺序索引。

> 工作日编号 \=
> 
> IF(
> 
>     \[工作日标记\]=1,
> 
>     CALCULATE(
> 
>         SUM('日期表'\[工作日标记\]),
> 
>         FILTER(ALL('日期表'),\[日期\]<=EARLIER('日期表'\[日期\]))
> 
>     )
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNbtiatk6CdmYgNu9SjpqPtAKbaX23icHwagk7mmSoVQcA7rJzfZgVjyeNKcic1lSFKQHBHAOOvus7Wg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个工作日编号非常好用，下面会看到它的用处。

至此，完成对日期表的补充构造，下面就可以开始工作日的相关计算了。

**统计某期间的工作日天数**

计算两个日期之间的工作日的天数，只需要这样写一个度量值：

> 工作日天数 = SUM('日期表'\[工作日标记\])

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNbtiatk6CdmYgNu9SjpqPtAtRrPs7Qddlr8RUAMNW0T3yrmzFFOdHelMic86P5o5CVBXjHicnjyjCWg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

是不是非常简单，这就是工作日标记用0和1的好处。  

**上/下个工作日**

如果想找出某个日期的上一个工作日，就可以这样写：

> 上个工作日 =
> 
> CALCULATE(
> 
>     MAX('日期表'\[日期\]),
> 
>     FILTER(
> 
>         ALL('日期表'),
> 
>         '日期表'\[日期\]<MAX('日期表'\[日期\])&&
> 
>         '日期表'\[工作日标记\]=1
> 
>     )
> 
> )

这个度量值的逻辑就是找小于当前日期，并且工作日标记为1的最大日期，也就是上一个工作日。

同理，下一个工作日的写法：

> 下个工作日 =
> 
> CALCULATE(
> 
>     MIN('日期表'\[日期\]),
> 
>     FILTER(
> 
>         ALL('日期表'),
> 
>         '日期表'\[日期\]>MAX('日期表'\[日期\])&&
> 
>         '日期表'\[工作日标记\]=1
> 
>     )
> 
> )

效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNbtiatk6CdmYgNu9SjpqPtAqTTt56hJMnqkdcDdTm1ficZewffTo4I3wmah99UBeKZ1lRFhjg5E91g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**N个工作日后是哪一天**

日常经常会遇到某些事项的办结期限是10个工作日、15个工作日等，那么如何快速计算出N个工作日后，是哪一天呢？  

这样的计算需要先[建立一个参数](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067672&idx=1&sn=1a141b81b4e20f83cabf410164f55974&chksm=8e0c778fb97bfe9904d988eb9972b26436c260e575d008d1414076b86df997fee74dc559ec73&scene=21#wechat_redirect)，然后写个度量值：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNbtiatk6CdmYgNu9SjpqPtA7eKh61CF8NADX41JUicHtTQ0KeWxOOKbrZriaMCGS8aJraWfgMAvPHVA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里就用到了日期表中添加的工作日编号，通过这个编号的加减，就可以快速定位到N个工作日后是哪一天。  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNbtiatk6CdmYgNu9SjpqPtAAOfSW7UeMnZd6Y4KAmSIcrIpAfymL42lk4gcPlXSYWGsmwViclXfeWg/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

这里的参数我也设置了负数，如果是-10，实际上是10个工作日前是哪一天。  

以上就是关于工作日的几种常见计算，有了日期，再计算这些日期对应的业务数据就很简单了。

**上面的计算并没有专门的函数，我们只需要掌握工作日的逻辑常识，配合常用的DAX函数就可以实现各种工作日相关的分析需要，其中的关键是，先完善带有假日标记的日期表。**

这种做法，和之前介绍的关于周的分析，思路是一致的：[学会了这个思路，你也可以轻松进行周分析！](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068253&idx=1&sn=ad3b2929ea9a378e42ac0d8e38ef9cff&chksm=8e0c754ab97bfc5ce978455efcbb7ad88f5f7556f009a79cdf43e2741cf4d294f75becbf17fa&scene=21#wechat_redirect)

当然本文构造的日期表中不仅有工作日，还有各种节假日字段，进行假日的分析同样很便捷，比如想比较每一年春节对应的销售数据，只需要一个切片器就可以了。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNbtiatk6CdmYgNu9SjpqPtAzmnNo2As7TmKH2sXgzjqia15hqHwlC5Eg3fZib9OWtRfIGqvBmsnABbQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN6oGnIQSa3kx3M0QQESdrYCTV9SBx5LXD4kp3icA9LouW3YN2z2njBWWQzM1zia9Fbeky0fdIpNakw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和3800+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMqicSUp5EfHiae4ibtEjIZsDCy5RUEz1Yp2hsG1ExlG3XiaqfWPqspJ1oiaEcKjuJCKPStBaWQXO6SOew/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
