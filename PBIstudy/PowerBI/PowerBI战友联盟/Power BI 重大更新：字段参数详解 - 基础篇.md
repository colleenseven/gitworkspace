---
create_date: 2022-05-18T13:14:11 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI 重大更新：字段参数详解 - 基础篇
source: https://mp.weixin.qq.com/s/BHpLr4VvaTpxTveHZSVKgA
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

Power BI 在 5 月迎来了重大更新，其中一个点就是：字段参数。

虽说是一个点，且在官方说明的篇幅非常少，但是这个特性却意义重大而深刻。我们会用不同的文章来说明这个特性的各种特点。

## 开启字段参数

字段参数，目前处于预览状态，可以在 Power BI 的【文件】【选项】中打开，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNElmoiasSkNhP5FtWCHTe2ae8ib5DIaV2066oP7IQb3icj4hSiaHyyDKZGwIibOzMxMZuhAicDKBA3EJOA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

重启 Power BI Desktop 即可使用。

## 预备知识

很多人在学习 Power BI 的时候，其实是一知半解，体现在对基本的概念的把握上基本是乱的。包括很多教程也没有准确用词，导致大部分的底层逻辑是错误。

首先，要来明确几个概念：

-   字段
    
-   表列
    
-   维度
    
-   度量值
    
-   参数
    

这几个名词，它们是什么关系，还是完全一样，怎么说并不重要，通过实验可以得出以下结论：

表列：基表的列。

维度：是一个逻辑上的概念，通常用某个表列来表示维度，用来观察。

度量值：保存 DAX 计算逻辑的单元。

字段：表列或度量值的统称。

注意：在 2013 年前，度量值叫计算字段，可见：在数据模型中，只有一类事物：字段。

记住这句话，就会领悟到一个重要思维：模型思维。其内涵大致为：

抽象意义上的数据模型由维度构成，而维度由字段构成，完毕。

字段，分为两种：

-   数据字段，保存了数据内容。
    
-   计算字段，保存了计算逻辑。
    

在表格系统中，表列与数据字段等价；度量值与计算字段等价。

在 Power BI Desktop 的界面中，有这样一个启示：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNElmoiasSkNhP5FtWCHTe2ao75DaibVwuFaCic3M12RC7rK7ukJykVwmkQZI994icuGqV2aib0aytAfcw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

对于分析师，要做的只有一件事，将字段拖拽出来放置到报表中，形成计算。

这里用字段一词，并非巧合，因为其内涵包括了：

-   表列，包括：来自基表（从外部数据源加载）的列，计算表的列。
    
-   度量值。
    

小结：

-   抽象的维度模型等价于表格模型。
    
-   字段等价于：表列和度量值。
    

> 关于系统的理解和学习表格思维及模型思维，可以学习《BI 真经》。

再来理解：什么是参数？

参数是一种可变量。

那么，字段参数则应该具有内涵：一种可变的字段。

根据上述对字段的描述，可以推论：

可变的字段就应该包括：

-   可变的表列；
    
-   可变的度量值。
    

以上概念有严格的逻辑链条，请读完本文再回来读一遍。

很多伙伴学习 Power BI，只是学习每一个技巧和函数，那么必定是一种穷举法，没有核心，没有体系，没有框架，也没有底层逻辑。

本文将展示如何根据以上概念，来推导【字段参数】可能或应该具备的特性，并实验证明。

整个过程希望大家可以学到三件事：

-   学习字段参数这个特性本身。
    
-   理解本小节所说的逻辑概念。
    
-   体会如何从理论框架指导实践的整个过程来体会万变不离其宗的感觉。
    

## 理解什么是字段参数

启动了 Power BI Desktop 的预览功能以后，就可以在这个位置找到字段参数，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNElmoiasSkNhP5FtWCHTe2a1om4UW55OPoGoGYzKHVnI6fRJE3K0gCug63PxPTTk19t0Mfj4nIvOQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

先通过一个实验来感受下。

## 用度量值构造字段参数

可以将度量值构建到一起，形成字段参数，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/09hv4Xua0LNElmoiasSkNhP5FtWCHTe2aQVqONpbOoJc0UCdFeeGric5MVSlDWAWfT2WxmKdgw7RLonZ2XNyEKKg/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

## 用表列构造字段参数

