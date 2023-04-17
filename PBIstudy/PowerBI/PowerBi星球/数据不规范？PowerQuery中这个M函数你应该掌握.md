---
create_date: 2020-09-20T20:37:33 (UTC +08:00)
tags:
aliases:
pagetitle: 数据不规范？PowerQuery中这个M函数你应该掌握
source: https://mp.weixin.qq.com/s/kWY5xfUB0tRuqf8Q0mDcgQ
author: Davis
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

> **文/Davis**  
> 
> 全栈BI工程师，数据分析爱好者，微软MCSE，个人博客：d-bi.gitee.io

Table.AddFuzzyClusterColumn是Power Query的表函数之一，**它可以对数据进行模糊匹配并分组，从而规范数据源中的数据**，什么意思呢？  

一个简单的例子，比如地名“北京”，在数据源中它可能是“北京”，“北京市”，“Beijing”甚至“北平”，而该函数需要解决的，就是由数据录入不规范，数据本身的标准不统一等原因导致的这种数据杂乱的问题。

为解决此问题，多数情况下，简单替换的方法显然不切实际，而该M函数可以使其规范化，这在数据清洗中特别实用。

幸运的是，自PowerBI Desktop上次更新（2020年8月）以来，已增加了对该函数的支持，下文讲解其具体用法。

### **基本用法**

对于基本用法，我想引用文档中的举例的数据进行说明。首先我们有一个简单的表，里面包含英文城市温哥华和西雅图（如下），你可以留意到其中的单词大小写不一，且存在拼写错误（如seattl）:

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMY3QZqic3XRdk34BYQSOI0IQRvgHIYz0lia9O9jibMuBgSAFYibLwrz7Jfp97czCDJBUABGDiaSUPEKxg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

现在，我们回到Table.AddFuzzyClusterColumn函数，其用法如下：

```
Table.AddFuzzyClusterColumn（
```

    源表，  //【必要】

    目标列列名， //【必要】

    规整后的列名， //【必要】

    其他参数 //【可选】

```
）
```

因此，针对以上数据，添加步骤，编写M语句如下：

> ```
> = Table.AddFuzzyClusterColumn(
> ```
> 
>         #"Changed Type",
> 
>         "Location",
> 
>         "Location\_Cleaned"
> 
>     )

这样，我们就可以得到如下结果，数据得到完美规范：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMY3QZqic3XRdk34BYQSOI0IxRtZ1yk629cUibFa4aZcH8sPTwibicCShkJpajb3HvKfxPRJMKsB5h3LQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

是不是很厉害！

上面只是基本的用法，利用该函数的可选参数，还有更强大的功能。

### **进阶用法**

在进阶用法中，会在基本用法的基础上讲解参数的原理和使用方法，此外，处理的数据也改为文档中未涉及的中文文本。

首先利用以下M语句模拟一个火车站站名不规范的简易数据表：

\--------  

```
let
```

```
 DATA =
```

```
  Table.FromRecords(
```

```
    {
```

```
      [ID = 1, Location = "北京西站"],
```

```
      [ID = 2, Location = "北京西站"],
```

```
      [ID = 3, Location = "广州东站"],
```

```
      [ID = 4, Location = "广州东站"],
```

```
      [ID = 5, Location = "广州东火车站"],
```

```
      [ID = 6, Location = "西九龙站"],
```

```
       [ID = 7, Location = "西九龙站"],
```

```
      [ID = 8, Location = "西九龙火车站"],
```

```
      [ID = 9, Location = "香港西九龙站"],
```

```
      [ID = 10, Location = "HK West Kowloon Railway Station"]
```

```
     },
```

```
     type table [ID = nullable number, Location = nullable text]
```

```
    ) 
```

```
in
```

```
 DATA--------
```

数据如下，当然你也可以手动先做好这个数据：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMY3QZqic3XRdk34BYQSOI0IiaNBkibEoicM4JSuzdyiavOO6rGP89ic0QLf1rQHZJ8gLiclRFOoYVibH39yA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

按上文使用Table.AddFuzzyClusterColumn的方式，此处使用第一个可选参数**【Culture】**。

文档对该参数的定义是**“****允许根据区域性特定规则对记录进行分组****”**，其实就是该函数默认处理对象是英文字符，如果是其他语言，就应该使用Culture指明要处理的语言。

于是编写M代码如下：

