---
create_date: 2023-04-04T23:26:47 (UTC +08:00)
tags: wx/pbi/数据处理功能 
aliases: null
pagetitle: PowerBI报告设计：一键应用/清除所有切片器
source: https://mp.weixin.qq.com/s/xWxDfQw61d1nxzI9JbF9jA
author: 采悟
status: 已完成
category: 浏览文章
notes: False
ZK: Origin
uid: 
---

在[上个月的更新](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484084105&idx=1&sn=57f2544083f86ed21310ea08a991866a&chksm=8e13b75eb9643e4875240bae7786aeabb621c5ca4f5301524e48df0cdf0e423c07cc92f6be18&scene=21#wechat_redirect)中，有一个新功能很好用，在报告中新增了2个按钮：一键应用/清除所有切片器。

当时只是简单提了一下，很多人没有注意到，所以这里再重新带你详细认识这个新功能。

如果==页面上切片器较多，报告数据量也比较大，那么切片器每选一次，其他图表都要开始转圈圈刷新等待几甚至几十秒==，是非常糟糕的体验。

如果选好所有的切片器以后，再一起刷新更合适。新增的“应用所有切片器”按钮就是解决这个场景的。

可以直接从“优化”功能区找到这个功能，点击即可添加。  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOyYGQt8mvu8c5ibgkpicJvzcL5gDC1JfSAWWr0TkQ2uibFNakiaXjH6f88l9ibASJduTems716qLzSlwA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

添加后会发现这个按钮是灰色的（如上图），当你调整切片器的选项后，它才会高亮显示。
![https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOyYGQt8mvu8c5ibgkpicJvzc6gPqib62bkyXQJbaK4nT0ubHMOz8WlfDI2D2QVHTqibnhAVORoK9vmbQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOyYGQt8mvu8c5ibgkpicJvzc6gPqib62bkyXQJbaK4nT0ubHMOz8WlfDI2D2QVHTqibnhAVORoK9vmbQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)
并且添加了“应用所有切片器”这个按钮以后，调整切片器的选项，图表是不会立即变化的，只有在点击这个按钮以后，图表才会显示变更后的数据，然后按钮重新变成禁用状态的灰色，直到你下一次调整切片器后，才会再次高亮显示。

以上就是“应用所有切片器”用法，它其实也是个普通的按钮，你同样可以来设置这个按钮每种状态的文本和格式，来进行美化。  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOyYGQt8mvu8c5ibgkpicJvzc3mehPRUw4h3nMaIDjuNEoaoajFVnrgEMVIl63iazTWzwOlT6AaaiaYPQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

除了“应用所有切片器”，还有个“清除所有切片器”按钮，不过它没有在“优化”功能区中，可以在插入>按钮中找到它：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMa29P4y37kuy9X8ica0jdhXWldD7NvTNzhyaWGFLxQ6TVWdhgpLI1sB2xVFz7cQwxkN53EzJ5hJqA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

或者你也插入任意一个按钮，在按钮的操作类型里改成“清除所有切片器”，

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOyYGQt8mvu8c5ibgkpicJvzcKs0o6xV2iaUI6KjsOe3rAQpK6micj2tvcuCDzKdJMbkdt7HxsT71IRSw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

修改这个按钮的文本等格式，就有了“一键清除所有切片器的按钮”。
![https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOyYGQt8mvu8c5ibgkpicJvzc2XlK8hgZNKCINzYvHs4SX41dzIGPjTp78PKbkFewpdp6Z7ibIibWX9PQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOyYGQt8mvu8c5ibgkpicJvzc2XlK8hgZNKCINzYvHs4SX41dzIGPjTp78PKbkFewpdp6Z7ibIibWX9PQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)
有了这两个按钮，在报告中进行切片器操作就方便多了，大幅提升了使用体验。

-   一键应用所有切片器，可以防止每选一次切片器就刷新一遍，只在切片器全部选定后点击按钮一次性应用，节省刷新时间；
    
-   一键清除所有切片器，当你不需要切片器筛选的时候，不用一个个去掉，点击按钮一次性清除所有，节省操作步骤。
    

不过如果你不想将切片器全部清除，而是返回到初始的筛选状态，还是需要用书签来实现的，参考之前的介绍：

[PowerBI报告设计技巧：一键重置](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073105&idx=1&sn=630078447d92ab54c9c049fb8a656953&chksm=8e0c5846b97bd150bd23d3af28b62bf9813d17b339a2a4199096cdb076fd664b0e744d2808b8&scene=21#wechat_redirect)

[PowerBI报告设计技巧：一键部分重置](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076778&idx=1&sn=e2cb9d89996185c4cc5c6a9084c7c9ec&chksm=8e13aa3db964232bd26f4c5db84fa9081437627c850ec39a954cfeb175886dcdf851aad9b7c1&scene=21#wechat_redirect)  
