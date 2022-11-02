---
create_date: 2022-03-19T11:58:23 (UTC +08:00)
tags: 
pagetitle: PowerBI 2022年3月更新，折线图支持添加误差线了
source: https://mp.weixin.qq.com/s/n2aG1MzeP_tLZUivzjMoYA
author: 采悟
status: 未阅读
category: 
uid: 
---

Power BI 2022年3月的更新来了，本月的最大亮点是折线图支持添加误差线，完整内容官方博客的介绍非常详尽，你可以在博客中浏览，点击阅读原文也可直接进入：

https://powerbi.microsoft.com/zh-cn/blog/power-bi-march-2022-feature-summary/

还可以在视频号中观看本月更新的微软官方视频讲解（已加中文字幕）:

别忘了给视频点个赞哦![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN14yQeO6mrLMKWcFy0ajELTV9rbmJyicKiavicjOz8g8OPEEKo4qMaicp5mIeial1GNFictPLvX477O6wQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

本月更新的其他功能都不是太常用，这里就专门介绍一下新增加的折线图误差线功能。  

误差线通常用于展示数据可能产生的偏差或者潜在的波动性，以一种更直观的方式在图表显示出来。

**怎么使用误差线功能**

目前这个功能还是预览，首先在预览功能中勾选“误差线”  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPvCDfTNq9VtviaVibqNktKqYAgQegzke2ZdBrtFGQNGdlQXWr2KC9Cwphticex74wYjAUvoK3kh1O3Q/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这里显示的是“错误栏”，应该是机器翻译的，太生硬了。

然后当我们做一个折线图，就可以在分析功能中看到这个功能：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPvCDfTNq9VtviaVibqNktKqYnCTKBPN3z1UAIr7AwIchgZecB7m1sWRJHtz6ic3XcLsaOspoxgDR3Sw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

展开这个功能，会发现它的功能设置还非常丰富，首先需要放入两个字段作为误差线的上限和下限。  

上面的折线图展示的是收入的趋势，假设误差线的区间是收入的0.1倍范围，可以写两个度量值作为收入误差的上限和下限：

上限 = \[收入\]\*1.1

下限 = \[收入\]\*0.9

然后启用误差线，并将这两个度量值分别放到上限框和下限框中：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPvCDfTNq9VtviaVibqNktKqYzedEQticq3XArjaL9rK7ll0H5b8JTQ2spKWp6bnYLvABF5FtONnSF0w/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

折线图上将出现误差线：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPvCDfTNq9VtviaVibqNktKqYgGalftbGq41ykRJTKU3juonxALlAwkSY4GsDSNfHmlXUk2qN4D2J0w/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

注意上面写的度量值是收入的1.1倍和0.9倍，所以误差线中的选项：**与度量值的关系应该选择“绝对”**，表示误差线的上下界就是该度量值本身的值。  

而如果选择相对，上限和下限的度量值应该这样写成：

0.1\*\[收入\]   

\-0.1\*\[收入\]

这样误差线的上下界就是在折线图的基础上，向上或者向下伸出相对的值。  

以上两种误差线效果等同。  

你可以根据你准备的上限和下限字段的情况，来选择相应的选项。  

**显示误差线的几种方式**

误差线不仅只是显示上图的样式，还有多种样式可供选择：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPQJMJfsGbibb9ribYY0nIYVicKAV8C87Xf8F3LuwybyXGbianaSz94SNLfgQ3g2wheKfqwgibUeMubHjQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

上图是用条形图来显示误差线，展开这个功能还可以调整条形的宽度，尾端的样式等。

**以线条显示的效果：**  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPQJMJfsGbibb9ribYY0nIYVicfaxDzPDftutoDXkFIabUXdGRy1R7GPt6LrOb3WicJzb4dx8fggx3iaZg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**以阴影区域显示的效果：**  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPQJMJfsGbibb9ribYY0nIYVicPppPcPCicQItQldBuz7MDsVaTUVtrh6tbnVySumfu21ggC6yYsZ2Onw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

还可以打开工具提示，在提示中显示误差线的上下限的值：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPQJMJfsGbibb9ribYY0nIYVic1wEv7odrmaXQ9s4Rcb55ZTetsXc3DRu7kPAJ9gwxmM9vGF3WHytUMg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

还可以多种效果同时展示：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPQJMJfsGbibb9ribYY0nIYVicCyqzEA3ty1VOZfasuBK7rKBctAibN7kecFOVjwfsGDdyicRZPtNrj1bQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

以上每一种效果，里面还有细节选项可以调整具体的显示样式。

**误差线的其他玩法**

利用误差线功能，不仅可以显示误差线，还可以探索出其他可视化效果，比如这个折线图中有两条折线，分别显示收入和利润：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPQJMJfsGbibb9ribYY0nIYVicKw34YK6VicUGZPZFCc04ib4Bn9BUlKcd82G4gB4gEHp226HibwickFbaww/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

那么将利润作为收入的下限值，并用阴影区域来显示，就可以做出两条折线之间显示阴影的效果：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPQJMJfsGbibb9ribYY0nIYVicE1JvkCg903Fkdb2kvCYAYicWrjibvVfzzNgLlKOIqbWDwZXFlP4JrQGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

如果更改为以条形来显示，就实现了在折线之间插入条形图的效果：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPQJMJfsGbibb9ribYY0nIYVicvmSvQypqsUq9qiax46yUiaicMYMBia2tMkk8rGq6HWyuPuhUBRZR2MFP6g/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这个功能很简单，但比较实用，关于它的更多细节和用法你可以继续探索。

___

PowerBI每月更新后，如果不能自动更新或者不方便下载，可以在公众号后台发送"**软件下载**",获取最新的PowerBI Desktop安装包；

如果要下载历史安装包，也可以发送**6位年月编号**获取，比如发送“202102”获取2021年2月的安装包（2021年2月是支持win7的最后一个安装包）。

更多安装说明请参考：[关于Power BI的下载和安装，你想知道的都在这里了](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078648&idx=1&sn=7e53496bd78498ed962696055a500474&chksm=8e13a2efb9642bf98bb73de730c5141d61eb2dfd22e1781c2603745137302ea56ba2ae4dd6ba&scene=21#wechat_redirect)

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI 

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