可以将表列构建到一起，形成字段参数，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/09hv4Xua0LNElmoiasSkNhP5FtWCHTe2a0wxZGcgZicdSZwjcIO1Ud6OQjuKYWMPUHBdP87jfQqgQhWXabOGXYug/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

值得注意的是：

这里用来自不同的表的表列放到一起构建成字段参数。

## 字段参数的使用

字段参数构建好了以后，其使用路径是唯一的，非常容易，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNElmoiasSkNhP5FtWCHTe2a8qklc8dUKhs5FSsYbP2g2U7Qm7tSjia6IlbU5IzrW9uFe8AArUSELRw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/09hv4Xua0LNElmoiasSkNhP5FtWCHTe2aLVFqHHSdBt6oc4gUZYtse9IwvHtlyGug0iaiazoya7mxFnEcLOUNuic0Q/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

表格的内容，根据选择的参数，切换到了参数所在的内容。

## 字段参数规律感悟

通过上述例子，以及预备知识，可以得到这样的体会：

-   字段放入透视表是实际的。
    
-   字段参数，允许用户选择不同的字段。
    

也就是说：

透视表实际使用的字段来自字段参数被选择以后的结果。

以下逐步给出字段参数各种场景。

## 字段参数 - 表列型

上述案例就是这样的，不再重复，具体如下：

## 字段参数 - 度量值型

既然度量值也是字段，那么自然可以构建由度量值构成的字段参数，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/09hv4Xua0LNElmoiasSkNhP5FtWCHTe2ayqXywZJtKFKMmmE030ia3YN3g0PuosWSAJcEWlXZN2lIJEibVXt82qGA/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

总结为：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNElmoiasSkNhP5FtWCHTe2anC2jPEFjv8XVsHB6XDTWfwIZhmDBmBRGNHxFmAhUQB61J4x7oGxp6A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

## 字段的平铺展开

在上述实验的过程中，很快就可以发现这样的规律，如下：

如果用户没有选择参数中的字段，则所有字段都将在透视表内展开。

总结为：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNElmoiasSkNhP5FtWCHTe2aKXpsGTUiaicR3dwVewkrVLQLb9D8t2mqZXzL04oa06lVfQ831SFLHFibw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

## 字段参数内部是什么样

可以发现，字段参数其实是一个计算表，内容结构大致如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNElmoiasSkNhP5FtWCHTe2adlp3fHEGkW0bPAEQdkv2sj19icASPMzjK5N66ZkCbicudZjwtIwTh9jg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

包括了三列，分别是：

-   名称
    
-   对应度量值名称
    
-   排序
    

这是常见的参数表结构。

这里面涉及到一个新的 DAX 函数，NAMEOF，顾名思义，它可以返回某字段（表列或度量值）的名字。

该计算表创建后，后两者是隐藏状态，在表视图中可以看到，如下：

可以看出这里的对应关系，以及在中文本地化的时候的错误：

” 个订单 “属于严重的翻译错误，可以猜测” 订单 “的原单词是” Order“，应为” 排序 “的意思。

查看英文版，可以看到：

其含义分别为：

-   参数
    
-   参数字段
    
-   参数顺序
    

## 字段参数改名

字段参数内容的名字需要在 DAX 中修改，如下：

```
// 改名前：字段参数_度量值 = {    ( "SalesAmount", NAMEOF('View Calc'[SalesAmount]), 0),    ( "SalesAmount G%", NAMEOF('View Calc'[SalesAmount G%]), 1),    ( "SalesAmount PY", NAMEOF('View Calc'[SalesAmount PY]), 2)}// 改名后：字段参数_度量值 改名 = {    ("销售额", NAMEOF('View Calc'[SalesAmount]), 0),    ("销售额 增长率 G%", NAMEOF('View Calc'[SalesAmount G%]), 1),    ("销售额 去年同期", NAMEOF('View Calc'[SalesAmount PY]), 2)}
```

由于改名属于内容，因此，不会对报表造成任何影响，这是我们希望的。

另外，不难推出由于在其中引用了度量值，度量值改名，也会动态随着改名，这也不会造成任何影响。

也就是说，不论修改字段的名字还是参数字段内容都会自动变化，报表不会受到影响。

如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNElmoiasSkNhP5FtWCHTe2aXmzGLiblgc4oAVVXNvQFiaQ8EibyfkvsSq6yibyibBNibGj0VzKoHV3pqakA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

