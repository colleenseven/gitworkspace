---
aliases: null
create_date: 2022-03-08T12:03:28 (UTC +08:00)
tags: 
pagetitle: Power BI报告中制作动态摘要，这个好用的方法推荐给你
source: https://mp.weixin.qq.com/s/oivdqD77JcPYcd1vI4Y1Lg
author: 采悟
status: 未阅读
category: 
uid: 
---

之前介绍了如何在PowerBI报告中制作一个动态的摘要，利用智能叙述的功能：

[利用Power BI智能叙述，生成动态报告摘要](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073801&idx=1&sn=3a6dcd73ed52e77a4159612fe49af3e7&chksm=8e0c5f9eb97bd68889ce7e6ae0af81e62b7ed6b7ea7827deb5ca1ba097c14e4965889736baa4&scene=21#wechat_redirect)  

这个做起来很简单，但是格式设置比较简陋，操作起来也不是太方便，此外，它也有许多限制，假如你的报告中用了计算组，那么这个功能就无法使用了。

今天介绍一个更灵活的方法，利用html content视觉对象来制作动态摘要。  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNP4NI90kWiak3r0ZZZrPLaQh9z2LYJU95kGACArl2Cv9BZMsE1EaXB1MxyNPLibosXVZMYMrmjRU3A/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

仍然以[前面的文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073801&idx=1&sn=3a6dcd73ed52e77a4159612fe49af3e7&chksm=8e0c5f9eb97bd68889ce7e6ae0af81e62b7ed6b7ea7827deb5ca1ba097c14e4965889736baa4&scene=21#wechat_redirect)为例来做一个摘要，基本内容如下：

___

_全年收入预算目标：xxx；截至到xxx日期，累计实现收入xxx；_

_假设未来期间的同比增长率xxx，预计全年实现收入xxx，与预算的差异是xxx_

___

其中"xxx"的位置是动态数据，可以替换为相应的度量值来代替。  

如果你会写html语言，可以直接**用html代码将上述文本**按照一定的格式**表达出来，生成一个文本度量值，然后将这个度量值放到html content就行了，这就是利用html content来呈现文本内容的基本原理。**

但是现实中，很多人并不会用html，我其实也不会，那我们如何实现上述需求呢？

虽然我们不会写html，但是有很多现成的工具可以帮助我们写，你可以搜索在线html编辑器，有很多种可以用，比如这个在线工具还可以，也比较简约：

https://wordhtml.com/

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNP4NI90kWiak3r0ZZZrPLaQ30iaMONx8GWbbrSl87kZ3MDrcibicOicjUhxoaHotibbic87lFLtxf6Zz7EQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

将上述文本复制到这个编辑框，然后用上面的格式化面板调整文本格式，界面和Word差不多：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNP4NI90kWiak3r0ZZZrPLaQHtDTibk1pVR1vA4r5EIjZHuUggMgH7W58WiaCZXNNyU9I3pGxTZlq7WQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

格式调整好以后，点击上方的HTML，就能看到这一串格式文本的HTML代码：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNP4NI90kWiak3r0ZZZrPLaQfYaqbnphPMIuNRlEuSWvlVEP6rgdsAPOTN1vTpGRamoVeKDWoMTbUA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

将这一串代码复制出来，直接建度量值，会看到很多错误提示：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNP4NI90kWiak3r0ZZZrPLaQsMxgtFQxFEpefBupibic15ibba5iaWR9gEq4orIqcohT9gx1iaaXftytlzg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

因为这一串代码是文本，我们需要用双引号""将它括起来，不过括起来之前，还需要做一个操作是，将这些代码中的 **"**，替换成 **""** ,因为 **"** 本身在html代码中特定的语法需要，两个引号之间并不是纯文本，所以再加个引号"作为转义符。  

替换的方法很简单，利用[DAX快捷键](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077119&idx=1&sn=9460a984173d3fd46896c2c263b89a1b&chksm=8e13a8e8b96421feb964c24c53a4fcc8198da9d83426cc46905af459ad927723821527af1ddd&scene=21#wechat_redirect) Ctrl+F2就可以很方便的一次替换：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNP4NI90kWiak3r0ZZZrPLaQk2MWtJQvn0BaOMaVpWTQomXR9iaWYQEW9ibR8Yrqn8QOuWE4f7hkpxsg/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

并在这一串代码的前后扩上引号，就不会再报错了。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNP4NI90kWiak3r0ZZZrPLaQN84WSI19FlbaoWwocU1hGCVtfLQCuL9qkLQhju7jEgdgCTbFwJC7pg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

然后将代码中的**XXX**替换为相应的度量值，不过前后要加上引号和连接符，变成：**"&\[度量值\]&"**

就是将之前的一个整的文本字符串：

**"完整字符串"** 

替换为 ：

"字符串前一部分"**&****\[度量值\]****&**"字符串后一部分"

将字符串分成前后两部分，中间放个度量值，他们之间再用连接符&连起来。

全部替换好以后，度量值如下：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNP4NI90kWiak3r0ZZZrPLaQcic6MJJiaQJCnG8IXjyE0LZWBS29tFSMUa1f6hFdAQjiaDPw3aDg9CMRQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

如果某个度量值需要显示为特定的格式，可以套个FORMAT函数来调整，这样就做好了摘要度量值，并不需要写html代码，只是简单的修改了一下而已。  

然后把这个度量值放到html Content中看看是什么效果：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNP4NI90kWiak3r0ZZZrPLaQPa9TYfQtInOSdk4yrulricJHf2DNkJkx8hicmib3AmRslB1FqLuXNorSw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

与之间在编辑器中设置的格式完全一致。

并且这里面的度量值都是可以动态变动的：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNP4NI90kWiak3r0ZZZrPLaQyC7hVosmO2CribRaKDYFu9VbyrnLsd7pqacZq93PtAoz9hHplNb3hsg/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

是不是和之前使用智能叙述的效果非常相似。

如果你不习惯或者由于各种原因不能用PowerBI的智能叙述功能，可以尝试用这种方法来生成动态摘要，当然html content的用法远不止于此，它可以做出各种很棒的可视化效果，比如之前分享的插入视频的方法也是用它实现的：

[如何在Power BI报告中插入视频？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078965&idx=1&sn=04e56b6c282a0d8ab4f9c179c71b80e2&chksm=8e13a3a2b9642ab4cc5822d7873b81176ea1b9702eeeda8820e8b0b0daccdb9a903088310be3&scene=21#wechat_redirect)  

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
