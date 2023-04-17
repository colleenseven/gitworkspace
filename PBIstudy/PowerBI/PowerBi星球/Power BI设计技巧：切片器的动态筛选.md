---
create_date: 2020-12-16T23:43:38 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI设计技巧：切片器的动态筛选
source: https://mp.weixin.qq.com/s/oRjkUcMjFtAddw1agYdFiw
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

经常碰到这样的需求，在报告中设置一个切片器，当用户打开报告时，默认显示的是最近一个期间的数据，比如当2020年11月30日打开报告时，显示的是2020年11月的数据，第二天再打开刷新，自动显示2020年12月的数据。

目前PowerBI没有办法动态的改变切片器的选项，当你选择某一个具体的期间时，下次再打开依然还是这个期间，不能自动变为最新的。

这个需求很普遍，很多人受此困扰，几年前就有很多人在微软PowerBI社区中提出过该需求，但这么多年过去了，现在的版本仍然还没有这个功能，那么我们就通过一个变通的方式来实现它吧。

**最终目的是要动态的筛选数据，由于切片器的选项不能自动改变，那么换一个思路，可以将该选项所代表的区间动态化**，以显示本月的数据为例，只需要在日期表中添加一个计算列就可以了：

> 年月 = 
> 
> IF(\[年度月份\]=FORMAT(TODAY(),"YYYYMM"),"本月",\[年度月份\])

这列的含义是，如果当前的年度月份是今天所有在年度月份，就返回本月，否则正常返回年度月份的值，结果如下：  

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

然后利用这一列，制作切片器即可。

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

因为计算列中的“本月”会根据TODAY的值动态计算，所以任何时候打开这个报告刷新，默认都会显示“本月”的数据，这样就实现了报告的自动筛选。  

还有个常见的情形是动态显示业务最后一天的数据，每次打开刷新后，报表自动显示最后一天的数据，而无需再选择切片器。  

同样的思路，在日期表中新建一列：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMTBmAIN2RegHGXTqiawoEfUbgVUbvP3uHZ7WaGicEgAwjvNUJdg2A0QQUeZ8nfj7FJ5PqwSzhIaf5w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个新建列的含义是，如果小于业务最后一天的日期，就正常返回该日期，如果等于最后一天的日期，返回“最新业务日期”，如果大于最后一天的日期，则返回空值BLANK。  

其中 MAXX(ALL('订单表'),'订单表'\[订单日期\]) 用于计算订单表中的最新日期，当然你也可以先把这个日期用度量值写出来，计算列中直接引用也可以的。

这个示例中，业务最后一天的日期是2020年12月8日，在日期表中这一列显示如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMTBmAIN2RegHGXTqiawoEfU0EJOibmU8Lymap7F5TDiak9T8uvsG1Cnz0xS2e8bTrW35Q9QjjEJqVYA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果订单表中业务更新到12月9日，则这一列自动在12月9日显示为“最新业务日期”，因此用这一列做切片器，并选择为“最新业务日期”，报表就可以自动随着订单表中的最新日期而自动切换数据。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMTBmAIN2RegHGXTqiawoEfUwiasrEuHdXXHsC5fojSpKoic1kOw3lw4oP1YpWvp4Iu0QL1CaaYofd8g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

因为这一列中有空值，所以切片器中会显示一个BLANK选项，如果不想显示，可以在筛选器中把它去掉。

或者使用内置的切片器，使用下拉模式，只显示最新业务日期的选项，为了让用户知道最新业务日期是哪一天，可以在报表中放个卡片图，来显示出这个日期：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMTBmAIN2RegHGXTqiawoEfU18w4icGJicdSJqk6w42UgK2x1sDnf9lNAe7PicCdGp3nUfL4bUo6NNxKg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

当然，如果你想选择其他日期，点开切片器选择就行了，用户仍有查看其他日期数据的自由。

上面是两种常见需求的解决方案，切片器的选项是固定的，但该选项代表的区间是动态变化的。同理，如果你的业务需求是在报表中默认显示为今日、昨日、上个月、本年等各种效果，都可以借鉴这种思路实现。

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtHORfNDsk1ibQ1luXtyibbDsnnwJXvdSpKwfPlcJCZSlvWYOK6p6VGeqw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 2k+ 学习者一起成长
