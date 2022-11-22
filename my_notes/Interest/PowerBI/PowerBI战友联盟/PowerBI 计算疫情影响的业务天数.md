---
create_date: 2022-08-04T11:39:59 (UTC +08:00)
tags: 
aliases: null
pagetitle: PowerBI 计算疫情影响的业务天数
source: https://mp.weixin.qq.com/s/nirCuxuRxleg2V596sCciA
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

小伙伴问如何通过记录疫情对业务的影响用来更进一步评估业务。

## 记录

首先，要记录疫情导致对业务的影响。疫情的影响表现在：某些日期无法正常工作。我们将这样的情况进行记录如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNYHhpPTpcsPe8icBhvvRvMdkoicibwFiamawRxWSyvsTB1jiae3JfzwJebpWjrIRxTIw3VQaicAcra2Vfw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里模拟了对关店日期的记录。可能导致某些数据的逻辑不合理，但不影响计算。空值表示关店后没有开店。

## 数据处理

首先在 Power Query 中进行预处理。首先用今日进行弥补。如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNYHhpPTpcsPe8icBhvvRvMdz6Isae1Q63AEbRY0TPmrtnvQC76RuzFTdg6E0j8ibnwnFeAH6UghBDA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

用今日来替换没有截止日期的情况，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNYHhpPTpcsPe8icBhvvRvMdLqnjAV75RFR14KfjYyFuAG9eZYVF4zic9csLn5T32HXoUDmUAThyYiag/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> **注意**
> 
> 每次重新计算时，需要刷新模型来获取新的计算结果。

然后，为了通过建模的方式实现日期筛选，这里将日期的起始点扩展为序列后再展开。

先生成序列，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNYHhpPTpcsPe8icBhvvRvMdEtmiaRnEZjcCiat9tCmEILF8gMibhRdmVkFv3YXnEoelu1pdBXUU9RclA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> **注意**
> 
> 这是在 Power Query 中为数不多的需要记住的写 M 函数的场景：构建序列。

再将构建的序列按多行展开，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNYHhpPTpcsPe8icBhvvRvMdicU7Cx9SVzdSKY5CNHBfaJAo7HoVDnjt0CibZchK55xpD8SvYdmrjABA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个步骤是整个模型计算的精华。

将日期范围全部平铺，后续可以与日期表构建模型，进而利用各种日期智能函数以及数据模型的优势来实现各种潜在的计算，而不是将计算保留在每行对应的日期范围细节中。

> **注意**
> 
> 其实也可以直接用日期起点终点来实现计算，只是无法利用到日期表的特点，这是两套不同的计算方案。

调整数据类型后，得到：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNYHhpPTpcsPe8icBhvvRvMdybyIzWFIujmhb6y92ATlyfRw1ZI0qWibqP751OGDmqlNctfKpnzmrUQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

将这个主要内容加载到数据模型。

## 数据模型

如果有作为维度的表，可以充分利用。这里使用日期表与之相连。得到：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNYHhpPTpcsPe8icBhvvRvMdSfRtv9BmFbh4yaCCApK2ibYDR8qJibCCI9LNHmkjFxicKZovt44Lsibchw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> **注意**
> 
> 若模型中存在表示业务的门店维度，应该继续构建连接。
> 
> 这里处于演示目的，不再提出这个维度。

> **注意**
> 
> 作为一个准则：当有可以作为维度可用的表时，应该总是使用该维度。
> 
> 也就是说：同样可以使用 “所在区域” 字段，如果有维度表与事实表相连，那永远应该使用来自维度表的字段。
> 
> 这是一个良好的习惯，对于初学者尤其重要。

## 故事素材

由于疫情对业务的影响是多方面的，在分析时应该注意：**要事第一**（来自《高效能人士的七个习惯》）。

例如：

在没有疫情的时候，某店应该一个月每天都开，共 30 日。

在受到疫情的影响，某店导致一个月只开部分，如 20 日。

那么，该店的销售业绩从预算的角度，只能完成到 2/3，这样就为业务带来了一个故事：

-   如果实际业务超过了预算的 2/3，但没有达标，从理论上也是具有合理性的。
    
-   如果实际业务大成了超过了 2/3，甚至完成目标，从理论上来说业务就突破了疫情的影响，维持了公司的业务。
    

不论实际情况是怎样的，在职场的角度，我们都需要为业务领导者提供讲故事的素材。

## 复杂度分析

如果某【店 A-1】应开 30 天，实际开了 20 天，则有效率：66.6%；

如果某【店 A-2】应开 20 天，实际开了 15 天，则有效率：75%。

以此类推。

但复杂度在于：

【店 A-1】和【店 A-1】都属于【地区 A】，如果要考察整个地区的天数有效率则需要：

( 20 + 15 ) / ( 30 + 20 )

当然，不仅仅可能从地区的角度，还可能从其他分类的角度，如：品牌角度；精品店 / 门店角度等。

