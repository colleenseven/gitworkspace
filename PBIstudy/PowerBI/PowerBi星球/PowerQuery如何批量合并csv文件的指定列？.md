---
create_date: 2022-12-21T23:46:54 (UTC +08:00)
tags: 
aliases: null
pagetitle: PowerQuery如何批量合并csv文件的指定列？
source: https://mp.weixin.qq.com/s/uDrdFJHCGCDXVybRoeRbgQ
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

之前介绍过批量合并Excel文件的特定列，方法可以参考：  

[利用PowerQuery，批量合并多个Excel的指定列](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073950&idx=1&sn=022f2b8806518ff03648eeea76950223&chksm=8e0c5f09b97bd61f3dc5a7509181aa42fd3545d009b9b8715b0ef387d4f50dffe0833dfa8ce4&scene=21#wechat_redirect)  

有星友问，如果有多个csv文件，像上面这篇文章中一样，列的顺序也是不同的，能够用这种方法批量合并吗？

对于这种情况的csv文件，同样可以用PowerQuery实现，不过相对于Excel文件的操作步骤，有两个细节需要调整：  

**1\. csv数据的解析函数是Csv.Document。**

在提取Excel数据时，用的是Excel.Workbook，而对于csv文件，就不能再用这个函数了，有专门针对csv文件的函数，它就是Csv.Document，之前这篇文章也介绍过：[_批量合并Excel，PowerQuery的这些技巧你应该掌握_](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070803&idx=1&sn=826d571e4133872ff3bedb4ad4d524f9&chksm=8e0c4344b97bca5281787e9a0cf1a3f2571227316537b1ba7069c5bf5f600d4a4249cfc18932&scene=21#wechat_redirect)  

具体方式就是添加自定义列时这样来写公式：

> Csv.Document(\[Content\],\[Delimiter=",",  Encoding=936\])

**2\. Csv.Document无法自动提升标题**

Excel.Workbook函数可以利用第二个参数true来自动将第一行用作标题，而Csv.Document函数无法自动提升标题，而每个csv文件的列顺序并不完全一致，所以不能直接展开。

虽然Csv.Document函数没有提升标题的参数，但是可以通过与提升标题的函数嵌套使用，来达到自动提升标题的目的。

对于第一步添加的自定义列，在Csv.Document的外层套上Table.PromoteHeaders函数，写法如下：

> Table.PromoteHeaders(
> 
>     Csv.Document(\[Content\],\[Delimiter=",",  Encoding=936\])
> 
> )

这样就将第一行用作标题了，达到了与Excel.Workbook(\[Content\],true)同样的效果，然后再展开自定义列，选择特定的列就可以了。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOWhJpSeIXQDicfszJJ7y5ic0cBqwYafEibZoia9Zt60Err1ib5DibFfObib9iagiaxU3q3HcznicbbASOwenyQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

对于合并Excel文件时遇到的其他情况，比如数据不是从第一行开始的、列名不一致等问题：  

[批量合并Excel，数据不是从第一行开始怎么办？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073974&idx=1&sn=f1c63db1ed01cbabd2a3293d663205a4&chksm=8e0c5f21b97bd637760e8cd51c9888c667e3b586da5bad7581c1749c73802656b60cf16456c6&scene=21#wechat_redirect)  

[批量合并Excel，前面有空行且不相等怎么办？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074215&idx=1&sn=5ec9f26de1277dd9cbcdbf134d9120a9&chksm=8e0c5c30b97bd526243f835d0625ebf5199103387555ac1ec5008553697215b8ba5af47b98b5&scene=21#wechat_redirect)  

[批量合并Excel，列顺序/列名都不一致怎么办？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484083224&idx=1&sn=0bce10c5cc6b2a14455aa3e533275fd8&chksm=8e13b0cfb96439d9cdf727a6cc257e0cf21de8ab90dbcaf8cb94a5e5631713f3be4e24fdd3fd&scene=21#wechat_redirect)  

如果你处理csv文件时也遇到这些情况，都可以利用上面的处理方式调整后实现数据的批量合并。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你想深入学习Power BI，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和5000+ 爱好者一起精进~**

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门Power BI》电子书，轻松入门。
