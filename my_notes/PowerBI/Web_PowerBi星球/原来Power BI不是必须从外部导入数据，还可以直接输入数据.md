---
created: 2022-10-27T17:43:34 (UTC +08:00)
tags: 
pagetitle: 原来Power BI不是必须从外部导入数据，还可以直接"输入数据"
source: https://mp.weixin.qq.com/s/TnxgSG6sXu8M-bENSo1slg
author: 采悟
status: 未阅读
category: 
uid: 
---

经常碰到有人问这个问题，在PowerBI中搞不清楚某个查询的数据源是什么，进入PowerQuery，看到的数据源是这样的代码，这到底是怎么做的呢？

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPCae35JZibltBuamz8icwialMS4xHwYBWccqdrxU91sh01DvpkgEKsOU0IFJdlEVtePHSMokk0erZ6A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其实你不需要搞懂这些代码，因为它并不是手动写的，而是通过**“输入数据”**这个功能创建表后，自动生成的代码，如果你还没有用过这个功能，可以看看下面的介绍。

在PowerBI中，不是所有的数据源都需要从外部导入，还可以利用“输入数据”这个功能，直接在PowerBI中写入数据。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPCae35JZibltBuamz8icwialMDibaHneicPr9RWPDm2POpUgurRltpbiaZCQfK2rurVqwl1nzYq32RzYcQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击这个功能，就会弹出一个创建表的窗口：

在这个窗口中，你可以像Excel一样直接一个个单元格输入数据，也可以将其他地方的数据复制后，粘贴进来。

这种方式如果创建表后，想修改之前输入的数据，也很方便，点击“转换数据”，进入Power Query编辑器，找到这个表，点击第一步【源】旁边的小齿轮，就可以再次进入到创建表的界面，每一个数据都可以编辑，也支持插入、删除行列的操作。

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNGXuShF3UbRFOSA5Qa9dQA0F8W9EpRFnJkACqkCibSQxJwraWnF8XAZW3h8qM56uS8df7DLsuagxA/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

“输入数据”创建的表，相比用DAX生成的计算表的好处是，它可以在PowerQuery编辑器中添加步骤继续整理。

并且这种方式输入的数据自动内置在pbix文件中，发文件给别人时，不需要单独再附带这个表的数据源文件，对方打开就可以直接看到数据，还可以在PQ中看到对应的整理步骤。

“输入数据”两个常见的应用场景。

**1\. 制作辅助表**

辅助表一般是数据源没有，但是分析过程中需要的，这种情况下，就非常适合通过“输入数据”的方式来建，关于制作辅助表的各种方式可以参考：

[Power BI 辅助表制作方式汇总](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071809&idx=1&sn=9e8f4916082c32cc0291a2e4e565f1fd&chksm=8e0c4756b97bce4087ec53dfb6e5380e7cb0662e73fa070f831e4283095505a5aced233e59c8&scene=21#wechat_redirect)  

**2\. 收纳度量值**

点击“输入数据”，但是不输入任何数据，直接点击确认，就会生成了一个空表，这个空表有什么用呢？它常用于收纳模型中创建的度量值，关于这个用法的详细介绍可参考：

[利用这3个步骤，轻松管理你的度量值](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484069973&idx=1&sn=b14786fae234c7da3055c38f641d8556&chksm=8e0c4c82b97bc594eb16dd48bdf2c8b853f741b3a29cb6d9eee7881fcd0fd114d1b4515adfe0&scene=21#wechat_redirect)  

“输入数据”目前的限制是3000个单元格，如果你要建的表不超过这个限制，就可以利用该功能，方便、快捷、无代码生成一个内置的小型数据表。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你想深入学习Power BI，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和5000+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMstwXX5zrKianmFXzyqbIVgh7byfo3V8JJPmhqicywbtYkM0j2ibngnT5XBZ2AwKvGZiby9ngoKfLvzg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门Power BI》电子书，轻松入门。
