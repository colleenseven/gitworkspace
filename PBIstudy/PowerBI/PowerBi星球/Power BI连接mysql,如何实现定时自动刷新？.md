---
create_date: 2021-05-17T19:58:49 (UTC +08:00)
tags:
aliases:
pagetitle: Power BI连接mysql,如何实现定时自动刷新？
source: https://mp.weixin.qq.com/s/noTCCaldPDRz3cscXEuQNw
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

最近在知识星球中有星友提问，Power BI连接mysql如何设置定时刷新？会员群里也有人问到，我安装了网关，但是数据刷新不成功，提示错误，如何解决呢？

正常情况下，Power BI连接sqlserver使用DirectQuery模式，可以设置自动刷新。然而现在很多公司使用的是mysql，Power BI连接mysql只能使用导入模式，导入模式和DirectQuery不同，不支持自动刷新。

今天我来汇总下解决上述问题的方法：利用网关实现数据的定时刷新。

以个人网关为例，以下操作步骤：

1\. 下载网关，网关app有两种，以第二种为例。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMAOGgCF1hLCCOtIoVy4GjP5OaP58EJarBvPFpamOnYrUrHyE5k4vXXGQVZibQVnymN5U6apIyUROQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

2\. 双击网关，点击下一步，网关类型选择第二种。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMAOGgCF1hLCCOtIoVy4GjPcv5gvQCJ2qNcnMiavG3PkKfoUprffkEDhGpf3nLxp8yTkslS2CU1RHA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

3\. 点击下一步之后，等待一段时间，出现安装路径的界面，不要更换安装路径，勾选我接受，然后点击安装。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMAOGgCF1hLCCOtIoVy4GjP7CIwsQ3Kt4kzn9lfjibL1TY8MOBqazDlTib4nP0V3TZxyTlym6NRQPNw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

4\. 填写Power BI账户，点击登录。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMAOGgCF1hLCCOtIoVy4GjPEibJNibzDOTOY4qGvJP2zX6UiadiaXPbIsIGYlO5icSNUia7kMpjtDbReyZw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

注意：如果出现找到一个现有网关的提示，不用管，可继续安装。

5\. 进行第4步之后，稍等一会儿会出现“网关处于联机状态且已准备就绪，可以使用的提示”。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMAOGgCF1hLCCOtIoVy4GjP74yOiawI1svfws0EQekdYQm6zatr3F3cAkYzV6Nxgr1T56nc9bW6JQg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

接下来很关键，有很多人这一步没有做，导致报错，数据刷新不了。

6\. 第5步出现的提示其实这是个假象，还需要进行一步配置，使用everything找到

Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config

这个文件。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMAOGgCF1hLCCOtIoVy4GjP7icTD3qkbJGr8bKyibicxF0V96n7TQN43VSSETFfuKuNN44xPrxbmHyibQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

将下面这段代码：

<setting name\="EnableFastCombine" serializeAs\="String">

  <value>true</value>

</setting>

复制粘贴到文本最下方，然后保存。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMAOGgCF1hLCCOtIoVy4GjPMC9Rd20tX12hp7Amfko8GKvxX2RIyBuQibMtUicbGfhlJeTr5xpNgxUA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

7\. 上一步文件配置之后，回到第5步出现的界面，选择服务设置，重启网关。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMAOGgCF1hLCCOtIoVy4GjPe2pPg1Mm4mHmQVqOQMhbrDI7wSq083UznhdDC85ia08dP0rGetQ009A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

8\. 登录Power BI服务之后，在数据集设置页面可以看到网关正在运行，凭据可以编辑。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMAOGgCF1hLCCOtIoVy4GjPyiaBwZZCHf5Vwibhy89vDvSruTMNZaKEkdTMCPujR1qegQqRs0Puhw1g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

9\. 编辑mysql凭据，身份验证选择Basic,用户名和密码选择数据库的用户名和密码。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMAOGgCF1hLCCOtIoVy4GjPTAhPA2ibXqJ1cWmJgOfYibSbiaDQgToW2O8hnZ62sgv4GV9KQjnfc4pOg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

10\. 可以在计划的刷新设置定时刷新，最多可以设置八次刷新。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMAOGgCF1hLCCOtIoVy4GjPoibshWibuyvWWvW05hNd6djOTRNrN4UNhNib5eKzzibRdxUeyWSyyvtC1A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

操作完成。

**注意事项：**

-   身份验证要选择Basic,然后填写自己数据库的用户名和密码，一定要确认自己的数据库账户和密码是否正确。
    
-   每天最多只能设置八次刷新，如果不介意不同时间段可以看不同的网页，可以设置3个链接，3\*8=24个小时，每小时刷新的目的也能达到。
    
-   个人网关不能关闭只能作为应用程序运行，而标准网关可以作为一个服务运行。
    
-   如果账户登录不上，可以多试几次，不是操作步骤的问题。
    

这种方法的优点：

-   定时刷新，免去手工刷新的烦恼，也能定时查看最新数据，实现数据自动化。
    
-   如果是大型数据集，也可以使用此方法，先上传一个小数据集，然后使用刷新的方法，将其余的数据刷新到Power BI服务。
    

如果你的数据库是mysql，不妨试试这种方法吧。

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
