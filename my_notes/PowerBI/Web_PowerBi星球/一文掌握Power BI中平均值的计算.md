---
create_date: 2022-09-06T23:29:31 (UTC +08:00)
tags: 
pagetitle: 一文掌握Power BI中平均值的计算
source: https://mp.weixin.qq.com/s/VRShOW9-X10ylLn-Zgy9Ww
author: 采悟
status: 未阅读
category: 
uid: 
---

本文介绍一下平均值的计算，平均与求和类似，也是一种常用的聚合运算，不过相对于求和，平均的逻辑稍微复杂一点。

比如对2022年的订单销售额求和，无论是先按日求和还是先按照月求和，全年销售额都是一样的，但是对于计算全年的平均值，是按日计算平均值、还是按月计算平均值呢？这两种逻辑的结果是完全不一样的。

计算平均值首先想到的函数肯定是AVERAGE，和Excel中的求平均一样。以PowerBI星球的案例数据为例，写个度量值：

> 平均值 \= AVERAGE('订单表'\[销售额\])

在没有任何上下文的情况下，结果是167.57。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO5zoYR6pbK9IbeSSraiaQlPzwE8ve8Rd8u9JaV8V53sYVpcbaEEULDoTHiabms3icW9JNrS1bpFgxIQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**但是这个数据代表的是什么含义呢？是每日的平均销售额、每个产品的平均销售额、还是每笔订单的平均销售额呢？**

经过验证，可以看出这个数字是汇总销售额除以订单数量，也就是每一笔订单的平均销售额，为什么是这个逻辑呢？

上面的度量值是一种简写，如果改用完整的写法，就能清晰看出这个平均值的逻辑，上面度量值的完整写法如下：

> 平均值 \=AVERAGEX( '订单表' , '订单表'\[销售额\] )

以上两个度量值的结果是一样的。

其实AVERAGE只是AVERAGEX的一种特殊形式，任何求平均值都可以用AVERAGEX来完成。

AVERAGEX是个迭代函数，其中第一个参数，是需要迭代计算的表，在这个表的范围内计算平均值。

对于上面写的度量值，就是迭代订单表的每一行，对每一行所对应的销售额，进行求平均值，也就是每笔订单的平均销售金额（这个示例中，每一行是一笔订单）。

简单来说，按照哪个维度求平均，就构造这个维度的不重复列表，作为AVERAGEX的第一个参数，比如计算每日的平均销售额，第1个参数应该用日期的列表，你可以试试这样写度量值：

> 平均销售额 按日 =
> 
> AVERAGEX(
> 
>     VALUES('日期表'\[日期\]),
> 
>     SUM('订单表'\[销售额\])
> 
> )

第1个参数是没有问题的，但是这个度量值返回的结果竟然和销售额总计是一致的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO5zoYR6pbK9IbeSSraiaQlPLrq80hEHHrygjVfj6jPqxdrMKkSic5bFhNgasZI6KVBq8RzuLyHGHVQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

为什么会出现这种情况呢？

这个问题出在第2个参数上，AVERAGEX的第一个参数表，提供的是行上下文，对第二个参数没有筛选作用，所以每个日期计算的都是销售额总计，然后对这些总计数求平均，最终结果还是总计数本身。  

这个问题该怎么解决呢？只需要行上下文转换为筛选上下文就可以了，有两种方式：  

**1、在第2个参数外面套上CALCULATE**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO5zoYR6pbK9IbeSSraiaQlPX7NauCG7fetoC9yKGHM5HIuicpyiaamYAicoFiax36icoGrW0lYlSdytnibA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**2、第2个参数用度量值**

度量值的特性是内置CALCULATE，可以自动将行上下文转换为筛选上下文，所以可以先写个基础度量值：  

> 销售额合计 \= SUM( '订单表'\[销售额\] )

然后把这个度量值放到第2个参数上。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO5zoYR6pbK9IbeSSraiaQlPhmpeCSg8yTzibprOMjMWibCic3icQJ3gK3nTGHSsgWZGSiaqQAcTpDm2wmw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

利用上面两种方式，就得到了正确的每日平均数据，关于迭代函数，一定要记住这个特性，当发现结果不符合预期时，不要忘了上下文转换的逻辑。

通过上面的解释，应该理解了AVERAGEX的用法，下面再通过几个计算平均值的常见场景来加深对它的理解。

**按年月计算平均销售额**

第1个参数构造不重复的年月维度，这样来写度量值：  

> 平均销售额 按月 \=
> 
> AVERAGEX(
> 
>     VALUES('日期表'\[年度月份\]),
> 
>     \[销售额合计\]
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO5zoYR6pbK9IbeSSraiaQlPEEMRlYjibOKKJGnr9JnSft4kAKzyTs8icg7SeAAWJ1ZWl3WNxC09c0nQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**本年至今按月计算平均销售额**

这个逻辑的详细描述是，如果上下文是2021年3月，则计算2021年1-3月的每月平均数、如果是6月，则计算1-6月的每月平均数，这就要构造一个本年至今的年度月份列表，如下面度量值公式中的阴影部分：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO5zoYR6pbK9IbeSSraiaQlP1nMCEhZSGhQkuPzOyZO3nFBIPx2YExlb5lVy19DyaSoAjEK6v6fFew/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

使用时间智能函数找出本年至今的所有日期，然后从这些日期中提取年月的不重复列表，作为AVERAGEX的第一个参数；第二个参数用指标的度量值。

结果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO5zoYR6pbK9IbeSSraiaQlPyCunUmawDXHfNPrLSAB9zB4Z6BqpRWicQr95TJ2aQpzJlRb3dpbu3RA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**按年月和产品两个维度计算平均值**

这个需求偶尔也会用到，计算平均每个产品每个月的销售额，按两个维度来计算平均，就需要构造两个维度的列表，可以这样来写度量值：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO5zoYR6pbK9IbeSSraiaQlPyhJGereHh20c4OVumTMf98LH2gSsbCXYDWOz10ia7NE1H6DGjYuUrBg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

因为日期表、产品表都与订单表建立有一对多的关系，所以这里可以用SUMMARIZE来构造这两个维度的列表，如果没有这种关系，还可以用CROSSJOIN函数来构造。

用年度作为上下文结果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO5zoYR6pbK9IbeSSraiaQlPy0gzAFL0sYfpP2EC7uP1Bxhib4ibwjvhHeRZUsk3grNBuuYJZSIdMrvg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

通过上面的介绍以及几个例子，关于平均值如何计算应该很清晰了，在写度量值之前，先想清楚，对哪个维度求平均，然后构造出这个维度的不重复列表作为AVERAGEX的第一个参数，将指标作为第二个参数，另外，使用迭代函数时也要懂得如何将行上下文转换为筛选上下文。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你想深入学习Power BI，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和5000+ 爱好者一起精进~**

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门Power BI》电子书，轻松入门。
