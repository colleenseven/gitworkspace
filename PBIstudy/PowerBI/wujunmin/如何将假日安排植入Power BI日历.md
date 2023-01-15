---
create_date: 2022-12-10T00:11:35 (UTC +08:00)
tags: 
aliases: null
pagetitle: 如何将假日安排植入Power BI日历?
source: https://mp.weixin.qq.com/s/0zjYTboK_OmJ_GGmWVTXuQ
author: wujunmin
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

国务院办公厅于12月8日发布了2023年假日安排通知。一月适逢元旦、春节在同一个月份，因此这也是很多企业2023年生意最重要的月份。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6St9GLicicic6tdRBjuwpNHicljPwA1aibODCtrQEEIg8Ftr6oZkDdIiaZ7Ww1RZR5mRsDwNECAc2Fq3BRQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在Power BI可视化的过程中，植入假日信息非常必要。以下是矩阵展示假日信息的一种方式，放假与上班的信息置于右上角。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6St9GLicicic6tdRBjuwpNHicljYRGHeJic206GLxsm7Zy0s64XlQWTSSrWVn2SGYV9vwL0QkwIu1qOkjA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在默认的矩阵格式下，文本无法实现这样的排版，此处我们巧妙的借助了条件格式图标。以下是使用SVG图形包裹文本，自定义图标的度量值：  

```
SVG条件格式假日 = 
```

把日期表对应的周、星期、天按如下方式排列：  

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

对日字段设置条件格式图标：  

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

这个条件格式图标能够实现右上角显示的关键窍门在于，我们为图标设置了一个100\*100的画布空间，但是文字的纵坐标进行偏上方设置，下方绝大多数区域留白，造成了右上角的感觉。

这个技巧可以按需扩展使用，比如1月份涉及春节，农历的信息就非常必要，以下是2023年1月公历和农历同时展现的效果。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6St9GLicicic6tdRBjuwpNHicljURa6yPdWf7kDGlYfGDZ4gcbryDsba9vIYzaKGLtl0V79vPicJB8ywXw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图标度量值和假日一致，只是显示文本进行替换：  

```
SVG条件格式农历 = 
```

条件格式毕竟限制较多，纯SVG可以实现更复杂的矩阵显示效果，如下农历、节气、节日、放假安排同时体现：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6St9GLicicic6tdRBjuwpNHicljYE8FxIMibTjCROt1SAiaNzM3Gibl3EyzClG8sKiaSwvc7Enh1rFGwDQuqg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

信息容量如果觉得不够，下方可以加一个条形颜色提示每天指标是否达成：  

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

还不够？不妨再加上数据标签：

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

在嵌入SVG的图表度量值中，使用text控制文本的位置和格式，可以任意组合排列你的内容。本文配套pbix源文件在下方知识星球下载。文件除了包含以上效果的度量值，还包含22、23年的完整日期表（假日安排、农历、节气、星座信息均有），可以直接应用于你明年的业务规划。

直达链接（可左下角阅读原文）：_https://t.zsxq.com/08OkYQAPB_

___

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/JHQQIBqYy6SrFOpSISmqT2k74QM76UrbIBKw9vBMzBUmBfibKCas2iccpABJdicQ4UNYGL2QCMLGaesXVyJ601kvw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

[详情](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491267&idx=1&sn=9f8011a4c2a7f38f17b6ef4168625c63&chksm=97db2793a0acae853c07277e58d55c0b8db67e953b44228508b7282f4e907af330cf64efbf51&scene=21#wechat_redirect)
