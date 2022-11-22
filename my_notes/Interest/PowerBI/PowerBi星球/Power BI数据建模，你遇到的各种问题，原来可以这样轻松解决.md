---
ZK: Origin
notes: False
aliases: null
create_date: 2022-09-28T22:35:24 (UTC +08:00)
tags: wx/pbi/建模技巧
pagetitle: Power BI数据建模，你遇到的各种问题，原来可以这样轻松解决
source: https://mp.weixin.qq.com/s/F3b3jrok9SGx737EBxcbbw
author: 采悟
status: 已完成 
category: 浏览文章 
uid: 
---

用PowerBI做数据分析，不仅仅是学习DAX，更关键的是先建好一个合适的数据模型，关于建模，刚开始接触PowerBI的同学可能有很多疑问，这里就通过一个简单的示例，介绍一下建模过程中可能会遇到的一些问题。  

假设有两张表，一个是每日销售表，一个是每月目标表，模拟数据如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNzyS6SiaKaf0Awj2rSHFYR0s2savVicUFOmiar2tyQT6BBEombNfuWAzS5jKHQLficUFHGq0QeqCcAOw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

通过这两张表，如何比较每个月每个产品的目标完成情况呢？

这是很常见的分析，对于熟练使用PowerBI的人来说非常简单，一个简易的数据模型就实现了，甚至不需要写DAX，但是对于初学者，可能不知道从哪下手，也许知道这两个表应该建立关系，但建立关系的过程中，就可能会遇到下面一些问题。

**1\. 多对多关系**

如果你想在销售表和目标表之间，通过产品名称字段建立关系，会弹出一条提示：

> <mark style="background: #FF5582A6;">此关系的基数是多对多</mark>。仅在两列都不包含唯一值，且多对多关系的显著不同行为被理解的情况下，才应使用此关系。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNP8zKqs3RUKn9SPYpHtoQ7viawxAYnMPkIQR1uc71gf8fRGpo2ARsLIgVibd7gxcr9vooOxVBZWOEw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**由于两个表的\[产品名称\]列，都不是唯一的，都有重复值，则只能建立多对多的关系。**

<mark style="background: #FF5582A6;">多对多关系是受支持的，但是这种关系在行为和性能上都有特殊性，会导致模型更加复杂</mark>，建议在充分理解的情况下采用，这就是上述提示的含义，仅仅是提示，并非不允许。

并且多对多关系，默认交叉筛选方式为双向，<mark style="background: #FF5582A6;">为了避免关系的混乱，方向最好改为"单一"</mark>，根据需要选择是从某个表筛选另一个表：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNzyS6SiaKaf0Awj2rSHFYR0g2stBI7kIzEEOls282LWyUXqGjCtSHyvuEicbuMMlw33JicrDtoYDjaQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

当然，其实不建议建立多对多的关系，为了说明建模过程中可能遇到的问题，这里暂且这样建，后面会介绍更优的建模方式。

**2\. 可用关系与不可用关系**

上面已经在目标表和销售表之间建立了\[产品名称\]列的关联关系，因为还需要按日期匹配，如果你想拖拽日期列再次建立关系，这次又弹出同样的窗口，还是提示多对多关系：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNP8zKqs3RUKn9SPYpHtoQ7dYDSsUOAS3VZOLrSiaEAjcyMZrWvvfwQ1eXNPSibib9PZaNw9NyiajN7yQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

依然是因为两个表的日期都有重复值，如果你直接点击确定，会发现这条关系线是一条虚线：

这是为什么呢？虚线是怎么回事？

**<mark style="background: #FF5582A6;">关系按活动状态分为两种：可用和不可用</mark>，可用的活动关系线用实线表示，不可用的未被激活的关系，用虚线表示。**  

**两个表之间只能有一条可用的活动关系，如果再建立其他关系，都只能是非活动状态的虚线关系。**

其实你仔细观察上面两次建立关系时，弹出的提示窗口，会发现还是有一个地方是不同的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNzyS6SiaKaf0Awj2rSHFYR0JjmL0sXaFdGgWb0JHwZ3bScKycY8gumWAdUibSCHavFxGnkUbibDc6mg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

第二次再建立关系时，左下角的“使此关系可用”默认是不勾选的，如果强行勾选，提示会变成：

> 目标表与销售表已存在可用关系。要使用此关系，请先停用现有关系。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNzyS6SiaKaf0Awj2rSHFYR0sr8ibxWm0zEP3UBBUMpOHNJ74BuA1I9n32GgEk5VH7q2c26vBbGfUxA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

由于<mark style="background: #FF5582A6;">两个表之间是不允许有两个同时存在的活动关系</mark>，所以“确定”按钮也变成灰色的，不允许建立这个关系。

两个表的活动关系只能有一条，非活动的虚线关系可以有多条，关于虚线关系有什么用，以及怎么用，可以参考这篇文章：

