---
create_date: 2022-05-25T11:41:33 (UTC +08:00)
tags: 
pagetitle: Power BI字段参数介绍以及常见应用场景
source: https://mp.weixin.qq.com/s/RocGEfGtWxmi3gLE12-ZvA
author: 采悟
status: 未阅读
category: 
uid: 
---

前面关于[5月更新](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484080166&idx=1&sn=d695a7775e0def6f997b394643e004e8&chksm=8e13a4f1b9642de7ff102538ba9654e13732352c0823781da7f19289b13b32f026fc6439dab0&scene=21#wechat_redirect)的文章，简单介绍了字段参数的用法，因为这个新的功能非常强大，也非常实用，这里再详细介绍一下它的用法，以及几个常见的应用场景。  

**什么是字段参数**

简单来说就是用字段（包括列字段和度量值）组成的动态变量，而列字段和度量值是制作可视化的维度和数据，通过切换字段参数，就可以动态的更改可视化图表中正在分析的维度/指标，因此利用字段参数可以便捷的实现动态可视化分析。

**如何启用“字段参数”**

首先将PowerBI Desktop更新到现在最新的版本，也就是2022年5月的版本，该功能目前是预览状态，首先到文件>选项>预览功能中，勾选“字段参数”。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0m1jPFZm0XQR9Wia691ibMjj40hCAicmdib6GS59WR0OlgvpKAJAoJohzQNsOplXZnKk4FFj6J8qlvg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后就可以在建模选项卡里面的新建参数中，看到一个新的选项：字段。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0m1jPFZm0XQR9Wia691ibMjyPxQBZlHOA1snIxW2AUFgOhnAia1lvZuOfgKJGYDBLg7X0QBLAoOrYQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

注：目前该功能是预览，所以需要先启用，也许之后很快就会变成普遍可用，到那时就不需要启用这个步骤了，直接使用即可。

**如何创建字段参数**

点击新建参数>字段，在弹出的窗口中，右侧是模型中的全部字段以供你选择：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0m1jPFZm0XQR9Wia691ibMjXvic8ZeHcY6seicFvxxkEobRiaWRgIydoKiaasFFz74oPDeJrQxPgTsH8A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击需要的字段，可以是列字段，也可以是度量值，或者二者混合，然后它会自动添加到此左侧的字段框中，对于已选择的字段，可以拖动更改字段的顺序，也可以双击所选字段来更改显示的名称。

创建参数之后，模型中会多一个参数表，页面上也会自动出现一个切片器。

**如何修改字段参数**

字段参数建好以后，目前不能再次进入创建该字段参数的窗口进入修改，不过我们可以在“数据视图”中，找到字段参数的对应的表。  

先来认识一下这个参数表，以上面创建的字段参数为例：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPlflEbSrmA3QTUztON95cmMXy9nt3HucnSxd2eW64nt34Z2icHPdCGaC5vRRKavyRIrBDwZT2f3qw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

参数表有三列，第一列是参数名称，也就是在切片器中显示的名称，第二列是字段来源，第三列是自动生成的序号。

其中后两列自动隐藏，所以标题呈灰色，由于是机器翻译的原因，这两列的默认名称非常生硬，可以双击修改，比如改成字段来源和排序，更容易理解。

点击参数列，就会发现，它已经自动对这一列进行了按列排序，排序的依据就是最后的排序列。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPlflEbSrmA3QTUztON95cmhSVC2Zjl58hfYdAeRkbmzCWQg8f4c2icZkwIRgomCiaZc2cWxqX3KW4w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果需要修改字段参数，直接修改这个DAX表达式即可，可以修改现有的行，也可以增加行、删除行。

其中这里用到了一个新的DAX函数：**NAMEOF，**它可以返回字段的名称，如果之后字段名称发生变动，这里也会自动更新。

使用参数制作图表，比如利用上面生成的参数，参数作为坐标轴时，直观上感觉坐标轴应该只有两个类别，因为这个表就只有两行，但实际上它却可以显示参数所在源字段的所有值。

比如动态坐标轴，通过参数切片器的切换，动态显示不同的值：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJP0m1jPFZm0XQR9Wia691ibMjZib5Vusxm1RBVU1Pcxh1uyKPWdtdeBRDMVpkTBL03XfStkBtSPL1Xsw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

这个参数表只有两列，为什么它能显示该参数所代表的值呢？

这就是字段参数的强大之处，表面上看起来字段参数是个简单的只有三列的表，其实内部封装了非常丰富的逻辑。

并且可以右键X轴中的参数，来切换字段参数是显示它本身，还是显示它所代表的值。

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPlflEbSrmA3QTUztON95cmhOWQHDlsx7eLWhyiaMg5VDqRIUbvgqIJZjdQvh9Ro0bccz5wOE88M0g/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

参数的基本用法就是这些，下面根据字段参数所选取字段类型的不同，来看看它的几种常见应用场景。  

**字段参数的几个常用场景**

**1、列字段组成的字段参数**

列字段一般作为可视化图表的坐标轴，因此全部用列字段生成的字段参数，常用于动态坐标轴的设计，前面的文章已经介绍：[Power BI 2022年5月更新，你应该知道的几个变化](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484080166&idx=1&sn=d695a7775e0def6f997b394643e004e8&chksm=8e13a4f1b9642de7ff102538ba9654e13732352c0823781da7f19289b13b32f026fc6439dab0&scene=21#wechat_redirect)  

之前关于[动态坐标轴设计](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068004&idx=1&sn=750fce682b8e15757b038d30aa5a540f&chksm=8e0c7473b97bfd65f68616c2ced6fe5a139e11ccd70b933f92bde1278ff02abedbbe377a3f71&scene=21#wechat_redirect)的方法可以弃用，改成用字段参数来设计。  

用列字段作为参数另一个常见的应用是矩阵的动态层级，如果将上面建的参数放到矩阵的行标题中，就可以得到如下的动态效果：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJM84Vdent275TDEEiaF53BFibVxFYeKeY1Yjqiaq9oaPc4HQtQrvtVwiclnrIzIkZNI9BQic1QnbXC3EYA/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

当参数切片器不选或者选择超过一个时，矩阵就会出现层级结构，并且先选择的字段在第一层级，这样就得到了动态层级的效果。  

**2、度量值组成的字段参数**

度量值一般作为可视化图表的数据来源，因此全部用度量值生成的字段参数，就可以动态的切换图表中的数据，常用的应用场景就是动态指标分析。

以之前介绍的[动态指标分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074205&idx=1&sn=d8c9d1a3f80245e6e3b1f5bd2d14a053&chksm=8e0c5c0ab97bd51c1cdcc44737ff0967f5179b716c5f0bc90c87abcd977153b10cd11cdc3219&scene=21#wechat_redirect)为例，新建字段参数，将收入、利润和利润率，这三个度量值添加进来，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPlflEbSrmA3QTUztON95cm1QLrp9xJ3jYG5F2TC5AKPIdFZRC7VeRRnLsKG37543mmnbWIJjHs2Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击确定，就建好了一个用3个度量值组成的字段参数，页面上会自动出现一个切片器，然后将年度季度作为X轴，参数作为Y轴制作一个面积图。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPlflEbSrmA3QTUztON95cmDry3WfF7CXCalXmiabHibme4Es9zYr18eX8QUjvp3UgkF86ExNMEOJXw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

利用自动生成的参数有切片器，切换效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPlflEbSrmA3QTUztON95cm6kjsg3TicOB0jDXxHFJRs8XhAV3iat9YUlMKtFzib2rrudxLY6EhibFXWQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

这样就实现了，通过点击切片器，就可以动态切换数据指标了。并且这种方式不仅只是动态切换指标的值，原度量值的数据格式也会继承过来。

通过这种方式，之前介绍的这两种动态技巧都可以用字段参数的方法，直接替换掉：

[动态指标分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067957&idx=1&sn=93e3f3b54fd902e26ce98f8c4112abbb&chksm=8e0c74a2b97bfdb405f86c58998f8320ea8c26853b039edfd2c7f6d8cef0d97d28dacfe9d23f&scene=21#wechat_redirect)  

[动态数据格式](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074205&idx=1&sn=d8c9d1a3f80245e6e3b1f5bd2d14a053&chksm=8e0c5c0ab97bd51c1cdcc44737ff0967f5179b716c5f0bc90c87abcd977153b10cd11cdc3219&scene=21#wechat_redirect)  

**3、列字段和度量值混合组成的字段参数**

这种字段参数一个日常应用场景就是表格的横向动态扩展。

新建一个参数如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM84Vdent275TDEEiaF53BFibDKMQiastODGmPWoFxOOAAE1co2DDiaibJMlx7zRb6dv7lcicgEsuHv50IA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个参数包含列字段和度量值，用它来制作一个表格，就可以得到下面的效果。

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJM84Vdent275TDEEiaF53BFibicxEf8k6YnZMpgWPNTXJY8vhrSZUppqe7icsP7LKB6KPf9q1DPliaRKVg/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

其实还可以将之间建的两个参数（列字段组成的参数和度量值组成的参数），一起放到表格中，然后用两个切片器进行控制，同样可以得到这个效果。

既然创建字段参数可以选择模型的任何字段，那么在此之前已经建的字段参数也可以被选择，这样就可以进行参数的嵌套，甚至是多层参数嵌套，这个思路打开以后，还可以继续摸索字段参数的更多用法。  

通过以上的介绍，你应该明白了什么是字段参数以及基本的用法，这个功能用起来非常简单，可以无代码、更快捷的完成多种动态可视化分析，我之后也会分享字段参数的更多应用场景。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4500+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1AEySOiakLF2kY7eb1kUw2DtfKoVz2ctBDia5dtNsPX2GhV0ZOCDDWpgpaTQtnqfqJrRXt5PNia95g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
