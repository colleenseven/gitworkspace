---
create_date: 2021-06-04T19:54:14 (UTC +08:00)
tags:
aliases:
pagetitle: PowerBI Web端报告快速刷新技巧
source: https://mp.weixin.qq.com/s/IsaFCVW-4lUTnVLgJVGSLQ
author: 瓶子
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

> 文/瓶子
> 
> PowerBI星球嘉宾，目前从事职考行业的数据运营，喜欢钻研power bi和excel来实现自动化

工作中经常遇到需要将报表发给其他人看，而他们并不一定会有Power BI账户，此时可以使用发布到web的方式，如果有自己的网站，也可以把报表嵌入到自己的网站。

如果你还不知道如何发布到web端，这里先简单介绍一下。

打开Power BI服务，找到要发布到web的报表，然后点击文件>嵌入报表>发布到web（公共），

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNBCBia3zPkZCSJdYTRH0E9EoBqM6C19jTyibEDImyQQEEygtQic3ITYMxFf48A4rCCHvIqwBlyicSsow/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后依次点击创建嵌入代码->发布，会出现一个弹框提示“成功！你的报表已准备好用于共享”，如下图：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNBCBia3zPkZCSJdYTRH0E9ENfMSEWn1icchltJfu31pXh3cvo5hDzF4spZV1rEn2ednKE0JM69Jcxg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其中第一个链接可直接粘贴到网页查看报表，第二个HTML代码可用于嵌入自己的网页。

通过以上步骤就成功将报表发布到web，如果你想将报表嵌入到自己的网页，以博客园为例，写文章时点击“编辑HTML网页源代码”，并将上面的操作生成的HTML代码粘贴到HTML源码编辑器中，并调整宽度和高度，然后点击更新，就嵌入到网页中了。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNBCBia3zPkZCSJdYTRH0E9E5AypCaO3LW5fnwE1qzVFfAcSFBmgAGusriajDYzJKGtzk27MsibGUK6w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

当我们将报表发布到web或嵌入到网页时，更新报表后是无法在web端立即在网页上查看到更新后的内容，因为系统会有一个小时左右的数据延迟，也就是需要等待大约一个小时才能在web端看到更新后的内容。

有没有办法可以立即让web端的报告立即刷新呢？当然也是有办法的，只需要下面两个步骤。

第一步，在PowerBI desktop更新数据并发布到Power BI服务后，点击编辑按钮。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNBCBia3zPkZCSJdYTRH0E9EbAQI0KtCELvdYlWJRDLnXzQwKKUtaCZ3L2MCzl4f5KUtpleK8VsW7A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

 然后在页面右上方出现保存按钮，点击保存，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNBCBia3zPkZCSJdYTRH0E9EL7jxEk7J0bkkpENv2ytafXy82JaqOYmibn2Lgg0FzV0dW1A38Qy5edA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

保存以后，你再打开Web端的报表，发现数据已经全部刷新了。

通过简单的两次点击操作，即可实现web端和嵌入网页端的报表数据的即时刷新，是不是很方便呢？ 

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