## 混合形态

根据预备知识以及对字段参数的实验，不难想到：

-   表列是字段；
    
-   度量值是字段；
    
-   字段参数凡是字段都可以用。
    

那是否可以将表列和度量值混合到一起，成为一个字段参数呢？答案是肯定的。

如下：

这不禁有些让人震撼，居然还能这么玩。

## 字段参数理论小结

通过以上实验，不难得到这样的认知：

-   字段包括表列和度量值。
    
-   字段参数可以通过三种形式构造：
    

-   纯表列构造；
    
-   纯度量值构造；
    
-   混合表列与度量值构造。
    

-   构造完毕的字段参数可以在 DAX 中改名，不会影响报表内容。
    
-   报表中透视表使用的字段参数，将随着用户的选择，动态决定实际参与的表列或度量值。
    
-   多个字段会默认平铺展开。
    

以上，我们没有做任何一件与业务有关的事，完全在一个抽象层面来实验和认知这个特性。其过程为：

-   基于模型的理论框架，万变不离其宗。
    
-   推测新特性具备的特征。
    
-   展开实验，验证想法。
    
-   归纳总结。
    

整个过程虽然没有创造业务价值，但这为构建业务价值提供了不变的底层逻辑。

接下来看看可以做哪些有意思的事情呢？

## 应用一：动态坐标轴

在很久以前我们构造过：日期切换，动态 ABC 分析的维度切换，其逻辑特点都是：坐标轴被动态赋予了内容。

用日期维度进行切换构建字段参数如下：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/09hv4Xua0LNElmoiasSkNhP5FtWCHTe2aCeJq1uTFQibYkibicWQcC2usH7fulPn7OkOeUvDicIU8B1Ya0RGZXibiaaWA/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

## 应用二：全动态图表

既然坐标轴可以是动态的，不难想到：

图表的构成的本质是：字段。包括：

-   用作轴的字段：数据字段。
    
-   用作图例的字段：数据字段。
    
-   用作指标的字段：度量值。
    

将以上三者全部构建成字段参数，那就可以在报表运行时，实时决定：

-   用哪个维度作为坐标轴；
    
-   用哪个维度作为图例；
    
-   用哪个度量值作为指标。
    

构建字段参数如下：

作图如下：

其效果为：

## 应用三：全面动态图表

作为动态，更彻底的表现在：

-   轴动态
    
-   图例动态
    
-   指标动态
    
-   图表类型动态
    

效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/09hv4Xua0LNElmoiasSkNhP5FtWCHTe2aUvulVjKzmEgcBUlnItAZCLyFH8P5DPP4LYicsTOAOiaKdrqJX5zNAlKw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

至此，字段参数可以带来的动态性就全部展示无遗了。

## 应用四：动态矩阵

我们知道，图表的本质是矩阵，那么也可以利用字段参数来构建全动态的矩阵，也就是：

-   矩阵的行头动态；
    
-   矩阵的猎头动态；
    
-   矩阵的指标动态。
    

效果如下：

矩阵的维度和指标计算均可以动态赋予。那么，矩阵就全面动态化了。

## 再探究计算原理

问题来了，我们知道矩阵的字段是一种计算，那么该字段参数是如何参与计算的呢。如下：

用户有两种选择：

-   显示所选字段。将显示目前正在参与计算的实际字段。
    
-   显示所选字段的值。将计算实际字段并显示计算结果。
    

## 二层抽象

对于字段参数来说，其本质是实现了二层抽象。

第一层抽象是字段本身。

例如：销售额是 1000 元是一个具体的值，但度量值 \[Sales\] 对其进行了抽象，销售额是多少，不知道，但该度量值会实时计算出来的。

第二层抽象是字段参数。

例如：销售额是一个度量值，但字段参数【字段参数\_指标】进行了抽象，到底是哪个度量值，不知道，但运行时会根据用户的选择，先决定用什么度量值，再根据现场的环境计算出实际的结果。

因此，字段参数的魅力在于：二层抽象（二次抽象），或者叫：再抽象。

抽象思维，是一种非常非常非常非常重要的人类独有的思维模式。值得重点指出。

知道：1 + 1 = 2；8 + 5 = 13；进行了抽象以后，变成了：a + b。

因此，初中所学习的代数，其本质在于对算术的一层抽象。

