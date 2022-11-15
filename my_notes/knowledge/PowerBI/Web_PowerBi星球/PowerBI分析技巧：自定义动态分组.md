---
notes: True
aliases: null
create_date: 2022-08-31T12:20:20 (UTC +08:00)
tags: wx/pbi/建模技巧
pagetitle: PowerBI分析技巧：自定义动态分组
source: https://mp.weixin.qq.com/s/1i3buocFqMwsYT9ilRc1Qg
author: 采悟
status: 已完成
category: 泛读文章
uid: 
---

DAX:: SWITCH, TRUE, MIN, MAX, SUMX, VALUES, FILTER, GENERATESERIES, SELECTEDVALUE,CROSSJOIN

---

关于<mark style="background: #FF5582A6;">数据分组，一般是通过辅助表来进行的</mark>，比如分享过一篇关于客户细分的文章：

[PowerBI业务分析：客户细分](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071357&idx=1&sn=e533d335e302b9ca5c76313dcac38852&chksm=8e0c416ab97bc87c1101fcbdb870356d9a400c68ba7c8ab6b91d4e6c54726b28cc358b6015fd&scene=21#wechat_redirect)

其中客户的分类是通过一个辅助的客户类型表表来确定的：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPWQnxE4lQ1u1sAZMvlIwjyicpkfuQcuVy02ib4H4NCgr5Hr7SYU8o4eeicesUvhhyPaiccLOOBXXjB3w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在这个类型表中，每个分类有固定的边界点，这种分类标准是固定的，那么**能否让用户可以自定义分类标准呢？**

下面就通过客户细分这个案例来介绍自定义分类标准的思路。

自定义标准，首先<mark style="background: #FF5582A6;">需要为用户提供个输入框，这个输入框我们利用切片器来实现，为了做这个切片器，这里先用DAX建一个序列表</mark>。

> 分组表 = GENERATESERIES(500,5000,1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPWQnxE4lQ1u1sAZMvlIwjyFSXsy0vkHibWzDd7YVRlrbQticsXeHOsmiahs4CL1f3cfw0D7ZsVNGq5w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里利用GENERATESERIES函数生成一个从500到5000的序列，假设分类标准都在这个范围内，具体起止点，你可以根据实际分析需要来调整。

然后用<mark style="background: #FF5582A6;">分组表的字段做个切片器，样式为“介于”</mark>，切片器就出现两个输入框，我们就利用这两个值来进行标准划分，为了让用户更清楚这两个值的用途，可以在标题上对它进行必要的文字说明，如下图。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPWQnxE4lQ1u1sAZMvlIwjyibLJT9SicrGNZCGFicXticXIcrz6fdmMHwscoPCtwoldaqiamEjYrz8LDkg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关于切片器的格式设置，可参考：[玩转PowerBI的切片器，看这篇就够了](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074560&idx=1&sn=7050c2194d5e0a5587ec6282ff17b4ad&chksm=8e0c5297b97bdb81d70e9a7ece3d0d557a1fe58fe7102ceedec734222a89777e8724f784acfe&scene=21#wechat_redirect)

当然关于客户的分类表，依然还是需要的，这里还是用上面的三个分类，只是每个类别的最大值和最小值不需要了。

这些基础工作做好以后，建立度量值：

```
利润 客户细分 = 
SWITCH(
    TRUE(),
    [利润]<MIN('分组表'[Value])&&SELECTEDVALUE('客户分类表'[客户分类])="低贡献客户",[利润],
    [利润]<=MAX('分组表'[Value])&&[利润]>=MIN('分组表'[Value])&&SELECTEDVALUE('客户分类表'[客户分类])="一般贡献客户",[利润],
    [利润]>MAX('分组表'[Value])&&SELECTEDVALUE('客户分类表'[客户分类])="高贡献客户",[利润]
)
```

这个度量值的逻辑是，判断<mark style="background: #FF5582A6;">利润所在区间以及分类表上下文的类型，如果利润小于分组表的最小值，并且客户分类是“低贡献客户”，返回利润</mark>，其他两个判断条件同理，这样判断的结果是，只有某个客户在正确的类型下面，才返回其利润数据，效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPWQnxE4lQ1u1sAZMvlIwjyRk2rBLKNianhu214Du5uQJmib35LzicaiaL62wCBibloTWR2OL8C4gBfjFQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

通过调整切片器的范围，就能够自定义分组了，按散点图的效果更加直观的看到随着分组标准的变化，客户所属类型的变化情况。

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPWQnxE4lQ1u1sAZMvlIwjyMYT190vZugmcZhHBhiburaBdjbJQZtiampzYh1ia3FdaEDibQYMlbuVDMw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

进一步的，如果想统计每种客户类型的利润总额和客户数量，可以这样来写度量值：

```
利润 按类型汇总 = 
SUMX(
    CROSSJOIN(
        VALUES('客户'[客户姓名]),
        VALUES('客户分类表'[客户分类])
    ),
    [利润 客户细分]
)
```

```
客户数量 按类型 = 
COUNTROWS(
    FILTER(
        CROSSJOIN(
            VALUES('客户'[客户姓名]),
            VALUES('客户分类表'[客户分类])
        ),
        [利润 客户细分]>0
    )
)
```

然后就可以随着分类标准的变化，动态即时统计出每个分类的指标：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPWQnxE4lQ1u1sAZMvlIwjyFibZNAz04yH41qVjtaUyFzbzG1FcZywZShc9E2gF4zVkib3Qb2adAYTA/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

以上就是自定义分组的思路，当你有类似的需求时可以尝试。
