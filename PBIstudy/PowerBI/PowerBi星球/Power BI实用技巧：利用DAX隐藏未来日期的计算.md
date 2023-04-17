---
create_date: 2020-10-07T20:33:36 (UTC +08:00)
tags:
aliases:
pagetitle: Power BI实用技巧：利用DAX隐藏未来日期的计算
source: https://mp.weixin.qq.com/s/BUe5s8xIC-kUjojnoHsb_w
author: 陆文捷
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

> 文/陆文捷
> 
> 物流供应链优化分析师，Power BI爱好者，知乎:Beethovenist

Power BI中日期智能函数进行同环比和累加等计算时，如果事实表数据是随时间动态更新，同时数据模型中的日期表已包含所有年份的完整日期，那么在报表和视图中会因多个日期智能相关度量值同时展现多出未来日期的部分：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOALjJDFtKIibG8jZFGoeawEzKRgt06raIpLybiagf6lNQ2WddK2U8TzjAic0cibyxWy37WdyblGIz7Iw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

示例中的利润数据在订单事实表中的记录截至2018年6月15日（按订单日期），这之后的利润均为缺省值，把年度至今的利润度量值放入报表，

> 利润.新.YTD\=CALCULATE( \[利润.新\] , DATESYTD( '日期表'\[日期\] ) )

7-12月份的数据分别出现了缺省和重复，虽然符合计算逻辑，但用户的设计初衷并不想呈现最大订单日期以后的数据汇总。

本文探讨如何在Power BI中对涉及日期智能函数的非必要行进行隐藏，使报表呈现更自然。

一种方法是通过计算列，判断日期表的每个日期是否大于事实表的最大订单日期，

> 大于最后订单日期\= '日期表'\[日期\] <=MAX( '订单表.新'\[订单日期\] )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOALjJDFtKIibG8jZFGoeawEKuft3oayiaAoiabwtHPhVhCh5ONAu5yRobIBNqdJ0HopqYdygNTvByJA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

要在报表中不显示还未发生订单交易期间的年度至今利润，结合DAX的运算逻辑，即是通过设立筛选条件排除相应的日期，辅助列正是为该目的而建的。

CALCULATE的兄弟函数CALCULATEABLE可以用来筛选表，用该函数和辅助列的值（True或False）筛选出符合条件的日期来用作CALCULATE的第二参数进行计算，

> 利润.新.YTD.ByClaculateColumn\= 
> 
> CALCULATE (
> 
>    \[利润.新\],
> 
>    CALCULATETABLE (
> 
>         DATESYTD ( '日期表'\[日期\] ), 
> 
>         '日期表'\[大于最后订单日期\] = TRUE )
> 
> )

经过这步处理，年度至今的利润汇总就不再会有7-12月期间的重复.

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOALjJDFtKIibG8jZFGoeawEb6yb8iauITPbKyUhUVlBsY4tIXbot7IVM7A5GDOyFiaFebC5QDOgficyQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

推而广之，该方法可作为处理此类问题的标准套路:

> **CALCULATE(**
> 
>     **\[度量值\],**
> 
>     **CALCULATETABLE (**
> 
>         **<日期智能函数> ( 日期),**
> 
>         **'日期表'\[大于最后订单日期\] =TRUE**
> 
>     **)**
> 
> **)**

固定的搭配可实现其他度量值和日期智能函数的组合应用。例如计算去年同期利润：

