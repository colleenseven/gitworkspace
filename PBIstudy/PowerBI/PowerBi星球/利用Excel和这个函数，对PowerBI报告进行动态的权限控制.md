---
create_date: 2021-08-26T22:45:09 (UTC +08:00)
tags: 
aliases: null
pagetitle: 利用Excel和这个函数，对PowerBI报告进行动态的权限控制
source: https://mp.weixin.qq.com/s/dFgkVUFEA7c5xXFOlCGh3w
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

关于PowerBI的行级安全性，之前已经介绍过怎么用，如果你还没有看过，请先看一下这两篇文章：  

[利用Power BI行级安全性，限制用户访问权限](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076638&idx=1&sn=04e90c833a99f5a0e9b2baa06b5c4a8e&chksm=8e13aa89b964239f010a579a4bfdb74ce2dd483b7d333d4a797ca03c12752ab75c1a0fa4e05e&scene=21#wechat_redirect)  

[Power BI行级安全性三种常见的角色规则设置](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076697&idx=1&sn=eac84b6115e8b0ee9dfa624e4b00f95a&chksm=8e13aa4eb96423589f27b1496d771af2ed526948113e7b9102ae79752c0c3bd4095e1ae1ad62&scene=21#wechat_redirect) 

有伙伴问能不能对每个账户的权限，进行动态的设置，让管理员能够更灵活的控制对每个用户的权限，而不用必须在角色设置里分别调整。  

其实还有个DAX函数USERNAME，它可以获取当前登录的账户，利用它就能够灵活的控制权限，这个函数也主要用于行级安全性。

假如这是在Excel中维护的一个权限表，有这三个账户，每个人可以查看的权限如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP4k1gIvITPJBm6SwiaeKK8ibzIZ25RVP79DyqW8HM7Dyia5PP7DrwaolT2YHwMdblJhBRqeCAxOo8dg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

以张三为例，它的权限是可以查看北京、上海的耳机和贴膜数据。将这个权限表，导入到需要控制权限的Power BI报告中，先在PowerQuery中将这个表整理一下。  

因为在Excel中为了方便录入和管理权限列表，让每个账户的产品权限和城市权限都挤在一个单元格中，现在需要将他们分开，可以利用PowerQuery的分列功能"拆分到行"来处理，比如选中“产品权限”列，执行按分隔符拆分列：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP4k1gIvITPJBm6SwiaeKK8ibDOj3h9fGZDyCphDdYhWcvjAlZcekMcC1N26SMECGGMtJhiav3hmwbicQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关于分列，可参考：[Powerquery数据处理：你应该会用到的分列技巧](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068514&idx=1&sn=19c0330d0855c4d9f2e4e065fa0ceab0&chksm=8e0c4a75b97bc3634aba27a8b52ae0b571bf81b438e4f1639d302543e23cfd42b65c3057fc42&scene=21#wechat_redirect)

对于“城市权限”列，也执行同样的操作，最终将数据整理如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP4k1gIvITPJBm6SwiaeKK8ibPHppZFOkk5thpUa0ABwh1oZ82IVibia7Tn0eM9BnQwvo6XTK2iagBNI6A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

权限表上载到模型后，不需要与其他表建立关系，而是写两个度量值：

```
产品权限 = 
```

  

这个度量值的逻辑是，通过当前登录的账户，筛选出它在权限表中可访问的产品名称列表，最后判断当前上下文的产品名称是否在这个列表内，返回一个布尔值。

同理，写一个城市权限的度量值。

```
城市权限 = 
```

然后创建一个角色“权限动态控制”，分别在产品表和客户表写入以下筛选表达式：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP4k1gIvITPJBm6SwiaeKK8ibNLQicGutSafXJrBKgOhywZu6SLrq147dYI3H1OSSPsJwLmEkjliaY7Tg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP4k1gIvITPJBm6SwiaeKK8ibYg0ia5CSz0WubK9OP2lHKvlLCcSImGPiaTVBU8oribQAQibFS8wyAUgA6g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样，按权限表的动态控制就设计好了，可以用“张三”的身份测试，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP4k1gIvITPJBm6SwiaeKK8ibibD7lv2wo4nZV9unBw5fDxu0AESmfDLW4g6QfMCVCgB5JrIEKClZwvA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP4k1gIvITPJBm6SwiaeKK8iblR6HwEBls9BicNFicUWyODllFm69DTouPDo8o6x5PeBRdx2V22azgtZw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

和权限表中该账户的权限是一致的。  

如果某个用户的权限需要调整，直接在Excel表中修改就可以，比如张三的权限增加“数据线”和“广州市”：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP4k1gIvITPJBm6SwiaeKK8ibeBO3ORJvaJ65qNy6sCC6cgdiaTpByPpyTia8CzB1WmGlpBNpNK4Diakxg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在PowerBI中无需再进行权限设置，只需要点击刷新，“张三”的报告就将显示为：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP4k1gIvITPJBm6SwiaeKK8ib4BJYeZ9CRZHvPg61lZ1j5LdicRfYMicD2VLju7umiaXegXO5qiaLKXU74A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

是不是非常灵活。

权限表可以根据自己的需要来设置，并不是必须是上面的格式，不过最终都要整理成类似一维表的样式，以方便获取当前用户的权限列表，并且权限表的格式一旦确定，不要随意改动，否则刷新可能会报错。

以上就是利用USERNAME和权限表动态分配权限的例子，利用这个特性，还可以有其他灵活的应用，下篇文章介绍一个更实用的技巧。

**[PowerBI商业数据分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)**

帮你从0到1，轻松上手PowerBI

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNuVIqc0mzbKDNPmI0mwcTkvUibMVjf4z1bY0MYFh7lAkqrcHiaEHE4UicvjJjibpmkxJjc4TDlVO04qg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOojexubCy39PJZJic24XlI9IC8Fhx57SVYiciave3T7sAxeLXXZgrAzhAsUHXC3dxpU1fp72ChD8ibfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077048&idx=1&sn=b3da0a4079ed8366c67982912e795d59&chksm=8e13ab2fb964223978c16d5647e4a28eaeb50bc7338c4e82f4e14f2cddc8bb844b956f09beb6&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

↑ 扫码加入，和 3k+ 学习者一起成长
