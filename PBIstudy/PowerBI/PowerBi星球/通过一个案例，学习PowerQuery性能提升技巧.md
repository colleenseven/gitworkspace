---
create_date: 2022-11-29T23:51:52 (UTC +08:00)
tags: wx/pbi/PQ数据处理 
aliases: null
pagetitle: 通过一个案例，学习PowerQuery性能提升技巧
source: https://mp.weixin.qq.com/s/iEgEQ_ZLI2sr2oR44_hjVg
author: 采悟
status: 已完成 
category: 泛读文章 
notes: False
ZK: Origin
uid: 
---

PowerQuery可以很方便的实现很多数据整理需求，不过当数据量变得很大时，处理速度通常会变得很慢，本文就通过一个简单的例子，来看看如何提升PowerQuery的处理效率。  

这个示例来自星友提出的一个问题，对于下面这个表，如何计算出某行的类型是第几次出现的：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMPQwhTSpTfPicFAAcDUNVshoBzxduFnhLoRMJsZQP0ib2cUr8ibanrST8CGs9o3OHlh89DHsEINhYWA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

对于这个问题，实现起来并不难，不过不同的方法性能差异很大，下面就来看看这个问题的三种实现方式，以及运行速度的差异。

**方法一：常规方式添加自定义列**

新建自定义列：

> List.Count(
> 
>     Table.SelectRows(
> 
>          更改的类型,
> 
>          (x)=>x\[序号\]<=\[序号\]  and x\[类型\]=\[类型\]
> 
>     )\[类型\]
> 
> )

![https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMPQwhTSpTfPicFAAcDUNVshcpWAVehDFaoIYiaIHyJeAp3FIfnDXN4xOZibHiaIBHJiaib9xrtuKtLYsUQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMPQwhTSpTfPicFAAcDUNVshcpWAVehDFaoIYiaIHyJeAp3FIfnDXN4xOZibHiaIBHJiaib9xrtuKtLYsUQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
计算列的逻辑是统计小于等于当前索引号并且等于当前类型的数量，这样可以计算出来，但是当数据量很大的时候，运算速度很慢，比如上述数据有3000行，我测试**大约需要25秒**才能运算出来，这是让我们难以接受的速度。

**方法二：方法一基础上运用Table.Buffer**

这不是一个新的方法，而是在方法一的基础上进行的优化。

对于方法一的操作步骤，在添加自定义之前，这个例子有个更改数据类型的步骤，利用自定义列进行计算就是在在一个步骤处理后的表的基础上计算的。  

这里优化的操作非常简单，就是==在添加自定义列之前，对上个步骤的M代码套个Table.Buffer函数==，如下：

![https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMPQwhTSpTfPicFAAcDUNVshiaHxe9qNwxvnjwEjiaN9lQdHQeSMibmyiacRaDIicqB54Oou0wXYkSLVsmQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMPQwhTSpTfPicFAAcDUNVshiaHxe9qNwxvnjwEjiaN9lQdHQeSMibmyiacRaDIicqB54Oou0wXYkSLVsmQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后再添加和方法一同样的自定义列，就可以实现需求了。

  
==Table.Buffer是个表缓存函数，在进行计算之前，先把表缓存起来，很可能会提升计算速度==，在Excel中点击全部刷新，方法2的运行速度明显更快。

通过上图可以看出二者的差异，**当方法二完成3000行的计算时，方法一才加载712行，性能提升约4倍。**
![https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMPQwhTSpTfPicFAAcDUNVshS5vCIfV96lQMCwPiaGdDrtXOJiayiaWjc3qaJIAbVQvToVzMlcpTz02KA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMPQwhTSpTfPicFAAcDUNVshS5vCIfV96lQMCwPiaGdDrtXOJiayiaWjc3qaJIAbVQvToVzMlcpTz02KA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**方法三：利用分组**

对于这个需求，计==算每个类别在当前行累计出现的次数，实际上是按类别添加索引==，那么我们就可以利用分组来实现这个需求。

关于按类别添加索引的具体做法可以参考这篇文章：[PowerQuery添加索引，这几种情况你应该知道怎么做](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484079711&idx=1&sn=8b4718135399c3bb8e6e1d917e3acd70&chksm=8e13a688b9642f9e25e06cd4c0460b9b472f549854b3645ea81c2457a5b3cc9c35c629ef0c7c&scene=21#wechat_redirect)

按分组添加索引列与上面添加自定义列的结果是一样的。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNknhR7Fxv7EJ6aQSh8nEolcc3jxUDNS0hezsExYEeU9z72LOWKxsXytnhhPhtrdPJssA1oaYgibiag/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

下面依然通过全部刷新的方式来看看处理速度的差异：  
![https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNknhR7Fxv7EJ6aQSh8nEolOIpZq9cAUxJyvDjbL8tN1yO4PRCLAC4WOsvdXbLSes0unKxhy9rEsA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNknhR7Fxv7EJ6aQSh8nEolOIpZq9cAUxJyvDjbL8tN1yO4PRCLAC4WOsvdXbLSes0unKxhy9rEsA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
**方法三点击刷新后即时加载完成，前面两种方式甚至还没有开始，这个处理速度非常快。**

通过上面三种方式的对比，第三种方式更优，但是这种方式取决于特定的需求，仅限于可以使用分组的情况；第二种方式适用范围更广，虽然添加这个函数并不一定能大幅提升性能，但是当你感觉速度很慢时，套用Buffer类函数都是一个便捷的尝试。
