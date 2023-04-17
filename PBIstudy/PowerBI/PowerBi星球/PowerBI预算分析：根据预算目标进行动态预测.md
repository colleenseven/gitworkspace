---
create_date: 2020-11-04T23:48:32 (UTC +08:00)
tags: 
aliases: null
pagetitle: PowerBI预算分析：根据预算目标进行动态预测
source: https://mp.weixin.qq.com/s/KH2amU8lxLjB4MrUZanJ2Q
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

上篇文章介绍了[预测数据与预算目标的比较](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073666&idx=1&sn=427f76eaeafb6473ade9cceb86056b96&chksm=8e0c5e15b97bd703d5b6a3cef12fc07c7f7fd0e04740366501e2c832235916417ea48df48faa&scene=21#wechat_redirect)，有星友后台问，如何让预测数据正好与预算目标一致呢？或者说，如何根据预算目标的完成情况来动态的确定预测数？

这个问题并不难，**基本思路是先计算出截至业务的最后一天，实际数据与年度预算目标的差异是多少，然后将这个差异按一定的方法分配到当年剩余的期间。**  

下面用两种方法来分配这个差额，使年度预测数据正好可以达成预算目标。  

**1、按平均分配进行预测**

这是最简单也是最易于理解的方式，度量值如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMNm6MmREunkic41ficI2dJ2XDvMMib8NzyWickoQh4sl5M0APWZkMkc7FV0BhfOnTicpI4ntuqgeokibfQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

度量值的逻辑请参考注释。

用柱形图来看看这个预测结果：

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

从这里可以看出，因为是平均分配，所以每一天的预测数据完全一样。

然后再根据上一篇文章的思路，将实际数与预测数汇总起来，看看是不是和预算目标一致：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMNm6MmREunkic41ficI2dJ2XufA6A05xtLVS5D12UFeLT9hX7nBrIxG68PseSkhUGXE7JkTgSZ55hQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

利用面积图显示如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMNm6MmREunkic41ficI2dJ2XMebXCYtfxYNGzXIGsnjiaLfYoQZeqicLKfHHeOfsOWeQ7sPIzBsnUMTw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

从图中可以看出，到年底，预测数据正好与预算目标重合，并且由于预测数据每天是相等的，所以累计数也是线型的增长，表现的趋势图上，预测线是一条上升的直线。

**2、按上年的业务趋势预测**

这种方式稍微麻烦一点，先计算出预算与实际的差异，然后计算上年同期的累计收入，预算差异与上年同期累计收入的比率就是为达成年度预算的增长率，用这个增长率乘以上年同期的收入，就是本年的预测数。  

用DAX将上述逻辑表达出来：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMNm6MmREunkic41ficI2dJ2Xwc85gcG2Q6dvbuK3OqDTwaMw7J9UL4TLkeWkkPoQTmsT6W8ROpe8oQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在柱形图中显示如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMNm6MmREunkic41ficI2dJ2X2MA3yTG7ib9azpZDeB12kquoHpZpHvicOuTOM0hKhWT9MUoWJVjcF8ibQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

同样的用度量值写出年度预测累计数：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMNm6MmREunkic41ficI2dJ2XdTibkO69KeKbiazQNfF8ntlbQMC2ksj38P3qBCZkEiaxG38c9Kiczr8icrg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

最终年度累计预测结果与预算对比如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMNm6MmREunkic41ficI2dJ2X5xhmeic0H5lnianc2ru4CCiaOlrv0gf544ZdoRzpZ8icKKVzCIU2PD2iaBQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

年底的预测结果同样与预算目标完全重合，并且预测线不再像第一种方法的直线，而是有一定的波动，这个波动就是上年的业务趋势，这种方法可能比平均分配更符合实际的业务情况。

以上的预测数据也是动态变动的，随着业务的进展，上面的度量值都会自动计算出当前实际业务与年度目标的差异，并按照上述方法分配到未来的期间，而无需再手动的干预，动态实时的根据目标进行滚动预测非常便捷。

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtHORfNDsk1ibQ1luXtyibbDsnnwJXvdSpKwfPlcJCZSlvWYOK6p6VGeqw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtVXYmWpicF9SVicdBBQYdaKG4icSfUTkS9dFIBW3NsL5ZrNpYH6icjgJaUA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 扫码加入，和2.6k+ 学习者一起成长
