---
create_date: 2022-01-05T13:37:59 (UTC +08:00)
tags: 
aliases: null
pagetitle: 用 DAX 快速构建一个日期表
source: https://mp.weixin.qq.com/s/wZiCVfsuLAvS-0f6DrqF6w
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

> 值得多次复习的一个技能。

如果用 DAX 构建一个日期表很常见，本文更多的从实务的角度来给出一些建议。

## 构造日期表的方法

一般构建日期表的方法包括：

-   方法一：在数据源中完成，如：Excel。
    
-   方法二：在 Power Query 中完成。
    
-   方法三：在数据模型中用 DAX 完成。
    

这里推荐使用第三种方法，原因如下：

-   方法一更适合对 DAX 不太熟悉的小白用户，用来理解什么是日期表并尽快完成建模。
    
-   方法二适合构建模板，但在实操中往往不需要模板提供的额外能力，修改需要查 Power Query 的逻辑，其复杂度带来的成本超过了收益。
    
-   方法三最直接简单，但需要有一定的 DAX 知识基础。
    

这里所说的 DAX 知识基础，不仅仅是理解什么是日期表，更多的是知道日期表如何构建可以兼顾到很多使用上的场景。

## 为什么必须用日期表

作为初学者的一个问题就是为什么必须用日期表，可以直接用交易数据中的日期吗？

答案是：不可以。

最直接的原因是：交易中的日期可能是残缺的。例如：某个日期是没有交易的。导致你想要的某日期是不存在于交易数据中的。

必须使用日期表的真正原因来自两点：

-   数据模型的设计学
    
-   复用
    

从设计的角度看，日期序列常常是分析中表征时间变化的最小时间跨度单位。

> 注意
> 
> 暂不考虑比日期级别还小的业务分析，它们的本质相同，只不过不考虑这个细节程度，可以大幅度优化整个设计。

而做分析的时候，我们往往需要使用的却不是日期级别的时间跨度，而是用诸如：

-   按年度看销售额趋势
    
-   按月份对比前后两年的销售额差异
    
-   按年度至今来比对当前目标完成度与年度总目标的差异
    

可见：

分析时所使用的日期区间跨度都是大于单个日期的。

更精确地说，对于某个日期，如：yyyy-MM-dd，记作 D1，其日期区间跨度为 1 日。而常用的日期区间的跨度都会大于 1 日。

为了可以得到任何范围的日期区间跨度，就需要一个可以容纳每一天日期的表，该表满足：

包括所需的所有日期。

从设计学的角度，我们称为了满足随后的分析而构建的这个表叫：日期表。

日期表的设计学用途是：

当希望从某段日期区间跨度去筛选交易业务数据时，都可以从日期表作为出发点，由于日期表如上描述的设计，它必然满足：

一定可以从日期表中找到所需要的日期区间来筛选业务数据。

再者，由于业务可能有多种明细记录，如：

-   销售明细表
    
-   采购明细表
    

因此，共享一个日期表，就起到了复用的目的。

## 日期表初始化

请思考一个问题：

作为一个日期表，应该最少包括几列？

A - 一列，日期时间

B - 一列，日期

C - 三列，年月日

D - 四列，年季月日

通过对上述内容的理解，不难看出 B 才是正确答案。

A 不是正确答案的原因是 A 所说的日期时间已经达到了时间的明细程度，其时间跨度太低，本场景所说的分析中并不会使用到这样级别的时间维度。

在 DAX 中，可以构建表，准确讲，是一个单列的表，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPibGsox1QhwwtkemXTYjrH9DfIE5m5BvuApdnnfOoNuJuzq0mNgV6HAVsnNhQfOzibDpYicxDqck0Rg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

DAX 函数 `CalendarAuto` 将轮询目前在数据模型中的每一个表中的日期类型列以便创建一个日期序列，该序列包括可以涵盖数模模型所有日期范围。也就意味着，完全可以通过这个序列找出某个日期区间，该日期区间可以用于筛选个业务数据表。

## 构建日期表的注意事项

前面讲过从日期维度筛选数据时，常常不是从日期级别进行，而是从更高的时间维度进行，如：年季月日，考虑到中文本地化以及排序的问题，最佳实践如下：

-   分两步构建日期表
    

-   先构建一个基础日期表，包括：年季月日等
    
-   再将其扩展出更多属性，包括：是否本月，是否本年，是否过去等
    

-   起名可以暗示文本或数字
    

-   YearName 表示文本
    
