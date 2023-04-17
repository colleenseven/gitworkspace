---
create_date: 2020-10-28T20:29:02 (UTC +08:00)
tags:
aliases:
pagetitle: Power BI根据历史数据进行预测的几种方式
source: https://mp.weixin.qq.com/s/rKlrUU_rJ2n5G7yOYFqghQ
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

预算分析时，还经常需要对未发生的业务进行预测，预测也是年度目标制定的重要依据，本文就来看看几种常用的简易预测方式，以及用PowerBI如何实现。

**1、利用上年数据作为本年的预测数**

获取上年同期的数据可以用时间智能函数SAMEPERIODLASTYEAR，也可以用更通用的DATEADD函数来表达，度量值如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO3fAjtwgJL5vnGf6HBRNweMgoEYURuicZMcQofvb0KhtULr2AcDIkMH10ohQQCKPwjsfxwYobPhGQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个度量值同样先做了判断，只有在未发生业务的日期，才返回预测数据，也就是上年同期数。

结果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO3fAjtwgJL5vnGf6HBRNweic84Zr7RdWhJHRqq0hv8vYsvO753QtC0wiaclC7p1nt35uQDPLczvpcA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

按上年同期数据进行预测，适合较为成熟稳定的业务。

**2、按上两年同期数据的平均值，作为本年的预测数**

先分别计算上年和前年的同期数据，然后取平均数，作为预测数据：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO3fAjtwgJL5vnGf6HBRNwe43IAVTrustFV4gDjUvzUzaUIiaziarcd9eaD7G8uVUaXW9FibkGFk1cAA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

结果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO3fAjtwgJL5vnGf6HBRNwevydgIcojIQ8qYjFDIA2hFpuzW1X5dCPuibcoQZzqbxyJtiaG8QkMuib6g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

逻辑与上面类似，只是为了避免一年数据的偶然性，使用了两年的数据进行折中，所以每天的数据，相对波动更小一些。

**3、按上年同期数据的移动平均值，作为本年的预测数**

比如按30天移动平均，度量值可以这样写：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO3fAjtwgJL5vnGf6HBRNwePIMuOwSSYbASKQjdSpUpUXqMKMpyGUqPtZp2wIzLt8PTU23UYnKtyQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

那么预测度量值就可以直接这样写了：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO3fAjtwgJL5vnGf6HBRNwe5LxRABmnf2CodVD4sucEODdiagOFnA6rN9MNyBYVxjf0QyeIPr8PV0Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

结果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO3fAjtwgJL5vnGf6HBRNwepJ3Rwy156vJ9PBxqxFDpibQjBDY7tlN2yqiaBFldVb02vFzHK5EKTlzA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

按移动平均做的预测，每日数据看起来平滑多了。

**实际应用中，不会完全按照历史数据本身作为预测数据，一般还会乘个增长系数，以第一种预测方式为例，比如按去年同期数据上涨10%来预测，度量值中乘以1.1即可。**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO3fAjtwgJL5vnGf6HBRNweFKtuPLomQkWUcW4SKpppKok8DJqAicxibAicYK7Ea4MxaqYetAiceoe06A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

进一步的，还可以利用[参数](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067672&idx=1&sn=1a141b81b4e20f83cabf410164f55974&chksm=8e0c778fb97bfe9904d988eb9972b26436c260e575d008d1414076b86df997fee74dc559ec73&scene=21#wechat_redirect)来做个动态系数，以便进行动态的调整预测，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO3fAjtwgJL5vnGf6HBRNweWS4iamsY4pOjVunZO0D7j2dtV6zENovYYvAxxE5J6eQBeae8aB4ngEA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后将度量值修改为：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO3fAjtwgJL5vnGf6HBRNwenDC5qHD6vGnURpKSOr53aQ16wZ9TJxiag3Qo9iaJuhlqq1kyibhOrF6Jw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJO3fAjtwgJL5vnGf6HBRNweP6icQ1YZWzgFjp8bKVRJ3581EznnnntM7Bp31BBx5hs1cuU1nlkM8Qg/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

其他两种预测方式也都可以结合参数来动态预测，这里不再一一介绍。

上面只是几种简易的根据历史数据进行预测的方式，逻辑很简单，对于更复杂的预测，只要有明确的计算逻辑，同样也可以在PowerBI中实现。

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtHORfNDsk1ibQ1luXtyibbDsnnwJXvdSpKwfPlcJCZSlvWYOK6p6VGeqw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和2.6k+ 学习者一起成长
