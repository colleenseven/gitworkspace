---
create_date: 2021-06-10T19:53:23 (UTC +08:00)
tags:
aliases:
pagetitle: 利用Power BI计算组，动态切换各种范围的数据标签
source: https://mp.weixin.qq.com/s/BYpF84lDCPVy-8CisMdCPg
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

[上篇文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076121&idx=1&sn=505f2d704bb46b641d21900a1fa9c3f6&chksm=8e0c548eb97bdd985786642ae697183cda036d6418757981aea2a380921a78b2af3d59b6cc7a&scene=21#wechat_redirect)介绍了利用计算组动态显示最高点和最低点数据标签的案例，其实还可以进一步展开，利用切片器来动态的展示不同范围的数据标签。

比如设计动态的切换，可以显示全部的数据标签，也可以只显示最高最低点的数据标签，甚至还可以设置，显示最高的前20%的数据标签。

这同样可以利用计算组来实现，依然使用[上文](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076121&idx=1&sn=505f2d704bb46b641d21900a1fa9c3f6&chksm=8e0c548eb97bdd985786642ae697183cda036d6418757981aea2a380921a78b2af3d59b6cc7a&scene=21#wechat_redirect)中用到的模型，在Tabular Editor中接着操作。

**1\. 增加计算项**

在之前已经建好的计算组“数据标签”里面，新增两个计算项："全部"和"前20%数据"。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN18cQkGaiat9nwicogeOGOJACELm6sCHibXr878aktrTk8726icd5BucxiacGsTfJVVvZjhsrDgCZibQdA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**2\. 设置计算项的逻辑表达式**

对于每个计算项,其逻辑表达式都一样，都直接写:

```
SELECTEDMEASURE()
```

就可以了。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN18cQkGaiat9nwicogeOGOJAickcSUr4nGFIibibx9wz7L7ibhqxctkJkqIgXO7SDctnZ1TJKRCqqYEYsQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**3\. 设置每个计算项的格式表达式**

选择计算项"全部"，它控制显示全部标签，不需要特别处理，就比较简单，直接写：  

```
SELECTEDMEASUREFORMATSTRING()
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN18cQkGaiat9nwicogeOGOJAr28MEYtJiaFEoGxySA0ib3cNszSf25FZZV5oQ6Gdexsg8k0zzdqicoicDA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后选择"前20%数据"，其格式表达式代码如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN18cQkGaiat9nwicogeOGOJAw9X5Ar2EJjDsmTKR0L9HG8MzkfhJmibibRfzfCepFNBQia1m7JsoMx7zw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**其逻辑与最高最低点的格式逻辑类似，不同的只是判断条件，大于等于最大值80%的部分，显示数据标签。**

然后点击保存，退出Tabular Editor，并在PowerBI界面刷新，就能实现下面的效果：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJN18cQkGaiat9nwicogeOGOJA4QpibLTBfCVIolMa39AVlju4QDLmNYmuJUkV2qUegeW2fVh5l2Lhg8A/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

通过变换切片器的选项，来动态的显示不同范围的数据标签。  

当然这种方式不仅仅对于上面的面积图或者折线图有效，切换成柱形图也是一样的效果：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJN18cQkGaiat9nwicogeOGOJA9U0iccibgtLkGlYKQwFaMM6w4NHWIkG5qoX6HYmzwAtjk0QOVwHKLArA/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

利用DAX计算组，可以实现很多个性化的视觉效果，而这些在原来的功能下难以实现的，以后也会分享更多计算组的玩法。

___

**[新书上市](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)**

帮你从0到1，轻松上手PowerBI

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOojexubCy39PJZJic24XlI9IC8Fhx57SVYiciave3T7sAxeLXXZgrAzhAsUHXC3dxpU1fp72ChD8ibfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072351&idx=1&sn=fabb08c54790ac1225b470fd647c7a5e&chksm=8e0c4548b97bcc5e0450f1945a2c76039bbb42650bcb1edbc856820836d63d32af4c7780e31a&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 3k+ 学习者一起成长
