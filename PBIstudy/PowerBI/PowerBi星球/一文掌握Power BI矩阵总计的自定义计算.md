---
ZK: Origin
create_date: 2021-12-07T12:51:18 (UTC +08:00)
tags: 
aliases: null
pagetitle: 一文掌握Power BI矩阵总计的自定义计算
source: https://mp.weixin.qq.com/s/ZdAJgr0KcA9RmdX6e8WxsQ
author: 采悟
status: 未阅读
category: 
notes: False
uid: 
---

关于PowerBI中表格/矩阵，默认的总计很多时候并不能满足我们的需要，最常见的就是总计不等于明细之和的问题，以前专门介绍过解决方案：

[Power BI 总计错误的终极解决方案(二)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072950&idx=1&sn=fdd3128f59f1797c5a1dad976604f0bb&chksm=8e0c5b21b97bd237c39d1afb7e89f7b453c4fc12b09456aaaca57dd83dbf3e71208752d11b6a&scene=21#wechat_redirect)  

除此之外，经常还会遇到特殊的需求，不是让总计行等于明细行之和，而是需要进行自定义的调整，本文以每种产品的收入制作的矩阵为例，通过几种常见的场景来介绍一下。

**1\. 让总计行等于明细行的平均值**  

这种问题很简单，只需要将上面提到的[总计错误的解决方案](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072950&idx=1&sn=fdd3128f59f1797c5a1dad976604f0bb&chksm=8e0c5b21b97bd237c39d1afb7e89f7b453c4fc12b09456aaaca57dd83dbf3e71208752d11b6a&scene=21#wechat_redirect)中，度量值里的SUMX替换为AVERAGEX就可以了。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPAGcszB3onE8Vz2DWrHSGHMDiaicwxhIzVjUmjTmiahPkTAubPNibKdjOwJ6A55Pe2VZw8sXAcdSwNSw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

同理，如果想让总计行等于明细行的最大值/最小值，就把SUMX替换为MAXX/MINX，这几个迭代函数的用法以及计算思路是一样的，只是最后聚合的方式不同而已。  

**2\. 让总计行不含某个明细行的数据**

**如果想让总计不计算某个数据，比如让总计的计算结果剔除U盘的收入，**可以这样来写：  

结果如下：

这里的关键是判断识别哪些是明细行，哪个是总计行，这种判断有很多种方式，**这里我用了最常用的SWITCH+ISINSCOPE组合来进行判断，如果上下文在产品名称的范围内，就是明细行，否则就是总计行。**

如果上下文有多个层级，对于每一层的小计，上面的度量值也同样适用。若在行标题中加入产品类别列，则矩阵中"电脑外设"的小计也会剔除U盘的数据。

而"手机配件"和"智能设备"的小计并没有变化，这是因为他们本来就不包含U盘，所以是否剔除不会影响结果。

**如果只将最后一行的总计剔除，而电脑配件的小计不剔除，应该怎么修改呢？**

度量值中的产品名称改成产品类别就行了，  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPAGcszB3onE8Vz2DWrHSGHwK9v101AVdWMRVgicr0JvLXLqQDv6bc9WHdKKeibqbAcciaOOkzbZic88w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个度量值的逻辑是，只要是产品类别这个范围内，无论是产品名称还是类别，都正常计算收入；否则不再这个范围内的，只能是总计，返回剔除后的数据，效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN1CNFwDGjgPQIE404E0khaH8ic3axTl5mkicOH8ibs6sic8qBa1ADF8ythw6PiaA9wgANWbCJTM2Hk5lQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**进一步再换个场景，让"电脑外设"的小计不包含“U盘”，而总计的数据包含"U盘"，应该怎么写这个度量值呢？**  

在上面度量值的基础上继续修改如下：  

因为有三层：产品明细行、产品类别小计行和总计行，所以度量值中分别判断，返回不同的计算。矩阵中的效果如下：

上面的小计和总计还是由明细行计算得来的，如果想让某个小计/总计按照特定的逻辑返回和明细行无关的数据，应该怎么做呢？下面接着介绍。

**3\. 自定义某个层级的数据**

假如需求是"电脑外设"小计行返回80万，总计行返回200万，其他行逻辑不变，度量值就可以这样写：  

效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN1CNFwDGjgPQIE404E0kha9UhmlNL1YibgdSbia5x2njP5kgkH0vrNCVGZBTicKsPWjCbkaPgib8mWvQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其计算逻辑和上面介绍的一样，通过这种方式，你可以控制任意一个层级的任意一个类别的计算逻辑。

这里是以80万和200万这两个固定的数字举例，如果是其他的逻辑，只要把逻辑用DAX表达出来，在这些数字的地方替换掉成相应的DAX表达式就可以了。  

上面介绍的这几种情况，其计算的逻辑都是类似的，就是灵活运用SWITCH和ISINSCOPE函数判断上下文的层级，相应返回特定的计算。

这里尤其要注意的是，**SWITCH的判断逻辑是有先后顺序的，先判断是否满足第一个条件，如果满足就返回第一个结果，不再进行后面的判断；如果第一个条件不满足，继续判断第二个条件，依次类推。**  

由于SWITCH的条件判断是有顺序的，所以**ISINSCOPE函数的参数要先从最明细层级开始，****如果你一开始就用最高层级（比如大类）作为它的参数，则下面的层级（比如小类和明细）都在大类的范围内，意味着肯定满足第一个判断条件，只返回第一个表达式的结果，后面的都不再判断，这样的结果显然不能达到目的。**

总计的自定义逻辑，很多情况下是作为分母用于占比的计算，通过本文的思路，你应该也能轻松的进行总计行的自定义占比。

关于按层级的占比，你还可以参考之前分享过的层级占比的文章，也是本文SWITCH+ISINSCOPE的组合实现的：

[ISINSCOPE,帮你按层级计算占比](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068912&idx=1&sn=70e9083b581019385e8877d4a91e5a26&chksm=8e0c48e7b97bc1f159d60622393ab8b7a30c3cde30006d465b10cf005ecb58238e84ab77415c&scene=21#wechat_redirect)

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
