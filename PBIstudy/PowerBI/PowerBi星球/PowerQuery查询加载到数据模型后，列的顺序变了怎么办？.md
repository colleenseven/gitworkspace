---
ZK: Origin
notes: True
aliases: null
create_date: 2022-10-26T23:16:48 (UTC +08:00)
tags: wx/pbi/建模技巧
pagetitle: PowerQuery查询加载到数据模型后，列的顺序变了怎么办？
source: https://mp.weixin.qq.com/s/ZOQH-vima84K5a3wXquBOQ
author: 采悟
status: 已完成
category: 泛读文章
uid: 
---

DAX ::  SELECTCOLUMNS , UNION  

---

你应该碰到过这样的问题，在PowerQuery编辑器中处理后的表，上载到模型以后，列的顺序变得不一致了，比如这个表，在PowerQuery中是这样显示的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMU58I3mBnfBsYpsODk574ZgQkMNL2rjv3hMHqCBuydEvwY1bN6QwyUN0kRFbXCibxqibHVt6KbSFNw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

但是上载到模型中以后，在数据视图中看到的表是这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMU58I3mBnfBsYpsODk574ZbPokiaz2BexRtFlozadib9NXCL89dGIDqo5yicm38YKT9Z8Kf8mMooic3Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

商品名称列的顺序是不一致的，为什么会出现这种情况呢？这篇文章就来介绍一下这个问题以及解决的思路。  

如果这个表是第一次从PowerQuery上载到数据模型，是不会出现这个问题的；但是上载后，再返回到PQ编辑器中进行数据整理，重新调整了列的顺序，调整完再次上载，就会出现不一致。

这个小问题几年前就有人提出来，但是微软也一直没有改进这个功能，对于这种情况，虽然可能看起来不舒服，一般情况下也并不需要做任何操作，完全可以忽略，也不会有什么影响。

不过在某些特殊场景下也会成为问题，常见的一种情况是，需要用DAX中的UNION函数对几个表进行合并，这时列顺序不一样就会报错，应该怎么办呢？  

可以通过以下两种方法来解决。  

### **1\. 在PQ中重新加载**

因为第一次加载时顺序就不会错乱，所以就可以先删掉这个查询，然后重新导入整理数据后再次加载，不过如果数据清洗比较复杂，需要的操作步骤也会很多，这样就太麻烦了。

有个更简单的方法，右键顺序变动的查询，去掉“启用加载”的勾选：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOrKXeJqfvtgURUujOD9YVN4o5ibPPCmkSCr3Hb8or3BPribBt7RbSNObnibe6IIHR0R5sAfBQcsibicGQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后点击关闭并应用，模型中就不会再有这个表，这时度量值/可视化图表可能因为缺少这个表的数据而报错，不用理会这些报错，直接再次进入PQ编辑器，重新勾选“启用加载”，再上载到模型以后，列的顺序就一样了，之前的报错也会消失。

### **2\. 利用SELECTCOLUMNS对列重新排序**

如果不想在PowerQuery操作，<mark style="background: #FF5582A6;">也可以用SELECTCOLUMNS函数重新排序后再用UNION合并。</mark>

比如正常的表1是这样的顺序：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMU58I3mBnfBsYpsODk574ZxSMywudRqZkj2TcSXxlvu0nGkp2aEcXFK5c0fUzf9fdljyuibQaDkicw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

表2是这个顺序：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMU58I3mBnfBsYpsODk574ZbPokiaz2BexRtFlozadib9NXCL89dGIDqo5yicm38YKT9Z8Kf8mMooic3Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果用UNION把这两个列顺序不一样的表合并起来，就可以这样来写：  

```
合并表 = 
UNION(
    '表1',
    SELECTCOLUMNS('表2',"订单日期",[订单日期],"商品名称",[商品名称],"订单数量",[订单数量],"销售金额",[销售金额])
)

```

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMU58I3mBnfBsYpsODk574ZdWotXBicyqVGZjv65YUEXDzApIUr7lEtaoiahvgn67vEeMN77NeeZ1Gg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果需要调整模型中某个表的列顺序，或者按一定的顺序提取某个表的列，都可以使用SELECTCOLUMNS函数来返回特定列顺序的表。  

通过上述两个方法，就可以轻松解决加载后列顺序不一致的问题。  

其实如果是做数据合并，并且这些表也都在PowerQuery中，建议在Powerquery中利用追加查询合并好再上载，而不必使用UNION函数在模型中合并。

___
