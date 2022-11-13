---
aliases: null
create_date: 2022-10-10T16:55:29 (UTC +08:00)
tags: wx/pbi/DAX函数 
pagetitle: Power BI如何进行收益率相关的计算？
source: https://mp.weixin.qq.com/s/IXGtLDzNBwL21ncx0zOn8A
author: 采悟
status: 已完成 
category: 泛读文章  
uid: 
---
DAX :: PRODUCT, 

在投资分析中，经常会碰到收益率相关的计算，本文介绍一下如何在PowerBI中实现，以下面这个从2017年到2022年每年的收益数据为例：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNnicYHklQVPkNUbztkWTlHvzQvOoeSliavpUMdzXExb4Faz5sbFbLkjtornjm2sh6pMjK9EDLnzT2A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如何计算这<mark style="background: #FF5582A6;">6年的累计收益率</mark>，以及年化平均收益率呢？

对于累计收益率，从逻辑上看肯定不是对这些年度的收益率相加，而是连续相乘，这种应该如何计算呢？

求和的函数是SUM，相乘也有对应的函数：<mark style="background: #FFB86CA6;">PRODUCT</mark>，不过对于上面的收益率，并不是该列数据的简单相乘，而应该是每年（1+收益率）的乘积，这种情况下使用迭代函数PRODUCTX更合适。

PRODUCTX函数的用法与SUMX类似，只是<mark style="background: #FF5582A6;">逻辑为迭代乘积</mark>而已，语法如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNnicYHklQVPkNUbztkWTlHvLSddszvR5fAOaqJAKMpT4fiaYgicDHevETrtxaoibyZIJ2SJ5XLaSl4rQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

参考：[DAX函数卡片](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078871&idx=1&sn=d1cb3e4e2b45dfb58e9b93186c656c11&chksm=8e13a3c0b9642ad6d13a7d9e1be88d69eeba9d9b43b365d8a06398081189eae0874897ee9bab&scene=21#wechat_redirect)

对于累计收益率的计算，可以用PRODUCTX直接写个度量值：

> 累计收益率 =
> 
> PRODUCTX(
> 
>     ALL('数据表'\[年度\]),
> 
>     1+\[当年收益率\]
> 
> )-1

其中当年收益率 = SUM('数据表'\[收益率\])

这个度量值的逻辑是迭代所有的年度，计算出每个年度的 1+\[当年收益率\] 后，对这些数据相乘，最后减去1，得到累计的收益率。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNnicYHklQVPkNUbztkWTlHvEmoPCCVDqdOcEM2t564gfAxGGY8nzvhfxPaqGP4tfLAbFh7OHicLtPg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

知道了累计收益率，如果还想计算这<mark style="background: #FFB86CA6;">6年平均每年的年化收益率</mark>，应该怎么做呢？

其实是对累计收益率开6次方根，这也有对应的DAX函数：<mark style="background: #FFB86CA6;">POWER</mark>，其语法如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNnicYHklQVPkNUbztkWTlHvluiciccS8lVVoZia2LFXDj1kulCGhuMmCfZwZO1gnavQNRDicqVkPyjsYA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

POWER是个幂函数，第二个参数如果大于1，就是计算某个数的N次方，如果是小于1的分数，相当于计算某个数的N次方根，对于上述年化收益率的计算，因为有6个年度，所以度量值可以这么写：  

> 年化收益率 = POWER( 1+\[累计收益率\] , **1/6** )-1

对 **1+\[累计收益率\]** 开六次方根，然后减去1，就计算出了年化收益率。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNnicYHklQVPkNUbztkWTlHvA3zvEMoXEr4JwGpdKzYQ3gIgTkIr8XxDUJVgw2xziaoHPynI5vfO1jQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

除了上面全部年度的整体计算，如果想计算出<mark style="background: #FF5582A6;">截至当前年度的累计收益率和年化收益率</mark>，应该如何做呢？

只需要利用<mark style="background: #FFB86CA6;">FILTER</mark>函数，筛选出小于等于当前年度的数据，进行在此基础上进行累计和年化就可以了。

> 截至当前年度 累计收益率 =
> 
> PRODUCTX(
> 
>     FILTER(ALL('数据表'\[年度\]),'数据表'\[年度\]<=MAX('数据表'\[年度\])),
> 
>     1+\[当年收益率\]
> 
> )-1

然后在此基础上计算年化收益率：  

> 截至当前年度 年化收益率 \=
> 
> POWER(
> 
>     1+\[截至当前年度 累计收益率\],
> 
>     1/(MAX('数据表'\[年度\])-2016)
> 
> )-1

结果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNnicYHklQVPkNUbztkWTlHvChr83Miby82wVHMPiaQ6oPHa1PoAkU8NN9sqR1eoMmuZIZRKoVkPkSOw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

理解了上面这个简单的例子，再进行收益率相关的计算应该就很轻松了，关键是掌握PRODUCTX和POWER函数的用法。
