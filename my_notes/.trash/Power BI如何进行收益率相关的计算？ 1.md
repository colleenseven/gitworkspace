---
create_date:2022-10-27T17:42:11 (UTC +08:00)
tags: 
pagetitle: Power BI如何进行收益率相关的计算？
source: https://mp.weixin.qq.com/s/IXGtLDzNBwL21ncx0zOn8A
author: 采悟
status: 
category: 
uid: 
---

在投资分析中，经常会碰到收益率相关的计算，本文介绍一下如何在PowerBI中实现，以下面这个从2017年到2022年每年的收益数据为例：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNnicYHklQVPkNUbztkWTlHvzQvOoeSliavpUMdzXExb4Faz5sbFbLkjtornjm2sh6pMjK9EDLnzT2A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如何计算这6年的累计收益率，以及年化平均收益率呢？

对于累计收益率，从逻辑上看肯定不是对这些年度的收益率相加，而是连续相乘，这种应该如何计算呢？

求和的函数是SUM，相乘也有对应的函数：PRODUCT，不过对于上面的收益率，并不是该列数据的简单相乘，而应该是每年（1+收益率）的乘积，这种情况下使用迭代函数PRODUCTX更合适。

PRODUCTX函数的用法与SUMX类似，只是逻辑为迭代乘积而已，语法如下：

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

知道了累计收益率，如果还想计算这6年平均每年的年化收益率，应该怎么做呢？

其实是对累计收益率开6次方根，这也有对应的DAX函数：POWER，其语法如下：  

POWER是个幂函数，第二个参数如果大于1，就是计算某个数的N次方，如果是小于1的分数，相当于计算某个数的N次方根，对于上述年化收益率的计算，因为有6个年度，所以度量值可以这么写：  

> 年化收益率 = POWER( 1+\[累计收益率\] , **1/6** )-1

对 **1+\[累计收益率\]** 开六次方根，然后减去1，就计算出了年化收益率。

除了上面全部年度的整体计算，如果想计算出截至当前年度的累计收益率和年化收益率，应该如何做呢？

只需要利用FILTER函数，筛选出小于等于当前年度的数据，进行在此基础上进行累计和年化就可以了。

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

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你想深入学习Power BI，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和5000+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMstwXX5zrKianmFXzyqbIVgh7byfo3V8JJPmhqicywbtYkM0j2ibngnT5XBZ2AwKvGZiby9ngoKfLvzg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门Power BI》电子书，轻松入门。
