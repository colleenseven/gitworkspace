---
create_date: 2023-01-09T00:04:47 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI公式中表达颜色的3种方式
source: https://mp.weixin.qq.com/s/OMiFdcb5V_nJCckK5aM_gg
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

在PowerBI中设置各种可视化元素的颜色时，可以直接根据颜色调色板来选择某个颜色。不过更灵活的方法，是通过DAX与条件格式结合起来，这样就可以动态地设置颜色了。

以下面这个柱形图为例：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOuiaKKng94tBP0vr9Kbac9fSLNrjEsziaj5MwPRqvFGHZePkbRXGsicBTwibo4BhL5mHA6KLwicMlJqiaw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在格式中可以直接设置颜色，也可以点击旁边的这个小按钮"fx"（如果没有这个图标，就是不支持条件格式），

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

可以在里面设置条件格式，其中最灵活的是格式样式中的“字段值”，

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

然后选择一个字段，可以是列字段，也可以是度量值，只要这个字段返回的是PowerBI支持的颜色代码就行。

最常用也是最灵活的方式是度量值，那么度量值如何返回颜色呢，或者说颜色如何用DAX来表达呢？

对于上面的柱形图，如果让季度销售额大于30万的柱子显示绿色、否则显示橙色，可以有下面三种方式。

**1\. 颜色名称**

直接用颜色的英文名称放到度量值里：  

> 配色 color名称 = 
> 
> IF(
> 
>     \[销售额\]>300000,
> 
>     **"green",**
> 
>     **"orange"**
> 
> )

然后利用这个度量值作为柱形图颜色的条件格式的字段值，效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOuiaKKng94tBP0vr9Kbac9fSGG2nNWHJq3Gd9oqq8un1xibSspIUdbAeyfmYsxoudGRCalIOuWAGCg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这种方式使DAX更易读，通过DAX中的颜色名称就知道是什么颜色，不过你要先记住一些颜色英文单词的写法（本文最后也会列出来这些常用的颜色名称）。

**2\. 颜色的16进制代码**

在DAX中，颜色还可以用16进制的代码表示，上面的度量值还可以这样写：  

> 配色 16进制 = 
> 
> IF(
> 
>     \[销售额\]>300000,
> 
>     **"#008000",**
> 
>     **"#FFA500"**
> 
> )

需要注意的是16进制代码前面要带上#，才能正确显示颜色。

效果与上图完全一样。

上面用的是6位数的16进制颜色代码，其实还可以加上2位，变成8位的颜色代码，**最后2位是用来控制透明度的，从00到FF，00表示完全透明，FF表示完全不透明**，如果要50%的透明度，16进制表示大约为80。

比如上图的柱形图中，销售额低于30万的颜色橙色设置为50%的透明度，度量值改成这样：  

> 配色 16进制 = 
> 
> IF(
> 
>     \[销售额\]>300000,
> 
>     "#008000",
> 
>     **"#FFA50080"**
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOuiaKKng94tBP0vr9Kbac9faGwxVL9wJFxgIsULicz46SMIcwmMLScia4hbYVEmofL0Vib68GJUnXRrw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果最后两位是00，就会完全不显示了，

> 配色 16进制 = 
> 
> IF(
> 
>     \[销售额\]>300000,
> 
>     "#008000",
> 
>     **"#FFA50000"**
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOuiaKKng94tBP0vr9Kbac9fcB6MyxJyBwJnVORIxNXBTMEocf2EwQ9Vw1q4pqiaBPMqPXDcqoE4d4g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

使用16进制的好处就是可以设置透明度，最常用的就是设置完全透明，**在6位16进制代码后面加上00，就是透明色。**

**3\. 颜色的rgb代码**

除了用16进制表示颜色，PowerBI还支持用rgb代码表示颜色，由红绿蓝三种颜色代码组合成不同的颜色，每个颜色取值分别为0-255，前面的度量值还可以改成这样：

> 配色 rgb = 
> 
> IF(
> 
>     \[销售额\]>300000,
> 
>     **"rgb( 0 , 128 , 0 )",**
> 
>     **"rgb( 255 , 165 , 0 )"**
> 
> )

并且这种方式也可以设置透明色，在rgb三个颜色的基础上，加上一个透明度参数，数值在0到1之间选择，0表示完全透明，1表示完全不透明，rgb的名字也变成rgba。

比如上面的柱形图，绿色改成35%不透明度，只要在rgba的第四个参数写成0.35就可以了：

> 配色 rgb = 
> 
> IF(
> 
>     \[销售额\]>300000,
> 
>     **"rgba( 0 , 128 , 0 , 0.35 )"**,
> 
>     "rgb(255,165,0)"
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOuiaKKng94tBP0vr9Kbac9fuJiadxOcSbya8bKAibHUbzIATUBgtvZSKrR1ZRX398DeSdsMgH1bczUw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

上面就是在DAX中表示颜色的几种方式，一般使用前两种方式就足够了，知道怎么在DAX中表示颜色，以及掌握16进制来设置透明色的做法。

以下是受支持的140种颜色的名称以及对应的16进制代码，你可以收藏起来，需要DAX配色时可直接查找使用：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOSoMP4DusOGaSZslnb182hCXwGv4lSN9ZsHXCXOfZLqXPm8yhsFWus6Y5Dec9fyy0juB4puOuZJA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
