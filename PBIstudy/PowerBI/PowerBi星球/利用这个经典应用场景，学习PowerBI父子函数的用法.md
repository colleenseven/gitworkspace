---
ZK: Origin
create_date: 2021-11-25T12:52:40 (UTC +08:00)
tags: 
aliases: null
pagetitle: 利用这个经典应用场景，学习PowerBI父子函数的用法
source: https://mp.weixin.qq.com/s/LZecwbjjbifjZIemTsYjMA
author: 采悟
status: 未阅读
category: 
notes: False
uid: 
---

本文分享一个父子层级结构的计算思路，源于昨天遇到星友提出这样一个问题，有两列数据，一列是邀请人、一列是被邀请人，示例如下图：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOYLnzicfJDJV6DKaHuLDTas6uWS6Gne9QuibtN3lyZBJB6PZ0yr1tvHmZcU3NBfH1OMDm8OUvc0OyQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**被邀请人还可以继续邀请其他人，并且所有的下级都视作上级的邀请，如****何计算每个人的邀请人数？**

这种需求是不是很常见，逻辑描述起来非常简单，但是计算并不容易，因为这种结构的数据虽然只有两列，但邀请人和被邀请人是可以来回变动的，每个人的角色并不固定，并且下面有多少邀请层级也是未知。

这种数据结构就是父子层级结构，邀请人是父级别，被邀请人是子级别，在PowerBI中，有一类DAX函数，父子函数，专门处理这种结构的计算，它可以将父子层级结构转换为扁平的普通层级结构。  

下面就以上面的需求为例，来介绍PowerBI处理这种计算的思路，并见识一下父子函数的用法。  

步骤如下：  

**1\. 补充完善原始数据**

为了方便使用父子函数，我们需要先对上面示例的数据进行补充整理，为父子结构添加编号。

因为**父子函数要求，所有父级列的数据都必须存在于子级列中**，所以对于以上示例，添加一行，将最顶级的人员“李一”，添加到被邀请人中，这也容易理解，所有的人都是被邀请人，只是最顶级的人员，无上级邀请人而已。

然后对子级列，也就是每个被邀请人添加一列编号，并相应的把邀请人的编号匹配上去，你也可以先在Excel中做好这个表：

这个表完善以后，下面就可以利用父子函数来转换层级了。

**2\. 将父子结构转换为普通层级结构**

以下计算都是利用计算列完成，首先利用PATH函数来获取完整的层级路径：

> 层级路径 = 
> 
> PATH('结构表'\[被邀请人编号\],'结构表'\[邀请人编号\])

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOYLnzicfJDJV6DKaHuLDTasUOuJ76qP2f59sibickRWAkJdg6djrEWOQmsNX0EpjAkLR2ElqlBrGp8Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

PATH函数有两个参数，第一个参数是子级的列，第二个参数是父级的列，它的计算结果是层级的完整路径，用 “|” 分割，通过这个路径，你可以看出每个人的上下级关系。  

有了路径之后，下面就可以计算每一层级的人员。

第一层级可以这样来写：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOYLnzicfJDJV6DKaHuLDTasSiaOvZoID7PU7uEqLZibMhrmWcTDr7ic3ZWSQQeibJeXxlv9o96fNOszKA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里用到的父子函数是PATHITEM，它可以从层级路径中获取某一个层级的值，第二个参数是1，就是获取第一层级的值，这个例子第一层级都是1。

然后利用LOOKUPVALUE函数，从被邀请人编号中，找出1对应的被邀请人名称，也就是“李一”，所有人的第一级邀请人都是他。  

同理，通过更改PATHITEM函数的第二个参数，获取第二、第三、第四个层级分别是谁：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOYLnzicfJDJV6DKaHuLDTasVXspPEWswQk2NuLFp0WicIC5L5V3e1L8f57PLTWTfnPGiayPtWqwZVgg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**上表中的后面四列是4个层级，就是我们常见的普通层级结构。**  

如果层级很多，无法一眼看出每个人有多少个层级，还有个父子函数是PATHLENGTH，它用来计算层级的深度：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOYLnzicfJDJV6DKaHuLDTasibEQAwEkq2ELiaNlwQgvb6DkzslR8x9T9Png0icgOzwR67SwUCPB71u4w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就可以看出每个人的上级有几层了，后面也会用到这个深度。

**3\. 展现结果**

有了上面的普通层级结构，就可以很方便的计算出每个人的邀请人数了，写个度量值：

> 邀请人数 = 
> 
> DISTINCTCOUNT('结构表'\[被邀请人\])-1

因为计算邀请人数时，不应该计算自己，所以减去1，剩下的就是本人的邀请人数。

将所有的层级放到矩阵的行中，邀请人数作为值，结果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOYLnzicfJDJV6DKaHuLDTasC0sEFjjemU26RWbumNhfic0iae1fQh2bp1x6IWwXtJu2nETWp5OGiaQkg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就一次性得到了每个人的邀请人数。

但是有一个问题，因为每个层级都有空值，所以这个矩阵结构有太多的空结构，有必要处理一下。

思路就是让空结构的计算结果等于空值，修正度量值如下：

这个度量值的计算逻辑是，比较当前层级结构与当前数据的层级深度，如果当前结构小于等于层级深度，正常计算邀请人数，否则返回BLANK。

这个逻辑可能不太好理解，你可以根据上下文，比如矩阵的第一行李一，对于上面度量值中的变量X，返回1，变量Y也返回1，所以满足条件，正常计算邀请人数；而第二行，X返回2，但是Y还是1，所以不满足条件，返回BLANK。

用这个修正后的度量值制作矩阵，效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOYLnzicfJDJV6DKaHuLDTasXr1g79Np61h7z5dNGMxXsE00R4eOPHVicsQUXTQtTt65mSXPLXicGpdQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就清晰直观了实现了该业务需求。

关于父子函数的计算，如果你刚开始接触，会感觉非常绕，其实理解了以后，并没有什么难度，关键是理解父子结构计算的整体思路，弄明白为什么需要将它转换为普通的层级结构，以及如何利用父子函数进行转换。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
