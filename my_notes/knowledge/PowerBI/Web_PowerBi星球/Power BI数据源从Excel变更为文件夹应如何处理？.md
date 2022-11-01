---
create_date: 2022-07-29T12:26:32 (UTC +08:00)
tags: 
pagetitle: Power BI数据源从Excel变更为文件夹应如何处理？
source: https://mp.weixin.qq.com/s/NBAnfc4l4jprGoQiD7LOvg
author: 采悟
status: 未阅读
category: 
uid: 
---

用PowerBI做分析报告，不可避免会遇到数据源变动的问题，比如数据源存放的路径发生变动，这种情况下可以利用参数进行路径的动态化，参考：

[PowerQuery报错？利用参数轻松解决源文件路径问题](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073358&idx=1&sn=99e86bdde3a9831509fc8017890e0af8&chksm=8e0c5959b97bd04f4023fe469acc7774bf8307856086b58133d10b61bf518970b4fa7fbbdfe7&scene=21#wechat_redirect)  

还经常被问到的问题是，有些人可能刚开始分析的时候，用的是一个Excel文件作为数据源，但之后文件格式变了，比如改用了csv文件作为数据源，或者把数据源都放到了文件夹里，需要变为文件夹作为数据源，这些情况应该怎么处理呢？

直观的做法，就是重新做个查询，不过如果处理步骤很多，这样重复操作一遍就太浪费时间了，其实我们可以通过修改M公式来直接变更数据源。  

下面以这两种情况为例来介绍一下如何修改，当然前提是数据本身是不变的，这样才能利用之前数据清洗的步骤自动刷新。

**从Excel文件变更为csv文件**

对于导入的Excel文件，打开高级编辑器，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMRib4laUf4KX2eddPr2TPZiakRdqDD5u3e5lJtaG8AkSFL397ibRTZQibUU1VyAFsUThQsUFHibdG18Yg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在高级编辑器中记录有这个数据从导入到处理的每个步骤的M代码，从Excel工作簿获取数据时，导入数据的步骤是前两行，如下图框住的部分。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMRib4laUf4KX2eddPr2TPZia7JyrVW7icia7EnicAdnxDVib8LftyGGx4icrvkGq0wEibXOjlh608ueCBMrg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

数据源从Excel变更为Csv，只需要修改这两行的公式就可以了。

但是可能很多人都记不住M函数，不会直接输入M公式修改，那应该怎么办呢？

我们可以利用PQ来生成csv文件导入的公式，具体做法就是再导入一下csv文件，导入后可不用做任何整理，打开高级编辑器，复制源这个步骤的M公式，下图中框住的部分。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMRib4laUf4KX2eddPr2TPZiaX5VrXRw1WPZUlCwYVFDHuS56HHapF3E0A7t5dRAErvDxc8NPcqic9Kw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后粘贴替换掉上面Excel查询里框住的部分，替换后的代码如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMRib4laUf4KX2eddPr2TPZiafAlBhWsXY0JKicEkNL7yZjTTKiancSq7lHsocRWmfWyGLoveDBibq5z8Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其中Excel查询，“提升的标题”这个步骤中，之前引用的是上个查询的步骤名，这里替换后只有一个步骤，所以直接改成“源”即可。

通过上面简单复制粘贴，就成功地将原来的Excel数据源替换成了csv数据源了。

**从Excel文件变更为文件夹**

这是个更常见的需求，前期可能只有一个Excel文件，随着数据量的增加，有很多相同格式Excel文件需要先合并到一起，这种情况可以所有的文件放到一个文件夹里面，我们就需要将原来的Excel数据源替换为文件夹数据源。

这种替换与上面的思路一样，同样新建个查询，从文件夹获取数据，并将文件夹中的表解析出来，合并成一个表（不用做进一步的整理，因为整理步骤原来的查询已经做过了），关于从文件夹合并Excel的具体的步骤可以参考：

[批量合并Excel，PowerQuery的这些技巧你应该掌握](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070803&idx=1&sn=826d571e4133872ff3bedb4ad4d524f9&chksm=8e0c4344b97bca5281787e9a0cf1a3f2571227316537b1ba7069c5bf5f600d4a4249cfc18932&scene=21#wechat_redirect)

导入文件夹中的文件并合并以后，打开高级编辑器，复制里面的相关代码：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMRib4laUf4KX2eddPr2TPZiaFd1KTsxAaXvKIO8y7TNVib5YicQjsfCnThLd3NMeaL0w2ic450icHJ7diaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后替换粘贴到原来的Excel数据源查询中（也要注意更改下一个步骤中所引用的上一个步骤的名称）。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMRib4laUf4KX2eddPr2TPZiaO5nf6q06s0NORC2CDuGQqtYs7Ch8cdtIO8zpzT5cs0HJObibkBPcy8g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就能将原来的Excel数据源更换为文件夹的方式。

上面主要是介绍替换的思路，其中高级编辑器的公式也不一定完全照搬，有些特殊情况可能还要根据实际的数据格式以及整理的具体步骤，进行相应的微调。

关键是要对自己的数据足够熟悉，并掌握基本的PQ操作，虽然不需要对M函数很精通，但是理解每个步骤公式的大概含义，并对整理后的数据进行必要的检查验证，确保整理的数据可以满足分析的需要。  

关于PowerQuery的更多技巧：

[PowerQuery常用的界面操作](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067158&idx=1&sn=4ad955112df2f40a93b684ed9147f26e&chksm=8e0c7181b97bf89777ae3d9de929867745edcbbfe1f2b396761c0cec716b86ee31e439279add&scene=21#wechat_redirect)

[PowerQuery源数据列名更改导致错误的问题](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484079358&idx=1&sn=bb7c9ab616473f416ff33d8b60b0e65f&chksm=8e13a029b964293f7000dd46ccdc1724690318c860455978c53b531a7e9c01fe783ac96d0fc3&scene=21#wechat_redirect)

[PowerQuery快速批量更改源文件路径的小技巧](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484075492&idx=1&sn=d5f8513f6f796c088f84a34f23ee1402&chksm=8e0c5133b97bd825755b12db418e8a9a801e7454541bd8d69e45e03f72eef22199a381465fdf&scene=21#wechat_redirect)  

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4500+ 爱好者一起精进~**

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门Power BI》电子书，轻松入门。
