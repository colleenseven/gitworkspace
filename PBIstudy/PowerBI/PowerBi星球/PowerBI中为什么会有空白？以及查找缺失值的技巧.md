---
create_date: 2021-06-02T19:54:38 (UTC +08:00)
tags:
aliases:
pagetitle: PowerBI中为什么会有"空白"？以及查找缺失值的技巧
source: https://mp.weixin.qq.com/s/70svSa552ZYNYSdSjMQ_KA
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

使用PowerBI制作可视化时，大家应该对莫名其妙出现的"空白"项都不陌生，比如一个简单的模型，产品表与订单表是一对多的关系，产品表中是没有空白的。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPKiaueL5CbTwee21gWA7zVia9KbCPucx6v6phXA9UicUZLXG12icicia50A6ia12ks7ibfZOeX1OKhXxAhAg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

但使用这个产品表中的产品名称字段生成的切片器，却可能会出现个"空白"：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPKiaueL5CbTwee21gWA7zVia0SJcrp7HUV3dbCluBaCzxdMBqDHbKicNHWcIgibibBMoNaBicItzHf9Jcg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

为什么产品表中明明没有空白，切片器中却出现了一个"空白"呢？

**出现“空白”的原因是产品表中的产品名称不全：订单表中有某些产品，是产品表没有涵盖的，所以以"空白"项来补齐。**

并且用产品表中的产品名称来统计每个产品的销售额，也会有个空白行：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPKiaueL5CbTwee21gWA7zVia7brpKm8D4kaULTOzicia0iaUwwTtszR1XOxSblpC3cuuxGtG6IrM84N3A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

第一行的332337，就是订单表中存在但产品表中没有涵盖的产品的销售额。  

如果只是想让空白项消失，可以利用筛选器将其中的 "空白"项的勾选去掉：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPKiaueL5CbTwee21gWA7zViaOZllkVraHuUXmWcgwwKmqc1eHGval1cbjGCvAcaVntiaj6mErcwcPBA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

但这样并没有解决问题，大多数情况下，缺失部分数据是不正常的，我们需要将缺失的数据找出来并在维度表中补充完整。  

那么如何找到缺失的是哪些数据呢？下面提供两种方法，以上面的模型为例，找出产品维度表中缺失的产品。

**方法1、使用RELATED函数在事实表中新建列**

在订单表中，添加计算列：

> 产品 = RELATED('产品表'\[产品名称\])

这一列的逻辑是，在订单表中，将每一行所对应的产品表中的产品名称匹配进来，并在这一列中筛选"空白"项：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPKiaueL5CbTwee21gWA7zViao2uVgYvYWt6h4dWNG0BeRhlKXU1TKmiaBvfJzzm4WGVRvbh2e85mjicw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后就能在订单表中的产品名称列中，发现有"硬盘"和"鼠标"，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPKiaueL5CbTwee21gWA7zViaJCwKg01HicUsZ0gpKSicfNBHPjBY6VsM1fnM6qicGtA62JjIUyI5YD2QQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

那么这两个产品就是订单表中有，而产品表是不存在的，这样就找出了维度表中缺失的产品。

**方法2、利用可视化表格查找缺失值**

在画布上建一个表格，将订单表中产品名称和产品表中的产品名称拖拽进来，  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPKiaueL5CbTwee21gWA7zVia34YTl90yFlYnRs6OWXI3EicoTJGEic9SkT36DH0wKASWzrricryw3fbow/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

产品表中的产品字段列为空值所对应的产品名称就是未涵盖的产品，这样就能更加直观的找出缺失的数据。

找到缺失的数据以后，在维度表中补充完整，再制作可视化时，一般就不会再出现"空白"项了。

___

**[新书上市](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)**

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
