---
create_date: 2021-08-28T22:44:42 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI页面级权限控制，其实只需要这3步
source: https://mp.weixin.qq.com/s/F6aJLTNdfJjm52F2WdnlwA
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

平时被经常问到的一个问题，就是PowerBI能不能按页面进行权限控制？比如A用户只允许查看报告的第2页，B用户只能查看第6页等，PowerBI本身是没有这个功能的，行级安全性（RLS）也是只能限制数据行，并不能按页面来控制。  

不过既然行级别安全性能控制行，我们就利用这个特性，**让每个页面的名称作权限表的行，不同的用户能看到不同的页面名称，然后利用导航跳转到对应的页面**，不就可以实现了吗？这也正是本文页面级权限控制方案的基本思路。  

运用这个方案需要先熟悉PowerBI的RLS功能，关于RLS我前面已经做了足够的铺垫，如果你还不熟悉，请先阅读这几篇文章：

[利用Power BI行级安全性，限制用户访问权限](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076638&idx=1&sn=04e90c833a99f5a0e9b2baa06b5c4a8e&chksm=8e13aa89b964239f010a579a4bfdb74ce2dd483b7d333d4a797ca03c12752ab75c1a0fa4e05e&scene=21#wechat_redirect)  

[Power BI行级安全性三种常见的角色规则设置](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076697&idx=1&sn=eac84b6115e8b0ee9dfa624e4b00f95a&chksm=8e13aa4eb96423589f27b1496d771af2ed526948113e7b9102ae79752c0c3bd4095e1ae1ad62&scene=21#wechat_redirect)  

[利用Excel和这个函数，对PowerBI报告进行动态的权限控制](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077172&idx=1&sn=9f82dd1b006ed613bf2dacba7a3db23b&chksm=8e13a8a3b96421b5c52b26cba6618d30000474c6f5c90bb85423f51deab9bc04457965e5caf4&scene=21#wechat_redirect)  

下面就让我们开始吧。

___

以下面这个PowerBI报告为例，正文报告有4个页面，页面名称分别为**整体、电脑外设、手机配件和智能设备**：

**1、导入权限表**

首先在Excel中制作一个页面权限表：

在权限表中，张三可以查看电脑外设页、手机配件页；李四只能查看智能设备页；王五可以查看所有页面。  

将这个表导入到PowerBI中，并利用PowerQuery的分列功能整理成下面的一维表样式：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNGzajt0LEeIK21oPd2wmggSnZT6ggXe5QNLCIdo7iaLBOb7cvuxqIJUKice81LvHrtEIgk9Zfvp8qw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其实你也可以按这个表的格式录入到Excel权限表，直接导入使用，不用在PowerQuery中整理了。

**2、创建角色**

创建一个新的角色"页面控制"，表达式非常简单，直接在页面权限表添加一个筛选条件：

```
[账号] = USERNAME()
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNGzajt0LEeIK21oPd2wmggIkrwEAsdYicu8TSaibGmCPGeCbwJt7YYS0Aozsz2r0tUPmh8B9vQfQlw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**3、设计封面页**

**因为是按页面控制权限，这个报告中原有的4个页面不能直接展现，要全部隐藏起来，取而代之的是设计一个封面落地页，让用户先看到该页，然后再根据权限导航到相应的页面，所以，封面页非常重要。**

在封面页中，利用权限表中的“页面权限”字段，添加一个切片器，这个切片的内容来自权限表，根据角色规则，它会随着不同的登录账户，返回不同的内容。

然后在切片旁边添加一个按钮：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNGzajt0LEeIK21oPd2wmgggQicVqj1NcwLYA0vReibjczVRMc8vpfnAySxmULX0OkXu3AwoIMUGVBQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

设置按钮的操作属性：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNGzajt0LEeIK21oPd2wmggVSA0icCAsscWQVsfibO8koSyPTGNh61ynmyrAicNt7APgBuIaAKJkJ6Mg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在【类型】里选择“页导航”，【目标】里放置一个度量值，它的写法为：

```
页面导航 = SELECTEDVALUE( '页面权限表'[页面权限] )
```

这个度量值很简单，返回当前切片器的选项内容，**但【目标】里可以放度量值，这个功能非常关键，可以说是这个解决方案不可或缺的一环，利用它，才可以实现点击按钮，导航到切片器所选的那一页。**

至此，所有的关键节点都已经部署完成。

关于封面页，既然是每个用户打开报告第一眼就看到的，要尽量做的高上大，可以找张图片在PPT中设计好，作为封面页的背景，将切片器和导航放置到相应的位置上，一个按页面级权限控制的报告就设计好了：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNGzajt0LEeIK21oPd2wmggiaeNjicHyD4dz2kSKqCBSIvfCxgFEK2TnUb9W5r0SHnBERYEEMdwxjfQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

还可以用度量值将当前登录的用户名显示出来放到封面上：

```
当前登录用户名 = 
```

然后将这个报告发布到相应的工作区中就可以了。

___

_某个夏日的午后，张三喝着咖啡，打开电脑，登录自己的PowerBI账户，查看他负责的业务进展情况：_

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNGzajt0LEeIK21oPd2wmggPFic5G3rNqHNTQ2EIRpibs7l15VB3hnaTYYqhSK5kLysTllAnsoS51Rw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

_一切都是那么的自然。_

_全神贯注的他，浑然不觉此时的李四，也打开了这个报告，看着与他完全不同的内容……_

___

同样，当有用户需要调整页面权限时，只需要在Excel中更改就行了，如果不在权限列表中的用户，也打开了这个报告，那么他只能欣赏一下封面，什么都看不了：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNGzajt0LEeIK21oPd2wmggBZJ9QesKhCiaHMgI9IcJGctnicXFxGyiaVKfds9OjSY3urX0gXVz6cbRw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个方案并不复杂，灵活运用了PowerBI中的常用功能，行级安全性是灵魂，动态页导航是关键。

本文介绍有总体思路，也详细描述了操作细节，希望能帮你设计一个页面级权限控制的PowerBI报告。

___

**[PowerBI商业数据分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)**

帮你从0到1，轻松上手PowerBI

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNuVIqc0mzbKDNPmI0mwcTkvUibMVjf4z1bY0MYFh7lAkqrcHiaEHE4UicvjJjibpmkxJjc4TDlVO04qg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOojexubCy39PJZJic24XlI9IC8Fhx57SVYiciave3T7sAxeLXXZgrAzhAsUHXC3dxpU1fp72ChD8ibfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNNJia1fBccdeD4HTtvAuUibkNI6YYicVJ3RPhufJhoh3lzY1e1dgUyxy6yGkk4UvZcuTfVGTc89iaI3Q/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077048&idx=1&sn=b3da0a4079ed8366c67982912e795d59&chksm=8e13ab2fb964223978c16d5647e4a28eaeb50bc7338c4e82f4e14f2cddc8bb844b956f09beb6&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072351&idx=1&sn=fabb08c54790ac1225b470fd647c7a5e&chksm=8e0c4548b97bcc5e0450f1945a2c76039bbb42650bcb1edbc856820836d63d32af4c7780e31a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

↑ 扫码加入，和 3k+ 学习者一起成长
