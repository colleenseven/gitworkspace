---
create_date: 2023-03-27T23:27:18 (UTC +08:00)
tags: wx/pbi/PQ数据处理 
aliases: null
pagetitle: 利用PowerQuery转换一维表，这种格式的表格你见过吗？
source: https://mp.weixin.qq.com/s/oi-A8J8zgz6xv7cYTe4ncw
author: 采悟
status: 已完成
category: 精读文章
notes: False
ZK: Origin
uid: 
---

大家在日常工作中可能都碰到过各种各样的奇葩表格，比如最近有星友从网上下载的表格长这样：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNZicCWvcBKCvOIB5bSwjUwONWiaqicpmiaXLo7BtHgMIvYuyicA0x4u0WFDPx5gmlNISAiaJmeJ4Q51k6Q/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

如何将这种表格快速转换为方便分析的一维表呢？  

这个格式确实很少见，也很难直接用，必须先整理成规范的结构才能进行下一步的分析，我们来看看PowerQuery如何快速处理这种表格。

下面直接进入操作步骤。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNZicCWvcBKCvOIB5bSwjUwOK0rHibNdS61iaNyBy9kPsAG9faIjYlpZjCwWwLTe5Pc3UcraUvCYsBSw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

↑合并列
![https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNZicCWvcBKCvOIB5bSwjUwOV173kYFRvQLwyyhfKolg0V4biaLoibqmhzwAQf7f9Q8P9XC7FdFNMjDw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNZicCWvcBKCvOIB5bSwjUwOV173kYFRvQLwyyhfKolg0V4biaLoibqmhzwAQf7f9Q8P9XC7FdFNMjDw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)
↑添加索引列

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNZicCWvcBKCvOIB5bSwjUwOtichX6zHyGOcUvUbvO1Q44kAO7oXSPc5WC0SeAodQPJcmoVcEBsb5Cw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

↑==对索引列取模，得到一列1和0交替的新列==

选中索引列，点击标准>取模，输入2。

取模的含义就是除以某个数的余数  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNZicCWvcBKCvOIB5bSwjUwON6vNaCeD2mmicDbmKWd165HNDQibN747LrX4y5QYXjk8btdPmwsZUfCA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

↑对==取模列进行透视==

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNZicCWvcBKCvOIB5bSwjUwO4yAsddJyBmYKeIR3vAg2jicYu2ZQxLmBAZsGHOtrw1vtA6gibpZF6UKQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

↑对\[1\]列进行向下填充
![https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNZicCWvcBKCvOIB5bSwjUwOpsZRAlHXibhrUvp4Wv7m90zo19vFqrf30vF6iceGa5NvojLnMUiaZY4lQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNZicCWvcBKCvOIB5bSwjUwOpsZRAlHXibhrUvp4Wv7m90zo19vFqrf30vF6iceGa5NvojLnMUiaZY4lQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)
↑筛选\[0\]列不为空的行

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNZicCWvcBKCvOIB5bSwjUwO8dvf7EczXRNvagA0JOQykDA0HDZk4BFDIqm0TRGXKG3k05UGgEKsLw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

↑添加自定义列

这个是最关键的一步，关于这个步骤的逻辑以及List.Zip函数，可参考：

[PowerQuery | 利用List.Zip进行特殊格式的一维表转换](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484082896&idx=1&sn=87b4ad28d5df98035c83e8c8512d78ce&chksm=8e13b207b9643b11d3f7172b62e086d499c7efa53871df5de5d16c252ed7a442f7850465679f&scene=21#wechat_redirect)  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNZicCWvcBKCvOIB5bSwjUwOvO5VJoe3hQAWUI1k38EaqT1U8qopD32KoqmTodPOTBaTZ6mpm5QgCg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

↑展开==上面添加的自定义列>扩展到新行==

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNZicCWvcBKCvOIB5bSwjUwOliclMLjQB4wa8iajZstFXlf2CsYicXKlaUq77v2fPP1Yblt3T6oeTL3Vw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

↑继续展开自定义列>提取值

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNZicCWvcBKCvOIB5bSwjUwOAv8mGZNJ7XLkGfIDaR7jaRYLuf4kFjXicduzotsBZhfY6OdzPm2raicw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

↑拆分自定义列

到这里就可以看到已经将原始表格转换成了一维表，然后删除其他无关列，重命名列名、调整数据类型后，就变成了最终我们需要的效果。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNZicCWvcBKCvOIB5bSwjUwOWIeKjicTYQ8e8YMzaMXIVbsUY4HgTZbqy7gmh5vyG8jN2TiccQ42TIsA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

上面看起来步骤很多，其实熟练掌握界面功能、以及List.Zip的用法后，分分钟就可以完成。

___
