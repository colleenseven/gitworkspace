---
create_date: 2017-12-31T20:52:22 (UTC +08:00)
tags: wx/pbi/数据处理功能 
aliases: null
pagetitle: Power BI数据建模
source: https://mp.weixin.qq.com/s/KeaAgIZO46udHe-GSf_Lxg
author: 采悟
status: 已完成
category: 浏览文章 
notes: False
ZK: Origin
uid: 
---

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN2LAX1DpRicGH8mmnRvuERyjEV3H3PoIyb7zvVc2G8zbbg64ibjicF6NmrYHHpPMCVREU5RSibST968A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> 数据建模并没有那么高深，你同样可以学会！这篇文章通过一个实例创建一个简单的数据建模，并引出两个重要的概念：**度量值**和**DAX**.

___

之前谈论PowerBI与Power Pivot的关系时就提到，Power BI数据建模其实就相当于Excel的Power Pivot插件，不过这个插件已内嵌到PowerBI Desktop中了，两者的功能基本相同。==Pivot是透视的意思==，那么PBI的数据建模也和透视有许多共通之处。  

使用的数据透视表的都知道，透视表只能从单个表中取数，如果想把其他表中的数据也放进来，只能先利用Vlookup把其他表的数据合并过来，然后再把这个字段放到透视表中。这只适用于数据非常简单的情况，如果数据量大或者维度很多，用透视表就无法满足需求了。

**Power BI突破了这个限制，可以从多个表格、多种来源的数据中，根据不同的维度、不同的逻辑来聚合分析数据；而提取数据的前提是要将这些数据表建立关系，这个建立关系的过程就是数据建模。**

以一个实例来理解数据建模。

> 比如有个电子产品专卖店，销售产品有三类：手机、电脑、平板，每一类又分别来自三个品牌：小米、苹果、三星，那么这个店销售的产品共计9个，其销售明细也是记录这些产品每天的销售数据，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN2LAX1DpRicGH8mmnRvuERyice3DSAI9Dh8tYmKSWNibu56LZ5Wvk1RQPBSD6XaSZY0g7yv0uQGVDpg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

为了能分析每个品牌的销售金额，或者分析每个产品类别的销售情况，其实还应该设计个产品明细表以及对应的品牌表和种类表，像这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN2LAX1DpRicGH8mmnRvuERyvRoq5C9eBbZmD91qiby8g5NLq7xWC37icGNziawicIaqoQcx5kiceqzQY5g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

从这四个表中很容易就能想到它们之间的关系，品牌表和产品类别表分别和产品明细表中的品牌与产品种类相对应，而产品明细表中的产品编号和销售明细表中的产品编号相对应。

下面就演示一下在Power BI Desktop中建立一个模型，导入以后点击关系，出现这4张表，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN2LAX1DpRicGH8mmnRvuERyqFzcYiaicy6EDxVUANoia4agib2DE9yFjEto3Kvms041UialwHEg3JuZzYQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以看出产品明细表和销售明细表之间已经有一条线，这是由于表格导入后，PowerBI会自动检测关系并联接，没有检测到的表，可以点击一个表中的字段托到另一个表的对应字段上，就可以建立关系了，把类别表、品牌表和产品明细表建立关系后，关系图如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN2LAX1DpRicGH8mmnRvuERy58moZK2YJOueXt3ducqT0Z70SstRES4hW47vcQyv0Y0QSTjV9AJiaBA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

一个简单的数据模型就建立好了，可以点进去看看建立模型的相关参数。  

点击关系连接线，两边的表对应的连接字段会框选，双击关系线，进入编辑关系窗口：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN2LAX1DpRicGH8mmnRvuERyB0keAfrKcKjibIREHkFZLyrSu14yJonwSahiaCwiakquS9MXpicKBUCy9w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

编辑关系窗口可以看出关联的两个表和对应的字段，也可以更改联结的字段；下面还有两个可选项，基数和交叉筛选方向。

___

**基数**  

基数就是两个连接字段的对应关系，分为多对一、一对一和一对多，一对多和多对一其实是一样的，实际上就是两种关系：  

-   ==多对一（\*：1）：这是最常见的类型，代表一个表中的关系列有重复值，而在另一个表中是单一值==
    
-   ==一对一（1：1）：两个表是一对一的关系，列中的每个值在两个表中都是唯一的==
    

具有唯一值的表通常称为“查找表”，而具有多个值的表称为“引用表”。在上述的关系图上，产品明细表上类别手机、平板、电脑都不是唯一的，每个品牌都有这种类型，是个引用表；但类别表上，几种类别都是唯一值，因此这两个表是多对一的关系，类别表也就是查找表。

**交叉筛选方向**  

表示数据筛选的流向，有两种类型：  

-   ==双向：两个表可以互相筛选==
    
-   ==单向：一个表只能对另一个表筛选，而不能反向==
    

这个稍微有点抽象，以后可以根据实例来理解。

___

根据刚才建立的数据模型，可以做一下分析，比如统计各品牌产品的销售额：  

在销售明细表中并不能直接统计出按品牌的销售额，可以先建一个度量值，在建模选项卡下，点击新建度量值，公式栏输入：  

> 销售额 = sum('销售明细表'\[金额\])

然后\[销售额\]这个度量值就建立了，在右边字段区可以看到。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN2LAX1DpRicGH8mmnRvuERyQbsr4iacsuNZ5xgGIfibh1B35rLGe4OY6uibkm0UMyI7tvMTtZnicSczeg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

为了在画布上直观的看到各品牌销售额，在可视化里添加“卡片图”，把度量值字段放进去，可以看到卡片图的数字出来了，  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJN2LAX1DpRicGH8mmnRvuERyTqia9YAiaTkYGcicqsbWCuoAWg6O2Byzgeu8qxfE4LOTvibdcpnPY7p2xg/0?wx_fmt=gif&wxfrom=5&wx_lazy=1)

这个数字是整体销售金额，因为还没有做任何筛选，为了看出各品牌的销售金额，现在添加一个品牌的切片器，

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJN2LAX1DpRicGH8mmnRvuERyYV7MYNHFnAtlMepIlh1kEoEyeae1ib4wjnswvMaqYdxsDIv5ibMZLO2Q/0?wx_fmt=gif&wxfrom=5&wx_lazy=1)  

点击不同的品牌，数值跟着变化，通过这个例子，可以看出：

-   展现的数字并不是一个表得出的，根据之前建立的关系模型，销售明细表中的数据被品牌表中的\[品牌名称\]字段所筛选，展现出来不同品牌的销售额，这就是数据模型的威力。
    
-   品牌销售额是通过\[销售额\]这个度量值，加入到卡片图中，并可与切片器交互，展现不同的数据。
    

通过这个实例，还看到了以前从未见过的的概念：==**度量值**，这可以说是PowerBI数据建模的灵魂，创建度量值的公式称为**DAX公式**（看起来和Excel公式非常相似）==，刚才创建的这个度量值只是一个简单的sum函数，并没有任何的过滤条件，但是却可以根据切片器的筛选而展现不同的数值，所以度量值被称为移动的公式，这里只是简单介绍，有个印象即可。

学习数据建模的更多知识，可以说都是依据度量值的逻辑以及建立度量值的DAX公式来展开，是下一步学习Power BI的重点。  

这是2017年的最后一篇文章，简单介绍了数据建模的概念，并引出下一步学习的重点，Power BI的大门已经推开，2018会更精彩。  

新年快乐！
