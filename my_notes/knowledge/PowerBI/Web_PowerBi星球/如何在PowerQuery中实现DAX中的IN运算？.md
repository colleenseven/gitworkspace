---
create_date: 2022-08-08T12:24:55 (UTC +08:00)
tags: wx/pbi/数据处理功能
pagetitle: 如何在PowerQuery中实现DAX中的IN运算？
source: https://mp.weixin.qq.com/s/WfzOTiH-A13vxHEgr-C4mg
author: 采悟
status: 已完成
category: 精读文章
uid: 
---

在DAX中有个IN运算符非常好用，之前介绍过它的用法，参考

[一文掌握Power BI中的IN运算符](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484079655&idx=1&sn=f728e8384c40def6a13f688c1ede6113&chksm=8e13a6f0b9642fe6d3747ef94ab003c8e816ea94738df85a73b38d9a77892e11ea256441ae50&scene=21#wechat_redirect)  

有很多人问如何在PowerQuery中使用IN，其实<mark style="background: #FF5582A6;">PowerQuery中并没有这个运算符</mark>，不过也有相应的函数可以实现类似的功能。  

本文以筛选下面这个表格为例来介绍一下在PowerQuery中是如何实现的。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMc82VTFw8um1CK1KxM4ibEVJbgB4KfRDhVwazwKI5rlPcSpFyPPjsQ1T1DSDkQwedibsR2vibBDtBRg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如需要筛选客户名称是"吴雷"、"孙静"、"林永"的数据，最简便的做法，可以直接使用筛选功能。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMc82VTFw8um1CK1KxM4ibEV5eY4iaAwLqExG98meBAsVSpCGcpk3u0dzzp5Zg3W9fQAqDbgXIk1U8w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

但是当需要筛选的数据比较多时，这样手动一个个勾选也不方便，那么还可以利用M函数实现。

需要插入一个步骤（右键最后一个步骤，点击“插入步骤后”）：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMc82VTFw8um1CK1KxM4ibEVJHdibvLaAIeBPdrYIibhoemuHmibj4VmDTNuDVURG9b1G9MhoLpsia285A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后在上面编辑栏输入：

> \= Table.SelectRows(
> 
>     更改的类型, 
> 
>     each **List.Contains({"吴雷","孙静","林永"},\[客户\])**
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMc82VTFw8um1CK1KxM4ibEVFKGsvoCTEtdo9yn1mahkIiaIic9Iicdd3jZPC4Fn9fnSvHbvFo7xJjIqA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就可以不再手动勾选，而是利用M实现筛选，其中用到的<mark style="background: #FF5582A6;">M函数是List.Contains，用来判断某个值（第2个参数）是否在列表中（第1个参数），如果在，返回true，然后通过 Table.SelectRows来返回对应的行</mark>。

上面的做法虽然可以实现，但是如果筛选的名称很多，都这样一个个列出来组成列表依然不够灵活。

对于这种情况，更常见的是有个筛选的条件表，把这个条件表导入进来：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMc82VTFw8um1CK1KxM4ibEVNRP2Yg4AgrecT7AN3O8EjKCEMbRzu1nvRo6ka357lW5GQ6fcXMbo2g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

对于这个表，先将它变成一个list列表，右键该列，点击“深化”：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMc82VTFw8um1CK1KxM4ibEV95AjZoibRTX3e90DNhGGK2XIp3FvrI6PKPRFlR5SKzGKBHRodRg31kA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后就变成了下面这样的列表（list），这个列表的名称命名为“条件表”，  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMc82VTFw8um1CK1KxM4ibEVZQSWkd4TLp1tK9F9ScWPHvpRibbeYhe5bCQI5NItbT3c5beTS5CJKrg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

有了这个条件表，可以直接更改上面的M函数：

> \= Table.SelectRows(
> 
>     更改的类型, 
> 
>     each **List.Contains(条件表,\[客户\])**
> 
> )

同样可以实现筛选的需求。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMc82VTFw8um1CK1KxM4ibEVOdS9H54u4vXiaZrwW9kRAmf89W9lsM7aZ8bhawK4Hp2Xs49My8shuxw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

之后如果筛选范围有改动，只需要更改条件表就可以了。  

以上List.Contains的做法，是不是和IN类似呢？

如果是用<mark style="background: #FF5582A6;">DAX来实现上述需求</mark>，可以直接这样来做，新建表：

> 表 = FILTER('示例表',**'示例表'\[客户\] IN '条件表'**)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMc82VTFw8um1CK1KxM4ibEVtey1O9tWBHZibA7ZRw0QOROgfMh1nFuNBYrUhDsUssmYKRInicbx47ibQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

