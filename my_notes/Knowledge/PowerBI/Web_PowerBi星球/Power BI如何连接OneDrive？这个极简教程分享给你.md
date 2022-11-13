---
create_date: 2021-11-28T12:52:09 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI如何连接OneDrive？这个极简教程分享给你
source: https://mp.weixin.qq.com/s/Sa-j3NKy_3sxI1hOKbmHvg
author: 采悟
status: 未阅读
category: 
notes: False
uid: 
---

OneDrive是微软出品的云盘，大家应该都不陌生，因为它也是Office套件中的一员，电脑安装Office的时候，一般连同Excel、Word、PPT同时就装上了，虽然你未必用过。

很多人会把Excel存放到OneDrive上，以便组织内多人共享，也正因为如此，用PowerBI 连接OneDrive上的数据会带来很多便利，有人负责准备数据并上传到OneDrive，有人用PowerBI连接OneDrive来制作报告。  

但实际连接时可能不会太顺利，所以它也是平时大家向我咨询最多的问题之一，这篇文章我就来专门介绍一下如何用PowerBI Desktop连接OneDrive的数据，根据常见的使用场景：分为连接单个Excel工作簿、以及连接OneDrive上的文件夹两种方式来分别介绍。

___

首先需要说明的是，由于国内网络的限制，OneDrive Personal（个人版）不能正常连接，不建议使用，这里介绍的是如何从OneDrive for Business 帐户中获取数据。

___

**连接OneDrive上的Excel工作簿**

放置到OneOneDrive上的工作簿，实际上是一个网页，找到这个网址并利用PowerBI连接Web的功能就可以实现了，具体步骤如下。

首先获取Excel工作簿的网址，在线登录OneDrive for Business，找到需要连接的工作簿，点击文件名称右侧的三个点，在弹出的菜单中找到"详细信息"：

在右侧的信息面板中找到路径，点击复制：  

然后进入PowerBI Desktop，获取数据>Web：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNF93fpF2snfxTrxiaKc1syic3V0YuCa5zicFVoxmDqmtXKjlPYzdmuiaTooH5fZdg4UByWQYRAnvOSiaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

将前面在OneDrive复制的网址，放到URL栏，点击确定，在弹出的窗口中，选择“组织账户”，并用你的OneDrive for Business账户登录：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNF93fpF2snfxTrxiaKc1syicmRFOD0RoHTiapbXcajtHHgFxR3MhVI9r8UX1Bn1USARopbWaWryFRfw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击连接，就可以正常连上这个Excel工作簿，后面的步骤与连接本地Excel完全一样，不再赘述。  

**连接OneDrive上的文件夹**

总体思路与前面获取Excel工作簿类似，也是先获取网址，不过在细节步骤上需要特别处理。  

以连接我的OneDrive里面"订单明细"文件夹为例，首先登录OneDrive页面，在浏览器URL栏复制这个网址：

**这里需要注意的是，从OneDrive获取某个文件夹的数据，我们只能先从根目录进入，所以这里复制的网址，只保留上图框中的部分就可以了。**

然后在PowerBI Desktop中，点击获取数据>空白查询：

进入PowerQuery编辑器，在编辑栏根据你自己的OneDrive根目录网址输入：

> \= SharePoint.Contents(
> 
>     "**根目录URL**",
> 
>     \[ApiVersion="AUTO"\]
> 
> )

之后会出现"编辑凭据"的提示:  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNF93fpF2snfxTrxiaKc1syicTVLbX23tNdJJUXFG4lcguklawaGXqjlmjLeDBzG9y3Eqfar28Jr36Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

进入以后，这里选择Microsoft账户，点击登录：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNF93fpF2snfxTrxiaKc1syicHhiafp8fAea0ib75VQe5IVnrHD9L634tTYiaqUiaeR1DSQt0OpXXqmnVwQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在弹出的窗口中，同样用你的OneDrive for Business账户登录，然后点击连接，就会连接上OneDrive的数据。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNF93fpF2snfxTrxiaKc1syicWEPMfydQQUMzEa3EBkBCn0eGfLOVnZUCc3e2OQCnE8w7OnSpmIkEiag/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

因为这里连接的是根目录，所以OneDrive上各种数据都会显示出来，而我们需要的只是里面的某个文件夹，这里只需筛选Name列中的"Documents"，并点击第一列Content右侧的展开按钮：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNF93fpF2snfxTrxiaKc1syicgxyU3U9ibtkplF25zhniaCQHIPVFgpFXKia8qExKmvDgicrwrgDsGj93RA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里就看到了里面的“PowerBI星球文件”这个文件夹，因为需要导入的数据就在这个文件夹下面，所以重复上面的步骤，只筛选这一行，然后展开，直到最终找到“订单明细”这个文件夹，展开后，就可以看到这个文件夹中的Excel工作簿了：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNF93fpF2snfxTrxiaKc1syica6qbvXcPFkrE3xaEmHib2N4YMaIluiceuoLebrtW6g8kqicWo61jTgXsg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

到这个界面是不是就非常熟悉了，和我们导入本地文件夹的界面完全一样，然后就可以批量合并这个文件夹里面的数据了，合并步骤我就不再展开介绍了，如果你还不熟悉如何批量合并文件夹，建议你看看这篇文章：

[批量合并Excel，PowerQuery的这些技巧你应该掌握](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070803&idx=1&sn=826d571e4133872ff3bedb4ad4d524f9&chksm=8e0c4344b97bca5281787e9a0cf1a3f2571227316537b1ba7069c5bf5f600d4a4249cfc18932&scene=21#wechat_redirect)  

至此，PowerBI连接OneDrive的两种常用方式介绍完毕，都是操作性的技巧，没有什么难度，动手操作一遍就会了，其中的关键是要先拥有适合国内使用的OneDrive for Business账户。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
