---
aliases: null
create_date: 2022-03-29T11:56:52 (UTC +08:00)
tags: 
pagetitle: 关于Power BI矩阵，这5个常见的问题你应该也遇到过
source: https://mp.weixin.qq.com/s/R4v1CpFsZ3u6JpPpbnwjUw
author: 采悟
status: 未阅读
category: 
uid: 
---

PowerBI中的矩阵作为最常用的可视化类型之一，每个人都用过，关于它的问题也是大家平时问的最多的，虽然难度不大，但是如果遇到这些问题总是很困扰，不知道如何解决，这里就挑选几个常见的问题，集中解答如下。

**1、构造矩阵为什么会报错？**

当你构造个矩阵，但是将行列字段放进去时，有时会发现报错了：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNTWUorjzibqYvnAtqGDADnvwCw6XGIklLib0E4jwIDv8HVNJWOjhDzI9hwY5Z6kKnstOrtz20lQzRQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

点击“请参阅详细信息”，会出现这个提示：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNTWUorjzibqYvnAtqGDADnvdcPP5TL7JXQJsvooAvSYo7xJGJBWgicDwdsKlbHte9TqfvAn8gdRshQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这是因为构造的矩阵，行和列本来也就没有关系，不过不用考虑这个报错，在【值】中放入相应的字段，报错自动就会消失的。  

**在使用PowerBI时，不要被操作过程中间出现的报错所影响，将图表要求的所有必须字段都放进去以后再看有没有报错。**

用DAX写度量值也是如此，你写一部分公式就按回车确定，肯定会报错，这时去找错误没有意义，只有全部写完，再按回车确定，才能确定你写的度量值有没有语法错误。

**2、为什么不显示数据？**

当你把所有字段放进去，还可能出现下面这个情况，矩阵里没有数据：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMTmUeqoNcUGWbQoEeDibYWGKQ078jtYYD2gstibrErJO7C1eXFEuianxksoia4O7icUZE1A1Q9ibAKXpWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

如果你的度量值是正确的，那么重新选中矩阵，点击右上角的按钮，展开层级就可以了。  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMTmUeqoNcUGWbQoEeDibYWGdYicTLxKToewTULic15DtIulrEth2YyNWm1YPuUmXEAeyGUJcicbmmOicw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**3、列标题排序问题**

行标题排序很简单，但是对于列标题的字段，如何按需要排序呢？  

如果列标题是文本，默认是按文本字母的顺序来排列的，如果需要对列标题自定义排序，其实还是利用"按列排序"功能，对列字段按照某个数字序列来排序，请参考：[自定义排序技巧](https://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068059&idx=1&sn=28dff6992fe6d167f4a2fbd6a0c40460&chksm=8e0c740cb97bfd1a55d7789987c7c1ed2ac94a07529cc0428b1cdf48216671f468fa7820c420&scene=21#wechat_redirect)  

**4、无法根据原始数据自动缩进**

为了让数据更有层次感，你设计的原始数据可能是这样的，用空格缩进了几个字符：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMTmUeqoNcUGWbQoEeDibYWG34qq9Pjbfiazkcv448rNKNUH6F6h5iaXkD7CuMnzT0Tv9J6bvz0ZkLiaA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

但是将字段放入到矩阵以后，发现这样做并没有用，这个字段仍然自动对齐了：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMTmUeqoNcUGWbQoEeDibYWGXm30bUHqe9SApyuLGIV4EibV4zibphibP7GsNaSFNKVWhIk1dNOiaRybfQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

其实想要和原始数据一致，只需要在行标题中，关闭文本的自动换行就可以了：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMTmUeqoNcUGWbQoEeDibYWGAAKJicWJMCK8j2f313699G37PLWPNWgUXqbkfytMowDcP1OedqyaYYQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

关闭后就会出现如原始数据一样的自动缩进效果：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMTmUeqoNcUGWbQoEeDibYWG4FvuGKSpvhLOG2SiabV9x3ognUt4V9YAVSpibaTss8hjW6DJicFPsP51g/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**5、按矩阵格式导出数据**

这个需求非常普遍，目前PowerBI desktop还不支持这个功能，不过目前在PowerBI服务中已支持，你只需要先将报表发布到PowerBI服务中，然后点击矩阵右上角的三个点，导出数据：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMTmUeqoNcUGWbQoEeDibYWGF2IibyPxicSvUvePzU87ne8G0VxTa815WfHCJTYmKE8PL9sX0yibbibesw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

然后选择按照“具有当前布局的数据”导出即可。

关于矩阵，还有很多人会问到格式的问题、总计行的问题等，这些之前都已经介绍过，你可以看看下面这些文章：

[Power BI矩阵格式设置13招](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071983&idx=1&sn=3fd379f7bf88141747ac9a09dc4273b7&chksm=8e0c44f8b97bcdee4cb068fd1e47e033629cf0734dd29c8341746d449372068dbb4e6d298cba&scene=21#wechat_redirect)  

[Power BI总计错误的终极解决方案](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072950&idx=1&sn=fdd3128f59f1797c5a1dad976604f0bb&chksm=8e0c5b21b97bd237c39d1afb7e89f7b453c4fc12b09456aaaca57dd83dbf3e71208752d11b6a&scene=21#wechat_redirect)  

[Power BI矩阵总计的自定义计算](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078406&idx=1&sn=3f64d35e34d0f9cd0d5483ee46bf124a&chksm=8e13ad91b9642487e4c2e64af7c944c76ef506eab1a9ecb731173a3cbfbf57b46da9c2cd855e&scene=21#wechat_redirect)  

[Power BI矩阵的自定义配色](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078467&idx=1&sn=ad4e9834b50b19df4b0d79d156dfe0b3&chksm=8e13ad54b964244279a717fb8ddaa704cc3b5a1bf6f63fb377dd1f2d7c97f4c868b14d7799c5&scene=21#wechat_redirect)  

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
