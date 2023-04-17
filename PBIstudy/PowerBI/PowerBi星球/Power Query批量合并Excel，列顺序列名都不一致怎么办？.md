---
create_date: 2022-12-13T23:49:18 (UTC +08:00)
tags: wx/pbi/PQ数据处理 
aliases: null
pagetitle: Power Query批量合并Excel，列顺序/列名都不一致怎么办？
source: https://mp.weixin.qq.com/s/gSCzl6qJCV3-fCxOUEC6nQ
author: 采悟
status: 已完成
category: 精读文章
notes: False
ZK: Origin
uid: 
---

关于批量合并Excel，以前分别介绍过各种情况下的不同处理方式，比如：

-   [利用PowerQuery，批量合并多个Excel的指定列](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073950&idx=1&sn=022f2b8806518ff03648eeea76950223&chksm=8e0c5f09b97bd61f3dc5a7509181aa42fd3545d009b9b8715b0ef387d4f50dffe0833dfa8ce4&scene=21#wechat_redirect)
    
-   [批量合并Excel，数据不是从第一行开始](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073974&idx=1&sn=f1c63db1ed01cbabd2a3293d663205a4&chksm=8e0c5f21b97bd637760e8cd51c9888c667e3b586da5bad7581c1749c73802656b60cf16456c6&scene=21#wechat_redirect)
    
-   [批量合并Excel，前面有空行且不相等的解决办法](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074215&idx=1&sn=5ec9f26de1277dd9cbcdbf134d9120a9&chksm=8e0c5c30b97bd526243f835d0625ebf5199103387555ac1ec5008553697215b8ba5af47b98b5&scene=21#wechat_redirect)
    

最近星友又问到一种情况，如果多个表的内容相似，但是列顺序不一致、并且列的名称也不一致，就像下面这三个表格，如何批量合并呢？  
![https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPQJozLEV9PBtYFibZHhERQIRtFQEa7y2awXjI7ZpbQlFDYwXhVLpS56LRSuCiaRKicTrLibl6y9vMrhg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPQJozLEV9PBtYFibZHhERQIRtFQEa7y2awXjI7ZpbQlFDYwXhVLpS56LRSuCiaRKicTrLibl6y9vMrhg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
列顺序不一致很容易解决，前面已经介绍过，但是列名也不一致就比较麻烦，系统无法识别两个不同名称的列是否应该合并到一起。  

对于这种情况，基本思路是先==整理一个列名映射表，将每个表修改为统一的列名==，然后再进行合并。批量修改列名的方法之前也介绍过，请参考：

[PowerQuery技巧：批量更改列名](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070606&idx=1&sn=b63225e34ec030ff9e306c1d511f5e36&chksm=8e0c4219b97bcb0fb9ec068781a08bee1db47931c3ce8d5ff7dad962752e00027a49893d3fd8&scene=21#wechat_redirect)

对于上述示例数据的列名映射表如下：
![https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPQJozLEV9PBtYFibZHhERQIjeer89dX1vwp1mmKppkAWiaJcgu1CjbvcgUlSGDzPIv2lbsl5lvaqEw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPQJozLEV9PBtYFibZHhERQIjeer89dX1vwp1mmKppkAWiaJcgu1CjbvcgUlSGDzPIv2lbsl5lvaqEw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后就是将==批量修改列名和批量合并两种技巧结合==起来就可以了，操作步骤如下。

**1\. 导入列名映射表并转为List。**

参考[批量更改列名](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070606&idx=1&sn=b63225e34ec030ff9e306c1d511f5e36&chksm=8e0c4219b97bcb0fb9ec068781a08bee1db47931c3ce8d5ff7dad962752e00027a49893d3fd8&scene=21#wechat_redirect)的操作步骤，将列名映射表转换为List列表，如下。  
![https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPQJozLEV9PBtYFibZHhERQIFrtkc2Y1hTNNdw5aYpMYg36L2Bl4MRfK3TX7bMtMqU67F1FDEqZzUA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPQJozLEV9PBtYFibZHhERQIFrtkc2Y1hTNNdw5aYpMYg36L2Bl4MRfK3TX7bMtMqU67F1FDEqZzUA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
**2\. 导入Excel工作簿所在的文件夹**

参考[批量合并Excel指定列](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073950&idx=1&sn=022f2b8806518ff03648eeea76950223&chksm=8e0c5f09b97bd61f3dc5a7509181aa42fd3545d009b9b8715b0ef387d4f50dffe0833dfa8ce4&scene=21#wechat_redirect)的步骤，将文件夹的工作簿导入，并利用Excel.Workbook(\[Content\],true)解析出数据，到达下面这个步骤。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPQJozLEV9PBtYFibZHhERQI9sT4y6m5jWDp1W9TI8yW8aBE2yUCVb4KlWglsu9vYLLEJrJ5uSaE0A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果在这里直接展开\[Data\]列的数据，由于列名不一致，合并的结果将是错乱的，因此这里先不要展开。

**3\. 批量修改\[Data\]列中Table的列名**

这个是==最关键的一步，在第2步的基础上添加自定义列来修改未展开的Table的列名==：

> Table.RenameColumns(
> 
>     \[Data\],
> 
>     列名映射表,
> 
>     MissingField.Ignore
> 
> )

  
至此每个Table中列名就是统一的了，点击展开，选择需要的列就可以得到合并后的数据。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPQJozLEV9PBtYFibZHhERQI0fHaMD2ic43XbGrNO6njPlicAXxZq4FTCW33bTNWS1ClziaKj8VeluP7A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

批量合并数据的关键是要先熟悉自己的数据，如果数据很规范，合并起来就非常轻松，但是碰到如本文的情况，列名都不统一，那就需要先花点时间，动手整理好列名映射表，然后再进行合并。  
