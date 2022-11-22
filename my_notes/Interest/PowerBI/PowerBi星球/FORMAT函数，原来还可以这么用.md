---
ZK: Origin
create_date: 2022-05-09T12:15:08 (UTC +08:00)
tags: wx/pbi/DAX函数
aliases: null
pagetitle: FORMAT函数，原来还可以这么用
source: https://mp.weixin.qq.com/s/XLSEpOIwS9hlqmmrGxi9DA
author: 采悟
status: 已完成
category: 精读文章
notes: True
uid: 
---

DAX:: FORMAT

---

本文开始之前，先来看一个很常见的小需求，<mark style="background: #FF5582A6;">在PowerBI中如何像Excel一样，将负数显示为外面套一个括号的样式</mark>呢？  

以下面这个数据为例，显示的是每个产品的同比增长率：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMwPYBMI3JxYJSaOWmHiaKHfOZAfpz1Gpkn6SjuMx3EbYF943ulhTBVyicJDAr5EdbQNtZTQtvhu5rg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如何让最下面三个负增长的数据，不用负号，而是用括号的方法来表示呢？，DAX可能有多种方法都可以实现，这里介绍一个FORMAT的妙用，建立度量值：

```
同比1 = FORMAT([同比], " 0% ; (0%) ")
```

结果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMwPYBMI3JxYJSaOWmHiaKHfTnoveeNSp7NoQVicF508Ut9WLdFOjMW3l9C5mhy1kAxWwqmoChjciasg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

是不是非常简单。

之前曾经介绍过FORMAT函数的用法([利用FORMAT函数自定义数据格式](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067980&idx=1&sn=4c314be995c216a5a6e6f7a49886cc2f&chksm=8e0c745bb97bfd4d1092fadd56e335ccb0d27f38cffeca7d234fef18eaae81da052c7c69900e&scene=21#wechat_redirect)),不过在这篇文章中，只是介绍了利用FORMAT的普通用法，其实利用第2个参数，还可以更加灵活地设置数值的格式。

FORMAT的<mark style="background: #FF5582A6;">第2个参数是格式表达式，它可以用分号，分隔为1个部分、2个部分和3个部分</mark>：

-   **1个部分**：<mark style="background: #FF5582A6;">格式表达式应用于所有值</mark>  
    
-   **2个部分**：<mark style="background: #FF5582A6;">第一部分用于正数和0的格式、第二部分用于负数的格式</mark>  
    
-   **3个部分**：<mark style="background: #FF5582A6;">第一部分用于正数、第二部分用于负数、第三部分用于0</mark>
    

之前文章的介绍都是只有1个部分，也就是格式表达式应用于所有值。

文本开头写的度量值：FORMAT(\[同比\], "0%;(0%)")，就是用一个分号将参数表达式分割为2个部分的用法：

第一个部分 0%，意思是将正数和0表示为正常的百分比格式；

**第二个部分****（0%）****，****表示将负数显示为带括号的百分比格式**。

理解了这个用法以后，就可以运用FORMAT函数更加灵活地设置数据格式了，下面来看几种常见的场景。

**<mark style="background: #FF5582A6;">正数前面显示“+”</mark>**

```
同比2 = FORMAT([同比]," +0% ; -0% ; 0% ")
```

这里第2参数分割为三个部分，分别设置正数、负数、0的格式：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMwPYBMI3JxYJSaOWmHiaKHfdEqw1ZM4c2eRTVAibh6Cj8Fm5wHNfWu2Hfa0E6wpdVNq6z3uA3UvuicA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**<mark style="background: #FF5582A6;">带上下箭头的正负数</mark>**

```
同比3 = FORMAT([同比],"0%↑ ; -0%↓ ; - ")
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMwPYBMI3JxYJSaOWmHiaKHf97JOu23v7sRJfAWyuJRYLAIdySdSv83V3RNUITjmpJHvenc5L1bibicg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**<mark style="background: #FF5582A6;">根据正负返回增长/下降字符</mark>**

```
同比4 = FORMAT([同比]," 增长 ; 下降 ; - ")
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMwPYBMI3JxYJSaOWmHiaKHf9y99PYT6ExcIl0bVtmBLWDe5yicrLPrmuI0hTAHy8ZaRCCfvbicf6P6w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**<mark style="background: #FF5582A6;">正负数配色</mark>**

如果让负数显示为红色括号的数据，可以用FORMAT这样写度量值，第二部分返回“red”：

```
配色 = FORMAT([同比]," ; r\e\d ")
```

然后将这个度量值用于前面同比1度量值的字体颜色，效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMwPYBMI3JxYJSaOWmHiaKHf8NwT6rMzMhiccuRWbP5L48qCpxMpb3DnaHhXgdNHlARtVRoCXS2yalg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

因为有很多字母在FORMAT的参数表达式中有特定的含义，所以用了反斜杠“\\”，让某些字母显示为它本身，而不表示特定的含义。  

由于这个原因，<mark style="background: #FF5582A6;">正负数配色度量值不建议使用FORMAT，直接用IF判断的方式来写配色度量值更简单</mark>，这里只是为了说明FORMAT的这个用法。

___

显示数据格式，还可以在格式窗口中直接设置，比如正数前面显示“+”，在格式窗口中输入这些字符也可以实现：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMwPYBMI3JxYJSaOWmHiaKHfDGibzic6icCCM8MoNlx4PqBAqKiaibjcaRJDhKOmJvkKqK184JYgdLMBhAA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

不过这里的设置只适合直接显示，用FORMAT函数的方式不仅能直接显示特定的格式，还可以嵌套在DAX中使用，使用场景更加丰富，建议灵活掌握FORMAT的这些用法。