代数，顾名思义，用字母代替数字，简称：代替数字，再简称：代数。这就是” 代数 “的本质。

在这里，我们可以充分感受到这种抽象的力量和魅力。

如果小伙伴的初中数学还不错，那么，本文内容是非常简单的。

但是小伙伴的抽象思维如果受到了损伤，那么，本文可能就会看不懂了。其本质在于：抽象思维能力不健全，受到了损伤了。

怎么办呢？肯定不适合再回去和儿子一起学习代数了。那么可以正确的学习和使用 Power BI，来实现三个目的：

-   学会 Power BI，驾驭数据分析；
    
-   提升个人竞争力，超越其他二；
    
-   修复抽象思维能力。
    

那么在哪里可以学习这样的 Power BI 知识呢？可以学习与众不同的《BI 真经》。

## 更改参数字段

问题来了，如果希望修改参数字段，怎么办？例如希望增加一个字段或删除一个字段。

在 Power BI 中是无法通过界面做到的。但可以直接在计算表中编辑，如下：

```
图表_指标 = {    ("销售额", NAMEOF('View Calc'[SalesAmount]), 0),    ("销售增长率%", NAMEOF('View Calc'[SalesAmount G%]), 1),    ("利润", NAMEOF('View Calc'[Profit]), 2),    ("利润率%", NAMEOF('View Calc'[Profit%]), 3),    // 增加一条：    ("销售额去年同期", NAMEOF('View Calc'[SalesAmount PY]), 4)}
```

这个结构非常简单容易理解，所以可以照抄复制改写即可。

也就是说：

可以从界面操作来生成字段参数，也就是生成这个计算表；

但是却不能根据已经生成的计算表内容来反向推导得到界面再修改。

通常这样的结构都说明了一个问题：

界面仅仅是用来生成代码的方式，却无法从代码重构出界面。

这进一步说明了：

参数字段的本质是一个计算表。而界面仅仅是在生成这个计算表而已。

只不过，这个计算表有些特别而已。（会在后续文章再介绍。）

## 无法独立构建

如果说字段参数的本质是计算表，且其结构似乎很容易理解，那么，可以自己构建一个。

如果你进行这个实验，你会发现这样的结论：

-   可以构建出完全一样的计算表；
    
-   但却没有这种特性。
    

问题来了，为什么只有用 Power BI 界面功能构造的这个计算表才有用呢？

有两种可能：

-   字段参数不仅仅是计算表。
    
-   字段参数是计算表，但发生了更复杂的情况，未知。
    

关于这个话题，我们知道普通用户无法独立构建，必须借助界面构建就可以。至于到底是什么原因，超越了本文的范围，我们会专门做一个专题来讲解。

## 再论字段参数平铺展开

需要注意的是：字段参数平铺展开，是一个很特别的特性。值得一提。

在本文的实验中中，已经见到了这种情况，如:

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNElmoiasSkNhP5FtWCHTe2aA6SYezHypGicjCVk3U33SRDyCtMF7kOy8CWYgSk4KUqP8dapcBCR9Ug/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

当字段参数不做出任何选择的时候，在矩阵中会平铺展开。也就是说，

将一个字段参数的字段，注意用词：字段参数的字段，放入表中，会自动展开成多个字段。

重点在于：一变多。一个字段变成了多个字段，且是并行展开。

请理解这个特性，未来在很多场景会继续用到这个特性。

## 字段参数应用小结

至此，已经可以很顺畅的使用字段参数了。这里总结一些要点：

-   字段参数必须且只能通过界面构建生成。
    
-   构建字段参数时无需编写 DAX，可以直接生成。
    
-   字段参数让用户决定实际使用的字段，实现了再抽象。
    
-   可以实现：动态维度和动态计算的特点。包括：
    

-   动态坐标轴
    
-   动态图例
    
-   动态指标
    
-   动态矩阵
    

## 疑惑与混淆

对于普通用户，刚刚接触不久，会有以下疑问：

-   字段参数效果和 SWITCH TRUE 类似，但区别是什么
    
-   字段参数效果和计算组类似，但区别是什么
    

先给出一个结论：

从原理上，

SWITCH TRUE 结构，计算组，字段参数是三种完全不同的实现，它们在某些场景有类似效果，但在某些场景又有各自的优势，彼此无法替代。

本文做简单说明，具体探讨，会单独后续文章再做说明。

