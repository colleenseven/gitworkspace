---
create_date: 2022-03-22T13:24:12 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power Query 真经 - 第 4 章 - 在 Excel 和 Power BI 之间迁移查询
source: https://mp.weixin.qq.com/s/zStWA4nK_iRaL2tU_x8iBw
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

Power Query 可以在 Power BI 或 Excel 中使用，很多人一开始就在想到底用哪个平台来使用 Power Query，其实不必为此纠结，总有一天会意识到需要把查询复制到一个另一个中的。这有可能是将查询从一个 Excel 工作簿中复制到另一个 Excel 工作簿中，从 Excel 复制到 Power BI，或者从 Power BI 复制到 Excel。在本章中，将探讨将查询从一个工具快速移植到另一个工具的方法。请记住，虽然本书的重点是 Excel 和 Power BI，但这些步骤对于任何承载 Power Query 的工具来说几乎是相同的，即使它包含在其他微软产品或服务中。

## 4.1 在工具之间复制查询

为了说明如何在工具之间迁移 Power Query 查询，这里先从一个在 Excel 中建立的查询链开始，其结构如图 4-1 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPYdanNJ0yXOIZP17zzlnZDXdnt1AFicPM4eKwKdGTWnj1HMM7icPLDJZ3AqnC1fIO3U3RibA96KNj2w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

_图 4-1 简单查询链 Excel 文件中的查询工作流程_

> Data.CSV ：CSV 格式数据
> 
> Raw Data：原始数据
> 
> Staging：暂存
> 
> Sales：销售
> 
> WorksheetTable：工作表

然而，在深入研究这个解决方案之前，需要确保数据源被正确地指向并保存在示例文件中。这将防止在探索解决方案之间移动查询的不同选项时，遇到与数据源有关的任何步骤级错误。

需按如下方式更新示例文件。

1.  在 Excel 中打开以下工作簿：
    

“第 04 章 示例文件 / Simple Query Chain.xlsx”。

2.  显示【查询 & 连接】选项卡。
    
3.  右击 “Raw Data” 查询【编辑】。
    
4.  进入【主页】选项卡【数据源设置】【更改源】选择【文件路径】【浏览】。
    
5.  更新文件路径，使其指向以下文件：
    

“第 01 章 示例文件 / Basic Import.csv”。

6.  【确定】【关闭】对话框。
    
7.  转到【主页】【关闭并上载】。
    
8.  保存工作簿。
    

> 【注意】
> 
> 此时用户通常不需要执行上述步骤，因为用户很可能已经在本机电脑上使用了可以访问的数据源建立了查询。但是，如果用户打开一个由其他人建立的解决方案，或者这个解决方案用到的数据源位置已经不同时，在将查询复制另一个位置之前，更新源文件路径是一个好主意。

### 4.1.1 Excel 到 Excel

将从最简单的场景开始：将一个查询从一个 Excel 工作簿复制到另一个 Excel 工作簿。

需要做的第一件事是确保 Excel 的【查询 & 连接】窗格处于活动状态，因为将在这里找到要处理的查询列表。在这里，用户通常要做的是选择一个或多个他们想要复制的查询。

【查询 & 连接】窗格支持所有用户所期望的正常的鼠标选择方法，如下所示。

1.  单击选择单个查询。
    
2.  通过选择第一个查询时，按住 Shift 键并单击最后一个查询来选择连续的多个查询。
    
3.  当只选择需要的查询时，可以按住 Ctrl 键选择非连续的一组查询。
    

> 【注意】
> 
> 不支持用 Ctrl+A 来选择多个查询。

虽然选择查询可能是有意义的，但如果查询有依赖的前序查询，而用户没有选择它们（要么是因为忘记了，要么是没有意识到它），会发生什么？一起来看看吧。

1.  右击 “Sales” 查询【复制（或选择它并按 Ctrl+C ）】。
    
2.  转到【文件】【新建】【空白工作簿】（在新的工作簿中）。
    
3.  转到【数据】【查询和连接】。
    
4.  右击【查询 & 连接】窗格的空背景 【粘贴（或者选择它并按 Ctrl + V ）】。
    

此时，Power Query 不仅粘贴了复制的查询，还粘贴了构成该查询链的任何依赖的前序查询。同时也应该注意到，它也正确地观察到了每个查询的配置的加载目的地，如图 4-2 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPYdanNJ0yXOIZP17zzlnZD68CIM98bNrjU59DWfpXiayrjKgwtzhr4xP0nXtIxuIztmoEHo87EvBw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

