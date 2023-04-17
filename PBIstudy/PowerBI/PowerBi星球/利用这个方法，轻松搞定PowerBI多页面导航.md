---
create_date: 2021-05-12T19:59:43 (UTC +08:00)
tags:
aliases:
pagetitle: 利用这个方法，轻松搞定PowerBI多页面导航
source: https://mp.weixin.qq.com/s/FCMeTb0WHPtA2APDXvoqKQ
author: 瓶子
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

> 文/瓶子
> 
> 目前从事职考行业的数据运营，喜欢钻研power bi和excel来实现自动化。

一般情况下，报表制作人员可以通过使用书签和按钮结合使用来制作导航，用户可以通过按钮来切换页面，关于书签请参考：[PowerBI中的书签，真的非常有用！](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068219&idx=1&sn=b74e0d16ac61413a90fb5f7837dea112&chksm=8e0c75acb97bfcba745fe9ba7eb4ca2aa83d0af34a17668284170b97c68b2d3dc909dc9eb936&scene=21#wechat_redirect)  

但在工作中，一个报告往往不是几个报告页面，很多是十几个，几十个，甚至更多，比如这种：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMypeAicqV4wqf6qOKF1rC2ficQbC6PYiarMUJB7fzsNLXRYI7k6otCFeicTjQVp5aiaexKkIehuYAGEfw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

当报告页面多达几十张的量的时候，无论是报表制作人员使用书签和按钮制作页面导航或者是用户通过按钮或底部页面选项卡来查找报表页都是一项极其繁重的工作，大大降低了工作效率。

其实有个更简便的方法，只需要你轻轻点几下，即可实现去你想去的页面。

现在以这个PowerBI报告为例，它有三个页面：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMypeAicqV4wqf6qOKF1rC2fkXWko9xm4pVbuyYiaF3CEd3IQlJceJE2WVz6Q9fnzhia8PBRWsv2ibgpA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

下面是制作导航的步骤：  

1\. 创建一个表，表中只需一个列，每行填上各个页面的名称，以页面导航为表名，导航页为列名，如图：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMypeAicqV4wqf6qOKF1rC2ftcfrzCnhg3vhXeGHVXp42hiayr1FvwayJRI3xHvekYsSiagyYRBCCZww/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

2\. 在第一页添加一个切片器，并将页面导航表中的导航列添加进切片器中，修改切片器格式，选择下拉方式，选择控件为单项选择，如图：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMypeAicqV4wqf6qOKF1rC2f6WJNhmuXbib2ban3LSJyDibcZAmLxSriciakI1O8y2vsz6VuT8Jamvr5Wg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

3\. 在切片器右侧添加图像，并调整图像到合适大小，如图：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMypeAicqV4wqf6qOKF1rC2fEL3fH1dA5wiavUcdibwSOiax6lJInkGiaYlB4GMJpFNp72pak9iaAibeCzyA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

4\. 调整图像格式，修改图像操作类型为”页导航”，如图：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMypeAicqV4wqf6qOKF1rC2f6MKRN2QksUDaAwzkmNBqN9RcX5WrAFjHCMoaciaHTyAHf6VibMxDqWwg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

5. 修改图像操作类型的目标格式，调整为字段值，依据字段为页面导航表的导航页列，点击确定

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMypeAicqV4wqf6qOKF1rC2fl2Voa07VmK54SibzJSB7PuHNVYsXRBUbaiatPEwrLQUiaZoNPGDpHGoibQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击确定之后，显示如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMypeAicqV4wqf6qOKF1rC2fHeGiaMzFXLe5ZWrgeBIviac9Wsf17tdjVUF7oMNQOaGMBGXQfnQvibLyQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

6\. 将切片器和图像一起复制到其他报告页，在弹出的“同步视觉对象”窗口中，选择“不同步”即可，如图：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMypeAicqV4wqf6qOKF1rC2fH3t2af1P6VPKpkYUkLzHM1o7WiczMJKp6cshR2ZoCrDC51MhxLhzbPg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

操作完成，动态效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMypeAicqV4wqf6qOKF1rC2f9f9Ofw6jegj40HkV4Iz3CWjmmdn1qhpLr49FribAMXlrtP0pm4GvBlg/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

其实无论多少个页面，都是上述几个简单的步骤。

通过将报表页各个页面选项卡的名字添加进一个新创建的表中，然后使用切片器和图像的组合，有至少3个优点：

-   **节省时间**：无论报表有哪怕几十张甚至上百张报告页，都可以快速制作
    
-   **节省空间**：无论多少个页面，一个按钮搞定，占用画布空间大大减少
    
-   **灵活性高**：报告增加页面时，只需在表中相应添加行，而无需对报表做任何操作
    

本文介绍了一个巧妙设计思路，来处理多页面的导航问题，更多设计细节大家可以自行探索。

___

**[新书上市](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)**

帮你从0到1，轻松上手PowerBI

___

\-精彩推荐-

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072351&idx=1&sn=fabb08c54790ac1225b470fd647c7a5e&chksm=8e0c4548b97bcc5e0450f1945a2c76039bbb42650bcb1edbc856820836d63d32af4c7780e31a&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 3k+ 学习者一起成长
