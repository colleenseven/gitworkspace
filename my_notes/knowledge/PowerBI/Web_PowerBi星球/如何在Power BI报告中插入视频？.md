---
notes: Fa'l'se
aliases: null
create_date: 2022-02-07T12:28:04 (UTC +08:00)
tags: 
pagetitle: 如何在Power BI报告中插入视频？
source: https://mp.weixin.qq.com/s/kXEKU-pQ6g6-PzA7PddzrA
author: 采悟
status: 未阅读
category: 
uid: 
---

经常有人问，如何在PowerBI报告中插入视频？以前曾经分享过一种方法，用的是自定义视觉对象html viewer，参考：  

[利用Html Viewer插入视频](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484069988&idx=1&sn=697c043319d15116cd028c23f98ae8b5&chksm=8e0c4cb3b97bc5a5abc34fe1817c950134b1f30c99408563cd83e3ac0526cd18562b9bbc4ccb&scene=21#wechat_redirect)

这种方法目前依然有效，不过稍微有点变化：

1、之前的html viewer视觉对象下架了，取而代之的是另一个视觉对象html content：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOBCgBSLyhqGkJibBvHtd00XVlAYqrIt0QiaaSEuW19HC26q5Wj0ibpiahq3sHPBEP2rlaicq29QCo1IOQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

其实看这两个视觉对象的logo就知道，两个完全一样，用法也是一样的，只是换了个名字而已。

2、之前在PowerBI desktop中无法播放视频，必须发布以后才能播放，而现在要方便多了，在PowerBI desktop中就可以直接播放视频。

并且PowerBI desktop中也支持倍速播放、下载、画中画等视频播放功能。

现在还有个视觉对象也可以播放视频：HTML & CSS Viewer。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOBCgBSLyhqGkJibBvHtd00XWJ3DOG9v3icYFSBTLS1v0alDRLLwgYuoQ1yNeuRV8T0iblh65icDzkJWA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

该视觉对象也非常强大，可以自定义生成各种个性的视觉效果，感兴趣的可以摸索一下。  

关于报告中嵌入视频，这里再介绍一下简易的步骤：

**01 | 获取在线视频的网址**

PowerBI报告中并不能嵌入本地视频，所以你的视频应该是在线的，先提取出来需要嵌入视频的网络地址。

**02 | 建立度量值**

可以用下属字符创建一个度量值：

___

视频代码 \=

"<video width='100%' controls>

<source

src=

' https://vt1.doubanio.com/202202062227/3159e5a4911418c7040d4d9f2f7942d8/view/movie/M/402850372.mp4 ' 

type='video/mp4'>"

___

其中绿色的字符就是一个在线视频的地址，你可以将这一部分替换为你的视频网址。

**03 | 利用html content嵌入视频**

添加html content视觉对象，将上面的度量值，拖拽到该图表的【values】中，即嵌入视频，点击可直接播放。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMec784Cj2ibbB7ib8wTlibdjD2ibeIXK5XjAfJEiajAhVjHIMg69TTUvLsic84ZIfFozzzRibHrb3Svicyyg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

当你需要在报告中嵌入视频时，利用上面三个步骤即可实现。

[**PowerBI星球的最新版****内容合辑****，值得你收藏学习：**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078675&idx=1&sn=07abf841815e43fb0a554081c82de72a&chksm=8e13a284b9642b92d07b518abe3e6e2e2ef5066c0941c1ced26a245a6990b4330830431789a9&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN8YOicNXzCaSLpQrKXOL0LsNeYw0fj3iaGFy7XSwwmibHicdtiaHEbhgmHSPXQlkg3WiaVA4hJ8PGDcdEQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078675&idx=1&sn=07abf841815e43fb0a554081c82de72a&chksm=8e13a284b9642b92d07b518abe3e6e2e2ef5066c0941c1ced26a245a6990b4330830431789a9&scene=21#wechat_redirect)

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
