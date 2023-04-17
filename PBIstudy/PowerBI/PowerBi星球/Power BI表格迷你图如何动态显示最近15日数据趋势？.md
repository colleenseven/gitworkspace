---
create_date: 2023-03-07T23:29:35 (UTC +08:00)
tags: wx/pbi/DAX函数 
aliases: null
pagetitle: Power BI表格迷你图如何动态显示最近15日数据趋势？
source: https://mp.weixin.qq.com/s/6gZb0wzJGyy6RtJZ4tDP6A
author: 采悟
status: 已完成 
category: 精读文章
notes: False
ZK: Origin
uid: 
---

DAX :: SELECTEDVALUE , AND, IF, CALCULATE ,TREATAS 

PowerBI中的表格/矩阵中从2021年底就开始支持迷你图了，它的基本用法请参考：  

[PowerBI 2021年12月更新，你应该知道的几个变化](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078544&idx=1&sn=4bbafb99f595a3e0785f394a7de5af0b&chksm=8e13ad07b9642411cd6c08f281ece6f6c6120a9ab6b2cef62ff0bd4fa1363a57bf81be3da342&scene=21#wechat_redirect)  

最近有星友在使用时，将日期作为迷你图的X轴时遇到了以下问题：  

**一、数据显示不全；**  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNRWEWn0tNVhxOaEL5OXrJ3YmdyxYSALibbYujuQs4ZgLHdsk8buppd9FTydaCquLo3icvj7rzr1NkA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这是因为==迷你图的X轴最多显示52个数据点==，超出无法显示，并在右上角出现感叹号提示。  

**二、外部日期切片器点击某个日期后，迷你图变成一个点**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNRWEWn0tNVhxOaEL5OXrJ32SpuOIibqt2Qp1zw9n6wYVQugxUQDTEETf0UicyRibuc3LUyCdRXSroxQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这是因为迷你图同样会受上下文的影响，选择某一日，迷你图也会只显示当日的数据，所以变成一个点。  

如果使用[编辑交互](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067514&idx=1&sn=3260286c5da96b96775fb73b72709d1f&chksm=8e0c766db97bff7b23897a1a3e08917a6e486ffea87124be22ba686e31bfabe55372a7488ce1&scene=21#wechat_redirect)，断开表格和切片器的筛选关系，那么表格中其他列的数据（比如上图第二列销售额）也没法显示与日期交互的结果了。

对于上面两个问题，第一个是PowerBI的限制，不能绕开，毕竟迷你图很小，显示太多数据点本来也不合适，减少数据点是必要的。  

第二个问题，可以通过DAX来解决。

如果将迷你图的展示需求改成，==只展示某个选定日期的最近15日的销售趋势，这样不仅不会超出迷你图的限制，也不会将迷你图变成一个点。==这个需求可以通过下面的步骤来实现。

**1\. 建一个独立的日期表.**

该表不要与模型中的其他表建立关系。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOKBEQ5iapShHdnIF2hKZBMPfu4UNuxdoCIo4Gcfo4kTFM4DQ0ToTVZiblevscA7q6mEN61YRDWouXQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**2\. 建度量值**

```
最近15日 销售额 = 
VAR T=15 
VAR slicerdate=SELECTEDVALUE('日期表'[日期])
RETURN 
IF(
    AND(
        SELECTEDVALUE('独立日期表'[日期])<=slicerdate,
        SELECTEDVALUE('独立日期表'[日期])>slicerdate-T
    ),
    CALCULATE([销售额],TREATAS('独立日期表','日期表'[日期]))
)
```

**3\. 生成迷你图**

在表格中，编辑迷你图，==利用独立日期表的日期作为x轴，度量值\[最近15日 销售额\]作为Y轴==。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNRWEWn0tNVhxOaEL5OXrJ3kxMu4RbniakqEbQclnX78zgUyrFcTyuCxOfrvpyCEibdDUMCxSHTtA8A/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

然后就可以实现迷你图来显示最近15日的效果。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNRWEWn0tNVhxOaEL5OXrJ3fS9IIZJ7ibvAcQbicZxBOYBGkc2vWMsC7wDGatt8P1fBNpocmK3yQibKw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

在这个例子中，你还可以将15换成动态的参数，就是动态展示最近N天的效果，，做法和之前介绍的普通图表显示最近N天完全一样：

[Power BI动态显示最近N天的数据-优化](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484075973&idx=1&sn=bf5b8a1b66b86a933544a2f9580d30c8&chksm=8e0c5712b97bde0422efa22f48fc490a14e1692d17047b16a95dbdd161fc765f3befa77c68fb&scene=21#wechat_redirect)  

不过N是不能大于最高限制52的。  

其实表格中的迷你图和普通的折线图/柱形图的可视化逻辑是一样的，只是X轴被隐藏起来了而已，理解了这个原理，平时用在折线图的一些技巧，在迷你图中也可以尝试。
