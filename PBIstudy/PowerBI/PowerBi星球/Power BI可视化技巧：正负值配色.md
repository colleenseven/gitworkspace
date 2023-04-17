---
create_date: 2021-06-26T19:51:10 (UTC +08:00)
tags:
aliases:
pagetitle: Power BI可视化技巧：正负值配色
source: https://mp.weixin.qq.com/s/EOqLcMZku9jsrIoQqBbmvw
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

周末分享一个PowerBI可视化的小技巧。  

用不同的颜色标识正负值，是数据可视化的一个很常见的需求，比如正常展示每日利润的柱形图效果一般是这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMpibMcWfz13TtsYoktOTnykNN8PyEsh64hQllCibJzZmrrrOONYk0yHP1YQqhQADYicAicOmKowd006g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

直接设置颜色，是无法分别按照数据的正负值来配色的，不过我们可以利用DAX来实现这种需求。

做起来非常简单，写两个度量值：

> 利润 正 = IF(\[利润额\]>0,\[利润额\],0)
> 
> 利润  负 = IF(\[利润额\]<0,\[利润额\],0)

把这两个度量值放入到【值】中，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMpibMcWfz13TtsYoktOTnykfcS5dfyibk43obu5QJHL0WfhqD0Eoz28ZrATPCFpiaeIDicwgZaG0ccUg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

并分别设置这两个值的颜色：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMpibMcWfz13TtsYoktOTnykcRSyQbgRkYrLrmnk8l0SyGS1rsUdERAv8NvVcuU9O800KbiaZEDJQrQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

就实现了正负数据分别着色的效果：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMpibMcWfz13TtsYoktOTnykZReNv6tRvpzKb3qkichVhORVLSmDhBLHW02mUNiaNgFooA8lD0aCImJw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

不仅仅是柱形图，还可以使用折线图来展现，为了让数据的走势看起来更合理，折线图的形状设置为“渐变”，就可以完成下面的效果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMpibMcWfz13TtsYoktOTnykuyCpJ7UW4AfjREy9mUXGwxJYwKL6E6T0lJwPiaHT5YUFibahupqkziccA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

对于折线图的0刻度线，为了让颜色统一，可以添加一条辅助线：在分析面板中，添加Y轴恒线：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMpibMcWfz13TtsYoktOTnykU4GQFfLwZvLnIsIZfLZFiccMz7bib0L9aZSvmJRfH1eQH8viczoUeRpBA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMpibMcWfz13TtsYoktOTnykHqQOgicNw5eLvdF38Vq0GyB6XQct7ibjIP6MjIKHR2vaibuxzKUl8AmBQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就轻松实现了折线图的正负值配色。

**掌握了上面的可视化思路，其实不仅仅是正负值分别配色，你还可以任意定义颜色显示的范围，**比如每日的利润目标是50，高于50的显示绿色，低于50的显示红色，同样的写两个度量值：

> 利润 超过50 = IF(\[利润额\]>50,\[利润额\],50)
> 
> 利润 低于50 = IF(\[利润额\]<50,\[利润额\],50)

把这两个度量值放到折线图中，并按上面的操作来设置格式，就可以得到这样的效果：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMpibMcWfz13TtsYoktOTnykOjodicZHr7PCGl9uDefBmPeOrOU1XnnwicWKVOiaBj6B1DdRCmyaUXxXQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

**[新书上市：PowerBI商业数据分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)**

帮你从0到1，轻松上手PowerBI

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOojexubCy39PJZJic24XlI9IC8Fhx57SVYiciave3T7sAxeLXXZgrAzhAsUHXC3dxpU1fp72ChD8ibfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072351&idx=1&sn=fabb08c54790ac1225b470fd647c7a5e&chksm=8e0c4548b97bcc5e0450f1945a2c76039bbb42650bcb1edbc856820836d63d32af4c7780e31a&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 3k+ 学习者一起成长