> ```
> = Table.AddFuzzyClusterColumn(
> ```
> 
> ```
>   DATA,//源表名    "Location",    "Location_Cleaned",    [Culture="cn-ZH"]
> ```
> 
> ```
>  )
> ```

这样我们得到如下效果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMY3QZqic3XRdk34BYQSOI0II8GGFlv5icsGEaibaItEibWWxSgpkDsPEo7LB4Yt3oRv9faibb1RNCTHRw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

现在北京西站这个名称得到了规范，空格问题得到处理。

但如何处理“广州东站zhan”这种混杂了拼音的记录呢？答案是使用强大的【**Threshold】**参数。

Threshold参数的范围为0到1.0，默认值是0.8，数值为1代表原数据不做任何处理，其越低代表其在纠正数据时，对数据本身的容错率越高。

此处将该参数设定为0.6后就解决了此问题。

注：此处你还可以增加IgnoreSpace= true参数显式地忽略空格。

```
= Table.AddFuzzyClusterColumn(    DATA,    "Location",    "Location_Cleaned",    [        Culture="cn-ZH",       Threshold=0.6      ]    )
```

效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMY3QZqic3XRdk34BYQSOI0Ir70zRAtTsdn79IZHnDWLxgR4lZhamp3WKUeYpVzAgksxP4icC0icjOrw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

到此我们发现以上方法，还未能解决表中第六行至第十行的命名杂乱问题，PQ没有足够的依据去智能地给他们归类，因为PQ并不清楚西九龙是香港的一个地名，当然更不可能了解"HKWest Kowloon Railway Station"的含义。

为解决此问题，该函数引入了**【TransformationTable】**参数，这将允许我们自定义一个转换表，以使得PQ可以按照转换表的定义来规范数据，从而彻底解决此类问题。

首先，定义转换表TRANS\_TABLE：

> ```
> = Table.FromRecords(
> ```
> 
>   {
> 
>      \[From = "西九龙站", To = "香港西九龙站"\],
> 
>      \[From = "西九龙火车站", To = "香港西九龙站"\],
> 
>      \[From = "HK West Kowloon Railway Station", To = "香港西九龙站"\]
> 
>   },
> 
>      type table \[From = nullable text, To = nullable text\]
> 
>     )
> 
> ```
> 
> ```

转换表如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMY3QZqic3XRdk34BYQSOI0IhYibzasBQb6Nl2gHFpRv2mn5Sj2lOmjhXuz2J7bxSPp6Lbeib4xjbtEg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后参数中引用该表：

> \= Table.AddFuzzyClusterColumn(
> 
>         DATA,
> 
>         "Location",
> 
>         "Location\_Cleaned",
> 
>         \[   
> 
>             Culture="cn-ZH",
> 
>             Threshold=0.6,
> 
>             **TransformationTable=TRANS\_TABLE**
> 
>         \]
> 
>     )

这样我们就完美地解决了问题。效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMY3QZqic3XRdk34BYQSOI0I4Jsl16hjUw4ibXKbbtcMN0IWdnIv3Uic09jcSYII6w2AOM1gWWsQibmXQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

### **总结**

Table.AddFuzzyClusterColumn函数在数据源不规范时十分有用，掌握它的用法就可以轻松处理这类问题，**但对于企业BI解决方案而言，通过ETL等方式从源头上解决数据杂乱的问题才是最规范的做法。**

我的更多文章：

[关于PBI Report Server 部署与配置，推荐你看看这篇文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070310&idx=1&sn=b5ccf51bdbf31b5bff04df0859d4660a&chksm=8e0c4d71b97bc4677a776199421b33a73b76ecafb39816c97e9cb828e12d4d4bff2927507ea4&scene=21#wechat_redirect)  

[当Power BI遇上数学：用DAX解决数据的循环迭代](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484069298&idx=1&sn=8e376e5934a12dd16d0d46ae9b55ebdf&chksm=8e0c4965b97bc073b9710535a51c64f7db42b69b45282e59d994f5770abc33d098cf2ccf1a88&scene=21#wechat_redirect)  

[Power BI实践:利用DAX解决库存余额计算问题](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071321&idx=1&sn=8354d34c6b1e8bdfc885f3b49d39060e&chksm=8e0c414eb97bc85876ce1f425202f7411e4d2ce9b041b81b7ad64c9b2719b487ac8afc2a6030&scene=21#wechat_redirect)

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和2.4k+ 学习者一起成长