_图 4-2 将 “Sales” 查询（仅）复制到一个新的 Excel 工作簿中_

> 【注意】
> 
> 当从一个 Excel 中复制到另一个 Excel 中时，这个效果符合预期，因为它意味着用户永远不会意外地忘记复制查询基础结构的关键部分。

当用户把整个查询链复制到一个解决方案中时（或者至少是一个不包含这个查询链的任何部分的解决方案），这个方法非常有效。但是，如果链的一部分已经存在了呢，会发生什么？例如，我们现在在新的工作簿里有 “Raw Data” 和 “Staging” 查询。那么，如果我们现在回去只复制 “Sales” 查询，会发生什么？当然，它将创建一个新的 “Sales” 查询副本，指向新工作簿中现有的 “Raw Data” 和 “Staging” 查询，不是吗？

1.  回到原来的工作簿中去。
    
2.  右击 “Sales” 查询【复制】。
    
3.  返回到新的工作簿中。
    
4.  右击【查询 & 窗格】中的空白区域【粘贴（或者选择它并按 CTRL + V ）】。
    

正如将看到的，Power Query 不是整合和附加到现有的查询，而是重新创建整个查询链。如果名字已经用过了，它会在括号里加上数字字符，以区分哪些查询是相关的，如图 4-3 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPYdanNJ0yXOIZP17zzlnZDsAu6knS4Nic3gcibcS1FoAibScMicMibtY9ktkusu0kbibef4ap8FUSC6usg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

_图 4-3 Power Query 重新创建查询链，而不是整合_

这可能有点令人沮丧，因为用户会更希望可以有一个选择，可以在复制和粘贴过程中解决此问题。但以这种方式使用复制和粘贴功时，没有这种选项。

如果用户在这种情况下最终需要 “Sales (2)” 重新使用来自 “Staging” 的数据，而不是 “Stating (2)”，则需更新 “Sales (2)” 中的 “Source” 步骤，以便从 “Stating” 来读取数据而不是从 “Stating (2)” 读取数据。要做到这一点，需要进行如下操作。

1.  编辑 “Sales (2)” 查询。
    
2.  选择 “Source” 步骤。
    
3.  更改公式栏中的公式，使其指向 “Staging” 查询，如下所示：
    

```
=Staging
```

4.  关闭 Power Query 编辑器 ，允许数据更新。
    

这时可以删除 “Raw Data (2)” 和 “Staging (2)” 查询，因为它们将不再被使用。

> 【注意】
> 
> 可以复制查询的源代码，并按上述方法创建它，但这涉及到使用【高级编辑器】的问题，将在本书后面的章节中探讨这个问题。

### 4.1.2 Excel 到 Power BI

现在已经知道了将查询从一个 Excel 文件复制到另一个 Excel 的基本知识，接下来就是如何将方案从 Excel 中复制到 Power BI 中。首先，按如下操作准备好，之后来做这件事。

1.  关闭为前面的例子所创建的新工作簿。
    
2.  打开 Power BI。
    
3.  返回到 Excel 中的查询链工作簿。
    

现在，正如看到的，从 Excel 中复制到 Power BI 中的方法与从 Excel 中复制到另一个 Excel 中的方法非常相似，如图 4-4 所示。

1.  右击 “Sales” 查询【复制（或者选择它并按 CTRL+C ）】。
    
2.  返回到 Power BI 文件。
    
3.  转到【主页】【转换数据】。
    
4.  右击【查询】导航器中的空白区域【粘贴】就像在 Excel 中一样，每个查询都将创建。
    

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPYdanNJ0yXOIZP17zzlnZDVleJycvvUqmV3DBK9pRABZB7LsBFiaY1mGahmfjIiaofib75OMG84YrxQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

_图 4-4 将查询从 Excel（左）复制到 Power BI（右）_

此时，所要做的就是单击【关闭并应用】，数据就会开始加载了。

> 【警告】
> 
> 只要查询是连接到外部数据源的，以这种方式复制的查询就能很好地工作。然而，如果数据源是一个 Excel 表，那么此时将会遇到挑战，因为 Power BI 没有自己的工作表。这将会由于无效的数据源而触发一个步骤级的错误。如果要移植一个基于 Excel 表的解决方案，需要导入查询，正如本章后面所讨论的那样。

### 4.1.3 Power BI 到 Excel

到现在为止，已经明白了用 Power Query 解决方案在应用程序之间移动是多么容易。那么，如果在 Power BI 中有一个查询，但由于某种原因需要在 Excel 中重新创建呢？没问题。

