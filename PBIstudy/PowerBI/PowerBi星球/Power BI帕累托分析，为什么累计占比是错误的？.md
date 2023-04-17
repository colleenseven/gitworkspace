---
create_date: 2021-04-01T20:05:58 (UTC +08:00)
tags:
aliases:
pagetitle: Power BI帕累托分析，为什么累计占比是错误的？
source: https://mp.weixin.qq.com/s/A3OGJrlW5OXq29S0QDOtbw
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

关于帕累托分析，大家用的比较多，有个小问题被很多人问过，就是计算出的累计占比结果是错误的，这里专门写篇文章说明一下。  

正常的帕累托分析是这样的，[以前的文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067854&idx=1&sn=bd282fa65514734b6762b63704fae8f2&chksm=8e0c74d9b97bfdcf7677fadf031b177fd1e89b8a5695928f8e33173cb6a338d03d221ebb7953&scene=21#wechat_redirect)中曾经举了个简单的例子，

> 占比 = DIVIDE(\[利润额\],CALCULATE(\[利润额\],ALL('数据表')))
> 
> 累计占比 =
> 
> var  cur\_rate=\[占比\]
> 
> return  CALCULATE(\[占比\],FILTER(ALL('数据表'),\[占比\]>=cur\_rate))

如果你分析的数据表只有一个表，并且还有重复值，比如表是这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP4HmZibqUt2UBVicG6uKVJ30742fONztcoSiapmTGy4SNyEDaB1MJaic5hibPkr9UqbKpzfWZLeYBE1Xg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

按上面的写法计算的结果将是错误的，比如第一个值没有数据，后面的也有错误，为什么会这样呢？

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNNJOabiaOcMCN8ZtsRXkMh1prqmnNdvc8KJmfNsvWrGiaR7WVsCQYN9uAibIMUfyj3YFKahkrKoNFuw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在计算占比的时候，会自动汇总，A1的占比是48%，但按上述累计占比度量值的计算逻辑，FILTER的第一个参数是使用整个数据表作为行上下文，在每一行中计算占比，不会按类别自动汇总，所以会出现上面的情况。

如果你还不理解，可以在数据表中添加一个计算列：

> 每行占比 \= DIVIDE(\[利润\],SUM('数据表'\[利润\]))

来模拟看看每一行的占比情况:  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNNJOabiaOcMCN8ZtsRXkMh1aMzWzwiavHCIYsZdlI9fzxlmiaZMOSCBLm2mn5I2iaibGgZ5ib22YSapJww/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

因为没有任何一行的占比，高于48%，所以A1对应的累计占比是空值，A2的占比是22%，只有43%大于等于22%，所以A2对应的的累计占比是43%，其它的结果都是这个逻辑，你是不是清楚了？  

所以只要有重复值，上述写法得到的就是错误的结果，那么应该如何修改呢？下面提供两个方法：

**方法一、修改累计占比度量值**

依然是利用这一个表，将累计占比的度量值修改为：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP4HmZibqUt2UBVicG6uKVJ30k4cXcmQH1NIHS0OkcR2f2xSXibq7gOl07nP0ywIHgcsSRQvQJkEWj3w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

它的逻辑是先在度量值内部构建一个中间表，也就是上面度量值中VAR定义的 table\_，它利用ADDCOLUMNS和SUMMARIZE函数构造了一个两列的表，一列是不重复的产品类别，另一列是每个类别对应的占比。

然后再计算大于等于当前产品类别占比的累计值，就不会出错了：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP4HmZibqUt2UBVicG6uKVJ30qr0UsGArb7pMZM0OrRB3KiapPZt9lzpxmN7kFGkGorNy6O2bN0hZxAw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**方法二、建立维度表，完善数据模型**

还有一种方式是建立维度表，如果你的源数据里没有这张表，可以直接通过DAX新建表：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP4HmZibqUt2UBVicG6uKVJ30VGicibj15vVCFErXcEKzfpYe7e4PRTIx40ZZgbUHypRKNtFJlzgfDKbw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

维度表肯定是不重复的，然后将维度表与事实表建立关系。

度量值的逻辑可以与最初的一样，只是其中的字段都改成维度表的字段：

> 占比 = DIVIDE(\[利润额\],CALCULATE(\[利润额\],ALL('产品维度表')))
> 
> 累计占比 =
> 
> var  cur\_rate=\[占比\]
> 
> return  CALCULATE(\[占比\],FILTER(ALL('产品维度表'),\[占比\]>=cur\_rate))

并用维度表的字段作为上下文，就可以正确的计算了：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP4HmZibqUt2UBVicG6uKVJ301VMJibrSpvwGsvHdUazHoNLyMSYsMs84vBcXiblJWJpxrNp7Vj9XTRlA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

是不是更简单。

**第二种才是PowerBI的自然做法，建立维度表，完善模型，用维度表的字段作为上下文，每一个学习者都应该把这些操作，作为使用PowerBI的常识。**

这也是数据模型的好处，建立一个规范的、良好的模型，可以用很简单的DAX就能解决问题，相反，模型没有建好，或者压根没有模型，导入一张大表就直接着手分析，很可能事倍功半。

___

[我的新书已上市](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)，帮你从0到1，轻松上手PowerBI

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOoBOqb2ddx32yTWcia8shjuj6zhsEQA5tc6ze1tv7E6QVprfOjKC9CIRrfibRFrX1AXNSibiajcl398g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

\-精彩推荐-

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072351&idx=1&sn=fabb08c54790ac1225b470fd647c7a5e&chksm=8e0c4548b97bcc5e0450f1945a2c76039bbb42650bcb1edbc856820836d63d32af4c7780e31a&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 3k+ 学习者一起成长
