---
create_date: 2020-09-22T20:37:09 (UTC +08:00)
tags:
aliases:
pagetitle: Power BI如何计算任意所选期间的环比？
source: https://mp.weixin.qq.com/s/4SdA05JZDrRaDEjxa1JOiw
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

Power BI内置了一系列日期智能函数，覆盖了计算同环比，上年同期，本期至今，期初期末，当期全局数据等高频需求。

星主也发表过基于标准日期智能函数思路的非标准日历计算方法和任意期间上期的计算方法。

[Power BI非标准日历的计算思路](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070813&idx=1&sn=70852e62479cfc082b34a63f62ef64dc&chksm=8e0c434ab97bca5c0d7d1ff838a8b1d07f481da3774555a962b0dd76156fd45535a487cfda7a&scene=21#wechat_redirect)  

[Power BI如何计算任意期间的上一期？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070897&idx=1&sn=e1c6df8847cd6b42ccb54d265a2e261e&chksm=8e0c4326b97bca304ebee7ec593de4084a63a7acf4d7b2cb2d09c057806edfbe28d4f9943051&scene=21#wechat_redirect)

这类方法在处理连续日期段的汇总比较(今年vs去年 / 当月vs上月/ 移动平均等)可谓得心应手；而对于非连续期间的处理，标准的日期智能函数往往捉襟见肘。

**例如选择某年3月、5月、9月份的数据，并将其与所选的上一期数据对比，也就是5月v s 3月，9月 vs 5月，这种需求如何计算呢？**

本文介绍如何用DAX处理该类问题的技巧。

日期表永远是是模型中的必要部分，如何构造及要求不再赘述。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMCApUtJMPCwL4FFF2JTqGibmVxYB0z8pqL2JdJicN3QjkyxZGxSdibMEw8I1F9vqHs5FFBtXmxVLDog/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

案例以 \[年度月份\] 维度对事实表的 \[利润\] 进行汇总，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMCApUtJMPCwL4FFF2JTqGibEkkS29ooC9L7mRKQgrGknn9lZPw6YibTnk5cIFLFfasY7KrhUkfpJVg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

接着计算每个年度月份所选上期利润，\[利润.上期所选\] 度量值公式：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMCApUtJMPCwL4FFF2JTqGibdE1ToIunW2Sjia0Il0UFric2K56JCpaSZTOH7yogebhicJOSXJEnabic4Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个度量值的逻辑是，对变量PreviousYearMonth用CALCULATE + ALLSELECED改变筛选上下文环境，返回上一期选择的年月，进而作为计算利润的筛选条件得出上一期所选数值。 

CALCULATE 与ALL系列函数的经典组合成功实现对视图层面的上一期利润计算。这里的关键在于对筛选环境的动态控制，请仔细体会下ALLSELECTED, ALL, KEEPFILTERS出现的位置和对CALCULATE筛选器的影响。

计算结果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMCApUtJMPCwL4FFF2JTqGibtxvocrib4iaIKfBNoa1ibWXwmSzc85QF5gXr3KBMN2s1OdFqsq6nL8uTg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

突破了计算非连续日期的上期利润瓶颈之后，便能轻松按照常规套路进一步处理，比较相隔期间的数据变动，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMCApUtJMPCwL4FFF2JTqGibLfEh8IyqmHH2XBdSdkWSiblM4Am2YibS6rYOw3icmyiak5xTTEofRG2mpg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后计算比率就很简单了，最终结果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMCApUtJMPCwL4FFF2JTqGibql01uT9aBFfgJjLzibDsib2x6Smt2qjn22iaGdicqunHibwJAxBlCp1SRbQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**总结**

  
本文作为按日期汇总数据方法的补充，本质还是基于的日期智能函数的套路并结合DAX强大的筛选器调整能力实现灵活计算。伙伴们可以多多实践，更好的驾驭DAX~

**参考文章：**

https://www.sqlbi.com/articles/comparing-with-previous-selected-time-period-in-dax/

示例数据基于星球案例文件。

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtHORfNDsk1ibQ1luXtyibbDsnnwJXvdSpKwfPlcJCZSlvWYOK6p6VGeqw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和2.4k+ 学习者一起成长
