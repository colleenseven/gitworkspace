---
create_date: 2022-09-13T23:28:55 (UTC +08:00)
tags: 
pagetitle: 多列结构的二维表转一维表，PowerQuery可以这样做
source: https://mp.weixin.qq.com/s/uLbXKUXQrTYIcmBS0LWXPA
author: 采悟
status: 未阅读
category: 
uid: 
---

由于分析的需要，最好使用一维表的数据结构，之前分享过二维表转一维表的方法：  

[关于一维表，你想知道的都在这里了](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068871&idx=1&sn=4ab596602ed0a4c851755673d8fcf37a&chksm=8e0c48d0b97bc1c6e8edc0d31110b669c87740e55601fce30e498c9801af972ca1f366eb7ab9&scene=21#wechat_redirect)  

该文介绍了几种常见数据结构的转换方法，不过还有一种结构也很常见，就像下面这种：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMHxg0uxa5YhybNgQARnJfuxWticnFUjOxpPCfIyoepx52bFUmsOseIgOcU3IdX6XCcGJrekriaQkuA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

课程和成绩都有多个列，无法直接通过逆透视来实现，那么这种如何转换为一维表呢？  

其实熟练掌握了PowerQuery基本界面功能，这种结构的转换也不难，下面来看一下转换步骤：  

**第一步：选中课程1和成绩1两列，点击合并列。**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMHxg0uxa5YhybNgQARnJfuiaFlibpeZBNJ2nTjV86u0KbsqM89dYvzLVt9WhDUIRCmicE0hicIjCC0mw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

分割符可以任选一个，比如选空格。

同样的方式把课程2和成绩2、课程3和成绩3合并，这几列两两合并后的数据：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMHxg0uxa5YhybNgQARnJfu3JqTm5t1NhOf6wKant3u7uXrvshJZRlEJdFXMN2lPJPIPsBefFf5sg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**第二步：选中“姓名”列，点击“逆透视其他列”，逆透视后数据结构如下。**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMHxg0uxa5YhybNgQARnJfuwsxJRibqVwqSG3zticxvTjruDibo88r5E1uwcickvD7jVVwXmwANBVCWZQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**第三步：删除“属性”列，拆分“值”列，以之前合并时候的分割符空格为拆分符，并修改拆分后的列名。**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMHxg0uxa5YhybNgQARnJfuA7zxYh6PfuRG8SK2bauwBntAX6F25Kibls6WGwZDtU8hEEcwvjqLuSQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就完成了一维表的转换。

上面的步骤很简单，不过如果列数特别多，第一步合并列将会非常繁琐。幸运的是，星友分享了一个自定义函数非常强悍（原创作者不详，如果作者看到这篇文章，可与我联系），通过输入几个参数，就可以一次性将这种结构的表转换为一维表。

自定义函数如下：

```
let
```

这里将这个自定义函数命名为“批量多列合并”，以上面的数据为例，只需要这样输入这几个参数：

-   第一个参数是需要处理的表
    
-   第二个参数是做几次循环合并(本示例做3次合并列）  
    
-   第三个参数是每次合并几列（本示例是每次进行课程和成绩2列的合并）  
    
-   第四个参数是前面固定几列不做合并（本示例中第1列姓名不需要合并）
    

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMHxg0uxa5YhybNgQARnJfu4IqJrhZuh5ibCYjd2TcgwmjGCRU5ej97HicGNfIyNTR4RTGQbU6cQrxQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后点击“调用”，就可以直接得到最终的结果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMHxg0uxa5YhybNgQARnJfuaFX5Yglh5ayG3yCNE0jmebeNricnmmfnTIOXIsNFNj77AlnT7FwYVgw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

是不是非常便捷。

关于这个自定义函数的逻辑，可以不去理解，只需要知道这几个参数应该输入什么数据就行，当你有类似的数据结构需要转换为一维表时，直接调用这个自定义函数就可以了。

本文示例文件请在公众号后台发送“PQ多列批量合并”获取。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你想深入学习Power BI，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和5000+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMstwXX5zrKianmFXzyqbIVgh7byfo3V8JJPmhqicywbtYkM0j2ibngnT5XBZ2AwKvGZiby9ngoKfLvzg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门Power BI》电子书，轻松入门。
