---
ZK: Origin
create_date: 2021-12-14T12:50:27 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI交互技巧：动态切换自然年/财年计算
source: https://mp.weixin.qq.com/s/TFaJAOWv-eOVnuSKLYHaPw
author: 采悟
status: 未阅读
category: 
notes: False
uid: 
---

之前分享过如何用Power BI进行财年的计算（[Power BI如何进行财年分析？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074450&idx=1&sn=9d93855543a3a7ef6df17233edc49b18&chksm=8e0c5d05b97bd41305136591195caed2eb8c15f7bf05f00e061b1f9b29d2698b2a5d3fd8e2f5&scene=21#wechat_redirect)），最近有星友问到，如果想在报告中动态切换财年和自然年的数据，应该怎么做呢？

这种动态效果用PowerBI设计并不复杂，以财年分析的数据为例，这里介绍一种简单的实现方式。

**1\. 构造混合日期表**

在[财年分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074450&idx=1&sn=9d93855543a3a7ef6df17233edc49b18&chksm=8e0c5d05b97bd41305136591195caed2eb8c15f7bf05f00e061b1f9b29d2698b2a5d3fd8e2f5&scene=21#wechat_redirect)中，已经在正常日期表的基础上增加了财年的字段：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNwdGaD6PCEPcE4mgDCfDAMJWtGqCr8NMjQAG3IOInarHe3OCia5LnoIsmpMLHWgkjE22XRqW0N8lw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里因为要动态切换自然年度和财务年度的计算，就需要在同一个字段中同时体现两种日历类型，用DAX新建表:

```
混合日期表 = 
```

生成如下一张日期表：

实际上就是将两种日期表合并为一张表，具体字段可根据你的业务需要补充，这个表不用和原模型中的表建立关系。

**2. 建立度量值**

由于混合日期表没有建立关系，如果要让这个日期表产生筛选作用就可以利用TREATAS函数来建立虚拟关系，计算每个期间的收入，可以这样写度量值：  

```
收入  = 
```

计算本年累计的收入可以这样来写：  

```
收入 YTD  = 
```

这里的财年假设是到9月30日结束，所以TOTALYTD的最后一个参数是“9-30”，实际应用中你根据具体情况修改该参数。  

**3. 展示结果**

利用混合日期表中类型生成切片器，并用该表的年度和季度作为矩阵的上下文，就可以动态切换每个期间在不同日历下的收入、本年累计收入：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPEX2fYQSAJzPABRHG7j0OjhYTBSOOt3CIkYV2LgNyqqWR6cNVEgplLotibafhJbcd4crt56uHx8nw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

还可以用柱形图来展示不同日历期间的收入：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPEX2fYQSAJzPABRHG7j0OjqiaOt7OWsXphSISzR5JqWibDlicug6yTbWHbXHSCtaw8sHAms2J1aJ0Ng/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

仔细看看这个图表，X轴显示的分类是也是动态变化的，其实这里介绍的动态切换财年/自然年度的计算，与之前介绍过的动态坐标轴设计思路完全一致：

[PowerBI技巧：制作动态坐标轴](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068004&idx=1&sn=750fce682b8e15757b038d30aa5a540f&chksm=8e0c7473b97bfd65f68616c2ced6fe5a139e11ccd70b933f92bde1278ff02abedbbe377a3f71&scene=21#wechat_redirect)  

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
