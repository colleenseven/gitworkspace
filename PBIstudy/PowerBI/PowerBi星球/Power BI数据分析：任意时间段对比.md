---
create_date: 2020-12-02T23:44:55 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI数据分析：任意时间段对比
source: https://mp.weixin.qq.com/s/AXeEummycf7YBAwXYGitqw
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

对于正常的有规律的时间段比较，像同比和环比，以前写的比较多，在PowerBI中也很容易计算。业务分析中还会遇到的一种场景是，选择任意区间的两组日期，展示其数据对比情况。

**比如对两次促销活动的效果进行对比分析，两次促销活动期间，可以是任何时间段，没有对应关系，天数也可能不一样，那么如何快速的比较这两个时间段的数据呢？**

以PowerBI星球常用的数据模型为例，已经有订单表以及对应的日期表、产品表，模型如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO8213JMWWIoRlFdibU9ktG934CicQ71fCLCgejkMdyvF65HtOh0VNBvXfia9aib2Sj9e7pHibtDbdNXwg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

想要达到的效果是，通过两个日期切片器，来选择两个时间段，报告中分别展示这两个时间段的产品销售额。  

下面来看看PowerBI如何实现这种分析需求。

**1、建立'比较日期表'**

因为需要两个互不影响的日期切片器，来选择不同的时间段，所以两个日期表是必须的，建立比较日期表很简单，直接复制原日期表就可以了，点击新建表，输入：

> 比较日期表 = '日期表'

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

**2，'比较日期表'与原'日期表'建立非活动关系**

如果两个日期表直接建立物理关系，依然会相互筛选，无法生成两个独立的时间段，所以这里的做法是**建立非活动的虚线关系**，关系图如下：  

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

关于非激活关系请参考：[认识Power BI中的非活动关系](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071870&idx=1&sn=f110592b92b23dd7d7515c4cc342c101&chksm=8e0c4769b97bce7f97489d4f34ca603a0e12af4c5acd90101205c670709ecf07f3ee95830a1d&scene=21#wechat_redirect)

**3，建立度量值**

有了上面的模型，就可以建立度量值了，当期收入很简单：  

> 当期收入 = SUM( '订单表'\[销售额\] )

比较期间的收入，就需要利用USERELATIONSHIP函数来激活上面的非活动关系，度量值如下：  

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

这个逻辑并不复杂，结合上一步建立的数据模型来理解：清除原日期表的筛选，并激活非活动关系，这样'比较日期表'的日期，就可以通过原日期表来筛选订单表，返回比较期间的收入。  

该度量值用到的REMOVEFILTERS是今年新的DAX函数，相当于ALL函数，这里也可以直接用ALL函数来替代，不过它相对更容易理解，通过函数名称本身，就能猜测到它是什么功能。

**4、展现结果**

利用原日期表与比较日期表中的日期，生成两个切片器，将当期收入和比较期间收入度量值放入的矩阵中，就可以显示出某产品任意两个期间的收入对比：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO8213JMWWIoRlFdibU9ktG9c4lLtcGdYL2wIdo250pv5nm3wMSUfFQz9zpjDAZYIfbByiaKtic9zdibw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

当然也可以利用图表来更直观的展示：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJO8213JMWWIoRlFdibU9ktG92icporRUw3R1pKzxBV9LVafRJZ8PlGXlw03Uw1OaOCkKDOrXE0xjPxQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

这样就实现了比较不同期间数据的效果。

不同时间段的比较分析很有用，上面的做法不改变原模型关系，只是通过两个日期表的非活动关系来实现，简化了模型的处理，当然方法不止一种，大家遇到类似的需求时可以尝试。

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtHORfNDsk1ibQ1luXtyibbDsnnwJXvdSpKwfPlcJCZSlvWYOK6p6VGeqw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtVXYmWpicF9SVicdBBQYdaKG4icSfUTkS9dFIBW3NsL5ZrNpYH6icjgJaUA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 扫码加入，与2k+ 学习者一起成长
