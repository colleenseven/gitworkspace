---
ZK: Origin
create_date: 2021-11-08T12:56:08 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI分析技巧：动态展示最近N个工作日
source: https://mp.weixin.qq.com/s/B0xbNFoiwejqXYJubwEL0A
author: 采悟
status: 已完成
category: 精读文章
notes: True
uid: 
---

DAX:: CALCULATE ,MAX,FILTER ,ALL,SELECTEDVALUE ,IF,TREATAS ,VALUES

本文源于一个星友的提问，如何在报告中展示最近7个工作日的数据？这个问题不难，其实更进一步的需求是，如何根据用户选择，动态的展示某个日期的最近N个工作日的数据呢？

这样的问题，其实在以前的文章中，已经介绍过类似的思路，简化一点的问题是，如何动态展示最近N的自然日的数据，这个做法可以参考：[Power BI动态显示最近N天的数据](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484075973&idx=1&sn=bf5b8a1b66b86a933544a2f9580d30c8&chksm=8e0c5712b97bde0422efa22f48fc490a14e1692d17047b16a95dbdd161fc765f3befa77c68fb&scene=21#wechat_redirect)。

在最近N个自然日的基础上，加入工作日的计算就可以了，关于工作日的计算，之前也介绍过：[如何用Power BI进行工作日相关的计算？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077728&idx=1&sn=5d7739914cb98e96b7abd32d402aba3e&chksm=8e13ae77b96427615638ed7351de474f87095c983d3d5c745b94ed1c0fc35a87e34ea247683d&scene=21#wechat_redirect)  

所以上述问题，其实只要把以上两种技巧结合到一起，就可以实现，这里简单介绍一下主要的步骤。

**1、为日期表中添加工作日标记**

方法见：[如何用Power BI进行工作日相关的计算？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077728&idx=1&sn=5d7739914cb98e96b7abd32d402aba3e&chksm=8e13ae77b96427615638ed7351de474f87095c983d3d5c745b94ed1c0fc35a87e34ea247683d&scene=21#wechat_redirect)  

**2、复制一个日期表**

这种<mark style="background: #ADCCFFA6;">动态需求，为了避免切片器与图表直接发生筛选作用，需要有一个独立的日期表，可以直接新建表='日期表'，就可以轻松复制出一个相同的日期表。</mark>
![https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMalyBYDdQeHcOnU56EtTUUdLD6xeScG3D5r2aafd5xljhez4hfkUkUVKpNov3AhlRrPo0fKLibiazQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMalyBYDdQeHcOnU56EtTUUdLD6xeScG3D5r2aafd5xljhez4hfkUkUVKpNov3AhlRrPo0fKLibiazQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
这个日期表无需与模型中的其他表建立关系，所以称之为独立日期表。

**3、新建参数**
在报告中新建一个参数，来动态的切换N天，方法参考：[创建PowerBI「参数」轻松搞定动态分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067672&idx=1&sn=1a141b81b4e20f83cabf410164f55974&chksm=8e0c778fb97bfe9904d988eb9972b26436c260e575d008d1414076b86df997fee74dc559ec73&scene=21#wechat_redirect)
**4、新建度量值**

在建度量值之前，首先应该想清楚，如何进行动态的展现，利用哪些元素来实现我们的需求？

可以用<mark style="background: #ADCCFFA6;">日期表的日期生成切片器，切片器所选作为锚定的日期，动态显示距离该日期最近的N个工作日的数据；用独立日期表的日期来制作图表，比如用柱形图展示，就用独立日期表中的日期作为x轴字段，这样可以避免日期切片器直接筛选柱形图</mark>。  

有了这个思路，就可以写度量值来计算最近N个工作日的每个日期的数据：
![https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMalyBYDdQeHcOnU56EtTUUt7picTuFTpcdE7z8GODSic87MywsMGUiaCvpkrVHs0blveTIPia1SwgwWw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMalyBYDdQeHcOnU56EtTUUt7picTuFTpcdE7z8GODSic87MywsMGUiaCvpkrVHs0blveTIPia1SwgwWw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
这个度量值看着长，实际上是因为我写了详细的注释，你可以根据注释来理解它的逻辑，其中的关键，依然是日期表中添加的工作日字段。  

把这个度量值放到柱形图中，就可以实现最终的效果：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMalyBYDdQeHcOnU56EtTUUDYWJvOJkakLOKduY6iblYS2e5icPEEZumrVibicBxMQ9rTBiaUs8ZqKprkQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

仔细观察X轴，就会发现，柱形图自动跳过了节假日，显示的都是工作日的数据。

如果你也有类似的需求，可以参考以上的做法。  