-   YearNumber 表示数字
    

-   用数字协助文本进行排序
    

-   Jan 是 1 月，但它的文本排序是晚于 Apr 4 月的
    
-   所以要使用对应的数字进行排序
    

## 构建一个日期表

基于上述考量，我们通过 DAX 构建日期表，如下：

```
Calendar = // 从最小日期表来进一步构建一个丰富的日期表VAR vCalendarBase =AddColumns(    CALENDARAUTO( ) ,    "YearNum" , YEAR( [Date] ) ,    "QuarterNum" , QUARTER( [Date] ) ,    "MonthNum" , MONTH( [Date] ) ,    "DayNumInMonth" , DAY( [Date] ) ,    "WeekNumInYear" , WEEKNUM( [Date] , 2 ) ,    "DayNumInWeek" , WEEKDAY( [Date] , 2 ))RETURN vCalendarBase
```

效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPibGsox1QhwwtkemXTYjrH99d3KGsXbkcvPznSg1ibXXhoqXVHcvvRACCIZwoka7OfU6SbC3AzdBSg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里先构建了数字。

> 注意
> 
> 列（字段）在数据模型中是不存在特定顺序的，其顺序不重要。这也是初学者会常常问及的问题。

## 扩展这个日期表

有了基本的日期表以后，可以进一步扩展，包括：

-   名称
    
-   属性
    
-   财务年月
    
-   其他
    

举例如下：

```
Calendar = VAR vDateLastUpdate = MAXX( ALL( Sheet1[订单日期] ) , [订单日期] ) // 请修改 Sheet1[订单日期]// 从最小日期表来进一步构建一个丰富的日期表VAR vCalendarBase =AddColumns(    CALENDARAUTO( ) ,    "YearNum" , YEAR( [Date] ) ,    "QuarterNum" , QUARTER( [Date] ) ,    "MonthNum" , MONTH( [Date] ) ,    "DayNumInMonth" , DAY( [Date] ) ,    "WeekNumInYear" , WEEKNUM( [Date] , 2 ) ,    "DayNumInWeek" , WEEKDAY( [Date] , 2 ))VAR vNumTable = SELECTCOLUMNS({   ( 1 , "一" ) , ( 2 , "二" ) ,( 3 , "三" ) ,( 4 , "四" ) ,( 5 , "五" ) ,    ( 6 , "六" ) , ( 7 , "七" ) ,( 8 , "八" ) ,( 9 , "九" ) ,( 10 , "十" ) ,    ( 11 , "十一" ) ,( 12 , "十二" ) } , "Num" , [Value1] , "NumCN" , [Value2] )VAR vCalendarEx =ADDCOLUMNS( vCalendarBase ,    "YearNameCN" , [YearNum] & "年" ,    "QuarterNameCN" , "季度" & SELECTCOLUMNS( FILTER( vNumTable , [Num] = [QuarterNum] ) , "Value" , [NumCN] ) ,    "MonthNameCN" , SELECTCOLUMNS( FILTER( vNumTable , [Num] = [MonthNum] ) , "Value" , [NumCN] ) & "月" ,    "MonthNameEN" , FORMAT( [Date] , "mmm" ) ,    "DayNameInWeekCN" , IF( [DayNumInWeek] = 7 , "周日" , "周" & SELECTCOLUMNS( FILTER( vNumTable , [Num] = [DayNumInWeek] ) , "Value" , [NumCN] ) ) ,    -- 其他属性 --    "IsHistory" , IF( [Date] <= vDateLastUpdate , "Y" , "N" ) ,     "IsCurrentMonth" , IF( [YearNum] * 100 + [MonthNum] = YEAR( vDateLastUpdate ) * 100 + MONTH( vDateLastUpdate ) , "Y" , "N" ))RETURN vCalendarEx
```

考虑到中文的显示，这里做了一个数字对照表进而将日期表扩展成符合中文显示的效果。如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPibGsox1QhwwtkemXTYjrH9tTKhKbvxxl1U1zkwQdZJAgwlKPWibntvekSq5YAXAfmrxrYMfkrSC8g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在此前的文章中，已经写过日期表的本质以及运营及财务日期表，结合本文就可以更好的理解这里面的设计思想了。

## 总结

关于日期表的讲解，的确看到了很多，但本文给出的视角以及如何从这个视角进行实际操作，相信能让很多刚刚入门不久的伙伴有快速而深入的理解。

以上 DAX 公式，你也可以直接复制粘贴使用，无需修改。
