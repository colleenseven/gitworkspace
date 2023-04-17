---
create_date: 2020-12-25T23:42:15 (UTC +08:00)
tags: 
aliases: null
pagetitle: PowerQuery批量合并Excel，前面有空行且不相等的解决办法
source: https://mp.weixin.qq.com/s/A-nm2wCr-X7ERh9F0jK9Nw
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

关于PowerQuery批量汇总多个Excel工作簿，该功能非常经典实用，操作起来也很简单，之前已经有几篇文章介绍过该功能以及可能遇到的各种问题，

-   [使用Power Query是一种什么体验？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067120&idx=1&sn=4188548c00910c7e9fd1cb5c2d5f8880&chksm=8e0c71e7b97bf8f135ea0bc07fff83152b9cf0ecc24b504eff1f999d92b65b58d0a4939c2c84&scene=21#wechat_redirect)  
    
-   [批量合并Excel，PowerQuery的这些技巧你应该掌握](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070803&idx=1&sn=826d571e4133872ff3bedb4ad4d524f9&chksm=8e0c4344b97bca5281787e9a0cf1a3f2571227316537b1ba7069c5bf5f600d4a4249cfc18932&scene=21#wechat_redirect)  
    
-   [利用PowerQuery，批量合并多个Excel的指定列](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073950&idx=1&sn=022f2b8806518ff03648eeea76950223&chksm=8e0c5f09b97bd61f3dc5a7509181aa42fd3545d009b9b8715b0ef387d4f50dffe0833dfa8ce4&scene=21#wechat_redirect)
    
-   [Power Query批量合并Excel，数据不是从第一行开始怎么办？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073974&idx=1&sn=f1c63db1ed01cbabd2a3293d663205a4&chksm=8e0c5f21b97bd637760e8cd51c9888c667e3b586da5bad7581c1749c73802656b60cf16456c6&scene=21#wechat_redirect)
    

上面的第四篇文章介绍的是数据不是从第一行开始但前面空行是相同数量的情况，这种合并起来还比较简单。有朋友提到更特殊的一种情况，**每张Excel表格前面的空行也不相同，那应该怎么快速批量合并呢？**

这篇文章继续探讨解决合并Excel时会遇到的这个问题，比如下面示例中的这几张表：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMLibGgibtR9kyoKJ6raiapTMSu6QDmULicj0IZBzMc1fMib2CIm529ZaZ7iclf0mGqZgpcthGjCtkjO6RQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

从这三张表可以看出，数据前面都有空行，且空行数量都不相等，以这个数据为例，我们依然从头开始，再详细介绍一下PowerQuery批量汇总空行不相等Excel的处理步骤。

**下面是详细操作步骤：**  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP8VjcxLFjQCpHWQPLjmlhlxWUdicuMbtQgMBkpzNskSumpttWAhicSpwLibt4jj69RbpXwF8BbvAVaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 获取数据>文件夹

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP8VjcxLFjQCpHWQPLjmlhliaAicfc2vz06dbzaBZZZ3S5sOic14zKonJlFtxRhj450jHaLGcr0ZBw7g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 点击“转换数据”进入PowerQuery编辑器

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOXHfCicV6btz7AxiaYMicNkEVn7uNKBAmw6GzKfhxo8uibJVaWtgerEic8ZUAZqbsYVEZm7iamjJtNZ5fQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 添加列>自定义列

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOXHfCicV6btz7AxiaYMicNkEVoOQqnefnkBRc2snHV9nx7DPV47GsdhGnVxlma2unJNibfBW00EfUbicQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 自定义列公式：Excel.Workbook(\[Content\])

这里的Excel.Workbook无需加第二个参数，因为第一行本来也不是标题行，将表的第一行作为标题没有意义。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOXHfCicV6btz7AxiaYMicNkEVxLhosEicHUiclGM6PJXEDiazmeRQyreYMIRAqf6F1E3lt0oNon4BRNIXQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 展开自定义列

展开以后，添加一个自定义列来解析\[Data\]列：  

> Table.PromoteHeaders(        //提升标题行
> 
>     Table.Skip(\[Data\],             //跳过表的前 x 行
> 
>         Table.PositionOf(         //计算 x
> 
>             \[Data\],
> 
>             \[Column1="订单日期"\],
> 
>             Occurrence.First,
> 
>             "Column1"
> 
>         )
> 
>     )
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPXTMExt0Wa1znNPd2qkFM2gPGoB37ISwRyYMd78Ocf8BynibhAlgSysEAtAoV2DLyyibEv1oXib2wWg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 添加自定义列  

这串M函数的含义已经注释计算逻辑，看起来比较长，与[上篇文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073974&idx=1&sn=f1c63db1ed01cbabd2a3293d663205a4&chksm=8e0c5f21b97bd637760e8cd51c9888c667e3b586da5bad7581c1749c73802656b60cf16456c6&scene=21#wechat_redirect)相比，只是多了 Table.PositionOf 函 数，该函数通过查询某个列名出现的位置，来计算每张表前面有多少空行，利用这个函数的计算结果，来动态返回空行的数量。

将计算出的空行数量传递给 Table.Skip 跳过空行数，并利用函数  Table.PromoteHeaders 提升标题。

然后就是正常的点击自定义列右上角的展开按钮，像往常一样看到每张表的字段列表，**想合并哪些列，直接勾选列名，**点击确定，就会自动将每张表的所选字段合并到一起。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOXHfCicV6btz7AxiaYMicNkEVes7N2tNh21DMYZE6FbAfG1esbicNoBwhgKpH6qC07iaOvjbpnK561HIQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOXHfCicV6btz7AxiaYMicNkEVg8iapx3mYR6RvLamoDbyy53vg9mmm8kc4D7aoEEOWLWianBU468whdug/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

因为这个示例中，Excel表不规范的地方更多，所以用到了更多的M函数来相应处理，如果能理解M的逻辑最好，即使不理解，遇到相似的问题时，直接复制上面的M代码套用即可。

至此，关于批量合并Excel可能遇到的问题基本都提到了，如果你还有其他问题或者解决方案，欢迎留言分享。

当然，最重要的还是规范数据源，让每一张表的格式有统一的标准，这样才能更简单高效的完成数据汇总工作，而无需使用各种复杂的M函数。

本文的练习数据，可以在「PowerBI星球」公众号对话框发送关键字“**批量合并Excel**”下载。

\-精彩推荐-

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtHORfNDsk1ibQ1luXtyibbDsnnwJXvdSpKwfPlcJCZSlvWYOK6p6VGeqw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtVXYmWpicF9SVicdBBQYdaKG4icSfUTkS9dFIBW3NsL5ZrNpYH6icjgJaUA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 扫码加入，与2k+ 学习者一起成长
