---
create_date: 2020-11-29T23:45:20 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power Query批量合并Excel，数据不是从第一行开始怎么办？
source: https://mp.weixin.qq.com/s/HNgWdu4gk-ld07yJMxikgw
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

[上篇文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073950&idx=1&sn=022f2b8806518ff03648eeea76950223&chksm=8e0c5f09b97bd61f3dc5a7509181aa42fd3545d009b9b8715b0ef387d4f50dffe0833dfa8ce4&scene=21#wechat_redirect)的末尾留了个小话题，让大家分享一下，关于批量合并还有哪些问题？其中有几位后台跟我说，如果数据不是从第一行开始的，怎样批量合并指定列呢？

这种情况确实很常见，因为大多数Excel表都会有个表头信息，具体的明细数据从下面的某行才开始，比如下面示例中的三个表就是这样：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJN0icM52LFGfSnpNsFHaGb8j4ttHYQUrclTyxhmuPbUMvxthY6ictibrk7vBwAZT4WJxIia2OiaM1ficnBA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这三张表的数据都是从第5行才开始的，并且数据字段的顺序也不一致，这种情况下怎样批量合并指定的列呢？  

难道需要把每个表打开，删除表头后再合并吗？这当然也是一个笨办法，不过这不符合我们利用PowerQuery批量合并提升效率的初衷，下面就给出一个这种类型表格的批量合并思路。

总体步骤和[上篇文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073950&idx=1&sn=022f2b8806518ff03648eeea76950223&chksm=8e0c5f09b97bd61f3dc5a7509181aa42fd3545d009b9b8715b0ef387d4f50dffe0833dfa8ce4&scene=21#wechat_redirect)类似，不过中间多了一个处理步骤，以及利用了两个M函数。

**下面进入分步详细操作：**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 获取数据>文件夹

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOXHfCicV6btz7AxiaYMicNkEVSdq3SerO2IYjTHm2H7hKorqhFQ0sSHMhXB3xwnj944TrQia46ZmUkQA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 点击“转换数据”进入PowerQuery编辑器

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOXHfCicV6btz7AxiaYMicNkEVn7uNKBAmw6GzKfhxo8uibJVaWtgerEic8ZUAZqbsYVEZm7iamjJtNZ5fQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 添加列>自定义列

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOXHfCicV6btz7AxiaYMicNkEVoOQqnefnkBRc2snHV9nx7DPV47GsdhGnVxlma2unJNibfBW00EfUbicQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 自定义列公式：Excel.Workbook(\[Content\])

**这里的Excel.Workbook无需加第二个参数，因为第一行本来也不是标题行，将表的第一行作为标题没有意义。**

Tips：利用PowerQuery进行数据处理时，可以先把其他无关列都删掉，看起来更加清爽，包括之后的步骤，如果展开后，发现有无用的列，可以随时删除。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOXHfCicV6btz7AxiaYMicNkEVxLhosEicHUiclGM6PJXEDiazmeRQyreYMIRAqf6F1E3lt0oNon4BRNIXQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 展开自定义列

展开以后，并不是像上篇文章一样，接着展开\[Data\]列，而是再添加一个自定义列：  

> Table.PromoteHeaders( 
> 
>    Table.Skip(\[Data\],4) 
> 
>  )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOXHfCicV6btz7AxiaYMicNkEV55iacnqPC6ic0hW0ibfK7hIKIhW7H4OARBChDUlHGPVZZmSkyroCicJ65Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 添加自定义列  

这串M函数的含义已经用注释说明，其实逻辑很简单，由于**原始数据表格是从第5行开始的，所以先跳过前4行数据，并将第五行数据，作为表的标题行，**然后展开这个新的自定义列，就可以正常提取并合并特定的列了。

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

比起上一篇文章，只是多了一个添加自定义列的步骤，利用两个M函数：Table.PromoteHeaders和Table.Skip，就可以轻松解决批量合并时跳过表格前几行的问题，并且也可以选择合并特定的某几列数据。

关于PowerQuery批量汇总Excel，如果你还有其他问题，欢迎留言分享，我们一起解决。

本文的练习数据，可以在「PowerBI星球」公众号对话框发送关键字“**批量合并Excel指定列**”下载。

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtHORfNDsk1ibQ1luXtyibbDsnnwJXvdSpKwfPlcJCZSlvWYOK6p6VGeqw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，与2k+ 学习者一起成长
