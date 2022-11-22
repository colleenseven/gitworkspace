---
ZK: Origin
notes: True
aliases: null
create_date: 2022-03-22T11:57:45 (UTC +08:00)
tags: wx/pbi/建模技巧
pagetitle: Power BI如何动态计算任意粒度的上期数据？
source: https://mp.weixin.qq.com/s/jE4MQnIwcIIORez4B-LywA
author: 采悟
status: 已完成
category: 精读文章
uid: 
---

DAX:: MAX,IF,AND,CALCULATE,TREATAS,VALUES,CALCULATETABLE,SAMEPERIODLASTYEAR,ALL,SWITCH,SELECTEDVALUE,DATEADD

之前分享了通过切换不同的粒度类型，来动态显示最近的N个粒度期间的数据（[PowerBI动态显示最近N期的数据](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071066&idx=1&sn=aa4ba5e2ba385b92f9dfa45dbce06da8&chksm=8e0c404db97bc95b3b0032961da86ae534a6422a49e9dfce5f7d532541322b01e0faffa3e70a&scene=21#wechat_redirect)），在这个案例中，用了<mark style="background: #FF5582A6;">独立的日期表作为切片器</mark>，这个做法也可以进一步优化，<mark style="background: #FF5582A6;">改用建立关系的日期粒度表来作为切片器，以便与报表的其他图表交互</mark>。

原模型不变，这里将切片器中的字段都改为来自日期粒度表，并写一个度量值：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOibKhEUCFnuRTmgKUSgC7p2YsA1cJnrZJvllLmk3Zj5u2RLCSiawfBIIr7BO843bgp8u1nSxCjnHjw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

并用这个<mark style="background: #FF5582A6;">度量值作为柱形图的值，未建立的关系的独立日期粒度表作为坐标轴</mark>，同样可以实现[上篇文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071066&idx=1&sn=aa4ba5e2ba385b92f9dfa45dbce06da8&chksm=8e0c404db97bc95b3b0032961da86ae534a6422a49e9dfce5f7d532541322b01e0faffa3e70a&scene=21#wechat_redirect)的效果：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPYQ3rS0vDd1G0bpUcmx2Ob4KVUhJmKhofHgnWj5t803aLYwJVWNcnRJg3sMqHkSW9ebFqET4NpiaA/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

此外，最近被星友问到，对于这种动态的粒度，如何选择不同粒度类型，来正确计算出上年同期以及上期的数据呢？

对于上年同期的数据，相对比较简单，只需要这样写一个度量值就可以了：  

> 收入 上年同期 \=
> 
> CALCULATE(
> 
>     \[收入\],
> 
>     CALCULATETABLE(
> 
>         SAMEPERIODLASTYEAR('日期表'\[日期\]),
> 
>         TREATAS(VALUES('日期粒度表'\[日期\]),'日期表'\[日期\])
> 
>     ),
> 
>     ALL('日期粒度表')
> 
> )

这个度量值的逻辑是<mark style="background: #FF5582A6;">将当前日期粒度表所筛选的日期范围，视同日期表的日期范围，并利用时间智能函数返回该范围的上年同期的时间段</mark>；当然，<mark style="background: #FF5582A6;">为了避免日期粒度表同时筛选，用ALL来忽略掉它</mark>。

这样，无论选择任何粒度，都可以轻松计算出上年同期的数据。

计算当前粒度的上期，同样可以使用上面度量值的思路，但是稍微麻烦的一点是，对于<mark style="background: #FF5582A6;">不同的粒度，计算上期用到的时间智能函数是不同的</mark>，所以还需要先判断当前所选择的粒度类型。  

上期的度量值写法如下：

```
收入 上期 = 
SWITCH(
    SELECTEDVALUE('日期粒度表'[类型]),
    "年",[收入 上年同期],
    "季",CALCULATE([收入],CALCULATETABLE(DATEADD('日期表'[日期],-1,QUARTER),TREATAS(VALUES('日期粒度表'[日期]),'日期表'[日期])),ALL('日期粒度表')),
    "月",CALCULATE([收入],CALCULATETABLE(DATEADD('日期表'[日期],-1,MONTH),TREATAS(VALUES('日期粒度表'[日期]),'日期表'[日期])),ALL('日期粒度表')),
    "日",CALCULATE([收入],CALCULATETABLE(DATEADD('日期表'[日期],-1,DAY),TREATAS(VALUES('日期粒度表'[日期]),'日期表'[日期])),ALL('日期粒度表'))    
)
```

当粒度类型为年时，上期就是上年同期，所以直接用上面建的上年同期度量值，当为其他粒度类型，则通过DATEADD函数来相应的计算该粒度的上期的时间段。

用本期、上期以及上年同期这三个度量值做个柱形图，来看看动态效果：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJOibKhEUCFnuRTmgKUSgC7p2lkVVk2DMkeh1Kiadj2ia90OwLDMMU7d5UUbQhItebz4wnKRVVgNsIreA/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

有上期和上年同期的数据以后，再计算任何粒度的同比和环比也就可以很轻松的实现了。
