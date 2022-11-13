---
create_date: 2021-12-21T12:49:39 (UTC +08:00)
tags: 
aliases: null
pagetitle: PowerBI业务分析：贡献TOP N%销售额的产品数量
source: https://mp.weixin.qq.com/s/iUqloC6PzT_IyNBKcBVzJA
author: 采悟
status: 未阅读
category: 
notes: False
uid: 
---

上周末碰到一个知乎用户的留言，问我如何计贡献前80%销售额的产品数量？之前也碰到星友提到过类似的问题，这也算是一个常见的分析需求，这里就来介绍一种计算思路。

这种计算首先要计算出每个产品的销售额累计占比，关于累计占比，和之前介绍的帕累托分析的累计占比是一样的，其实这也是帕累托分析的一种形式，帕累托分析是根据累计占比进行分类，这里是统计某分类的数量有多少。

下面就以计算前80%销售额的产品数量为例，并在此基础上实现任意TOP N%销售额的产品数量统计。

**1\. 计算每个产品的累计占比**

关于累计占比的逻辑可以参考之前介绍的[帕累托分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067854&idx=1&sn=bd282fa65514734b6762b63704fae8f2&chksm=8e0c74d9b97bfdcf7677fadf031b177fd1e89b8a5695928f8e33173cb6a338d03d221ebb7953&scene=21#wechat_redirect)，不再介绍，这里直接写一个累计占比的度量值。

```
累计占比 = 
```

这样就可以计算出每个产品所对应的累计占比：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP2ywNHibqKicOs8bhBnicZS5JqFEqNSEjgpiajETic3YPWiaHSBbfLcsoHd039DYq7tZicyZgjjrU4I1pOw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**2\. 计算贡献前80%销售额的产品数量**

关于这个计算，换一种说法是，按销售额从高到低排序，哪些产品的销售额合计超过总体的80%，所以并不能简单按累计占比小于等于80%来统计（很可能贡献不到80%），而应该按照超过80%的最小累计占比来统计产品数量。

写度量值如下：

```
销售额贡献前80%的产品数量 = 
```

这个度量值的逻辑是先构造每个产品所对应的累计占比的虚拟表（这个虚拟表与上面的表格完全一致），然后找出累计占比大于等于80%的最小值，最后统计累计占比小于等于该最小值的产品数量。

这个度量值的结果返回7，通过上面的表格也可以看出，销售额排名前7个产品到"智能手表"，累计占比为80.9%，恰好刚超过80%。

**3\. 计算贡献销售额TOP N%的产品数量**

生成一个[参数](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067672&idx=1&sn=1a141b81b4e20f83cabf410164f55974&chksm=8e0c778fb97bfe9904d988eb9972b26436c260e575d008d1414076b86df997fee74dc559ec73&scene=21#wechat_redirect)，并将上面度量值中的0.8替换为参数:  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP2ywNHibqKicOs8bhBnicZS5Jpyady3Aow2Inoo3FZsT8iaUeV2icEUH9UKCOV0SmO8qVlODtFIRse27w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

就可以得到任意一个贡献百分比的产品数量。

更进一步的，如果还想动态显示出来具体是哪些产品，可以参考之前[动态展示表](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074639&idx=1&sn=03b003d199f754794c0bac8af15c50e0&chksm=8e0c5258b97bdb4e0aa92667a047bca5c7705f86a6c2b4ac66e3eefc171ca95e6891a433ecff&scene=21#wechat_redirect)的思路，写一个度量值：

```
是否在TOP N% = IF([排名]<=[销售额贡献前TOP N%的产品数量],1)
```

其中排名是一个已经写好的度量值（参考：[这几个示例，帮你深入理解RANKX排名](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068781&idx=1&sn=4f7d7abed75b6db6cae3b23a45e7dfbe&chksm=8e0c4b7ab97bc26c2303edcd22dad9261981486689833504f129603f5b20a7b8f8d3669517e6&scene=21#wechat_redirect)），就是每个产品的销售额排名，如果排名小于等于上面计算的产品数量，返回1，然后将它放到矩阵的筛选器中，筛选等于1的数据，就可以得到这个动态的效果：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJP2ywNHibqKicOs8bhBnicZS5Jne6OibbraNeTuoBTH7RkCRjic4YBECczEibN37oON6s1wJBwlR8GmMZ9g/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

本文是以计算产品数量为例，实际业务中你也可能是想计算贡献前80%的客户、贡献前70%的部门等，都可以参照这个思路。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