## 与 SWITCH TRUE 的不同

如果要实现指标的切换，还可以用 SWITCH TRUE 的方法，但字段参数与之不同。

一个明显的不同在于：

用 SWITCH TRUE 的时候仅仅是一个度量值，返回一个结果一个格式。往往在值和率的格式上成了痛点。

而字段参数则不同，它可以完美地返回值或率且不需要编写任何 DAX 就可以直接实现相同效果。

在这一点上，字段参数的确就可以解决以往地问题了。但并不是说字段参数就比 SWITCH TRUE 结构更好，在某些场景下，必须用 SWITCH TRUE。后续文章再做说明，但你可以记住，如果你无法用字段参数实现，那就是用考虑 SWITCH TRUE 结构的时候了。

## 与 计算组 的不同

字段参数与计算组也是完全不同的。计算组在运行时改变计算；而字段参数是动态决定计算什么。

具体的讨论也会放在后续文章再做展开。

也就是说，字段参数，SWITCH TRUE，计算组三者是完全不同的。这些具体的不同和本质在哪里，我们在后续文章再做说明。

## Excel 无法使用

有的伙伴会问：字段参数到底是一个模型层的功能，还是一个界面层的功能？

这个问题是相当本质的。这里给出结论先：字段参数是一个界面层的功能，数据模型中的计算根本不知道发生了什么。

一个可以证明这个观点的实验就是，在 Excel 中使用字段参数是完全不可用的，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNElmoiasSkNhP5FtWCHTe2aAQeBkFsaDCvESYXc0wZ5n7hV6lFbxLn8eu0IMQGNWKiaDxAvHNykUNg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这说明，数据模型的引擎无法给 Excel 提供相应的计算支持。进而说明，字段参数是一个特定于 Power BI 界面层的功能，而不是数据模型或引擎的功能。

## 总结

可以总结一下了。

本文从概念，原理，实验，应用，差异对比等方面对字段参数做了详解的介绍，现在是时候动手自己操作再重读和消化本文了。然而，本文是字段参数详解的基础篇，文本留有几个重要内容需要再做单独说明。

但从普通用户的应用上来说，本文足以指导完成所有可行的操作以及知道哪些操作是不可行的。

当然，很多高级用户对于字段参数还会存在更多深度好奇以及复杂应用的需求，这些我们也将在后续讲解。

最后，有小伙伴问，微软刚刚发布这个特性，市面上没有任何文档，那是怎么在短时间内完全驾驭到这么细的呢？答案很简单，正确地学习 Power BI 就会形成一个体系；Power BI 再发布的几乎任何特性都是对已有思维框架某些细节的再实现以及对一些不完美的补充而已。Power BI 的技术学习已经完毕，尽在《BI 真经》。

没有看懂？不要紧，不要错过直播哦  

![](https://wx.qlogo.cn/finderhead/Q3auHgzwzM4Rz9mYvEFH2tuPTpv0svaghGlMxxNNbNjkwBJCRr1RFw/0)

**PowerBIMBA**

，

05月18日 20:00 直播

BI进行时-字段参数详解

视频号

在订阅了BI佐罗讲授的《BI真经》之《BI进行时》课程区，除了可以下载本文案例，还可以观看视频讲解。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNhia5Pc4XC1Um7IYgQhGEoEC1yK05ibUFoPBYpcoAMvibuZh2BZaibMzULeDwNfSeQ0KHRcDUdX3FzVA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**Power BI 终极系列课程《BI真经》**

[

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/09hv4Xua0LNBM1lxlQYHJBicic4CvPoRGLqHgdTZOr8goNRh0asDXA48mRDzc9zxW4UMQiayHwgDmx7mlt4cQxtjg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

BI真经 - 让数据真正成为你的力量





](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650788512&idx=1&sn=76972ff4b0cf265fe9479c6457b04b47&chksm=f18cd2b1c6fb5ba7386eb0bb835280bd8a651bfe0481cc78f20fc30b80c60d2d4cb7eb5b1e3e&scene=21#wechat_redirect)

扫码与精英一起讨论 Power BI，验证码：data2022

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOiad5BOrdQTKpB733esKiaxZa53LXWIPlQicMjxntaRr3a2hnMmuibTib8QacXeiakucDr7lSNGkuV2MXw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击“阅读原文”进入学习中心

**↙**