> 利润.新.YTD.PY.ByClaculateColumn\=
> 
> CALCULATE(
> 
>     \[利润.新\],
> 
>     CALCULATETABLE( 
> 
>         SAMEPERIODLASTYEAR ( '日期表'\[日期\] ),
> 
>         '日期表'\[大于最后订单日期\] = TRUE
> 
>      )
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOALjJDFtKIibG8jZFGoeawE6Q61RdyQM3Q9PecEbnacHwiclZ24Up5Y4ibylVr4AR5ib3vBDibODXUrLQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以看到筛选了日期后，当年（2018）7-12月尚未发生交易期间被筛选不做计算。以此进一步计算同比增长率（YOY%）就避免了上年（2017）利润与当年（2018）7-12月期间的利润（此时均为0）在业务逻辑上的无效运算。

细心的小伙伴还可以注意到201706期间利润为11,098，而201806期间的去年同期结果为5,713，并不相等，想一想这是为什么？

以上，新增计算列结合固定DAX套路，极为便利地隐藏了非必要行。但是还做不到一招鲜吃遍天，如果作为筛选判断依据的特定日期是动态变化的，以及通过DirectQuery直连模式访问数据无法新增计算列的情况下，这个方法就难以应付了。

此时从DAX的角度通过IF的条件判断筛选日期汇总：

> 利润.新.YTD.ByMeasure\=
> 
> VAR 
> 
>     LastOrderDate =CALCULATE ( MAX ( '订单表.新'\[订单日期\] ), ALL ( '订单表.新' ) )
> 
> VAR 
> 
>     FirstDayInSelection =MIN ( '日期表'\[日期\] )
> 
> VAR 
> 
>     ShowData = ( FirstDayInSelection <= LastOrderDate )
> 
> VAR 
> 
>     Result = IF ( ShowData, CALCULATE ( \[利润.新\], DATESYTD ( '日期表'\[日期\] ) ) )
> 
> RETURN
> 
>    Result

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOALjJDFtKIibG8jZFGoeawEDv5ENPFn4aXuJMWKjia43icXxMC72qujt46HY0lzh29ILxzExSg00tqQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

度量值内用IF判断日期表日期是否在最大交易日期之内也起到了和借助计算列筛选日期同样的作用。

同样的套路计算去年的年度至今利润：

> 利润.新.PY.ByMeasure\=
> 
> VAR
> 
>     LastOrderDate =CALCULATE ( MAX ( '订单表.新'\[订单日期\] ), ALL ( '订单表.新' ) )
> 
> VAR
> 
>     FirstDayInSelection =MIN ( '日期表'\[日期\] )
> 
> VAR
> 
>     ShowData = ( FirstDayInSelection <= LastOrderDate )
> 
> VAR
> 
>     Result =IF ( ShowData, CALCULATE ( \[利润.新\], SAMEPERIODLASTYEAR ( '日期表'\[日期\] ) ) )
> 
> RETURN
> 
>     Result

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOALjJDFtKIibG8jZFGoeawE0bczf9q6INPuVLjnicLHek6z92d274XwN6ibBH2SGJeNYlUHV4A8pj6Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

仔细对比201806期间的去年至今利润数额，用计算列筛选日期和纯DAX的方法返回不同结果。

向下钻取该期每天的数据明细进行核对：虽然逐日的去年同期结果相同，但在总计行上，计算列的方法可以做到按天的颗粒度汇总去年同期（事实表中最后交易日为2018/6/15，总计行去年同期则相应为2017/6/15），而DAX的用法只精确到了月份(总计行去年同期按2017年整个6月汇总)。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOALjJDFtKIibG8jZFGoeawEvfiaFAic8nC4fbHJ5XCEzAmZkTQFZt7oHunrXWLSbV76Qfgx0KuQtU4Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在业务逻辑上借助计算列筛选日期方法的结果更为合理，因此纯DAX的方法对于不同维度的分析不具有普适性，还得根据分析的角度控制度量值计算的数据颗粒度：

> 利润.新.PY.ByMeasure.Correct\=
> 
> VAR
> 
>     LastOrderDate =CALCULATE ( MAX ( '订单表.新'\[订单日期\] ), ALL ( '订单表.新' ) )
> 
> VAR 
> 
>     CurrentDates =FILTER ( VALUES ( '日期表'\[日期\] ), '日期表'\[日期\] <= LastOrderDate )
> 
> VAR
> 
>     Result =CALCULATE ( \[利润.新\], SAMEPERIODLASTYEAR ( CurrentDates ) )
> 
> RETURN
> 
>     Result

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOALjJDFtKIibG8jZFGoeawEu3s0QkEiadBK2WBauTCWGLI0lIX1tAjPD12lvA7qibcFkToPv2Wmmhhw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

用FILTER以最后订单日为界限按日筛选日期表（VAR CurrentDates），进而用作计算上年利润的CALCULATE表参数，结果和辅助计算列方法殊途同归。

**总结**

借助计算列，按照固定套路可以实现在行级别对日期进行筛选控制日期智能函数的报表展现，简单易用；在无法编辑数据源的情况下，也可以通过DAX根据汇总数据的颗粒度，灵活改变筛选环境，达成同样效果。

**参考文章：**

https://www.sqlbi.com/articles/hiding-future-dates-for-calculations-in-dax/

示例数据基于PowerBI星球案例文件。

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和2.5k+ 学习者一起成长
