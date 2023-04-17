---
create_date: 2020-11-26T23:45:49 (UTC +08:00)
tags: 
aliases: null
pagetitle: 利用PowerQuery，批量合并多个Excel的指定列
source: https://mp.weixin.qq.com/s/CGuKaHdjUe6gevqSI71YKQ
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

PowerQuery批量汇总多个Excel工作簿的功能非常实用，即使没有学习Power BI，也应该学会这个功能，如果你还不会，可以看看这两篇文章：

[使用Power Query是一种什么体验？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067120&idx=1&sn=4188548c00910c7e9fd1cb5c2d5f8880&chksm=8e0c71e7b97bf8f135ea0bc07fff83152b9cf0ecc24b504eff1f999d92b65b58d0a4939c2c84&scene=21#wechat_redirect)  

[批量合并Excel，PowerQuery的这些技巧你应该掌握](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070803&idx=1&sn=826d571e4133872ff3bedb4ad4d524f9&chksm=8e0c4344b97bca5281787e9a0cf1a3f2571227316537b1ba7069c5bf5f600d4a4249cfc18932&scene=21#wechat_redirect)  

虽然刚开始练习时，有可能会碰到各种各样的问题，但仔细看看上面这两篇文章，并熟练运用，应该能满足90%以上的Excel合并场景，除非你的数据源非常不规范。  

数据源不规范的一种形式是，每个表的字段是不完全一致的，比如下面示例中的这几张表：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOMtH0lCwDNibY6eFMNJRb6VggCR9qNfQDIiczeXEK6oleuJfSV72TJH9Vn8odeHkt3gqB8D9UvjOzQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这三张表的字段数量以及先后顺序都不一致，如果直接合并，就会是错乱的汇总结果、或者直接报错无法汇总。

这种情况比较常见，曾经多次有星友问过这个问题，之前给出了一个用M解决的思路（[PowerQuery：批量合并Excel表的指定列](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068880&idx=1&sn=2267bb651cdf93cf25bad76c31d685ac&chksm=8e0c48c7b97bc1d14df21a8360a9c43fd95d14bcec42a61c9529b382aad6d53c1d0821cf5871&scene=21#wechat_redirect)），略显复杂并且不够灵活，本文介绍一个更简单的方法。

以上面的数据为例，我们从头开始，再详细介绍一下PowerQuery批量合并的操作过程。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP8VjcxLFjQCpHWQPLjmlhlxWUdicuMbtQgMBkpzNskSumpttWAhicSpwLibt4jj69RbpXwF8BbvAVaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 获取数据>文件夹

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 点击“转换数据”进入PowerQuery编辑器

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP8VjcxLFjQCpHWQPLjmlhlFsVEv3aaxwc0EMWjmted1YDN1R8Qu4sv5htiaGPIJV346Y2cpeb28KQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 添加列>自定义列

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP8VjcxLFjQCpHWQPLjmlhlfgzQ2fI6gfAsCu0E2csWds2mIk8JLFwKR7YwZJlRnTjmL5RibQWq8Wg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 自定义列公式：Excel.Workbook(\[Content\],true)

**这是最关键的一步，平时使用Excel.Workbook来解析二进制数据时，第二个参数常常是省略的，但这里为了合并特定的某些列，一定要加上参数true，该参数的作用是，默认将表的第一行作为标题。**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP8VjcxLFjQCpHWQPLjmlhlvwWZ0wpjMK34K2icvoNrWqQFt7KNibaVErjd44E4kvnu4dFRV0lPqEYQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 展开自定义列

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP8VjcxLFjQCpHWQPLjmlhleD95pxyV7ibqwHrSciaqcib9ZI2aFuvDDNCfa53e6S9eWJ8jPvH6MIXDg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 展开Data列

点击Data列右上角的展开按钮后，就会看到每张表的字段列表，**想合并哪些列，直接勾选列名，**点击确定，就会自动将每张表的所选字段按顺序合并到一起，是不是非常简单呢？

(合并后对于不需要的行，可以筛选出去，对于不需要的列，直接删除，按需要简单整理即可，不再详细介绍，你如果还不熟悉，请参考：[数据清洗中最常使用的十三招](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067158&idx=1&sn=4ad955112df2f40a93b684ed9147f26e&chksm=8e0c7181b97bf89777ae3d9de929867745edcbbfe1f2b396761c0cec716b86ee31e439279add&scene=21#wechat_redirect))

这里并没有用到复杂的M函数，也没有繁琐的操作步骤，只是在文件夹汇总的正常操作步骤基础上，为Excel.Workbook函数添加一个参数，就实现了批量合并特定的列。

关于PowerQuery批量汇总Excel文件，如果你还有其他问题或者解决方案，欢迎留言分享。

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtHORfNDsk1ibQ1luXtyibbDsnnwJXvdSpKwfPlcJCZSlvWYOK6p6VGeqw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，与2k+ 学习者一起成长
