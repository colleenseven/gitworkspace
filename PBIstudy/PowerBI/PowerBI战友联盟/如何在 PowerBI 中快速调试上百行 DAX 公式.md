---
create_date: 2022-01-18T13:36:57 (UTC +08:00)
tags: 
aliases: null
pagetitle: 如何在 PowerBI 中快速调试上百行 DAX 公式
source: https://mp.weixin.qq.com/s/iy_60Kd3eMR4nq4QAXbd-A
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

作为刚刚开始写 DAX 公式的小伙伴，会遇到一个非常明显的问题，那就是：我怎么知道我的 DAX 公式在某一步算出来了什么。

## DAX 公式的特点

DAX 公式是可以嵌套的，且中间是可以产生出表的，但最终以度量值呈现的结果必须返回值。

也就是说，不论中间步骤产生了多么复杂的表结构，最后必须返回一个值。

这就导致很多伙伴希望知道中间过程中的表到底与预期是否一致。

## 典型的错误

来看一个典型的错误信息：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMZxr111go0e9Zy8R9eiczp7tAArOSo62PialbRF5Mcu1v4fndacz9V729bPunCjiaKoL6jUBVVoXEpw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

Power BI 的错误信息并不友好，真不知道产品经理是怎么想的，一旦出现错误就给出一个恐怖的差子，而且还就是这么设计的，导致很多伙伴遇到这样的恐怖信息就望而却步了。

这里首先要告诉大家的是：不必担心自己编写的 DAX 公式，它们不会在本质有任何负面破坏性效果，仅仅是无法计算出来结果而已。

## 分析错误信息

排除错误信息的第一步，是要分析错误信息，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMZxr111go0e9Zy8R9eiczp7VSDZ0eKD0Ow1kPHjGr88rib6hyJ77x3Uibtaqt0fgxtQ1PibXgnSSZwXw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

绝大多数伙伴遇到这步的第一反应是：

> 啊，出错了。啊！哪里错了？然后就点击【关闭】了。然后就去思考自己的公式哪里出错了。

这是不正确的表现，因为这个信息非常重要，它可以告诉我们问题是什么，至少可以帮助我们锁定问题出现的位置。

我们仔细来看下这个信息：

> 百分位数值必须介于 xxxx 范围之间，其中 N 是数据值的个数。

这个信息几乎可以帮助我们锁定出现问题的位置是_百分位数_的计算位置。

## 进行调试

回到 DAX 公式中，大概如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMZxr111go0e9Zy8R9eiczp7ia8Ny3SNvo70dBziad6d66sO9tgWRGJyVHDuODataHgAF6OiaBBtekbibw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

不难发现错误是在这里引起的。

> 很多伙伴看到这么长的公式直接就放弃了，但是的确可以进行调试。而不需要借助复杂的工具。

首先来确定是不是这个公式引起的，可以替换为一个特征值，如：9999999。如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMZxr111go0e9Zy8R9eiczp7dRCibiaVVicO2rCMEojib2VpFj5aYP9Mrnt3DGNgDGWMRjhic1wBbg4InAQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMZxr111go0e9Zy8R9eiczp7yj5yZPGYvmrJShxPYdtRYJeBibfrkLxrFLSpY2jcXI6QYapMtU6Npmw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以看出：此时的错误消除了，而返回了特征值，说明：定位的错误位置是正确的。

接下来，就是要分析这个错误到底是为什么了。

这时候的技巧在于三点：

-   【技巧一】再次审视错误信息。
    
-   【技巧二】看函数中涉及的中间表数据。
    
-   【技巧三】分析函数的执行过程。（可能涉及到上下文转换）
    

如果可以同时考虑到上述三点，几乎 80% 的错误就可以被分析出来。我们来试一试。

先来看【技巧一】错误信息：

> 百分位数值必须介于 1/(N+1) ... N/(N+1) 范围之间，其中 N 是数据值的个数。

也就是说，错误来自于数值的范围不对。我们尝试代入：

N = 1，则：1/2 ... 1/2

N = 2，则：1/3 ... 2/3

而我们使用的公式是：

```
PERCENTILEX.EXC( SoldDaysList , [已售在库天数] , 0.75 )
```

这个公式中用到了一个表中的元素 \[已售在库天数\]，后面的参数 0.75 必须介于合理的范围之间，如果：

N = 1 或 N = 2，都会导致这个公式错误，那么 SoldDaysList 的 \[已售在库天数\] 会有多少个元素呢？

我们需要提取 SoldDaysList 的信息，就需要【技巧二】了，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMZxr111go0e9Zy8R9eiczp7TtgoMUibxxIep6PibzTMqxzib9utxicFxvmsy7ulzy4g1aKIGJTBa2XD4A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

得到：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMZxr111go0e9Zy8R9eiczp7ic357pYm0Jzpp09nFuCTKQ4FiccvwUQeCP6ItJUaZY8o2iaJkLvQUYkZg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个元素的确很多，还可以看到：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMZxr111go0e9Zy8R9eiczp7kQbR8kOASS2OQrPonYfVNMiaOBxwfYkFgzJvpOruqy8iatqMibXP9kHuQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个元素只有一个，因此正好命中了错误信息的含义。

我们找到了问题所在。

调整公式如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMZxr111go0e9Zy8R9eiczp7mf54HptYQEpffa9WtjmEaSaZ5DVmlTLWc4LV99WKrSLPcxUoB1oMUw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

返回的结果不再报错。问题得解。

当然，如果这个语义不合理，可以进一步调整公式。但已经至少排除了错误本身。

## 总结

DAX 公式的调试的确是一个问题，这里给出了不依赖任何第三方工具，完全依靠逻辑上的分析以及 CONCATENATEX 这个既具技巧的函数来返回中间表内容结果以便排除问题的过程。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNhia5Pc4XC1Um7IYgQhGEoEC1yK05ibUFoPBYpcoAMvibuZh2BZaibMzULeDwNfSeQ0KHRcDUdX3FzVA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

与精英一起讨论 Power BI，验证码：data2022  

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOiad5BOrdQTKpB733esKiaxZa53LXWIPlQicMjxntaRr3a2hnMmuibTib8QacXeiakucDr7lSNGkuV2MXw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击“阅读原文”进入学习中心

**↙**