1.  打开 Power BI 解决方案。
    
2.  单击【查询】。
    
3.  复制需要的内容。
    
4.  切换到 Excel 并显示【查询 & 连接】窗格。
    
5.  粘贴查询。
    

将查询从 Power BI 复制到 Excel 和将查询从 Excel 复制到 Power BI 中一样简单，只要查询中没有使用在 Excel 中的 Power Query 不支持的数据源连接器。

实际情况是，Power BI 比 Excel 包含更多的数据源连接器（其中很多都处于测试阶段）。此外与 Excel 不同的是 Power BI 还支持自定义连接器。

那么，如果把一个依赖于 Excel 中没有的连接器的解决方案复制到 Excel 中，会发生什么？将会得到一个如图 4-5 所示的步骤级表达式错误。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPYdanNJ0yXOIZP17zzlnZD9cicDCEM13yTG6gMCTMtib6sf2Q9qds8ibwOaC8BtFIbQpCpA7YjY0kWg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

_图 4-5 自定义 “WooCommerce” 连接器在 Excel 中不可用_

（译者注：WooCommerce 是一个国际范围著名的电商程序，在国内应用较少，该连接器将允许 Power BI 可以直接从该电商程序中获取数据。）

> 【注意】
> 
> 不幸的是，在 Power Query 团队为 Excel 中的给定连接器添加支持或提供在 Excel 中使用自定义连接器的方法之前，没有办法解决这个问题。所有建立在这类连接器上的解决方案只能在 Power BI 中运行。

### 4.1.4 Power BI 到 Power BI

好消息是，从一个 Power BI 实例复制到另一个 Power BI 实例是相当简单的。事实上，对于大多数用户来说，由于他们的电脑上只有一个版本的 Power BI 桌面版，直接复制在一个 Power BI 文件中有效的查询肯定也会在另一个文件中有效。

> 【警告】
> 
> 有一种情况是：一个用户在本机电脑上运行多个版本的 Power BI 安装程序（ Windows 商店、直接下载和 Power BI 报表服务器版本的组合），那么这类用户可能会遇到从较新版本复制和粘贴到较旧版本的 Power BI 桌面版的问题。这种类型的问题通常只在用户针对一个新的或升级的连接器建立一个解决方案，然后把它复制到旧版本的 Power BI 应用程序时才会出现。如果这种情况发生时，几乎肯定会得到一个步骤级别的错误，即一个参数或整个连接器不能被解决。

## 4.2 导入查询

虽然复制和粘贴查询肯定是将查询从 Excel 到 Power BI 中一种有效的方法，但也可以导入查询。那么，为什么有这种模式呢？

那就来比较一下不同的方法以及它们能够做什么，如表 4-1 所示。

|   
 | 复制粘贴模式 | 导入模式 |
| --- | --- | --- |
| 原始的 Excel 工作簿 | 必须为开启状态 | 必须为关闭状态 |
| 复制 / 导入特定的查询 | 支持 | 不支持 |
| 复制 / 导入所有查询 | 支持 | 支持 |
| 导入数据模型结构 | 不支持 | 支持 |
| 导入度量值 | 不支持 | 支持 |
| 连接到 Excel 中的表 | 不支持 | 支持，但会将数据复制 |

_表 4-1 比较了从 Excel 导入 Power BI 时 Power Query 的 不同方法_

如果用户没有在 Excel 中使用 Power Pivot 数据模型，对于引用了原 Excel 工作簿中的表格的查询，应该 “导入模式”。正如本章前面提到的，将这些查询从 Excel 复制和粘贴到 Power BI 会导致步骤级错误，因为 Power BI 不识别 Excel 中的作为表格的数据源。当使用【导入】功能时，Power BI 给用户一个选择，即用户可以选择如何处理这些 Excel 中的表。

如果用户选择的导入模式是使用 Excel 数据模型，那么用户会立即看到不仅导入了查询，而且导入了关系、层次结构和度量值。

在本节中，将看三个不同的场景，展示不同的数据源如何影响导入过程。

### 4.2.1 仅外部数据源

首先，来看当用户将一个 Excel 文件导入 Power BI 时，同时 Excel 中查询只依赖于该 Excel 的外部数据源，会发生什么。

1.  打开一个新的 Power BI 桌面文件。
    
2.  转到【文件】【导入】【Power Query , Power Pivot , Power View】。
    
3.  浏览在前面的例子中复制的 Excel 文件的查询结果：
    
    “第 04 章 示例文件 / Simple Query Chain.xlsx”【打开】。
    
