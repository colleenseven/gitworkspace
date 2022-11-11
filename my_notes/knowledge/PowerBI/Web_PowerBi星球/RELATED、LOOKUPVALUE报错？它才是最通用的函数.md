---
aliases: null
create_date: 2022-08-19T12:22:27 (UTC +08:00)
tags: wx/pbi/DAX函数
pagetitle: RELATED、LOOKUPVALUE报错？它才是最通用的函数
source: https://mp.weixin.qq.com/s/PMRGL8LCAUUHSCsSJaIogA
author: 采悟
status: 已完成
category: 精读文章
uid: 
---

<mark style="background: #FF5582A6;">不同表之间的查找匹配是很常用的操作</mark>，类似于Excel中的VLOOKUP的做法，很多人在PowerBI中，也习惯于<mark style="background: #FF5582A6;">用RELATED或者LOOKUPVALUE函数创建计算列</mark>，那么也应该碰到过报错的情况，这篇文章就来介绍一下这两个函数的区别、为什么会报错以及一个更通用的写法。

以下面以这个简易的订单表为例：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOaPvUnuiaHJ7oicpt4dfktiaMnIb3gicPibb4y09bUywqdnycfLyuqWrmeKiaAVNtIo3XMic9RxwCib70icvQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其中有不同的币种和相应的外币金额，如果想转换为本币金额，就需要乘以对应的汇率，所以还有一个汇率表：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOaPvUnuiaHJ7oicpt4dfktiaM6QFScbhlVS38eURxc7IFibJCmncxsVcFPlJBXj4DTAqRq5lan1ib3lkg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

需要汇率表中的汇率匹配到订单表中，应该怎么做呢？

下面根据不同的汇率表结构来介绍不同方法，以及相互之间的区别。

**RELATED函数**

对上面两个表建立的关系如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOaPvUnuiaHJ7oicpt4dfktiaMpia7EWUZKf3UfUpLlCwlCVDVFeaqWQBZRfkO6ialJrAfnxIWdAVUcsRg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

一对多的模型关系，可以直接使用RELATED函数，在订单表中新建计算列：

