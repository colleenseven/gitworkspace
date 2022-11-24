---
ZK: Origin
create_date: 2021-11-17T12:54:12 (UTC +08:00)
tags: 
aliases: null
pagetitle: PowerBI 2021年11月更新，你应该知道的几个变化
source: https://mp.weixin.qq.com/s/w2tHDwNMt1_qlYQAp6HV_Q
author: 采悟
status: 未阅读
category: 
notes: False
uid: 
---

PowerBI 2021年11月的更新来了，没想到在平淡无奇的11月放了一个大招，众多实用的新功能和新的界面一起亮相，完整内容官方博客的介绍非常详尽，你可以在博客中浏览，点击阅读原文也可直接进入：

https://powerbi.microsoft.com/zh-cn/blog/power-bi-november-2021-feature-summary/

还可以在视频号中观看本月更新的官方视频讲解（已加中文字幕）:

这里我主要挑选几个你很可能会用到的功能简要介绍一下。

**1\. 新的格式窗格**

## 这是对界面外观的一次巨大的改动，为了让界面更友好、结构更合理，PowerBI重新设计了格式窗格，目前还是预览功能，如果已安装好11月的版本，到文件 > 选项和设置 > 选项 > 预览功能，勾选"新格式窗格",

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMahe9oVia8Xtibuxgqup1ic36vSvAiabAgqiaTsQb3st5ibj88g1GEGX3TPBBe9TUtkCAOS64J57cUiaXeQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后重启打开，就会发现视觉对象面板上的界面发生了变化：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMahe9oVia8Xtibuxgqup1ic36Uqv66puriaHVgGghYEiauE8gdKbPCPSbTsBn4BGqSyb1QId8qGBks2LQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

上方出现了两个新的图标，默认在左侧的生成可视化对象上，下面是各种格式化类型，右侧的图标是设置报表页的格式，点击进入，可视化类型就看不到了，只有页面设置的选项：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMahe9oVia8Xtibuxgqup1ic36spiaTF32MDCwgdc3KJt6fYiblqz6IiaOm6051CTk5w5QfBPWyY2bmfl1g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样设计的确更加清晰合理，以前很多人都找不到如何设置页面背景、页面尺寸等功能，就是因为设计不合理，隐藏的太深了。

以上是没有点击任何视觉对象的效果，如果选中画布上的某个视觉对象，上方将出现三个图标，分别点击进入到下面的三个界面：

也就是将之前在可视化类型下面的"字段"、"格式设置"和"分析"都移到了上面，更加直观，并且空间更大，不再受视觉对象的影响（之前如果加载了很多自定义图表，会把格式设置的空间压缩的非常小）。

除此之外，格式窗格的每个功能的名称和图标等细节也做了大量的优化，总之是变得更直观更好用了。

关于这些界面改动，并不会对你的使用有太大的影响，毕竟功能还是那些，只是位置等细节变化了而已，建议你先摸索了解一番，知道这些都在什么地方，以便在使用时能更快的找到。

**2\. 新增页面和书签导航器**

以前在报告中设置页面导航或书签导航可能非常耗时，因为你需要为每个页面或书签设置每个单独的按钮，本月更新后，PowerBI Desktop内置了两款导航器，你只需点击几下即可快速构建页面和书签导航。

点击“插入”选项卡 >“按钮” >“导航器”中找到此新功能：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMahe9oVia8Xtibuxgqup1ic36F5w9lrG7MUHeNicNXbsC3laBSSbIw17WvJIfIhZLqia4TGvOyXRpEaRQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

比如点击页面导航器，页面上将自动出现一排包含每个页面名称的按钮，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMahe9oVia8Xtibuxgqup1ic36vgWasx2vnh6WFIrzUtsNoLvL88v7ia1nZSbOwWPHWibJdoricpPsibu8JA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击即可进入相应页面，你还可以整体设置这些导航按钮的格式，这将大大节省报告设计的时间，关于该功能的详细用法，之后会单独介绍。

**3\. 支持图例排序**

新增了对图表中的图例排序的功能，点击图标右上角三点进入即可看到：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMahe9oVia8Xtibuxgqup1ic36UdeYrCHhxAPJWibVQAkIEuvKAAuica1vJnB2VbiaCc56qnn1ATAo1ZC7A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

不过如果需要对文本进行自定义排序，依然需要先对图例字段进行[按列排序](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068059&idx=1&sn=28dff6992fe6d167f4a2fbd6a0c40460&chksm=8e0c740cb97bfd1a55d7789987c7c1ed2ac94a07529cc0428b1cdf48216671f468fa7820c420&scene=21#wechat_redirect)，这次更新后，只是可以选择按照升序/降序排列了，算是增加了一点灵活性吧。  

**4\. 文本格式支持粗体/斜体/下划线**

现在PowerBI中所有关于文本的设置都增加了粗体/斜体/下划线功能，比如对表格中值的文本：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMahe9oVia8Xtibuxgqup1ic36KBdfAZtKuSSR7iazR2yBiar0vsNqWG8cCEmQsnXfT6gA22Tmm2hFXToQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个功能虽小，但也算是解决了一大痛点。

**5\. 新的文本框格式选项**

文本框现在增加了三个新的格式选项：上标、下标和项目符号列表，对于特殊的文本输入还是很有帮助的。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMahe9oVia8Xtibuxgqup1ic36aJicuVk33DH7Jj3zexrx4mBJibAwfZF6K39yDpKx9fKlXR7kkXaewA5Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**6\. 饼图和环形图支持旋转**

之前饼图和环形图是按顺时针顺序绘制的，从十二点钟位置开始，本月更新后，支持调整开始位置：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMahe9oVia8Xtibuxgqup1ic36V5gGfc43PGwiaVWktqmSjZXlbesepUBgM4LyoCG5tengqgkHwJJSdaw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其实这样调整并不符合饼图的设计规范，但也算是增加了一个自定义选项，有胜于无。  

**7\. 新增记分卡视觉对象**

这是Power BI中的目标功能（Goals），之前只能在PowerBI服务中设计和查看，本次更新后，在PowerBI Desktop中添加了新的记分卡视觉对象，可将Goals添加到 Power BI 报告中，让用户更方便的看到整个记分卡。

这个视觉对象目前是预览状态，启用后才能在可视化面板中看到它：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMahe9oVia8Xtibuxgqup1ic36iaZjOukNDU3z8fSFF14bIlpLyeRPQDbZFyYDwwpx5mdtNI4tMgNicOuA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

官方公布的可视化效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMahe9oVia8Xtibuxgqup1ic369ic2jHWq6TRnctibD5h7MRWicJ14bR3mRG3iaCicSfzWxobNbbUYEsaZtpw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

对于该视觉对象，之后会单独介绍。

11月的更新就简单介绍这几个，更全面的可以去看官方博客或者我的视频号中观看中文字幕的视频讲解。

___

PowerBI每月更新后，如果不能自动更新或者不方便下载，可以在公众号后台发送"**软件下载**",获取最新的PowerBI Desktop安装包；

如果要下载历史安装包，也可以发送**6位年月编号**获取，比如发送“202102”获取2021年2月的安装包（2021年2月是支持win7的最后一个安装包）。

___

  

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
