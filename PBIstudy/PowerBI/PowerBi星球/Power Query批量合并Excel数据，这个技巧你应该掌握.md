---
create_date: 2023-01-28T09:10:48 (UTC +08:00)
tags: wx/pbi/PQ数据处理 
aliases: null
pagetitle: Power Query批量合并Excel数据，这个技巧你应该掌握
source: https://mp.weixin.qq.com/s/Z6ZIxHvMPzZjbA39CL8QZw
author: 采悟
status: 已完成
category: 精读文章 
notes: False
ZK: Origin
uid: 
---



关于Excel数据的[批量合并](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070803&idx=1&sn=826d571e4133872ff3bedb4ad4d524f9&chksm=8e0c4344b97bca5281787e9a0cf1a3f2571227316537b1ba7069c5bf5f600d4a4249cfc18932&scene=21#wechat_redirect)，之前介绍过很多种情况，一般是导入后展开直接合并，但是对于特殊的数据格式，并不能直接合并，比如一个文件夹中有三个excel文件，分别是下面这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPibRkQTpkk3Ropx14aIkWb0zoqV2A0zApf6w5oOnZDxOfjOsG6mnt7kfP1Hx7QmU3YXia2NZGISN1g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPibRkQTpkk3Ropx14aIkWb046L0MFLe2lyoY6KbxQ22T6fQibyoiaQsHCgd8T2icJ9E7Cc5WMAl6XNDQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
![https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPibRkQTpkk3Ropx14aIkWb0JNiaTGWV9iaA8Q9IpEb4Wp5Vv4xsnCQiaQy3fhgekuAjMibia7Pw8yiaXyXQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPibRkQTpkk3Ropx14aIkWb0JNiaTGWV9iaA8Q9IpEb4Wp5Vv4xsnCQiaQy3fhgekuAjMibia7Pw8yiaXyXQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
之前介绍的方法是利用自定义函数来合并，参考：  

[PowerQuery批量合并Excel，原来这个方法更好用](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077355&idx=1&sn=a90e985627bff1b90c57b2ed5ac7c602&chksm=8e13a9fcb96420ead0721bd421aea25c3f4c4fe3ca3451e0dbba7fd074534c50c767be6e19fc&scene=21#wechat_redirect)  

这个方法可以实现，但是发布后如果想设置计划刷新时，会有下面这个提示：

此数据集包含一个动态数据源。由于 Power BI 服务中不刷新动态数据源，因此不会刷新此数据集。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMH6GutShoSibSvJz0YbYicccBwstaKHdNo5oYVNTG4KUn61OPTsBlNwJAbicC94u6MgKL2Qo85kIclA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

关于动态数据源，有些情况可以通过修改M公式解决，但并不总是都能找到方法，上面的情况就不容易解决，所以如果需要设置计划刷新，就不要使用自定义函数的方法了，对于上述表格的情况，其实还有个更简便的合并方法。

以上面的数据为例，我们从头开始，再介绍一下这种情况的批量合并操作的主要过程。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP8VjcxLFjQCpHWQPLjmlhlxWUdicuMbtQgMBkpzNskSumpttWAhicSpwLibt4jj69RbpXwF8BbvAVaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 获取数据>文件夹

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP8VjcxLFjQCpHWQPLjmlhliaAicfc2vz06dbzaBZZZ3S5sOic14zKonJlFtxRhj450jHaLGcr0ZBw7g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 点击“转换数据”进入PowerQuery编辑器

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP8VjcxLFjQCpHWQPLjmlhlFsVEv3aaxwc0EMWjmted1YDN1R8Qu4sv5htiaGPIJV346Y2cpeb28KQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 添加列>自定义列

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP8VjcxLFjQCpHWQPLjmlhlfgzQ2fI6gfAsCu0E2csWds2mIk8JLFwKR7YwZJlRnTjmL5RibQWq8Wg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 自定义列公式：==Excel.Workbook(\[Content\],true)==

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP8VjcxLFjQCpHWQPLjmlhlvwWZ0wpjMK34K2icvoNrWqQFt7KNibaVErjd44E4kvnu4dFRV0lPqEYQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 展开自定义列

然后就可以看到\[Data\]列（其他无关列可以删除），点击某一行的“Table”，就能看到某个原始表格的数据：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMl2Pt18siaS6qQWEGCJAXR5ibUMl37LnrGqftR4JDvic1NV5yiczJQu4oEXxe6A1hYhGbCDVYO5FFJrw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

对于这一列不要直接展开，而是添加自定义列，对==尚未展开的Table进行逆透视操作==：  

> Table.UnpivotOtherColumns(
> 
>     \[Data\],
> 
>     {"门店"},
> 
>     "年月","金额"
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMl2Pt18siaS6qQWEGCJAXR5WC0NXTuWmUhnicjACvL8zQHY7bkSnibs3WFGkI8rZAGib3SNicxjgDPbbQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

Table.UnpivotOtherColumns是逆透视其他列的M函数，它将\[Data\]中的每一个表，除“门店”列之外的其他列进行逆透视，逆透视后生成的两列的列名分别命名为“年月”和“金额”。

添加的自定义列的效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMl2Pt18siaS6qQWEGCJAXR5bLIpGVzjZQq3p9ib3lhPicfowibV5cS4wraNGAOictJwJcu0GtxoCbRjRQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这样每一行的表都是同样的格式了，然后直接展开自定义列，即可完成合并，合并后的表也已经是一维表，并且可以设置计划刷新而不会遇到动态数据源的问题。

这个方法的基本思路是在==展开数据前，对数据进行逆透视，让每一行的Table变成同样的格式以后再进行合并==。

如果你的数据需要在展开Table前进行一定的操作，都可以参考这个方法，关键是了解一些常用的M函数的用法。

关于PowerQuery批量汇总Excel文件，如果你还遇到其他特殊情况或者解决方案，欢迎留言分享。

___
