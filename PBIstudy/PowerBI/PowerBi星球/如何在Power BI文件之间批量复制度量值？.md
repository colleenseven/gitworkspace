---
create_date: 2020-09-27T20:36:20 (UTC +08:00)
tags:
aliases:
pagetitle: 如何在Power BI文件之间批量复制度量值？
source: https://mp.weixin.qq.com/s/eNDMo26svlOTM1uiH-8jjw
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

这几天在星球里面分享关于Tabular Editor内容比较多，应星主邀请，编辑一篇关于TabularEditor 常用功能的文章。  

星主之前介绍计算组的时候已经提过这个工具了：

[PowerBI发布重磅更新，一文带你熟悉计算组怎么用](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072054&idx=1&sn=d403fdef264cbfb6fca46d33bd0083b9&chksm=8e0c44a1b97bcdb7fe466afe90d0f3d4b86738a0da7241f9125d4f36a1fcbd89c094b7ea42d8&scene=21#wechat_redirect)  

Tabular Editor可以建立计算组，编辑DAX函数，但是当你深入去了解Tabular Editor的时候，你会发现它更多有趣又好玩的功能。

  
对于PowerBI的普通用户来说，PowerBI自带的表格编辑功能已经很好用，但是当你需要处理大量的数据，如新建10条、20条甚至更多条度量值的时候，或者说当你想把一个文件中的某个表中很多个度量值复制到另一个文件中的时候，你会发现PowerBI自带的功能效率很低，甚至无法实现。

而利用Tabular Editor则可以轻松实现批量复制度量值，这篇文章就先介绍一下Tabular Editor的这个功能：

操作步骤如下：

**第一步：分别打开要处理的两个PBI文件.**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0f2a9PeaPdvlPTZewQ455rSRtMECopLNlU7Ea610QibdSvf9SX1gpicEibgiaXvNFic8dY0FQbGnqDmQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

目的要将转化率2文件z14度量值表中的度量值复制到转化率1文件z14度量值表中。

**第二步：使用外部工具Tabular Editor分别打开需要处理的两个文件。**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0f2a9PeaPdvlPTZewQ455iaYlcVqPtCOjqhSRdFRX0dj4NuHCDuGiaBhIhkrYMMaibTB7icSIfAGBkQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**第三步：点选转化率2文件中其中一个度量值，使用Ctrl 或shift多选，然后Ctrl+ C复制。**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0f2a9PeaPdvlPTZewQ45545ibGia5RJkTCPibVicT29YSc171tzqIKAFnc2hj52BrRc9mWJKlkUY0Gw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**第四步：切换到要粘贴的另一个Tabular Editor界面，粘贴进去。**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0f2a9PeaPdvlPTZewQ455HWMs6HsROrvLerww3icRkVNoj9eic8TjJ8qKYsHJxvkZwzaibvaibrWGbg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0f2a9PeaPdvlPTZewQ4555ia6lbvzmvbwx8fe80LdphfHyI9kqFF0I6jKNT9HQfuZLl7kM1DHbWw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**第五步：点击Edit下面那个紫色按钮或按Ctrl+S保存修改。**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0f2a9PeaPdvlPTZewQ45534WsOOicgrkzhqDBMh5FPiaXPG6gpFKEAssdu4EHIUYeomTqFic8wOl3w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后来看一下两个文件对比效果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0f2a9PeaPdvlPTZewQ455X4A32QYic1ictia8uibH4jibq7XP9j8yKFogAojsdSvQVIRRaKquS1aD6Tw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

度量值已经成功复制过去了。  

**注意要点：**

a.  如果两个文件中的表名不同，度量值和使用的视觉对象会报错，需要去修改。

b.  也可以直接复制度量值表，步骤和上述步骤相同。

当理解度量值可以批量复制粘贴到另一个文件，此时可以联想到同文件内是否可以批量复制粘贴呢，答案是肯定的，并且可以选中某一个度量值，按F2直接重命名。

以批量复制转化率2文件中9月大搜度量值为例，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0f2a9PeaPdvlPTZewQ455MtJibLrIFHX3rsHSDobhiagaJ5L6H1R74VQTDrricMrYOaLPEjP2FlXUg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

步骤是类似的，先打开Tabular Editor,选中要复制的度量值，然后粘贴  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0f2a9PeaPdvlPTZewQ455yXiaOysCOK7YDyJtR2Uoq3qWZcVmebYVYHwxpgxCaOjJGiapXALdiaoJg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

看下效果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0f2a9PeaPdvlPTZewQ455ThfhPTA0m9xprvvodGxIu8GvId5fWYNcp3gEclNXIKU3yhLQ4RicQnA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后点击Edit下面那个紫色按钮或按Ctrl+S保存修改，在PBIX文件中就可以看到多个复制的度量值了：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0f2a9PeaPdvlPTZewQ455PUxQNMCF5GYQictA4ROreqP1h160Ky77fibtQpMibSTo0vn2wvKyne2YA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

按上述步骤复制数据列、数据表的时候不适用，估计是软件的不完善导致的bug。

其实TabularEditor的功能很多，除了复制度量值，还有其他好用的功能，下面也一并简单介绍一下另外两个好用的功能，希望能起到抛砖引玉的效果。

**1、批量重命名**

打开Tabular Editor,选择要重命名的度量值或列或度量值表名，如修改DDtpyenew列名，  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0f2a9PeaPdvlPTZewQ455CFBaAvATwsrjZB7ZlveHv7FRXicVUbm6DicJSUeuPhnkox4437tkzHmA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

选中它，按F2即可重命名，然后保存修改即可，效果是这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0f2a9PeaPdvlPTZewQ455An2zFjdXIPoicBv8tOOzib27WeTVQA7EwT63OliaGu8dFZ4iaZClVicMNNQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

注意：重命名数据表名时保存不成功，即无法重命名数据表名，如dsjcrm user\_DDtypenew，估计是bug，软件不完善导致的。

**2、批量管理关系**

假如有这样一个关系模型，这些关系需要重新梳理，先删除所有的关系，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0f2a9PeaPdvlPTZewQ4559sDe79ficp3ImuAFA8ibQnq4Y1qrSxON8557bgB41P4ATkNub1npQquA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以在PowerBI中一条条删除，也可以利用Tabular Editor批量删除。

先选中需要删除的关系，可以使用shift或Ctrl键多选，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0f2a9PeaPdvlPTZewQ455L9IFp0eSxxkibtmm3SLUwLZjesYodQ9F0xswYNtjvwcdqBQWZBlr1wg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后右键Delete可以选择删除。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0f2a9PeaPdvlPTZewQ455EtC0xibSZJCCwaLIBvxYwISzUYQdmHDQJQib2ZEdTZbgHicxNhVia3FzxQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击保存就可以了，看下最终效果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0f2a9PeaPdvlPTZewQ455Y0ucZ6K0oBrveYCQuoqsanMAFy4GqMEvrxxqdicP0GyUrictI6iafAadQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关系线全部没有了。

理论上也可以新建关系，但可能会出现报错的情况，没有使用建模视图建立关系方便。

**你可以在公众号后台回复“****TabularEditor****”，获取Tabular Editor最新版本的安装包。**

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtHORfNDsk1ibQ1luXtyibbDsnnwJXvdSpKwfPlcJCZSlvWYOK6p6VGeqw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和2.4k+ 学习者一起成长
