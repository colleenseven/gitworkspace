---
create_date: 2021-07-19T19:41:44 (UTC +08:00)
tags:
aliases:
pagetitle: 利用Power BI行级安全性，限制用户访问权限
source: https://mp.weixin.qq.com/s/LnPrm4ipm_M21TU0KZaK_g
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

Power BI报告有多种分享协作方式，不仅可以让用户查看报告的所有数据，还可以根据用户角色进行数据限制，让特定用户只查看部分与之相关的数据。

按角色分享用到的就是PowerBI中的行级安全性（Row-Level Security，RLS）,本文就来介绍一下这个功能是如何使用的。

**首先使用行级安全性的前提是，报告分享者和查看者都应具有PowerBI Pro或者Premium账户，且在一个组织内。**

以这个PowerBI报表为例，展示的是每个产品销往各个地区的销售额，该报表需要分享给各区域人员查看，为了限制用户的访问权限，让各区域负责人只能查看本区域的数据，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPBO6wTjsAnvQrQtib8AqrRN3fmCUWGRw0PoJlNavX7I2kD876jKUvRGmuczOr65xW61TzEBRD8icxA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**这种情况下，并不需要为每个区域制作单独的报表，只需要制作一个完整的报告分享出去，利用行级安全性，如果张三负责上海地区的销售，那么张三收到的报表，只含有上海的数据，是怎么做到的呢？**

根据这个场景来看看按角色分享的操作步骤。

**1、在Power BI Desktop中创建角色**

进入【建模】选项卡中的"管理角色"功能：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPBO6wTjsAnvQrQtib8AqrRNCVlMkKVPtwgAAsia7upg8D7Cxw3icFgG2RKRjwfO0aZ7DibhH4hcLliaWg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击创建，建立一个角色：上海区域。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPBO6wTjsAnvQrQtib8AqrRNOyXHrQErJTPoUOdialQXKbk4YtWLUBkfqBSxkav816vXlpdsbX8nOqA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**2\. 在Power BI Desktop中定义角色规则**

对"上海区域"这个角色,如果只查看销往上海的数据，可以对客户表设置规则，点击客户表右侧的三个点，添加筛选器：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPBO6wTjsAnvQrQtib8AqrRNdlhyBRRkCWicOX1jRehMnxS2uNuMtiaA23KmvDOLOibg29ZcKtT6kxSng/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

设置规则为：\[客户城市\] = "上海市"

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPBO6wTjsAnvQrQtib8AqrRNOibDibKzrnKCXLQFQU8ZkXsr871KiaRrYks9MPtO9qic4NvV2JL4uBbCog/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样上海区域的规则就设置好了。

我们可以点击“通过以下身份查看”，来验证这个规则：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPBO6wTjsAnvQrQtib8AqrRNUUwPsdQUYkqaF60BibJNfEniacmoleydx7IXNb86XGjD8x59lEt2by8w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPBO6wTjsAnvQrQtib8AqrRN3jfibS367fqN4MDian6WVnVicwXpK4XQ63EFfJyKzUD2OiaicITQeibNsJcg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

角色身份选择为上面创建的“上海区域”，报表的数据就会变成只有上海市的：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPBO6wTjsAnvQrQtib8AqrRNJcicFADVRNAE4yMdPw5Aezzq0rdqmJuFTtpTNBvQQC7nibWpnLRDuVnQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

当你点开数据视图，也会发现，和城市相关的数据都变成了只有上海市的数据，**所以定义角色，实质上就是筛选数据，该角色只能查看符合条件的数据行，因此称为行级别安全性**。

在PowerBI Desktop中创建角色并定义规则后，将报告发布到PowerBI服务的新工作区中。  

**3\. 在PowerBI服务中，为工作区添加"查看者"用户。**

登录PowerBI服务 ，找到上一个步骤发布的目标工作区，点击“访问”：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPBO6wTjsAnvQrQtib8AqrRNrJk79vrCLAPzBOKic6LAdQ3w3H2nfHOvwueuNjTU6bWWE6uJ8V0Vricw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

输入张三的账户，设置其对该工作区的访问权限为“查看者”，  

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

访问权限有四种，上图中的前三种，管理者、成员和参与者对数据集都具有编辑权限，他们可以查看所有的数据，所以行级安全性不适用于他们，**必须将该用户设置为"查看者"，相当于只读权限，只有这样行级安全性才会生效**。  

如果想让某个账户查看所有的数据，可以在这里将该账户设置为"成员"或者"参与者"。

**注：这个步骤其实在建立工作区的时候就可以设置每个用户的访问权限，不必在创建角色之后。**

**4\. 在Power BI 服务中为角色分配用户**

在目标工作区中，找到该报表的数据集，点击右侧的更多选项，设置"安全性"：

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

然后就会看到该报告中已设置的角色"上海区域"，输入张三的账户，点击添加并保存:  

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

点击角色右侧的三个点，同样可以在不登录该账户的情况下，测试该用户可访问的数据效果，

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

至此，行级安全性设置完成，当张三登录自己的账户，就可以看到分享给他的报表，当然，报表中只有上海的数据。

以上就是利用行级安全性限制数据访问的通用设置方式，关于角色设置、访问规则等更多用法，下篇文章接着讲。

___

**[新书上市：PowerBI商业数据分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)**

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
