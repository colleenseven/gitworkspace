---
create_date: 2022-05-22T13:13:09 (UTC +08:00)
tags: 
aliases: null
pagetitle: 一秒钟一句话生成 PowerBI 数据字典并与同事分享
source: https://mp.weixin.qq.com/s/bmXVKdq8MpbdZfFn1x104A
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

![](https://wx.qlogo.cn/finderhead/Q3auHgzwzM4Rz9mYvEFH2tuPTpv0svaghGlMxxNNbNjkwBJCRr1RFw/0)

**PowerBIMBA**

，

05月22日 20:00 直播

一句话构建数据字典

视频号

很多伙伴问罗叔是否可以给小白直接直接操作的技巧，例如：直接点一个按钮，直接写一个公式，直接解决一个问题的。  

## 我是小白我怕谁

可以的。

尽管讲解一个按钮，公式，问题是很直接的。但不排除一句话可以解决大问题的神技，小白不需要理解为什么，只需要用，只需要欣赏，只需要赞叹，不仅仅帮助小白解决问题，同时让小白可以增加兴趣，来体会 Power BI 和数据分析中的美和艺术。

## 如何提取数据模型的信息

有很多方法提取数据模型的信息，但是对小白来说，我们需要：

一秒钟一句话生成 Power BI 数据字典并与同事分享。

这看似是一个不可能完成的任务。

的确，有很多方法和工具可以从 Power BI Desktop 的数据模型中提取信息，但是对于小白来说，怎么可以快速实现呢？

小白的标准操作在于：

第一步，复制粘贴 “度量值” 内容。

第二步，复制粘贴 “结果” 即可。

本文就是这样的案例，我们从正统的思路开始做事，让大家知道其来龙去脉，然后构建实用的解决方案，然后重构，然后优化，然后再优化，然后再反思再优化，然后再封装，然后适配小白的思想，拿来就用。

请大家一起来欣赏吧。

## DAX 新函数

DAX 引擎还在进化，每一次的进化都是在主体框架下的一些小补充。但每次的小补充可能带来新的可能。今天要和大家介绍的是：

DAX 出了一个新的函数：COLUMNSTATISTICS。它可以直接返回当前数据模型中所有表和列的信息。

打开 DAX Studio，直接输入：

```
EVALUATE COLUMNSTATISTICS()
```

便可以得到：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNUMZicE3a0gStd2j2XQkvtgYDK86ocN6SeFQM5n1IMwgQg2vKXGMoS3UXvqDRNddRYNzBgjkMibwWg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

分别是：

-   表名
    
-   列名
    
-   最小值
    
-   最大值
    
-   非重复元素数
    
-   最大长度（如果是文本类型）
    

## 模型数据字典

如果你正考虑输出一个模型数据字典来告知相关人员，数据模型的信息，可以快速用这个函数实现。

这样就可以获得一套当前模型中所有表和列的字典。

## 无法用于计算表

不难想到可以用计算表来计算以上的字典并放入当前数据模型，可惜是不行的，例如在 Power BI Desktop 中，创建计算表，并写入：

这就出现了一个循环依赖的错误。道理很简单：

正在创建的计算表也是该 DAX 函数统计的对象；而该表还没创建完；要创建该表就要计算完该 DAX 函数；而要计算完该 DAX 函数，该表就要计算完；导致循环依赖。

好可惜啊，有没有。

我们希望这个很实用的函数可以使用。

## 度量值实现

既然该 DAX 函数仅仅依赖表和列，但并不会依赖度量值，所以，可以通过度量值来获取信息。在写度量值前，还注意到一点，有些系统生成的表，我们并不需要，因此，可以过滤掉，写出度量值的示例，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNUMZicE3a0gStd2j2XQkvtg0hdOnXibz9arO43z8f3tIHjMFcJ7ibSvOB4wZ1OcLuUBOjeNaicamaWQA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以看出：

-   的确可以运行成功。
    
-   编辑器的智能提示出错，说明 Power BI 的公式编辑器并没有支持对该函数的解析。但的确存在该函数。
    

## 显示信息

用度量值显示一个数值不是我们想要的，毕竟我们想要的是信息，而不是有多少条数据。

根据上述实验，我们可知有这样的限制：

-   我们想要表，但却不能用计算表；
    
-   可以用度量值，但度量值却不能返回表。
    

这导致一个矛盾。先考虑在度量值中用字符串来实现，如下：

这的确显示了信息，但不是特别紧凑，以及有的表里面没有列，也可以不必显示，因此，可以对这个度量值再做优化，得到：

这个效果的确是我们想要的了。

其优化的度量值内容为：

```
Model.Info.Text = // 设置要排除的表，默认留空VAR vFilterOutTables = { "" }// 设置要排除的辅助表，如：参数，度量值容器VAR vFilterOutTables_OneColumn = { BLANK() , "列" , "列 1" , "Value" , "Column" , "Column 1" }// 以下内容无需修改VAR vDictionary =     FILTER( COLUMNSTATISTICS() ,         // 清除掉系统生成的内容        NOT CONTAINSSTRING( [Table Name] , "DateTableTemplate" ) &&        NOT CONTAINSSTRING( [Column Name] , "RowNumber" )    )VAR vDictionaryFiltered = FILTER( vDictionary , NOT [Table Name] IN vFilterOutTables )VAR vTableInfoFilterd =FILTER(    ADDCOLUMNS(        SUMMARIZE( vDictionaryFiltered , [Table Name] ) ,         "@ColumnContent" ,             CONCATENATEX( FILTER( vDictionaryFiltered ,  [Table Name] = EARLIER( [Table Name] ) ) , [Column Name] , ", " )    ) ,    NOT [@ColumnContent] IN vFilterOutTables_OneColumn)RETURN     CONCATENATEX( vTableInfoFilterd ,         "表【" & [Table Name] & "】" & UNICHAR( 10 ) & "包括列：" & [@ColumnContent]         , UNICHAR( 10 )    )
```

只需要复制上述内容就可以立即提取自己的模型信息。还可以复制给工作伙伴，直接复制粘贴到微信与别人沟通。

然后粘贴到微信吧，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNUMZicE3a0gStd2j2XQkvtg4ibYSOjkC9rpoayuuIAVdGAmDQ3PYpjDMicwvyDyp23kn1RInNgfCVAw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

至此，主体已经完成。已经可以拿来就用了。

但这不是我们的调性，接下来我们一起进入思想时刻。

## 重构

什么是” 重构” 呢？

在我们写的每篇文章以及给出的每个案例中，几乎都有 “重构” 的影子。

重构，顾名思义，就是：重新构建，说白了，就是重新做一遍。

为什么要重新做一遍呢？

重新做一遍的底层逻辑就是：超越上一个版本的自己。

因此，重构是一种重要的思想。

重构，是一种反思，它总是提醒我们进行反思，一件事情是不是可以做得更好。

大家还记得爱因斯坦用纸做小板凳的故事，做了三个版本，拿出了最好的一个。

这里的重构，除了超过上一个版本的意思，还有一层更重要的底层逻辑是：

怎么才算 “更好” 呢？

一般在我们的这个领域来形容更好，有两个方面：

-   情感方面，你是不是有一种 “哇” 的感觉，获得了一种喜悦，超过了自己。
    
-   理性方面，是不是对内容本身有意义。例如：更高更快更通用。
    

很明显，这两者是常常伴随而来的。

在我们的这个领域，重构，往往意味着去实现：复用，健壮性。

什么意思？

例如：对于正在看本文的小白来说，也许你对度量值一无所知，但你知道如何创建一个度量值，那么只需要复制粘贴就可以解决本文所叙述的目标下的所有问题，那么就说，这个方案是：1）通用的；2）健壮的。

下面，就让我们一起进入重构的过程，对于小白来说，可以欣赏这个过程；对于高手来说，可以参考这个过程。

## 第一次重构：解除名称硬编码

任何用 "" 写出的文本都存在不够通用的问题，因此，需要将硬编码的部分提取，以便未来需求变化时，在一个位置维护变化的内容。

可以对度量值再做优化，得到：

```
Model.Info.Text = // 设置要排除的表，默认留空VAR vFilterOutTables = { "日期" , "ModelInfo" }// 设置要排除的辅助表，如：参数，度量值容器VAR vFilterOutTables_OneColumn = { BLANK() , "列" , "列 1" , "Value" , "Column" , "Column 1" }// 设置表前缀等信息，默认如下，可不修改VAR vText_Table_Prefix = "表【" // 设置表前缀VAR vText_Table_Suffix = "】" // 设置表后缀VAR vText_Table_IncludingColumns = "包括列：" // 设置包括列VAR vText_Column_Splitter = ", " // 设置列分隔符// 以下内容无需修改VAR vDictionary =     FILTER( COLUMNSTATISTICS() ,         // 清除掉系统生成的内容        NOT CONTAINSSTRING( [Table Name] , "DateTableTemplate" ) &&        NOT CONTAINSSTRING( [Column Name] , "RowNumber" )    )VAR vDictionaryFiltered = FILTER( vDictionary , NOT [Table Name] IN vFilterOutTables )VAR vTableInfoFilterd =FILTER(    ADDCOLUMNS(        SUMMARIZE( vDictionaryFiltered , [Table Name] ) ,         "@ColumnContent" ,             CONCATENATEX(                 FILTER( vDictionaryFiltered ,  [Table Name] = EARLIER( [Table Name] ) ) ,                 [Column Name] , vText_Column_Splitter             )    ) ,    NOT [@ColumnContent] IN vFilterOutTables_OneColumn)RETURN     CONCATENATEX( vTableInfoFilterd ,         vText_Table_Prefix & [Table Name] & vText_Table_Suffix &         UNICHAR( 10 ) & vText_Table_IncludingColumns & [@ColumnContent]        , UNICHAR( 10 )    )
```

这就完成了，效果上没有区别。

## 第二次重构：应对复杂工程

我们刚刚的截图非常简单，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNUMZicE3a0gStd2j2XQkvtgeuA1DOKZDiaQyjm2Ud2DhT05Uicbp05FpKM43qGrjFGqSefoqEDBicPuQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

现在的问题是，如果面对的是一个大型的复杂工程，还可以吗？

第一步：先从业务逻辑上想想，有没有这个需求？

思考如下：

同事会不会问我们，数据模型中有哪些表和列的信息呢？然后要快速给出，并进行沟通。

想了一会儿，发现：的确很可能。而且还发现了另一种可能，那就是：

我们也会自己不断从数据库或文件中提取信息，但提取的信息是不是太多了，我们也不知道，尤其是表很多的时候，那么就说明这个需求是有意义的。

第二步：在实际大型工程中，试一试如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNUMZicE3a0gStd2j2XQkvtgIwLiaqzgRgtTTg5FmTzQBxDmzibGb1INpC8zB3fjicKl2ibGaGUd16v1Xg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

不难看出，非常实用，一下子就全部提取了。

一个特别实用的动作是，可以在记事本里分析和反查这些列是否合理。如下：

这可以非常快地帮助我们发现问题。

但问题来了，我们发现有的表有很多列，是否可以直观的写下有多少列呢？

因此，进行优化，效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNUMZicE3a0gStd2j2XQkvtgmX1pRRATvUCJiaa1Bf8D5Udo4pteBfDw0g8Dicwh5TSmHxOPXSiaUXqmw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这的确帮了大忙，我们快速地知道哪些表的列数，以便有针对性的研究下。

## 第三次重构：修复问题

现在就可以不断使用这个技能了。

直到发现它的问题：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNUMZicE3a0gStd2j2XQkvtg2jPBYibnmbPRywD2ibNoOMwf8bxZHJveMicWXWjI3f5Oku6SVtsWfz2zg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

只要报表界面上有任何筛选器，都会导致这个错误。仔细阅读错误信息：

COLUMNSTATISTICS () 不能与筛选上下文一起使用。

仔细思考一下原因，由于 COLUMNSTATISTICS 是用来获得模型信息的，并不是用来进行计算的，因此，DAX 引擎将其隔绝在筛选上下文之外是有道理的。

如何进行修复呢？

既然错误是：不能与筛选上下文一起使用。那么可以清除掉所有的筛选上下文即可。

最后得到了带有这种保护的版本。如下：

```
Model.Info.Text = // 进行设置：    // 设置要排除的表，默认留空    VAR vFilterOutTables = { "" } // 如果要排除某表，如日期表，可以将表名放入。    // 设置要排除的辅助表，如：参数，度量值容器    VAR vFilterOutTables_OneColumn = { BLANK() , "列" , "列 1" , "Value" , "Column" , "Column 1" , "Column1" }    // 设置表前缀等信息，默认如下，可不修改    VAR vText_Table_Prefix = "表【" // 设置表前缀    VAR vText_Table_Suffix = "】" // 设置表后缀    VAR vText_Table_IncludingColumns = "包括列：" // 设置包括列    VAR vText_Table_IncludingColumns_Prefix = "（共 " // 设置 共 x 列    VAR vText_Table_IncludingColumns_Suffix = " ）" // 设置 共 x 列    VAR vText_Column_Splitter = ", " // 设置列分隔符// 以下内容无需修改RETURNCALCULATE(        VAR vDictionary =         FILTER( COLUMNSTATISTICS() ,             // 清除掉系统生成的内容            NOT CONTAINSSTRING( [Table Name] , "DateTableTemplate" ) && //系统的日期表            NOT CONTAINSSTRING( [Table Name] , "LocalDateTable" ) && //表列对应的日期表列            NOT CONTAINSSTRING( [Column Name] , "RowNumber" ) // 系统生成的表索引        )    VAR vDictionaryFiltered = FILTER( vDictionary , NOT [Table Name] IN vFilterOutTables )    VAR vTableInfoFilterd =    FILTER(        ADDCOLUMNS(            SUMMARIZE( vDictionaryFiltered , [Table Name] ) ,             "@ColumnCount" , COUNTROWS( FILTER( vDictionaryFiltered ,  [Table Name] = EARLIER( [Table Name] ) ) ) ,            "@ColumnContent" ,                 CONCATENATEX(                     FILTER( vDictionaryFiltered ,  [Table Name] = EARLIER( [Table Name] ) ) ,                     [Column Name] , vText_Column_Splitter                 )        ) ,        NOT [@ColumnContent] IN vFilterOutTables_OneColumn    )    RETURN        CONCATENATEX( vTableInfoFilterd ,             vText_Table_Prefix & [Table Name] & vText_Table_Suffix &             vText_Table_IncludingColumns_Prefix  & [@ColumnCount] & vText_Table_IncludingColumns_Suffix &                        UNICHAR( 10 ) & vText_Table_IncludingColumns & [@ColumnContent]            , UNICHAR( 10 )        )    // 清除筛选上下文    , REMOVEFILTERS( ))// by BI佐罗
```

用 CALCULATE 配合 REMOVEFILTERS 来保护 COLUMNSTATISTICS 的执行。

于是，此时就得到了一个无懈可击的重构版本，它具备这样的特点：

-   可以直接复制粘贴使用，无任何依赖。
    
-   可以设置各种配置。
    
-   针对问题给出保护，没有了复杂度。
    

## 小白时刻

作为小白，如果你整个文章都没有读懂，完全没有关系，只需要看以下三句话即可。

要获得数据模型的数据字典信息并与同事分享交流，只需要两步：

第一步，新建度量值，复制粘贴上述 “Model.Info.Text” 内容。

第二步，拖入 Power BI Desktop 报表，复制后去微信粘贴即可。

## 高手时刻

如果你正在学习 DAX，那你可以看到 DAX 的一个综合运用了，可以体会其中每一步的 DAX 用法。

如果你可以正确地 Thinking In Table，那么用 DAX 就可以帮助我们构建灵巧的解决方案。

## 总结

快去复制粘贴到你的项目中试试吧。

## 扩展思考

在此强调，如果仅仅是为了解决一个目标：快速提取数据模型的信息，那仅仅复制粘贴以上度量值即可。

但这里怀着再进一步重构的想法，我们观察到：

在整套解决方案的逻辑链条中，有这样的前提假设：

-   我们想要表，但 COLUMNSTATISTICS 却不能用于计算表；
    
-   可以用度量值，但度量值却不能返回表。
    

再加上：

-   一个度量值提取信息的先入为主的设计初衷。
    

导致：

我们得到了现在的解决方案。

但是，

如果我们真的想得到一个表怎么办呢？

当我们第一次这样尝试的时候，会触发一个错误：

不能与筛选上下文一起使用。

但是，我们已经发现了这个问题的弥补方法，那就是：用 CALCULATE 配合 REMOVEFILTERS 来保护 COLUMNSTATISTICS 的执行。

既然如此，我们思考：

是不是可以构建一套表格方式的解决方案呢？

也就是：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNUMZicE3a0gStd2j2XQkvtgY34r9Vr3EcT1rgGm0l8E4vc6OhpNRZjnQGfBmQkFZTPHrAcL4rnr9Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个问题就留给大家思考吧。

![](https://wx.qlogo.cn/finderhead/Q3auHgzwzM4Rz9mYvEFH2tuPTpv0svaghGlMxxNNbNjkwBJCRr1RFw/0)

**PowerBIMBA**

，

05月22日 20:00 直播

一句话构建数据字典

视频号

在订阅了BI佐罗讲授的《BI真经》之《BI进行时》课程区，除了可以下载本文案例，还可以观看视频讲解。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNhia5Pc4XC1Um7IYgQhGEoEC1yK05ibUFoPBYpcoAMvibuZh2BZaibMzULeDwNfSeQ0KHRcDUdX3FzVA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**Power BI 终极系列课程《BI真经》**

**推荐刚刚接触 Power BI 的朋友学习**

**[BI真经-精英系列-第一集-自助商业智能分析的底层逻辑揭秘](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650793681&idx=1&sn=03a565f434ebd06275809a2261612285&chksm=f18ce6c0c6fb6fd6e29ca09440916ed68202c08478367d41a7a13539fd1e5f6769fb685f4995&scene=21#wechat_redirect)  
**

[

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/09hv4Xua0LNBM1lxlQYHJBicic4CvPoRGLqHgdTZOr8goNRh0asDXA48mRDzc9zxW4UMQiayHwgDmx7mlt4cQxtjg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

BI真经 - 让数据真正成为你的力量





](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650788512&idx=1&sn=76972ff4b0cf265fe9479c6457b04b47&chksm=f18cd2b1c6fb5ba7386eb0bb835280bd8a651bfe0481cc78f20fc30b80c60d2d4cb7eb5b1e3e&scene=21#wechat_redirect)

扫码与精英一起讨论 Power BI，验证码：data2022

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOiad5BOrdQTKpB733esKiaxZa53LXWIPlQicMjxntaRr3a2hnMmuibTib8QacXeiakucDr7lSNGkuV2MXw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击“阅读原文”进入学习中心

**↙**
