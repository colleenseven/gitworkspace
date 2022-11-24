---
ZK: Origin
notes: True
aliases: null
create_date: 2022-02-21T12:22:44 (UTC +08:00)
tags: wx/pbi/建模技巧
pagetitle: PowerBI分析技巧：部门变动问题
source: https://mp.weixin.qq.com/s/3I73MnIdmsZfp2kYO1zV0A
author: 采悟
status: 已完成
category: 精读文章
uid: 
---

DAX:: CALCULATE, MAX,FILTER, ADDCOLUMNS,SUMX

在之前介绍的很多分析中，假定<mark style="background: #FF5582A6;">维度表不会随时间发生变动，但实际情况并不总是如此</mark>，比如我经常会被问到关于部门变动的问题，每个人员所属的部门，随着时间的推移，很可能会发生变动，那么在统计变动前后的部门数据时，就有点困难，这篇文章就来介绍一下这种问题的解决思路。

先看一下部门不发生变动的情况，下面两个表，一个人员表，一个销售表，

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNrVdQ6LHXAloNuuljI8tB2DY8ByPibDvzC6W1eNSuoN4nVvf4zFyCwibM0ee0DEVibN67lkM6kAgPPQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

有四个业务员分别归属于AB两个部门，利用上面两个表，计算每个部门的销量很简单，只需要通过业务员将两个表建立关系就行了。  

上面是理想的情况，实际业务中每个人所属的部门是大概率会变动的，就无法简单的靠一条关系计算出部门的数据了。

假如上面的部门人员表变成下面的结构，记录了每个人员的所属部门以及在该部门的起止日期：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNrVdQ6LHXAloNuuljI8tB2gImzyJ9KndLTicwicaE6fTEZliaicTsYBz9LM51ar9l16nZKuwvQlERwnw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

业务员甲在1月15日之前属于部门A，之后调到了B部门，而业务员丁1月份在B部门，2月份调到了A部门。

在这种情况下，就不能简单的通过一条关系拖拽出部门的销量，并且即使建立关系，也将是多对多的关系，直接聚合的数据是不准确的，那么在PowerBI中如何解决这个问题呢？

最直接的做法是，<mark style="background: #FF5582A6;">在销售表中添加一列部门属性，记录每笔销售业务发生时，该业务员的所属部门</mark>。

计算列可以这样写：

> 部门 =
> 
> VAR date\_=\[日期\]
> 
> VAR name\_=\[业务员\]
> 
> RETURN
> 
> CALCULATE(
> 
>     MAX('部门人员表'\[所属部门\]),
> 
>     FILTER(
> 
>         '部门人员表',
> 
>       '部门人员表'\[业务员\]=name\_&&'部门人员表'\[开始日期\]<=date\_&&'部门人员表'\[结束日期\]>=date\_)
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNrVdQ6LHXAloNuuljI8tB2dTVibZU0ibawj9QXLgzlEqicJ4kvwYo8X5o19WOyA8SftQDUAc6QugzkQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这个计算列的逻辑就是<mark style="background: #FF5582A6;">通过销售表每一行的日期和业务员名称，去部门人员表中筛选匹配对应的部门。  </mark>

有了这一列部门，再去统计每个部门的销量就非常简单了，直接用部门列和销量生成一个表格就行了。

除了使用计算列，也可以<mark style="background: #FF5582A6;">用度量值实现</mark>的，度量值如下：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNrVdQ6LHXAloNuuljI8tB26mjiaIk2wibcHVlYXu7dhY9ED3IbChjOQSxu6oakS2hZepzs5BeT6stw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

度量值的逻辑其实<mark style="background: #FF5582A6;">和计算列是一样的，计算列是在销售表上直接添加可见的部门列，而这个度量值是构造了一个虚拟销售表</mark>，在虚拟表中添加了一列部门，然后利用当前上下文来筛选虚拟表中的部门，返回销量合计。  

度量值的好处是，可以在<mark style="background: #FF5582A6;">不对模型中的表做任何改动的前提下，来实现分析目的</mark>。将部门人员表中的部门作为上下文，这个度量值就可以计算出该部门的销量：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNrVdQ6LHXAloNuuljI8tB2oZyusl11naqx6aKtUDsnbiby6ibSouOAficjplQ21EZgSMyPCibBcKCZFw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

如果表格的合计数不正确，请根据这篇文章修正：[Power BI 总计错误的终极解决方案(二)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072950&idx=1&sn=fdd3128f59f1797c5a1dad976604f0bb&chksm=8e0c5b21b97bd237c39d1afb7e89f7b453c4fc12b09456aaaca57dd83dbf3e71208752d11b6a&scene=21#wechat_redirect)

上面两种方式都可以解决部门发生变动的数据统计问题，当然方法也不止这两种，另外具体的计算逻辑也取决于维度表的结构。

上面的部门人员表，有两列日期，记录了每个人的在该部门的起止日期，可能有的变动表只有一列日期，记录每个业务员在某部门的开始日期和每次变动日期，这种结构也很常见，计算起来也并不难，整体思路与本文类似。

无论是什么结构，都必须清晰记录必要的部门变动信息，才有可能准确统计出部门的数据。  
