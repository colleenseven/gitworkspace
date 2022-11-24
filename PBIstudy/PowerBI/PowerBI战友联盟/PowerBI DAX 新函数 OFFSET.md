---
create_date: 2022-09-23T11:36:12 (UTC +08:00)
tags: 
aliases: null
pagetitle: PowerBI DAX 新函数 OFFSET
source: https://mp.weixin.qq.com/s/8-cILwJxqf7sfikswhtQeQ
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

DAX 出了一个新函数，叫：OFFSET。

## 案例

先来看看它的效果。如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM9pn7twDLrs24oTO3FiajWSmgAEFtmWndehibOZxdG9QLlkwofgTfKCicHHFpTgH9FgMzbG5rVFUUKA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果我们希望在透视表的另一列可以获取前一列的上一项的值，该怎么做呢？这个问题在以前需要做定位。而有了新的函数 OFFSET 可以简化这个过程。如下：

```
KPI.Prev.按产品类别 = CALCULATE( [KPI] ,    OFFSET(        -1,        ALLSELECTED( 'Dim 产品'[产品子类别] ),        ORDERBY( 'Dim 产品'[产品子类别] , ASC )    ))
```

如果使用 2022 年 9 月的 Power BI Desktop 编辑这个度量值，可以看到：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM9pn7twDLrs24oTO3FiajWSyWHrzOEdvb8cCads1pxzpFBvrCaIll2lupB2svs6e5xTbj0tlHXeYw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

系统对 OFFSET 以及它的伴随函数 ORDERBY 并没有支持，但它们的确可以使用了。

还可以看这样一个例子如下：

对应的 DAX 公式，如下：

```
KPI.Prev.按月份名称 = CALCULATE( [KPI] ,    OFFSET(        -1,        ALLSELECTED( 'Dim Calendar'[MonthNameCN] , 'Dim Calendar'[MonthNum] ),        ORDERBY( 'Dim Calendar'[MonthNum] , ASC )    ))
```

通过观察，不难发现 OFFSET 的作用在于将当前筛选上下文中的表按照数据模型中某列引用进行排序，并按指定数字进行偏移。

例如：

1.  OFFSET 第二个参数：针对当前筛选上下文中的四月，构建全部月份与月序号的表，记为 T，由于使用了 ALLSELECTED，不受到筛选上下文的影响。
    
2.  OFFSET 第三个参数：指定 T 按照日期序号列升序排序。
    
3.  OFFSET 第一个参数：指定当前筛选上下文中的日期列序号是 4，向前移动一位是 3。
    
4.  3 对应了 T 的三月和序号。
    
5.  此时 OFFSET 生成的筛选上下文覆盖了外部的筛选上下文。
    
6.  因此，计算结果是上一个月的值。
    

## 参数

OFFSET 第二个参数必须是表。

OFFSET 第三个参数必须是列引用。

OFFSET 第二个参数所计算的表必须与第三个参数的列引用有关系。

## 更复杂的案例

来看一个更复杂的案例，已知这样的结构：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM9pn7twDLrs24oTO3FiajWSLZwEBTTLRPibfAp1oBibHcg0ZYO3YFib6rGicG2icss20UEjO5IU3bhFSEA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

对于 DAX 查询：

```
CALCULATETABLE(     OFFSET( 0 , SUMMARIZE( ALL( 'Fact 订单' ) , [产品子类别] , [产品类别] ) , ORDERBY( 'Dim 产品'[产品子类别] ) ) ,        'Dim 产品'[产品类别]   = "办公用品")
```

这里的 OFFSET 使用了 0，结果为：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM9pn7twDLrs24oTO3FiajWSCYRo3vbkNu4AVtJtUxYWoiaQlzHTzvNP2tNFsOltYsrQ6rlW2PUPwrA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这说明 OFFSET 的第一个参数可以是多列的表，而不一定非要与 ORDERBY 的列引用完全一致。

对 DAX 查询调整下，如下：

```
CALCULATETABLE(     OFFSET( 1 , SUMMARIZE( ALL( 'Fact 订单' ) , [产品子类别] , [产品类别] ) , ORDERBY( 'Dim 产品'[产品子类别] ) ) ,        'Dim 产品'[产品类别] = "办公用品")
```

这里的 OFFSET 使用了 1，结果为：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM9pn7twDLrs24oTO3FiajWSDxvIYrPwZSKgVwQa1jjZO7AJicLhJb5V61icmaZCzr0viaVPGYdbP1kEQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个结构相当费解，经过多次实验，我们发现了这里的规律，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM9pn7twDLrs24oTO3FiajWSbvibINUw9Wl4znqMGCoes0a3745tfyH0ICCpmuuOJo9iaiaMDkvPuFuzg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以理解为：

1.  按照产品子类别排序，形成一个双列的表，记作 T。
    
2.  从中挑选产品类别为 “办公用品” 的。
    
3.  对上述结果依次在 T 中向下移动一行，取出这个子集。
    

这么复杂的逻辑可以对起来，绝非偶然，这应该就是这个函数的运行逻辑。

将案例做一个调整，如下：

```
CALCULATETABLE(     OFFSET( 0 , SUMMARIZE( ALL( 'Fact 订单' ) , [产品子类别] , [产品类别] ) , ORDERBY( 'Dim 产品'[产品子类别] ) ) ,        'Dim 产品'[产品子类别] = "电话" // 这里调整为产品子类别)
```

这里的 OFFSET 使用了 0，结果为：

将这里的 OFFSET 使用了 1，结果为：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM9pn7twDLrs24oTO3FiajWSibiaWYNAAVjm7ROE95U4yZPONIGo0nAQWbOzYHIzxDibrLibwaAQEBdibibQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果对照上述的列表，符合上述总结的规律。

## 运行的规律

OFFSET 在筛选上下文中取出一个表，同时对表中元素实现偏移。其过程为：

1.  有一个筛选上下文，记作 F。
    
2.  在 F 下计算 OFFSET 的第二个参数，得到一个表，记作 T。（可以用 ALL 族函数清除筛选）
    
3.  OFFSET 的第三个参数必须是列引用，记作 BaseTable \[C\]，且出现在表 T 中，并按此列引用进行排序。
    
4.  对 T 按照 F 再次筛选，对符合筛选的元素分别进行位移，按 OFFSET 的第一个参数进行。
    
5.  返回 3 的结果构成的表。
    

这里需要注意的一个细节是：

OFFSET 的第二个参数会先在外部筛选上下文中计算，得到 T。

得到的 T 会再次在外部筛选上下文中计算。

也就是说外部的筛选上下文会使用两次。

## 注意

从操作数据的角度，让我们来简化理解 OFFSET 的意义。

第一步，我们需要在数据模型中取数。

第二步，取到的数不着急直接拿出来。

第三步，先偏移一下再取出来。

也就是说，OFFSET 实现了在取数时实现偏移。由于 OFFSET 取出的数形成表，因此可以覆盖外部已经存在的筛选上下文。

也就是说，OFFSET 实现了取数构表过程中，在取数后偏移后再构表返回。

注意：由于 ORDERBY 中的内容必须是列引用，因此，对表的排序只能是预先定义好的位置，而不能根据度量值动态排序。

## 总结

目前，Power BI 官方文档还没有披露这个函数的技术细节，这里的解释仅供参考，未来进一步补充。

除了这里给出了计算前后元素对应指标，OFFSET 的作用既然是移位，那么大家还能想到什么应用呢？欢迎留言谈谈你想到的案例。

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
