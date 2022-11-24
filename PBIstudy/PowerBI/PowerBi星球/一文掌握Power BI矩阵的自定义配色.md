---
ZK: Origin
create_date: 2021-12-10T12:50:52 (UTC +08:00)
tags: 
aliases: null
pagetitle: 一文掌握Power BI矩阵的自定义配色
source: https://mp.weixin.qq.com/s/iiLQqkMbZTR7SokrFpayTg
author: 采悟
status: 未阅读
category: 
notes: False
uid: 
---

上篇文章（[一文掌握Power BI矩阵总计的自定义计算](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078406&idx=1&sn=3f64d35e34d0f9cd0d5483ee46bf124a&chksm=8e13ad91b9642487e4c2e64af7c944c76ef506eab1a9ecb731173a3cbfbf57b46da9c2cd855e&scene=21#wechat_redirect)）介绍了如何利用DAX进行总计行的自定义计算，其实这种方式不仅仅用于返回特定的数据，还可以自定义每个数据的背景色或者字体色。

比如这个矩阵，如果将经特殊调整的U盘和总计数据背景换个颜色：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOSoMP4DusOGaSZslnb182hLsnNChpaLDUXfQny6R01EfvR1uKA6ECnUaibU7J4YOibDtz6lFuLBmmw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

就可以写个度量值，如下：

这个度量值同样是利用SWITCH和ISINSCOPE来判断上下文，来返回不同的颜色。  

然后点开这个矩阵的格式面板，找到“单元格元素”(之前的版本是条件格式),选择某个度量值，然后打开背景色并点击fx按钮：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOSoMP4DusOGaSZslnb182hrxhvTYHaPTauStPB3gTZbTOV15HFzB5ViaXOmw8zRWblCoD0BZ4eXdw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在弹出的窗口中，设置格式样式为“字段值”，选择前面建好的配色度量值，并应用于“值和总计”：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOSoMP4DusOGaSZslnb182hLnHUKYE5lUL6eMgiadIMGjNzXWdRszIiadon1icNxRoLa5xUZ2FfiahJIg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

矩阵中这一列的颜色就会变成下面这样的效果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOSoMP4DusOGaSZslnb182hxBYTIW2gtCLBGQh8MnmGpgZGDCVCKcib5SibxbmvRbWNDHpe5bdaoJaQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里设置的是背景颜色，字体颜色也可以同样的方式设置，并且这种配色方式，不仅是静态的配色，也可以根据数据的逻辑来进行动态的配色。

上面是一个层级的效果，如果有多个层级，也可以利用这种方式，为不同层级的数据设置不同的颜色。  

比如下面这个度量值，定义了每个层级显示的颜色：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOSoMP4DusOGaSZslnb182hoYJaFic6adbU4VTf8eZgjRNHmicpldeMx6fGgylJD6odBplyUoc0CZFw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

按照上面介绍的设置方法，将这个配色度量值作为背景色效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOSoMP4DusOGaSZslnb182hyaF5fLovXaBfoLaphqlO2HKcmeFbOic5D72ibmepCk276a4qicwHpKPSA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这就是利用DAX，实现矩阵每个单元格元素自定义配色的效果。

另外，通过上面的度量值应该也看到了，PowerBI不仅支持16进制代码来表示颜色，其实还能直接使用这些颜色的英文名称，这样DAX更具有可读性了。

以下是受支持的140种颜色名称以及对应的颜色，你可以收藏起来，需要DAX配色时可直接查找使用：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOSoMP4DusOGaSZslnb182hCXwGv4lSN9ZsHXCXOfZLqXPm8yhsFWus6Y5Dec9fyy0juB4puOuZJA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
