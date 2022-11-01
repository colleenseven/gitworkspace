---
create_date: 2022-08-02T12:25:56 (UTC +08:00)
tags: 
pagetitle: 通过这个设置，Power BI表格秒变高大上
source: https://mp.weixin.qq.com/s/ABsfeFcHoJoI2ARv1uhYNQ
author: 采悟
status: 未阅读
category: 
uid: 
---

今天分享个表格可视化格式设置的小技巧。

关于PowerBI表格/矩阵可视化的用法和常用格式设置，之前专门介绍过：

[玩转PowerBI中的「表格」](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067625&idx=1&sn=6d48553aea3bc7baffecedb3d23af924&chksm=8e0c77feb97bfee877dfcdce78764746dd24f445b3bc6fd43c964a99eb08839983ad4b98f614&scene=21#wechat_redirect)

[Power BI矩阵格式设置13招](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071983&idx=1&sn=3fd379f7bf88141747ac9a09dc4273b7&chksm=8e0c44f8b97bcdee4cb068fd1e47e033629cf0734dd29c8341746d449372068dbb4e6d298cba&scene=21#wechat_redirect)

还有个问题经常被小伙伴问到，**如何将表格/矩阵的背景设置为透明？**

正常情况下，如果画背景是纯色的，不会有表格透明的需求，当设置页面背景为一张图片的时候，可视化的背景不透明就变得不太协调，比如这页报告右侧的矩阵：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMVCAHpJojicCnSvxJ8CtJFykVoYsJfDD0ib9ouPAYSOL3XAEoKUj1ZMNDffQiclvFSCp5SwEAWZbhfw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其他区域都已经设置为透明，只有右侧的这个矩阵的背景还不透明，如何将它设置为透明呢？

如果你直接设置背景颜色，需要设置值、行、列等每一个元素的背景颜色，透明色还需要写度量值才能实现，列标题还无法按度量值来设置颜色，这样操作起来比较繁琐，而且还无法实现完全透明的效果。

其实表格/矩阵中还有个选项可以直接设置为透明，打开格式面板，找到“**样式预设”，将“默认值”更改为“无”**：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMVCAHpJojicCnSvxJ8CtJFyGhdKcpTAdRWh0psXibyzibTSCWFFIndSNBqMMiajDicZ6Vu66Ay7TUn7tw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后就可以实现表格全部区域变为透明的效果了。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMVCAHpJojicCnSvxJ8CtJFyrrdOVWic4vrBJ2IKTlTgFklTIf8OgiaiaiaOF1OHicBIbjYFgxXJtK4d0jQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样看起来是不是舒服多了。

"样式预设"变为无以后，可能字体颜色、边框等格式也会改变，这些再单独调整就行了，这个设置主要是将背景色快速调整为透明。

通过上面的介绍，其实让PowerBI表格变得高大上的技巧只需要两步：  

-   插入高大上图片作为背景
    
-   设置表格为透明
    

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4500+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1AEySOiakLF2kY7eb1kUw2DtfKoVz2ctBDia5dtNsPX2GhV0ZOCDDWpgpaTQtnqfqJrRXt5PNia95g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门Power BI》电子书，轻松入门。