> 汇率 = RELATED('汇率表'\[汇率\])

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOaPvUnuiaHJ7oicpt4dfktiaMDYUKZia4L81tBE9Z1qncvvhk4nYanzoTUEpzAickKJMuRdA0dXF8RAmA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关于RELATED函数，可参考：[_RELATED和RELATEDTABLE_](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068015&idx=1&sn=60ac1e8e4b8ca602f174bab633b61a3b&chksm=8e0c7478b97bfd6e0ffec8cb900aa3eed088cdecbd460da388489a99d9bb9b545611d8e2d089&scene=21#wechat_redirect)  

这样就可以很轻松的将汇率匹配进来。  

但是如果汇率表<mark style="background: #FF5582A6;">增加一个维度，不仅有币种，在不同的年月也是不同的</mark>，变成下面的结构：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOaPvUnuiaHJ7oicpt4dfktiaM5QODHUUyKcgKQVuicVWjLVLg5fTfyOGV5RoBdF3QibOm6kictxFrsnDicQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

需要两个维度匹配才能得到汇率，如果还是<mark style="background: #FF5582A6;">用币种建立关系，只能是多对多关系</mark>。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOaPvUnuiaHJ7oicpt4dfktiaMPCy9TmicJGcjKDr5ibNA3GTMYCmo537RlP0DySpRIiczicbdcEOViaBMByw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这种情况下，用RELATED函数是会报错：_"列不存在，或与当前上下文中的可用表没有关系"。_

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOaPvUnuiaHJ7oicpt4dfktiaMsP2J3jmgaXcPpVPdQhhbOzP6NZ6E8h93qXVl5RVW1F2aDSicq9aPvHg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

报错信息看起来莫名其妙，其实真实原因是：**<mark style="background: #FF5582A6;">RELATED函数只能在一对多的关系中，在关系多端的表(订单表）中使用，提取关系一端的表（汇率表）的数据</mark>，**<mark style="background: #FF5582A6;">如果不存在一对多的关系，将会报错。</mark>

并且对于新的汇率表，还需要按两个维度来匹配，RELATED函数无法做到，这种情况下可以用LOOKUPVALUE函数来实现。

**LOOKUPVALUE函数**

对于上面的情形，RELATED函数不再适用，我们可以<mark style="background: #FF5582A6;">用LOOKUPVALUE函数来建计算列</mark>，这个函数的用法与Excel中的VLOOKUP类似。

> 汇率 =
> 
> LOOKUPVALUE(
> 
>     '汇率表'\[汇率\],
> 
>     '汇率表'\[年月\],\[年月\],
> 
>     '汇率表'\[币种\],\[币种\]
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOaPvUnuiaHJ7oicpt4dfktiaM1r9gOsibiabYx4Ooh0gB14falR4bzEGcEarWQe1Kc6W7icNWCcyKyXN2w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就把汇率匹配过来了。

**<mark style="background: #FF5582A6;">LOOKUPVALUE函数不依赖于关系，无论是什么类型的关系，甚至不建立关系，都不影响，并且它可以按多个维度匹配</mark>。**

正因为如此，LOOKUPVALUE函数的应用场景要比RELATED函数更加丰富。

不过如果汇率表变成下面这样的，<mark style="background: #FF5582A6;">每个月有多个汇率</mark>：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOaPvUnuiaHJ7oicpt4dfktiaM0xOeNZnmPj5S4ELuEavzoqLNtLev1DCSuZQWBicUwdetqmUjtSibrO3A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这种情况如果还用LOOKUPVALUE函数，将会报错：_“提供了含多个值的表，但表中应该具有单个值”。_

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOaPvUnuiaHJ7oicpt4dfktiaMjQOCKYF6jpLRJAQk7h2PkVnzKKxqTI5kcqbYanKSIn5VglcZBLtFPQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这是因为**<mark style="background: #FF5582A6;">LOOKUPVALUE要求查询的结果必须是唯一值</mark>**，如果有多个值将会显示上面的报错信息。从逻辑上来说也容易理解，如果结果有多个值，应该返回哪个值呢？  

对于结果有多个值的情况，LOOKUPVALUE函数也失效了，那么还有什么办法呢？

**<mark style="background: #FF5582A6;">CALCULATE+FILTER组合</mark>**

其实更通用的做法是CALCULATE+FILTER组合，它能够进行各种情况的匹配，对于上面的例子，我们需要的结果是，<mark style="background: #FF5582A6;">如果有一个值就返回该值；如果查找结果有多个值，就返回多个值的平均值</mark>，CALCULATE+FILTER的写法如下：  

> 汇率 \=
> 
> VAR currency\_=\[币种\]
> 
> VAR yearmonth\_=\[年月\]
> 
> RETURN
> 
> CALCULATE(
> 
>     AVERAGE('汇率表'\[汇率\]),
> 
>     FILTER(
> 
>         '汇率表',
> 
>         '汇率表'\[币种\]=currency\_&&'汇率表'\[年月\]=yearmonth\_
> 
>     )
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOaPvUnuiaHJ7oicpt4dfktiaMiaJyVaBRRJOD0ibFeVIvub0Y8uxoYbuX56l6UhKn7h02h4XicvpWYfItw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**<mark style="background: #FF5582A6;">CALCULATE+FILTER组合是更普适的做法，无论建立的是什么关系，无论多少个条件、无论查询结果是否唯一，都可以轻松处理</mark>。**  

通过上面的介绍，你是不是知道了多种匹配的方式，更加理解了这些函数的差异呢？

上面都是用的计算列的方式，再延伸一下，如果用度量值，应该怎么做呢？

**度量值法**

其实上面的这个需求更适合用度量值来实现，在PowerBI中做分析首先应该建立合适的模型，对于上面的订单表和汇率表，有两个分析维度，就是年月和币种，先建两个维度表，然后建立下面的模型：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP1awejph4cohzwxJ5knJic9OPDoJU0lvHrvJicr11MDySrzHTqNnG35fcOZMxBh439IbRGGcN4C0fA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关于维度表和建模可以参考：[_Power BI数据分析入门案例：目标实际对比_](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078691&idx=1&sn=af288fc6a65368973fd64d53fd392a08&chksm=8e13a2b4b9642ba273bd2f6e9b2547048fe0b4c50dfea6188a6a7b7e63aeb3d586d79534a1f5&scene=21#wechat_redirect)

模型建好以后，只需要用聚合函数写个简单的度量值：  

> 汇率 度量值 = AVERAGE('汇率表'\[汇率\])

然后拉个表格，将币种和年月维度表的字段作为上下文，就能匹配出订单中外币金额所对应的汇率：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP1awejph4cohzwxJ5knJic91ARWYVrR3ERBarMj93vzTkLib2POgH9qicTVI9ib6S4aPAcnJ6GyLmang/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

度量值的做法是不是非常简单呢。

**总结**

-   一对多关系的单维度匹配，可以用RELATED函数创建计算列;  
    
-   任意关系、多个维度的匹配，查询结果唯一，可以用LOOKUPVALUE函数创建计算列；  
    
-   任意关系、任意多个维度的匹配，无论查询结果是否唯一，都可以使用CALCULATE+FILTER组合来实现；
    
-   能用度量值尽量使用度量值，模型和度量值的配合通常可以更简单地实现同样的需求、以及更好的性能。
    
