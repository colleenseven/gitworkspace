---
notes: Fa'l'se
aliases: null
create_date: 2022-02-13T12:27:13 (UTC +08:00)
tags: 
pagetitle: 利用微软输入法，轻松为PowerBI报表添加图标
source: https://mp.weixin.qq.com/s/NRQcinxQxijpaJ4inK_w_w
author: 采悟
status: 未阅读
category: 
uid: 
---

在制作可视化报告的时候，不仅仅只能是用文字来表示相关的类别标签，还可以添加一些适合的图标更能彰显图表的个性，本文就介绍一个添加图标的简易方式。  

以冬奥会的奖牌榜为例，利用表格可以简单生成这样的榜单：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOcwBqm4om7d6iacCbVyQ7iazbvqg8wiacXrWAMTWZVL6gwiauCy3bOFAdWQGicCLsoUaRAl9oqiaON1BPA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这里的列标题是直接用文字显示的金银铜牌，如果能直接用金牌、银牌、铜牌的图标来显示，是不是更直观呢？

将列标题的金银铜牌换成对应的图标很简单，只需灵活利用微软拼音输入法就可以了。

首先将电脑的输入法切换为，微软拼音输入法中文状态，然后输入金牌的拼音，就可以看到金牌的符号：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOcwBqm4om7d6iacCbVyQ7iazYJl9r3UD8dBcUUfRsly2uiaVuUUMLVt9j3z1BlPNo7AUYKbCavZwZGw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

或者在要输入文字的地方随便输入一个字母，这时，输入法将会跟随光标弹出一个字符提示条，点击字符提示条最右侧的笑脸符号，就可以进入表情符号面板：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOcwBqm4om7d6iacCbVyQ7iazfibfa2XgBiaI5A7q10MMV1GHHoIp0HU0Hq2ic8W7icuHiaSnY9n440KGj7g/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

快捷键**win+.**  也可直接调出该面板

在这个符号面板中，对所有表情进行了分类排列，在其中选择适合的图标就可以了。

以上介绍的微软输入法的表情符号，这些符号就可以作为PowerBI中可视化的图标来源。

回到上面冬奥会奖牌榜的例子，只需要双击表格【值】中的字段，删掉原来的字段名称，替换为表情符号中的金牌等图标就行了：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOcwBqm4om7d6iacCbVyQ7iaz8caXnnR2miaUwYk3EPhTTeBPqib25lSB0IxJJGricSb0QePyCDM8bbbFA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

表格就变成了这样的效果：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOcwBqm4om7d6iacCbVyQ7iazYoVYTZHU5NLeiaRmkdMeDcDOwXjgUhSFTvXFUTyCe0BDNX7ltJicOgEg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

看起来是不是更有趣了。

除了上面的列标题，还可以为下面这个表格的奖牌旁边添加个图标：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOcwBqm4om7d6iacCbVyQ7iazzYpqXKSsBpeH6xwbdOy5icWOXjx0c8HvjHEMBEQu74nE4JH12x1eO5g/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

只需要添加一个计算列：

> 奖牌图标 =
> 
> SWITCH(
> 
>      \[奖牌类型\],
> 
>     "金牌","🥇"&\[奖牌类型\],
> 
>     "银牌","🥈"&\[奖牌类型\],
> 
>     "铜牌","🥉"&\[奖牌类型\]
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOcwBqm4om7d6iacCbVyQ7iazSAQ37rRdJIruFlN5Zt5ZyJ8zXibsQstBGOYyXkWhJWpzkibsmV4QoKVA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

然后把这个新的字段放到表格里，就有了图标的效果：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOcwBqm4om7d6iacCbVyQ7iazhow1UjWqQOotfia2GCf6NT9FoicyFfnnzCN7fC8cDBxSQ3ZpUkQDF3kA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这种方式也不仅仅是用作表格可视化，用在其他地方也是可以的，比如图表的类别：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOcwBqm4om7d6iacCbVyQ7iaz90qCenMZa0nBNeTJ3JdQoYja6WrQBT7OzNG61ibfZymdJXksQtO38xw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

或者报表的页面名称上：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOcwBqm4om7d6iacCbVyQ7iazI9bk4Y0xEpvTACLG3GsEVXkzCeUTyzyDFSodxQmFNPXQrnQvmJjAiaQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

只需要把这些符号当成普通的字符，像平时打字输入一样，只是它最终会显示为一个图标而已。

其实微软输入法的这些表情就是emoj，你也可以网上搜索喜欢的emoj符号，然后复制粘贴到PowerBI中使用也是可以的。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
