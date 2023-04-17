---
create_date: 2021-05-26T19:57:54 (UTC +08:00)
tags:
aliases:
pagetitle: Power Query如何从局域网文件夹中获取数据？
source: https://mp.weixin.qq.com/s/VkVqe0jamFDmNRdFMb62nA
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

最近有人在星球里提了一个有趣的问题：**PowerQuery如何获取局域网共享文件夹的数据？**

因为他需要在同一个局域网下把其他电脑里的文件定时拷贝过来再进行导入，太费时费力了，会员群里也有其他人实现这个需求，但他使用的是ftp，这个方法太麻烦了，今天分享一个更简单的方法。

以win10系统为例，假设同事A要访问同事B电脑的共享文件夹，操作步骤如下。

第一步：在B的电脑打开网络和共享中心-更改高级共享设置-对专用，来宾或公用：勾选两个启用。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMAOGgCF1hLCCOtIoVy4GjPMK7vateqrssB8Ohq63P391pA6ShcK9p4AEPiaSQFfameta89vUmWTyg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMAOGgCF1hLCCOtIoVy4GjP9ziaqfjFkBic70bBLhZlO6ib202kT8uFw4cgEr9PgPibq4eVuMxZDOYosw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

第二步：修改所有网络配置（所有网络都勾选启用，且密码保护的共享，勾选无密码。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMAOGgCF1hLCCOtIoVy4GjP2NuOXgo9U96bBeu0t0OderlbzucNdicurKQ5GN1EQnj5fmAlhgP3wDA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

第三步：选中要共享的文件夹，右键-授予访问权限-特定用户。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMAOGgCF1hLCCOtIoVy4GjP0oO8EicXiaV7QSWadLokENBia1enwFUDsTBbvZibY2BnPS6ztYYexDZJJA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

第四步：点击下拉框，添加Everyone用户，权限选择读取/写入，再点击共享。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMAOGgCF1hLCCOtIoVy4GjPSIicWiab23Xn8JTNqG3N9oZEfaibqHUEZNicBvzSwL5VlCXnMgwArsicRcw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

第五步：点击复制，然后将链接发给要访问共享文件夹的人，如同事A。（蓝色文字复制上有共享文件夹的路径）

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMAOGgCF1hLCCOtIoVy4GjPIGwkkzIl8WurnGq4mvDiczdls8Tpq7w62CMW1JjFyM7FiaJZkHibptokA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

第六步：测试，同事A将第五步中的路径粘贴在自己的电脑并回车，发现可以访问到，则共享文件夹设置成功。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMAOGgCF1hLCCOtIoVy4GjPxoso2WtgIMRpibiczQRbXicH4YnLMqkjLD4CAxTgpmpP5RIBj7mpaaNNg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

第七步：使用power query导入共享文件夹中的文件，可以成功导入，设置完成。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMAOGgCF1hLCCOtIoVy4GjP7Wus9nXsOt0vzlia8xUKhIuzWHjRiaRX0KQUXB36z3hcnK8bJDFQNBkw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

则通过以上步骤简单实现了PowerQuery连接局域网文件夹。

上面用的是Excel连接局域网的文件夹，其实如果使用PowerBI也是一样可以实现的。

注意事项：

**1\. 第三步所有网络的配置中，密码保护的共享必须设置为无密码保护，否则会提示输入网络凭据，且该凭据不是电脑开机密码。**

**2\. 主要是对共享文件夹所在的电脑进行配置，因为要在其他电脑上发现这个电脑，并有权限读取该共享文件夹。**

通过这个方法 可以轻松实现在同一个局域网内获取不同电脑或某一台电脑中的固定文件或文件夹，省去了文件跨电脑传输的动作，节省大量时间和精力。

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