如果是常规计算将导致复杂性。

## 计算的自适应性

由于建立了拉平日期的关店日期数据，并与日期表关联，这就可以弥补两个重要难题：

-   在计算日期天数的时候，其计算逻辑是统一的，且简单的计数。
    
-   在用不同维度做筛选时，计算逻辑保持不变，公式不变。
    

以下给出相关度量值计算。

```
// 计算理论天数的度量值Days.Normal = // 这里假设全日期工作，则有：COUNTROWS( 'Calendar' ) * COUNTROWS( VALUES( DImStore[门店ID] ) )// 计算关店天数的度量值Days.Closed = // 关店天数，由于该表的每行表示一天关闭，只需要计数即可。// COUNTROWS( FactData )// 为了兼容重复记录的问题，可以优化为：COUNTROWS( VALUES( FactData[Date] ) )// 计算可用天数的度量值Days.Runing = [Days.Normal] - [Days.Closed]// 计算可用率的度量值Days.Runing.Ratio = [Days.Runing] / [Days.Normal]
```

值得注意的是：

-   这里假设理论上每个店每天都营业。
    

-   实际上，可能不是这样
    
-   则可以根据不同店的理论营业日期区间数据做同样变换计算
    

-   这里考虑到用户可能多选不同的店铺
    

-   则应该将每个店铺的理论营业天数乘以所选范围的店数
    
-   实际情况若每个店的理论营业日期天数不同，则应该用 SUMX 单独考虑
    

特别需要注意的是：

根据这里的模型启发，为了适配更广泛的通用性，需要考虑的是：

-   可比店
    
-   店铺的每个店的理论不可用日期（如：装修导致，而非疫情）
    
-   店铺的每个店受到疫情影响的不可用日期
    

为此，应该参考这个架构，构建更多的表以涵盖这些变化。这个问题留待后续演示。

## 可视化分析

根据这些计算，分别构建三个结构来展示这个结果：

-   按门店的计算
    
-   按区域的计算
    
-   可视化显示
    

可以看出：

-   所有门店的理论可用日期天数都是 30（对于更复杂场景，另外考虑，这里演示一种框架思维和主干逻辑）；
    
-   从区域角度计算，也得到了正确的计算结果。
    

另外，根据以上内容，还可以做出一些有创意的可视化分析。如：散点图的二维分析，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNYHhpPTpcsPe8icBhvvRvMdefQYzvM3umZz069QQiajr0gX6JibuVaE771hBic1tu3Z7NbiaK03geeIsQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里显示不同门店受到疫情影响导致的不可用日期以及可用时间比例。

## 更复杂的问题

从业务角度可能会在分析阶段有更复杂的要求，例如：

如果某个店已经由于疫情在 3 月关店了，且一直没有恢复，那么在 4 月的时候，它的理论可用时间到底是 0 天还是 30 天呢？

如果某个店不是由于疫情在 4 月关店了，且一直没有恢复，那么在 4 月的时候，它的理论可用时间到底是 0 天还是 30 天呢？

不同的业务的答案，都会导致上述的计算逻辑的微调。

## 测试比对

在实际中，要针对上述内容对某些店抽样观察计算，看是否满足实际计算结果。

## 总结

本文虽然题为 “疫情影响的业务天数”，但这里给出了一种通用的思维模式：

-   将每个店的天数计算，改为在模型层用日期表连锁，以更高效统一地计算。
    
-   疫情，常规，各种问题都可以抽象为：不可用日期信息记录表。
    

只要可以驾驭上述两点思维，就可以建立完全通用的不可用日期分析模型。

希望大家可以举一反三，构建灵活的数据模型。

在订阅了BI佐罗讲授的《BI真经》之《BI进行时》课程区，除了可以下载本文案例，还可以观看视频讲解。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNhia5Pc4XC1Um7IYgQhGEoEC1yK05ibUFoPBYpcoAMvibuZh2BZaibMzULeDwNfSeQ0KHRcDUdX3FzVA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**Power BI 终极系列课程《BI真经》**

[

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/09hv4Xua0LNBM1lxlQYHJBicic4CvPoRGLqHgdTZOr8goNRh0asDXA48mRDzc9zxW4UMQiayHwgDmx7mlt4cQxtjg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

BI真经 - 让数据真正成为你的力量





](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650788512&idx=1&sn=76972ff4b0cf265fe9479c6457b04b47&chksm=f18cd2b1c6fb5ba7386eb0bb835280bd8a651bfe0481cc78f20fc30b80c60d2d4cb7eb5b1e3e&scene=21#wechat_redirect)

扫码与精英一起讨论 Power BI，验证码：data2022

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOiad5BOrdQTKpB733esKiaxZa53LXWIPlQicMjxntaRr3a2hnMmuibTib8QacXeiakucDr7lSNGkuV2MXw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击“阅读原文”进入学习中心

**↙**