[认识Power BI中的非活动关系](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071870&idx=1&sn=f110592b92b23dd7d7515c4cc342c101&chksm=8e0c4769b97bce7f97489d4f34ca603a0e12af4c5acd90101205c670709ecf07f3ee95830a1d&scene=21#wechat_redirect)  

不能建立多条活动关系，那两个表如何利用多个字段建立关系呢？下面接着介绍。

**3\. 关系歧义**

既然不能在已经存在活动关系的两个表之间再建立活动关系，那么通过一个中间的维度表[^1]来过渡应该可以的吧？

接着上面的步骤，建立日期表（建日期表可参考：[玩PowerBI必备的日期表制作方式汇总](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067654&idx=1&sn=905c186a9cbd91159b6615924a2d5068&chksm=8e0c7791b97bfe87623904f7002cd6cb726f711c6e7a289a36c9a4973964d907493aa2397fe7&scene=21#wechat_redirect)），然后利用日期表与销售表、目标表分别建立关系。

先建立日期表与目标表的关系：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNzyS6SiaKaf0Awj2rSHFYR0pogXSGgAkcWFZ9kDeAgVZpZmCzYiaxaWAYXlUqvRnz1NkzAIGbbS0WQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后再建立日期表与销售表的关系，但是却发现只能建立非活动的虚线关系？

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNzyS6SiaKaf0Awj2rSHFYR0I36rSKUop7YhJVGbzowMl0XPCCTs00w5jVibPdiczL4aVJBDCQJ0iaAbA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这是怎么回事呢？明明日期表和目标表之间还没有建立关系，为什么还是不让建立活动关系呢？

双击虚线关系进入编辑，如果强行勾选左下角的“使此关系可用”，将会出现以下提示：  

> 无法在销售表和日期表之间创建直接可用关系，因为<mark style="background: #FF5582A6;">这些表之间已经存在间接关系的可用集合</mark>。要使此关系可用，请先将交叉筛选方向设置为“单向”，删除或停用任何间接关系。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNzyS6SiaKaf0Awj2rSHFYR0kxOvziaicy67Kd9VPAmclJdALCjSF6dHliaaXc98AN9yeiaSYicEgvMibfTQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

右下角的“确认”按钮也是灰色的，不允许激活该关系。  

其实上图中的提示信息非常清晰，**因为<mark style="background: #FF5582A6;">两个表之间只能有一条活动关系</mark>，这条关系不仅仅是直接连接的活动关系，也包括间接连接的活动关系。**

日期表和销售表之间已经有一条间接关系（下图路线1），如果在日期表和销售表之间，再直接建立个活动关系，从日期表到销售表的筛选，就有两条路线：

**路线1：日期表→目标表→销售表**

**路线2：日期表→销售表**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNzyS6SiaKaf0Awj2rSHFYR0TSRuwWzia5wAlydFnqp6cMJibibia8htQoKziaC9E7l5TPYhlLeQnskr4DQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

日期表应该按哪一条路线来筛选销售表呢？因此产生了歧义，这也是为什么会出现以上提示、以及不允许建立路线2实线关系的原因。

碰到这种情况，想建的关系建不了，就应该意识到前面的关系建错了，应该重新梳理模型关系，把错误的不必要的关系删掉。

___

如何梳理关系呢，首先应该先分清楚模型中的表，哪些是事实表，哪些是维度表？（在PowerBI中的表并没有事实表和维度表的区别，这里用这两个概念来区分表，主要是为了更方便理解数据模型）

-   <mark style="background: #FF5582A6;">事实表，记录明细数据的表，是分析指标的数据来源</mark>，比如上面的销售表和目标表，都是事实表，销售表提供实际数据指标，目标表提供目标数据指标；
    
-   <mark style="background: #FF5582A6;">维度表，是分析的角度</mark>，比如产品维度表提供产品的角度、日期维度表提供时间的分析角度等，报告中的各种筛选器，图表的坐标轴等都应该来自维度表的字段。如果<mark style="background: #FF5582A6;">模型中本来没有维度表，可以根据需要来建立维度表。</mark>
    

对于这个示例，完善所需的维度表，分清楚事实表和维度表之后，然后就可以建立关系了，主要把握住这些<mark style="background: #FF5582A6;">基本原则</mark>：

-   **<mark style="background: #FFB86CA6;">事实表之间不要直接建立关系</mark>；**
    
-   **<mark style="background: #FFB86CA6;">维度表与事实表之间建立一对多的单方向关系</mark>；**
    
-   **<mark style="background: #FFB86CA6;">连接事实表的维度表之间不建立关系</mark>。**
    

基于以上原则，对于这个示例：

**目标表和销售表都是事实表，两个表之间不建立关系；**

**产品表和日期表是维度表，分别与目标表和销售表建立一对多的单向关系；**

**两个维度表，产品维度表和日期维度表不建立关系，由于维度表是相互独立的，一般也没有建立关系的可能；**

最终模型是这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOm979TXruJWZHVXibA13nZNnicujC20EGwD2b3l0LsOo9YSvRibINXiasza7fsyFG6aR6SrFJjn9zIXQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关于维度表如何建立，以及最终如何进行分析，请参考：**[Power BI数据分析入门案例：目标实际对比](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078691&idx=1&sn=af288fc6a65368973fd64d53fd392a08&chksm=8e13a2b4b9642ba273bd2f6e9b2547048fe0b4c50dfea6188a6a7b7e63aeb3d586d79534a1f5&scene=21#wechat_redirect)**

这样建立的模型，就是一个星型模型，它能有效避免上面可能遇到的各种关系问题。

本文根据一个非常简易的模型，来介绍建模过程中可能遇到的各种问题，更复杂的模型，也会有更大概率碰到上述问题。

你需要理解模型的每个数据表的业务含义，不要随意拖拽字段建立关系，系统自动建立的不必要的关系，应该删掉，脑海中应该有事实表维度表的概念，然后根据上面的原则来建立关系，大概率不会再遇到问题，这样建立的模型也会更方便的实现分析目的。


[^1]: 中间桥表可以让事实表之间多条多对多关系变成单向的一对多关系