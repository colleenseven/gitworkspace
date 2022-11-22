---
ZK: Origin
notes: Fa'l'se
aliases: null
create_date: 2022-01-14T12:31:47 (UTC +08:00)
tags: 
pagetitle: Power BI数据分析入门案例：折扣计算问题
source: https://mp.weixin.qq.com/s/RX0xUbDXwyP3Q5hqzDIIHQ
author: 采悟
status: 未阅读
category: 
uid: 
---

前面介绍了两个Power BI数据分析入门案例：

[Power BI数据分析入门案例：目标实际对比](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078691&idx=1&sn=af288fc6a65368973fd64d53fd392a08&chksm=8e13a2b4b9642ba273bd2f6e9b2547048fe0b4c50dfea6188a6a7b7e63aeb3d586d79534a1f5&scene=21#wechat_redirect)  

[Power BI数据分析入门案例：费用分摊问题](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078793&idx=1&sn=b095fe7e6e4d4bd1e85dbbc558313b3f&chksm=8e13a21eb9642b085b9086c1a7792e4656f4c3ad6a14b2111a3a57dd0c20996481d4fac9141c&scene=21#wechat_redirect)  

本文再介绍一个经常会遇到的折扣计算问题，下面这个案例以前也曾经介绍过，这里作为一个PowerBI入门分析案例再梳理如下。

假设订单表结构如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNtvAKNYHIAkpAcdCBUMIUqxdeEBL5q7tj0xHxiaoVJ8gofrapf3EgVJ2f9H9gpFqMcs30GdyM3y6w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

记录有每个产品在各个平台上的原价和每日销售数量。

另外还有一个折扣表，记录了促销期间每种产品在各个平台的折扣率：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNtvAKNYHIAkpAcdCBUMIUqjwhjpHHAqMboDMUqOKDBXONqZKSA7iac0vBralxaYs6XZjCsicUEiaYdQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**每个平台上的折扣不同，并且促销起止日期也有差异，如何通过以上两个表快速计算各种维度下扣除折扣后的净销售额呢？**

这个案例相比前两个稍微复杂一点点，产品在不同的平台和期间有不同的折扣率，并且日期有两列，不过整体思路依然不变，下面是实现步骤。

**1\. 完善维度表建立模型**

构造模型是PowerBI数据分析的基础，先梳理需要分析的维度，建立合适的模型，而不建议拿到数据，直接就利用这些表开始写度量值计算。

就以上的分析需求来说，分析维度是三个：日期、平台和产品，所以先做三个维度表，都可以利用DAX来生成。

日期表制作很简单，以前专门介绍过：[玩PowerBI必备的日期表制作方式汇总](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067654&idx=1&sn=905c186a9cbd91159b6615924a2d5068&chksm=8e0c7791b97bfe87623904f7002cd6cb726f711c6e7a289a36c9a4973964d907493aa2397fe7&scene=21#wechat_redirect)

平台表和产品表都可以从订单表中抽取不重复的数据作为维度表，直接这样写就可以了：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNtvAKNYHIAkpAcdCBUMIUqNLyJKSIF9WPUM0KxVLXmvqfbhzfGTKBlmtDNDIJXtuTLqcAbgE2y8g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOmElzQibiamP2zWRMt33oCQoic1ebWZqDkIOTuic9nKVZOl4uOHTPStgHYY2nHMgA5SCZTSFtEgia6nsw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

维度表做好以后，可以这样来建立模型：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNtvAKNYHIAkpAcdCBUMIUqacH6SngeXTT3uVcNwY5rr54sib5WDIsGUS3ok34DI8yOaMHkibFF31XQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里需要注意的是，由于日期表与折扣表中的日期并不存在直接的对应关系，不用建立关系；虽然没有建立关系，我们还可以利用DAX来实现按日期的筛选查找，下面会看到。

**2、建立度量值**

首先写一个基础度量值来计算折扣前的原始销售额：  

> 毛销售额 \= 
> 
> SUMX('订单表','订单表'\[单价\]\*'订单表'\[销售数量\])

然后是折扣率的计算，如何计算出每个订单所对应的折扣率是重点，度量值可以这样写：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNtvAKNYHIAkpAcdCBUMIUqLBmx82AI2ibdZOia1kRLicCjlkCcmu7bj2Ky0eribmzRRCEiaHIU9z50wjQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这就是利用DAX，通过上下文的信息去筛选折扣表（日期没有建立关系，利用FILTER按起止日期两列筛选），找出筛选后的折扣表所对应的折扣率。  

有了这个折扣率，就可以计算净销售额了：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNtvAKNYHIAkpAcdCBUMIUqbBsfFEzf2B23WKH697esGKLentsCGMqVmwuX1z6Okf94ibRvtRES5GQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里并不能简单的用毛销售额乘以折扣率来计算，因为如果没有明细的上下文，是无法准确的计算折扣率的。这个度量值中SUMMARIZE返回的表，是构造折扣率计算所需要的内部行上下文，无论外部筛选上下文是什么，在这个度量值内部，总能提供包含日期、平台、产品维度的上下文。  

并且这样的写法也能确保总计等于明细行之和（关于总计行的问题可以参考：[Power BI 总计错误的终极解决方案](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072950&idx=1&sn=fdd3128f59f1797c5a1dad976604f0bb&chksm=8e0c5b21b97bd237c39d1afb7e89f7b453c4fc12b09456aaaca57dd83dbf3e71208752d11b6a&scene=21#wechat_redirect)）。

**3、展示计算结果**

完成了上面的步骤，最后这一步就非常简单了，选择合适的可视化类型展现就可以了。

这里用矩阵来展示结果，将维度表中的字段放到矩阵的行中，毛销售额和净销售额度量值放到值中，就可以利用上下钻取来查看每一个维度折扣前后的销售额。  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNtvAKNYHIAkpAcdCBUMIUq1lKLOhy1j2KxDAj7PMrtau1EqYGKzu8ibLfKBQg8cpJ4XdpdL71JmUA/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

以上就是PowerBI折扣计算的实现思路，这里因为特殊的数据结构，在建模时无法直接建立的时候，利用DAX完成最终的计算。

建立合适的模型可以更简单的完成分析，但并不能仅通过建立模型就能实现变幻多端的分析需求，所以想掌握PowerBI，还必须学习DAX，二者结合，才能灵活解决各种业务分析问题。  

其实用PowerBI做各种业务分析，抛开细节的业务逻辑，主要的步骤均是如此，关键是要多思考多练习，做到举一反三。

本文示例文件可以在「PowerBI星球」公众号后台发送"折扣计算"获取。

[**PowerBI星球的最新版****内容合辑****，值得你收藏学习：**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078675&idx=1&sn=07abf841815e43fb0a554081c82de72a&chksm=8e13a284b9642b92d07b518abe3e6e2e2ef5066c0941c1ced26a245a6990b4330830431789a9&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN8YOicNXzCaSLpQrKXOL0LsNeYw0fj3iaGFy7XSwwmibHicdtiaHEbhgmHSPXQlkg3WiaVA4hJ8PGDcdEQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078675&idx=1&sn=07abf841815e43fb0a554081c82de72a&chksm=8e13a284b9642b92d07b518abe3e6e2e2ef5066c0941c1ced26a245a6990b4330830431789a9&scene=21#wechat_redirect)

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**  

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