4.  单击【启动】。
    

此时，Power BI 将执行从文件中导入数据的过程，并在完成后显示结果，如图 4-6 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPYdanNJ0yXOIZP17zzlnZDAKMcX0d0P252b4Uxb0kPJM6HNStpybY6mo0gjF3x1HibJr28ia0Q3F3A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

_图 4-6 成功导入 Excel 文件_

此时，用户以为一切都经完成了，但实际上有几处还需要处理，如图 4-7 所示。

1.  单击【关闭（关闭上面显示的对话框）】。
    
2.  单击【应用更改（实际加载数据）】。
    

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPYdanNJ0yXOIZP17zzlnZDNxdVplulGhQDmNHmrj4niaDn9ibDRTriaI8ITuh3HKf915n4h9d1B9KibQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1) _图 4-7 直到告诉 Power BI 【应用更改】，导入才算完成_

按照正常理解，此时 Power BI 应该会执行查询，将数据加载到数据模型中，以便可以构建报告。但实际上这一切并没有发生，根本没有创建任何表，尽管单击了【应用更改】按钮。这到底是怎么回事？

这里不难体会到，虽然在 Excel 工作簿中该查询已经加载，且已基于此构建了透视表（PivotTables）和透视图（PivotCharts）等，但 Power BI 并不能识别或兼容 Excel 工作簿中 Power Query 加载以后的内容。它也不会对 Power BI 产生任何影响。任何没有加载到 Power Pivot 数据模型的 Excel 查询将只在 Power BI 中被设置为连接。

要解决这个问题，需要编辑查询的【启用加载】设置，如图 4-8 所示。

1.  转到【主页】【转换数据】。
    
2.  右击 “Sales” 查询，确保【启用加载】被选中。
    
