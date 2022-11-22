---
create_date: 2021-08-05T22:52:57 (UTC +08:00)
tags: 
aliases: null
pagetitle: 利用网关实现Power BI报告的自动刷新
source: https://mp.weixin.qq.com/s/AW9OeOyQTTKssV8CeqjYMA
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

[上篇文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076841&idx=1&sn=f5159bfa6daa1653ffe2230476570156&chksm=8e13abfeb96422e81705fe6179af37165856193cc5ab1f993542dbfab7b4e8879d628a23dcd4&scene=21#wechat_redirect)介绍了如何利用PowerBI制作一个迷你的东京奥运奖牌榜，除了可视化技巧，如果你通过上篇文章的"阅读原文"链接，仔细看过这个报告，会发现数据是自动更新的，报告web链接如下：

https://app.powerbi.cn/view?r=eyJrIjoiMmY0YzQ4YTUtMjk2Ni00MDI5LTkxZmUtYjk3YjZhMWE5NDAzIiwidCI6IjNhN2Y1MzA4LTU0MDctNDU2Zi1iY2VkLTRlODI0NzJlMWIzZCJ9

这篇文章接着以这个奥运奖牌榜报告为例，介绍如何让PowerBI报告实现自动更新。

首先自计划刷新的前提是需要在电脑中安装数据网关（Gateway），你可以简单把网关理解为本地数据和云端在线报告连接的枢纽。

数据网关工作的基本原理是，它根据云端的指令，连接本地所使用的数据源，并将获取的数据推送到云端，实现云端数据集的定时自动刷新。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOr8u9Y3M0Vpfj89Q4jtb4qwsQqrM2SJzcnHbQsb0Ddy7Vozev3nMSX8PJ8wlibTn7t9SrGpxiaX3zw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关于网关的介绍以及下载安装、配置，可以参考官方文档：

https://docs.microsoft.com/zh-cn/power-bi/connect-data/service-gateway-onprem

这个文档以及其中的链接，详细介绍了网关安装步骤和可能遇到的问题，这里不再展开，大家可以自行下载安装配置。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMwuW4rAwk0IDuJSEZYTRE4DSicM14KPnABwED0qf4eJuicNLY7tVdA41eESQRB1ZdrbkNzVDGG4Fwg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

网关安装并配置完成以后，只需要简单几个步骤就能实现PowerBI报告的自动刷新了。  

**1\. 将PowerBI Desktop制作的报告发布到PowerBI服务**

PowerBI Desktop中设计完成以后，点击发布，将报告发布到PowerBI服务中。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMwuW4rAwk0IDuJSEZYTRE4Pf2w9OyLiaaMRQT0WrxhLKPPZtg8SvtkFWDpJFjgkib9EGn73gpqtR7Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**2\. PowerBI服务中设置网关连接**

登录PowerBI服务，在工作区中找到之前发布的数据集，点击设置：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMwuW4rAwk0IDuJSEZYTRE4UA5htibDiazB2SP05bJURX1AsWicUic4kNvVn4SEhcDadECjEnUpxNV2cg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后展开"网关连接"，下图是尚未配置网关的状态，点击右侧的操作箭头，

将此数据集所使用的数据源添加到网关，在弹出的数据源设置窗口中，会自动带出关于该数据源的信息，可以修改数据源的名称，如果有空白需要填写的信息也补充完整，完成数据源的添加。

然后再回到"网关连接"，将数据集映射到已添加的数据源中，点击应用完成连接。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPOyJNtWH9wJPEaXepYQRafZurYompnRUESug1XxuibR9tV3Jy54qe74WBn3y9FfoianjL0HXroXwkw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**3. 设置刷新计划**

依然在网关连接的界面，展开下方的"计划的刷新"，就可以设置刷新计划了，  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMwuW4rAwk0IDuJSEZYTRE4uJaPcFUl72xdIIvkh6sRPibp2PIicHMzFnqvTmnLHjFSVOPnQXC3BIibg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

免费以及Pro账户每天最多设置计划刷新8次，Premium账户高级工作区中的数据集每天计划刷新的上限是48次，间隔都是半小时的倍数，可以根据实际的需要设置每天何时刷新、一天刷新几次。

这里配置完成以后，PowerBI服务中的报告就能自动刷新了，在刷新历史记录中可以看到刷新的实际执行情况。

如果是可以公开的数据，你还可以将报告发布到web，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMwuW4rAwk0IDuJSEZYTRE4whPq5vicKJqykibLD90KWiapmiaRGMowbk94Tibzj4Alu7AD40q3DMDQhrw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后就会得到一个网址，生成如同这个奥运奖牌榜一样的公开在线报告，并且报告的数据是按照既定的刷新计划定时更新的。

最后，还有一个小细节，为了在报告中显示每次刷新的具体时间，可以在报告中利用M函数生成一个数据：

> DateTime.LocalNow()+#duration( 0 , **8** , 0  ,0 )

这个公式在本地时间的基础上加上8个小时，目的是为了在线报告中能按中国北京时间来正确显示，把这个时间添加到报告页即可（关于在线时间的问题参考：[Power BI服务中时间显示错误的解决办法](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070077&idx=1&sn=a26e7dda64f27e5116524d63e2684f82&chksm=8e0c4c6ab97bc57cc6d7a58e7d7715f143e6802c1fa9b6b464beb7d6fee6cc39adcc6513a680&scene=21#wechat_redirect)）。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPOyJNtWH9wJPEaXepYQRafvW3IicTeRWgZmlklumUVdmpZjxHZDrbt9G5AyYNGR70NouEnGC7YK8A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

通过以上的设置，就实现了一个自动更新的PowerBI在线报告，它不需要在本地重新发布，甚至不需要打开pbix文件，就会按计划定时刷新数据。

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOojexubCy39PJZJic24XlI9IC8Fhx57SVYiciave3T7sAxeLXXZgrAzhAsUHXC3dxpU1fp72ChD8ibfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtTuz8KBs1WLQiaGY8A0XAV02IfuoqQNQHr0UHvPPOZWSOticN3kyGkR6g/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484069195&idx=1&sn=2efa6240de0dcd522edef3ac7e5650fb&chksm=8e0c499cb97bc08ae20b16fc5528f9420ca02ade398d95b4d1d952fdb111d8cc65e06029f4b6&scene=21#wechat_redirect)

[](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484069915&idx=1&sn=57c8d756ba43f7bb21860eccc908ec1c&chksm=8e0c4cccb97bc5da9b6e3452d50f1e5062ed3574dc429149902f5f413ec6f7c8bdb0a88b326c&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

↑ 扫码加入，和 3k+ 学习者一起成长
