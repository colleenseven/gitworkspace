---
ZK: Origin
create_date: 2021-10-26T12:58:14 (UTC +08:00)
tags: 
aliases: null
pagetitle: 这个PowerQuery数据整理技巧，你应该会用到
source: https://mp.weixin.qq.com/s/z6OM5Ai-RCqgdA6XuLbosg
author: 采悟
status: 未阅读
category: 
notes: False
uid: 
---

当我们把Excel中的数据导入到PowerBI中，常常会遇到，数据莫名的变了，比如这列数据，在Excel中是这样显示的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOW7rZKa10l2WGJrAyaP5YD4wgbsiaHDXh3zLBydFYyfxfgoPJgQI7c7pLicgda74rJ8GfmnSabeiaJA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

当把这个excel导入到PowerQuery编辑器后，你很可能看到的数据是这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOW7rZKa10l2WGJrAyaP5YDrZqkFTnHtcjoWdxEdQynichz44gKbUM47WssWCOxSbkTYZUclDnOpvw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

数据前面的0自动消失了，为什么会出现这种情况，以及如何避免呢？

这是因为数据导入后，PowerQuery自动检测并更改了数据类型，对于数值的数据，最前面是不会显示0的，你可以在右侧看到这个步骤：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOW7rZKa10l2WGJrAyaP5YDG6uIEofKqNRE75k6cYvk1msqTQGLtW0Ru4JYFJ9eT4ts5icJYicTlKeg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

那么解决的办法也非常简单，直接把“更改的类型”这个步骤删掉，数据就恢复为与Excel一样的格式了：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOW7rZKa10l2WGJrAyaP5YDFpRdYib0BSDPLic7MUC5Jtd0hMlwWyMf54MDT44e6JcViashPrq0mntibw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

更彻底的做法是，将自动检测数据类型的功能禁用，在文件>选项>数据加载中，勾选“从不检测未结构化源的列类型和标题”：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOW7rZKa10l2WGJrAyaP5YDy1LUpQpGfDgKiagoazem7k2SA5CdrMiaCibo1TtXjibFxVAVaeoyxKKribQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样设置以后，系统就不会自动检测并调整数据类型了。

**不过系统不自动调整，并不是数据类型就不需要调整，在数据上载到模型之前，你仍应该根据分析的需要，手动将每个字段调整为正确的类型。**

接着上面的问题再说一个技巧，如果有一列数据本来就是这样的文本：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOW7rZKa10l2WGJrAyaP5YDsRWZm8GzZxZMjAqzxsE7YJvjdGenadukftTH49c9oibdicT5hFUHWDZw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果需要将这样的数字，调整为8位代码，不足8位的，前面用字符0补齐，应该怎么做呢？

这种情况下有个M函数专门做这种计算，它就是Text.PadStart，用于在字符串前面补充指定的字符。

添加自定义列，写法如下：

Text.PadStart(\[编码\],8,"0")

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOW7rZKa10l2WGJrAyaP5YDPd8H4bY9stOuI9TgGrDOuKR46bE8V0rPv1Sia8e7WgUMaZuOftWDE5A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

就得到了8位编码的效果：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOW7rZKa10l2WGJrAyaP5YD771SHLyo1zu59iarZLOtvUXYTuU94ahHI7AMibZfCFkl5fibQ0qTJE4cA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果把这个问题反过来，先有一个8位编码的字段，我们需要把前面的字符0都去掉，这些0的个数是不同的，并且在后面部分也有可能会出现0，是不能去掉的，所以不能用分列的方式来实现。  

对于这种情况，仍然有M函数专门处理：Text.TrimStart，它用来清除文本字符串中的前导相同字符。

添加自定义列：

Text.TrimStart(\[8位编码\],"0")

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOW7rZKa10l2WGJrAyaP5YDSyURQyUxFuv43G1GLpibQY3XhYK7ibkcib6uOup4W8t46B5tH2wNibsc8A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

效果如下：  

以上就是几个简单的PQ技巧，对于PowerQuery，在熟练操作界面功能的基础上，掌握一些常用的M函数，可以帮我们快速的完成数据整理。  

**更多PowerQuery技巧：**

[文本处理技巧：移除和提取](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067947&idx=1&sn=193910835700587b71e74889f62244fd&chksm=8e0c74bcb97bfdaa4db1076e9bd92ac27a86be732b3d771b4b34f5111f53ed16969fcb3cce38&scene=21#wechat_redirect)

[PowerQuery:空值(null)运算的的解决思路](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484069447&idx=1&sn=2c5eb332df256349769962e07307308d&chksm=8e0c4e90b97bc7864a8993e056aeb14afa9b4e1739c744c5c8e7b58d8b3a4874d0744c5aef8a&scene=21#wechat_redirect)  

[批量合并Excel，PowerQuery的这些技巧你应该掌握](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070803&idx=1&sn=826d571e4133872ff3bedb4ad4d524f9&chksm=8e0c4344b97bca5281787e9a0cf1a3f2571227316537b1ba7069c5bf5f600d4a4249cfc18932&scene=21#wechat_redirect) 

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN6oGnIQSa3kx3M0QQESdrYCTV9SBx5LXD4kp3icA9LouW3YN2z2njBWWQzM1zia9Fbeky0fdIpNakw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和3900+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMqicSUp5EfHiae4ibtEjIZsDCy5RUEz1Yp2hsG1ExlG3XiaqfWPqspJ1oiaEcKjuJCKPStBaWQXO6SOew/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