3.  转到【主页】【关闭并应用】。
    
    ![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPYdanNJ0yXOIZP17zzlnZDlRrLibLquxzSXaTjV928sc5D8oicz4cB1F8UVRMZSGCdc3E8G4P1gSYg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
    

_图 4-8 加载到工作表的查询显示其加载被禁用_

这一次，表才会被加载到数据模型中。

### 4.2.2 数据模型的导入

现在是时候导入一个包含数据模型的解决方案了，它的数据也来自于主机 Excel 工作簿中的表。图 4-9 显示 Excel 工作簿的查询依赖链的视图。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPYdanNJ0yXOIZP17zzlnZD7fwFodY7qGuQ9VHjXhibqxBib2hibiagDTbf2IEmwqZOCvic9tPr12HGgxw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

_图 4-9 两个 Excel 表和十二个查询将生成四个表，加载到 Excel 的数据模型中_

虽然理解这些查询的工作原理并不重要，但重要的是要认识到这两个表（Raw Data - Sales，Raw Data - Budgets）是存储在 “当前工作簿” 中的，也就是说，数据和查询都在同一个 Excel 文件中。

还应该知道，这个文件中的 Power Query 结构作为 ETL 层，为下面的 Power Pivot 数据模型服务，其中包括四个指定的表、四个关系和两个度量值（Sales 和 Budget），如图 4-10 所示。

_图 4-10 显示的数据模型来源是由 Power Query 结构衍生出来的_

最后，文件中有一个名为 “Report” 的工作表，其中包含基于数据模型的 PivotChart 和切片器，如图 4-11 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPYdanNJ0yXOIZP17zzlnZDCHiaAWIWdu2IcCNaiaOA7aLec0sL2sUWwN3a7Oa1z12RqGnsyFoShibBQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

_图 4-11 基于 Excel 的报表，包含在 Simple Model.xlsx 文件中_

这是一个相当简单的基于 Power Query 和 Power Pivot 的解决方案，用户可以建立这个解决方案，它显示了这些工具是如何很好地协同工作的。如果想更详细地了解它，可以在示例文件中找到如下文件：

“第 04 章 示例文件 / Simple Model.xlsx”。

（译者注：这是一个经典的案例，虽然此处并不讲解如何建立这个模型，但该案例文件却展示了大多数业务人员所面对的场景，用 Power Query 处理数据，并将数据加载到 Excel 数据模型（Power Pivot），并基于数据模型构建关系，计算列，度量值进而创建透视表进行分析。这是一个标准的通用套路。）

假设新用户从同事那里拿到这个模型文件，然后用户决定需要将解决方案转移到 Power BI 中。这将带来一个挑战，所有的数据、查询、数据模型和 BI 报告都在同一个文件中，而用户还不知道原同事建立它的所有逻辑。当然，用户可以一次性选择 Excel 文件中的所有查询，然后把它们复制到一个新的 Power BI 文件中，正如本章前面所讨论的。但是，虽然这样做会导入查询，但它不会导入关系和度量值。这样用户就需要手动重新创建，这可能是非常痛苦。

### 4.2.3 导入时复制数据

基于前面讨论的模型的复杂性，要确保尽可能容易地将其从 Excel 转移到 Power BI 。

Power BI 的【导入】功能正是为了处理这种情况而建立的，来探讨一下它是如何工作的吧。将从如下方法从 Excel 文件中导入内容。

1.  打开一个新的 Power BI 桌面文件。
    
2.  转到【文件】【导入】【Power Query, Power Pivot, Power View】。
    
3.  浏览到以下位置的文件：
    

“第 04 章 示例文件 / Simple Model.xlsx”。

4.  选择该文件【打开】。
    

> 【注意】
> 
> 从 Excel 工作簿中导入的能力并不依赖于 Excel 程序。（译者注：即使电脑没有安装 Excel，而直接使用 Power BI 导入 .xlsx 中的数据模型也是可以的。）

一旦单击出现的对话框中的【启动】选项，将得到一个选择，如图 4-12 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPYdanNJ0yXOIZP17zzlnZDqPQPCTc9SDS604YPgHc0ll5ygy0IWfUuOSV9yG2icRtfuPXlxGLnzXA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

_图 4-12 想要如何导入 Power BI 数据呢_

现在，使用默认选项【复制数据】 ，这将启动查询和数据模型组件的导入，如图 4-13 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPYdanNJ0yXOIZP17zzlnZDxoKBYcBYRCBQLJUgvdSL7XUsJHicQJYCWnqgllO2kK4ibLGicvEHrLcmA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

_图 4-13 Power BI 已成功导入查询、数据模型和度量值_

到目前为止，一切看起来都很好。事实上，如果单击 Power BI 桌面窗口左侧的【模型】按钮。则会看到数据模型结构，包括关系、度量值，甚至字段的可见 / 隐藏状态都已经正确导入，如图 4-14 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPYdanNJ0yXOIZP17zzlnZDx1h3xSoJUMgl3jGhLj20OfKk2EmZQxia3ibjAcR4DmLp1A0j4ZKlRymg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

_图 4-14 Excel 中的数据模型已经全部导入到 Power BI 中_

转到 Power BI 的报告页面，可以快速复原 Excel 中的图表，如图 4-15 所示。

1.  在 Power BI 窗口的左侧选择【报告】页面。
    
2.  转到【可视化】窗格，选择【簇状柱状图】。
    
3.  进入字段列表，展开 “Sales” 勾选 “Sales” 度量值。
    
4.  进入字段列表，展开 “Budgets” 勾选 “Budget” 度量值。
    
5.  进入字段列表，展开 “Calendar” 勾选 “Month Short” 字段。
    
    ![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPYdanNJ0yXOIZP17zzlnZDYA1gXolJslGDjY9dic21PLbm3USfdawYQjLcbl3qXGy7cJiahDKBld9Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
    

_图 4-15 虽然在图片中很难看到，但 “Calendar” 甚至是按照正确的顺序排序的_

这是相当惊人的，因为一切看起来都很好。至少，在【刷新】解决方案之前它是这样的。但如果单击【刷新】将会令人失望，如图 4-16 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPYdanNJ0yXOIZP17zzlnZDHgwHAP24woxnSlawb8snSZ9dnwvibBE1mQ1sXJCp4UMpyHSxVntrkSg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

_4-16 这是怎么回事_

> 【注意】
> 
> 如果刷新后没有报错，说明和这里的情况有所不同，处于学习目的，建议用户通过本节示例文件来学习，了解情况。

为了解决这个问题，此时需要编辑这些查询。先看一下其中一个原始数据查询，看看 Power BI 是如何复制 Excel 表的。

1.  转到【主页】【转换数据】。
    
2.  选择 “Raw Data - Budgets”。会立即发现有些地方不对，如图 4-17 所示。
    

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPYdanNJ0yXOIZP17zzlnZD3GGW49MpPf4j7SFzCArEXWmTGmJRd6tHA7rxzEnHy38j0k5qVo388A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

_图 4-17 为什么 “Date” 列所有的值都显示为 “Error”_

在阅读错误信息时，可以看到该列正试图将 “43131” 设置为一个日期。但是这个数字是怎么来的呢？

1.  选择 “Source” 步骤，单击齿轮图标。
    

在这里看到的是 Power BI 在文件中创建的表，这是从 Excel 中复制数据的结果。有趣的是，它的 “Date” 列中不包含日期，而是包含一列数值，如图 4-18 所示。

_图 4-18 “Date” 列为什么会有这么多数值而不是日期_

在这个特定的步骤中，有如下三件事一定要注意到。

1.  这个表完全包含在 Power BI 中，如果需要对源数据做任何更改，必须在这里更新（在【刷新】时，对 Excel 文件的更新不会流入该文件）。
    
2.  所有的日期都被复制为日期序列号（自 1900 年 1 月 1 日以来的天数），而不是可识别的日期。
    
3.  在这一步中，Power BI 显示的数据量是有限制的。如果超过了这个限制，Power BI 就不允许用户编辑这个表，因为这个表是使用压缩的 JSON 格式创建的，如果超过了这个限制，就不能直接编辑 Power Query 公式来增加数值。
    

虽然查询中是有错误的，但并没报错，这并不是用户操作的问题。

（译者注：Power BI 在导入的时候，实际是将查询导入为查询，将数据模型导入为数据模型，这是分开进行的，导入的数据模型是一定与 Power BI 数据模型兼容的，因此，数据模型中不会报错；而导入的查询，并没有执行，因此也不会报错。直到点击【刷新】运行查询，看到错误。）

在关闭这个对话框并返回到 “Changed Type” 步骤后，仍然会遇到这样的错误，它报错称不能将 “43131” 的值设置为日期。所以来重写 “Changed Type” 步骤。

1.  选择 “Date” 列并单击【日期】数据类型图标。
    
2.  将数据类型改为【整数】。
    
3.  选择【替换当前转换】（不是【添加新的步骤】）。
    

结果错误消失了，现在看到的是满满一列的整数（代表日期序列号），如图 4-19 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPYdanNJ0yXOIZP17zzlnZD1oe5dX2m0Tun826H8La2QDdHgBDVTvf405FhARrOutuZcQDTNxuBvA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

_图 4-19 我们有我们的日期序列号_

> 【注意】
> 
> 一个奇怪的细微差别是，“Date” 列顶部的错误栏可能继续显示为红色。如果发生这种情况，要么暂时忽略它，要么选择另一个查询，并返回到 “Raw Data - Budgets” 查询，以强制它更新。

因此，虽然这是一个进步，但显然仍还不理想，因为仍希望将数据类型设置为【日期】。但问题是，如果把 “Date” 列改为使用【日期】数据类型，并替换掉包含在 “Changed Type” 步骤包含的现有数据类型，那么将回到错误开始时的位置。相反，此时需要按如下步骤进行操作。

1.  选择 “Date” 列并单击【整数】数据类型图标。
    
2.  将数据类型更改为【日期】。
    
3.  选择【添加新的步骤】（不是【替换当前转换】）。结果将完全符合要求，如图 4-20 所示。
    

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPYdanNJ0yXOIZP17zzlnZDaUmHpRTKjhic1Fb8wSq8ol6xgEbdfEwoqsdjvpDfIoMk2H9OQqxuLTQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

_图 4-20 “Date” 列数据正常显示_

记住，如第 3 章数据类型和错误中所述，一旦更改了数据类型，任何后续的更改都将基于这个输出。虽然不能将一个基于【文本】类型的数值改为【日期】类型，但可以将【文本】类型更改为值，然后将值类型更改为【日期】。

现在这已经完成了，也需要对 “Raw Data – Sales” 查询采取同样的步骤。要做到这一点，需要进行如下操作。

1.  选择 “Raw Data – Sales” 查询。
    
2.  选择 “Date” 列并单击【日期】数据类型图标。
    
3.  将数据类型更改【整数】。
    
4.  选择【替换当前转换】（不是【添加新的步骤】 ）。
    
5.  选择 “Date” 列（再次）并单击【整数】数据类型图标。
    
6.  将数据类型更改为【日期】。
    
7.  选择【添加新的步骤】（不是【替换当前转换】）。
    

完成此操作后，就可以通过进入【主页】【关闭并应用】，让 Power BI 应用这些改变来最终完成查询。然后，数据就会顺利加载。

> 【警告】
> 
> Power BI 导入 Excel 表格并将其转换为 JSON 表格的方法有一个与专门与导入日期列有关的错误。在这个错误被修复之前，导入任何一个带有日期列的 Excel 表到 Power BI，都需要做上述的调整。

尽管在数据类型方面存在缺陷，但这个功能对于从 Excel 导入数据模型到 Power BI 中是非常有效的。而且就像原来的 Excel 解决方案一样，它完全包含在一个文件中，Power BI 的解决方案也是如此，这使得它非常容易与别人分享，而无需更新数据源。

尽管如此，使用这种方法也有一些潜在的危险。请记住，当完成后，需要对源数据进行的任何更新都需要编辑 “查询” 和更新 “Source” 步骤。这可能会使事情变得很尴尬，因为不仅要编辑和导航查询结构来编辑源数据，而且它往往很慢，因为必须等待查询预览更新。但即使是这些问题也不是真正的杀手，一旦表超过了一定的大小，Power BI 就会拒绝让用户做任何进一步的修改，告诉用户该表超过了大小限制，如图 4-21 所示。

_图 4-21 对不起，无法修复在 “Raw Data – Sales” 查询中发现的不正确的记录_

> The Table exceeds the size limit：表大小超过了限制。

> 【注意】
> 
> 实际工作中，不会将 Excel 中的表作为数据库且不再更新，不仅导入时会限制大小，又无法很好地处理。出于这个原因，建议用户尽量少使用这个功能。建议从外部文件（无论是 Excel 工作簿、数据库或任何其来源）导入数据，而不是将其存储在同一文件中。

### 4.2.4 导入时保持连接

前面的示例通过将数据复制到文件中，从 Excel 中导入了一个数据模型，但这是两种不同的选项之一。另一种方法是，不将数据从 Excel 复制到 Power BI 文件中，而是与保存数据的 Excel 文件建立一个连接。

虽然这确实会产生风险，即用户必须更新一个外部文件的路径，但它避免了与日期有关的错误，以及无法在数据源中添加行或修改记录的风险。数据将继续存在于 Excel 文件中，这意味着在 Excel 文件中进行的任何添加、删除或更新都只需简单的刷新即可。

来重做之前的例子，但这次选择创建一个与 Excel 文件的连接，而不是复制数据。这样做的步骤如下。

1.  打开一个新的 Power BI 桌面文件。
    
2.  转到【文件】【导入】【Power Query, Power Pivot, Power View】。
    
3.  浏览到以下位置的文件：
    

“第 04 章 示例文件 \\Simple Model.xlsx”。

4.  选择该文件【打开】。
    
5.  单击【启动】【保持连接】。
    

> 【注意】
> 
> 虽然【复制数据】选项被推荐为默认选择，但【保持连接】才是一个更好的方法。

同样，Power BI 将导入数据并创建数据模型、关系和度量值。再一次，可以快速建立前一个例子中的簇形柱状图，如图 4-22 所示。

1.  选择 Power BI 窗口左侧的报告页面。
    
2.  进入【可视化】窗格，【簇形柱状图】。
    
3.  进入字段列表，展开 “Sales”，选择 “Sales” 度量值。
    
4.  进入字段列表，展开 “Budgets”，选择 “Budget” 度量值。
    
5.  进入字段列表，展开 “Calendar”，选择 “Month Short” 列。
    
    ![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPYdanNJ0yXOIZP17zzlnZDYA1gXolJslGDjY9dic21PLbm3USfdawYQjLcbl3qXGy7cJiahDKBld9Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
    

_图 4-22 这看起来很熟悉_

此时，用户可能会认为所有结果都与前面示例中的结果相同。唯一的区别是，在本例中，数据仍然存在于 Excel 文件中，数据是从那里导入的，而不是复制它并把数据存储在 Power BI 文件中。所以现在，如果 Excel 文件移动了。用户需要通过编辑查询来更新数据源，或者通过以下方式更改数据源。

1.  【主页】【转换数据】【数据源设置】。
    

实际上，这个具体的解决方案有一个非常大的区别。Power BI 应用于将查询指向 Excel 文件的结果，在不需要任何修改的情况下，查询会被刷新，如图 4-23 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPYdanNJ0yXOIZP17zzlnZDibxv5FcWEYpaETvGGhb8VoA3ag4P82icxHqK31mEicx14OeZA5pVjYwnw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

_图 4-23 这就是希望从副本中获得的进展_

## 4.3 在工具之间迁移查询的思考

现在已经对在 Excel 和 Power BI 文件之间轻松移动查询的方法有了充分的了解。一般的经验法则如下。

1.  如果想要特定的查询或查询组，并且不考虑数据模型，那么只需复制和粘贴。
    
2.  如果想把整个解决方案从 Excel 转移到 Power BI 中，请导入它（最好是选择保持与 Excel 文件的连接） 。
    

目前没有涉及的一个解决方案是，从 Power BI 导入到 Excel 的方法。不幸的是，由于 Power BI 的数据模型版本比 Excel 的数据模型版本更新，并且支持许多新的功能，微软并没有提供一种方法来实现这一点。乍一看，这意味着要把解决方案从 Power BI 移动到 Excel 中，唯一的方法是复制和粘贴查询，然后手动重建数据模型。

Ken 的 Monkey Tools 插件确实包含一个将 Power BI 模型导入 Excel 的功能。虽然它显然不能创建 Excel 的数据模型不支持的项目，但它可以重建查询结构、多对一关系和度量值。而且它甚至还提供了一个未能正确导入的列表。无论用户只想提取和导入查询，还是整个数据模型，Monkey Tools 都可以轻松完成这一任务。如图 4-24 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LPYdanNJ0yXOIZP17zzlnZDC4S5NibotozhOa1Hm4wPdu0oZS7n8NWSm86RlxNy8J7aPDjTia7MFbOA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

_图 4-24 使用 Monkey Tools 将 Power BI 模型导入到 Excel 中_

> 【注意】
> 
> 可以在 Ken 的网站上了解更多关于这个插件的信息，并可以下载一个免费试用。

（译者注：在实际中，由于 Power BI 数据模型中支持的 DAX 特性已经远远超过 Excel 数据模型支持的范围，所以一般不存在把 Power BI 数据模型导入到 Excel 中的需求。另外，即使需要从 Excel 中使用 Power BI 数据模型，也可以通过透视表直接连接 Power BI 数据模型。具体可以参考译者网站。）

正在学习 Power Query 吗？可以加入本主题的交流群一些交流分享。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNhia5Pc4XC1Um7IYgQhGEoEC1yK05ibUFoPBYpcoAMvibuZh2BZaibMzULeDwNfSeQ0KHRcDUdX3FzVA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**Power Query 真经连载**

往期推荐

[

Power Query 真经 - 前言



](https://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650791950&idx=1&sn=bc3e8ad6a5227ec65ab6bfab127d3797&chksm=f18ce01fc6fb6909bfcb46566f6bc442e9d983449936db9c43baf9a140a492124b2f1a430b03&scene=21#wechat_redirect)

[

Power Query 真经 - 导言：一场新的革命



](https://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650791970&idx=1&sn=8d4d020790002c23f2c5fcf96634abdf&chksm=f18ce033c6fb6925fa91b3c2939ec957007b3bcbf124af39233bab7b3df3f504de13dda49a8c&scene=21#wechat_redirect)

[

Power Query 真经 - 第 1 章 - 基础知识



](https://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650792095&idx=1&sn=64be944a0dc61db368492cbee5961cad&chksm=f18ce08ec6fb69980cace536c3659d4b42e14a1fa497f7d03e280374f0db6aef600dddabf81a&scene=21#wechat_redirect)

[

Power Query 真经 - 第 2 章 - 查询管理



](https://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650792336&idx=1&sn=2688e47daed09b17c10930b381349f96&chksm=f18ce181c6fb6897453398f3386999b6c76c9175e7417995e1b591fec340eca042f6a608a9cc&scene=21#wechat_redirect)

[

Power Query 真经 - 第 3 章 - 数据类型与错误



](https://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650792422&idx=1&sn=2bcdc5b321352c4f929c1783cf3040d2&chksm=f18ce1f7c6fb68e172d445f7553cfd3b1cbce99da1382e4b2098d72adf6f8c51f89ceb29cf36&scene=21#wechat_redirect)

**Power BI 终极系列课程《BI真经》**

[

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/09hv4Xua0LNBM1lxlQYHJBicic4CvPoRGLqHgdTZOr8goNRh0asDXA48mRDzc9zxW4UMQiayHwgDmx7mlt4cQxtjg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

BI真经 - 让数据真正成为你的力量





](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650788512&idx=1&sn=76972ff4b0cf265fe9479c6457b04b47&chksm=f18cd2b1c6fb5ba7386eb0bb835280bd8a651bfe0481cc78f20fc30b80c60d2d4cb7eb5b1e3e&scene=21#wechat_redirect)

扫码与精英一起讨论 Power BI，验证码：data2022  
扫码与精英一起学习 Power Query，验证码：PQ真经

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOiad5BOrdQTKpB733esKiaxZa53LXWIPlQicMjxntaRr3a2hnMmuibTib8QacXeiakucDr7lSNGkuV2MXw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击“阅读原文”进入学习中心

**↙**
