---
create_date: 2022-05-16T13:15:35 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power Query 真经 - 第 8 章 - 纵向追加数据
source: https://mp.weixin.qq.com/s/dHci7ARnuM3pjrev62ROzA
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

数据专业人员经常做的工作之一是将多个数据集追加到一起。无论这些数据集是包含在一个 Excel 工作簿中，还是分布在多个文件中，问题是它们需要被纵向【追加】到一个表中。

类似这一需求的一个常见场景是，每月从中央数据库中提取的数据需要合并用来进行年初至今的分析。在 2 月份，用户提取了 1 月份的数据，并将其发送给分析师。然后在 3 月份的时候，用户又将 2 月份的数据发送给分析师，分析师将数据添加到解决方案中，如此循环，按月持续到全年。

处理这种解决方案的经典 Excel 流程最初通常可以归结为以下几点。

1.  将一月份的文件导入并转换为表格格式。
    
2.  将数据转化为正式的 Excel 表格。
    
3.  根据 Excel 表格建立分析报告。
    
4.  保存该文件。
    

然后，在每月的基础上按进行如下操作。

1.  导入并转换新收到的数据文件。
    
2.  复制新的数据，并将其粘贴到原始表格的末尾。
    
3.  刷新报告和视觉对象。
    

虽然可以这样做，但这个过程显然不是够完美的，因为这里有一些非常明显的问题。本章不会解决用户在转换中触发错误的问题（尽管以后的章节会解决），但会向用户展示 Power Query 如何合并两个或更多的数据集，而不必担心用户把最后几行的数据粘贴过来导致数据重复。

## 8.1 基本追加

“第 08 章 示例文件” 包含三个 “CSV” 文件：“Jan 2008.csv”、“Feb 2008.csv” 和 “Mar 2008.csv”。本节将介绍导入和追加每个文件的过程。

导入文件非常简单，如下所示。

1.  创建一个新的查询【来自文件】【从文本 / CSV】。
    
2.  浏览 “第 08 章 示例文件 / Jan 2008.csv”【导入】【转换数据】。
    

Power Query 将打开该文件，并为该数据源自动执行以下步骤。

1.  将第一行提升为标题，显示列为：“Date”、“Account” 、“Dept” 和 “Amount”。
    
2.  数据类型自动转换为【日期】、【整数】、【整数】和【小数】。
    

为了数据类型的转换更加稳妥，不再依赖于系统默认的自动转换，这里删除 “Changed Type” 步骤，并重新创建它，迫使 “Date” 根据它的来源数据格式美国标准导入。

1.  删除 “Changed Type” 步骤。
    
2.  更改 “Date” 列的数据类型【使用区域设置】【日期】【英语 (美国)】【确定】。
    
3.  更改 “Amount” 列的数据类型【使用区域设置】【货币】【英语 (美国)】【确定】。
    
4.  更改 “Account” 列的数据类型【整数】。
    
5.  更改 “Dept” 列的数据类型【整数】。
    

此时，查询将如图 8-1 所示。

图 8-1 加载前的 “Jan 2008” 查询

由于用户的目标不是只报告一月份的销售情况，所以此时把这个查询只作为一个连接来加载，为以后追加数据做准备。

> 【注意】
> 
> 在 Power BI 中，可以右击查询，取消勾选【启用加载】复选框，而在 Excel 中，需要转到【主页】【关闭并上载至】【仅创建连接】【确定】。

现在用完全相同的步骤导入 “Feb 2008.csv” 和 “Mar 2008.csv” 文件，导入完成后应该有如下所示的三个新查询，每个都作为一个连接加载。

1.  Jan 2008。
    
2.  Feb 2008。
    
3.  Mar 2008。
    

完成后，三个查询都应该在 Excel 的【查询 & 连接】窗格中，或在 Power Query 编辑器的【查询】导航窗格中也可看见，如图 8-2 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMDVa47HScOlsXldabrQBNAWVUyTK2icEjKAT8DWYDZM4xJWpBamlT8Vockap3FUwfBwV2YIdNf62w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 8-2 这些查询显示在 Excel 的【查询 & 连接】窗格（左）和在 Power Query【查询】导航窗格（右）

### 8.1.1 追加两个表

下一项工作是创建用于后续分析的整个表，这需要将上述表格追加在一起。在 Excel 中完成这项工作的一个方法是，右击【查询 & 连接】窗格中的任意一个查询，并选择【追加】。此时将弹出如图 8-3 所示的对话框。

图 8-3 【追加】查询对话框

虽然这看起来相当容易，但实际上建议用户不要使用这个功能来追加表。是的，它允许用户追加两个查询（如果有需要，的确可以将一个查询追加到自身）。它甚至允许用户一次性追加多个表，只需要切换到【三个或更多表】视图进行操作。但这里有一些注意事项。

1.  在 Power BI 中没有【查询 & 连接】窗格，建议用户学习一种能在多个程序中都适用的方法来做到这一点。
    
2.  这将创建一个名为 “Append 1” 的新查询，它将所有合并的表合并到【应用的步骤】窗口中的一个 “Source” 步骤中，使得检查更加困难。
    

与其使用这种功能，更建议用户学会对第一个表进行【引用】，然后在 Power Query 编辑器里面执行【追加】操作。这些方法的主要区别在于，这个方法可以在任何拥有 Power Query 的工具上工作，而且它还会为【追加】到查询的每个表记录一个不同的 “Appended Query（追加的查询）” 步骤。有了不同的步骤，以后检查查询变得非常容易，而不是把未知数量的查询都合并到一个 “Source” 步骤中。

将选择使用 “Jan 2008” 查询作为最初的数据，并向它追加（仅）“Feb 2008” 查询。

1.  右击任意一个查询【编辑】，然后展开【查询】导航器窗格。
    
2.  右击 “Jan 2008” 查询【引用】。
    
3.  将 “Jan 2008” 查询重命名为 “Transactions”。
    
4.  转到【主页】【追加查询】。
    
5.  【要追加的表】选择 “Feb 2008”【确定】。
    

此时的结果将如图 8-4 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMDVa47HScOlsXldabrQBNADlbcBiaoA2PNfiavdq1yKP3SCU1RRaAQUMJnYRNriblduQw5Ytokf059w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 8-4 将 “Feb 2008” 查询追加到 “Transactions” 查询的结果

> 【注意】
> 
> 如果用户直接从 Excel 用户界面【追加】查询（或者在 Power Query 窗口中，选择 “Jan 2008” 查询后直接转到【主页】【将查询追加为新查询】），会有一个名为 “Source” 的步骤。虽然【应用的步骤】窗口中的步骤会比较少，但这意味着用户必须单击 “Source” 步骤，并阅读公式栏来了解发生了什么。在这个示例中，检查跟踪非常清楚，因为 “Source” 步骤指向 “Jan 2008” 查询，可以清楚地看到另一个查询被【追加】到了这个数据上。

此时，用户可能很想向下滚动查询，看看是否所有的记录都在那里。不幸的是，这并没有显示全部数据，因为 Power Query 实际上并不会在窗口加载所有的数据，而是显示数据的预览。它显示的行数随用户添加的数据而变化，可以在 Power Query 编辑器的左下角看到这一点，如图 8-5 所示。

图 8-5 Power Query 向用户显示了它现在可以处理的预览行数

当然，这里存在一个问题：如果用户不能看到所有的数据，那怎么知道数据是否成功追加了呢？答案是要加载查询。所以把数据加载到一个工作表中，看看能得到什么，结果将如图 8-6 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMDVa47HScOlsXldabrQBNAw7jf6GiaZ3zx3oxejIfJgJGSibicxnZQCftFvELrVSWnPbFTA3mzEmPZg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 8-6 【查询 & 连接】窗格显示，“Transaction” 查询有 3,887 行记录

> 【注意】
> 
> 要在 Power BI 中查看数据量，进入【数据】视图（在左侧），在【字段】列表中选择要查看的表。行数将显示在界面的左下方。

为了验证和可视化加载到 Excel 中的数据量，可以在这里用数据透视表来汇总数据。

1.  选择 “Transaction” 表中的任何单元格【插入】【数据透视表】。
    
2.  将【数据透视表】放在当前工作表的 F2 单元格中。
    
3.  将 “Amount” 拖到数【值】。
    
4.  将 “Date” 拖到数【行】。
    
5.  右击 F3 单元格【组合】【月（仅）】【确定】。
    

一旦完成，会看到有一个【数据透视表】，显示 “Jan 2008” 表和 “Feb 2008” 表确实合并为一个表了，如图 8-7 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMDVa47HScOlsXldabrQBNA8zuGnhuTIzBjwpwh5cc8Ibf2xJEBvw72l4ia76WGgoF0zmjoMIoicY4g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 8-7 “Jan 2008” 和 “Feb 2008” 交易数据现在在一个【数据透视表】中

### 8.1.2 追加额外的表

此时，用户想把三月的记录也追加到 “Transaction” 查询中。这就是那些在【查询 & 连接】窗格中使用【追加】功能的 Excel 用户的苦恼所在。他们的本能是右击 “Transaction” 查询，然后将三月份的数据【追加】到它上面。这种方法的问题是，它将创建一个新的查询，而不是将这一步骤添加到 “Transaction” 查询中。由于【数据透视表】是基于 “Transaction” 表的结果，所以此时需要在 “Transaction” 查询中添加新的【追加】步骤，而不是添加一个新的查询步骤。

为了将三月的数据添加到现有的 “Transactions” 查询中，需要编辑 “Transactions” 查询。此时，用户需要做出选择。是编辑现有的 “Appended Query” 步骤，还是添加一个新的步骤呢？这个问题的答案实际上取决于随着时间的推移，用户将向解决方案添加的数据量，以及用户希望检查跟踪此查询的清晰程度。

比方说，用户将在一段时间内添加 12 个追加项，并且不希望有一个很长的步骤列表。在这种情况下，按如下操作即可。

1.  单击 “Appended Query” 步骤旁边的齿轮，弹出的【追加】对话框选择【三个或更多表】。
    
2.  选择需要追加的每个表，单击【添加】。
    

此时结果如图 8-8 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMDVa47HScOlsXldabrQBNAnKpN4tIncJDlzmI5qZNXl7eC2jIWPa3ic6VUtH5FOLicJSCiagkn6V0kg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 8-8 在一个步骤中添加多个追加项

或者，如果想要一次执行一个查询，并专注于创建一个易于使用的检查跟踪路径，那么可以在每次向数据源添加一个新的查询时采取如下操作。

1.  右击 “Transaction” 查询【编辑】。
    
2.  进入【主页】【追加查询】。
    
3.  选择新增加一个【追加查询】。
    

此时结果如图 8-9 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMDVa47HScOlsXldabrQBNARceicssibH1lFH87JCRarvlpE1CZnry7gM3sSOiaSVtTuzcbC8I6k32KA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 8-9 一次添加一个查询，创建不同的步骤

事实上，用户如果想让检查线索更加清晰，可以右击步骤名称并选择【属性】，来修改步骤名称并提供在悬停时显示的注释。

此时结果如图 8-10 所示。

图 8-10 设置步骤名称与工具提示描述

要自定义步骤名称并添加工具提示，只需右击步骤并选择【属性】。这将允许用户修改默认的步骤名称，并添加一个自定义的描述，在鼠标悬停在信息图标上时显示出来。

> 【警告】
> 
> 除了 “Source” 步骤之外的所有步骤都可以用这种方式重命名。要重新命名 “Source” 步骤，需要学会编辑查询的底层 M 代码。

> 【注意】
> 
> 关于编辑默认查询名称有两种观点。虽然编辑每个步骤的名称以使其更具描述性是很诱人的，但对于一个真正的 Power Query 专家来说，挑战在于他们现在需要花更多的时间来检查每个步骤，来理解公式实际上是什么。本书建议使用默认的步骤名称并与它们的实际操作联系起来，而可以使用 “描述”（【说明】）功能来记录关于操作意图的注释。

无论用户决定用哪种方式将三月的表追加到数据集上（通过编辑现有的步骤或创建一个新的步骤），现在都是时候加载数据并验证三月数据的追加是否真的成功。

现在，要重新考虑 Power Queries 在加载到 Excel 表格时的一个不幸的问题。当用户查看包含【数据透视表】的工作表时，可以看到 “Transaction” 查询（也就是 Excel 表），确实保存了所有的 6,084 行数据，之前三个月数据的总和。然而，【数据透视表】并没有改变，如图 8-11 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMDVa47HScOlsXldabrQBNAZomB2WLPic6a9B5n8aRQ4E6eibicqvEiaFySJjaE0Iyc7icNWOozIDa1Huw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 8-11 “Transaction” 表已经更新，但【数据透视表】却没有更新

这不是什么大问题，只是一个小小的不便和提醒。如果用户把数据加载到一个 Excel 表中，然后把它放入到一个 【数据透视表】中，是需要刷新【数据透视表】，以便让更新的数据流入【数据透视表】。

右击【数据透视表】【刷新】。

此时，【数据透视表】确实更新了，如图 8-12 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMDVa47HScOlsXldabrQBNAXdBJLSCrgjA7ibd4PwA7ENo4k5Xx4MRfK93GBBsKRZy1fXYsXOpmzPA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 8-12 一月到三月的记录现在显示在一个【数据透视表】中

> 【注意】
> 
> 记住，如果查询被加载到 Excel 或 Power BI 的数据模型中，点击一次【刷新】就可以更新数据源和任何透视或可视化对象。

显然，每月编辑文件来添加和转换新的数据源，然后将其【追加】到 “Transactions” 查询中，这种方法很快就会过时。在第 9 章中，将向用户展示一种更简单的方法。但事实如这里所示，追加和编辑单独的追加项，是一项重要的技能，用户必须掌握它，才能熟练地使用 Power Query。

## 8.2 追加列标题不同的数据

在【追加】查询时，只要被合并的查询的列标题是相同的，第二个查询就会按用户所期望的那样被【追加】到第一个查询上。但是，如果这些列没有相同的列标题呢？

如图 8-13 所示，“Date” 列的名称在 “Mar 2008” 的查询中变成了 “TranDate”，而分析师并没有注意到。当 “Jan 2008” 和 “Feb 2008” 的记录被【追加】时，一切都很正常。但是当分析师把 “Mar 2008”【追加】到记录的表中时，事情就变得糟糕。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMDVa47HScOlsXldabrQBNAn0KooZ4soic69uYO0T6GKKg8KwKBrh97l9N1qu4BDGtUgyNFPxjeMcw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 8-13 Power Query 如何知道 “TranDate” 列值应该进入 “Date” 列呢

当【追加】两个表时，Power Query 将从第一个查询中加载数据。然后扫描第二个（和后续）查询的标题行。如果任何标题不存在于现有列中，新的列将被添加。然后，它将适当的记录填入每个数据集的每一列，用 “null” 值填补所有空白。

按这个逻辑，这意味着 “TranDate” 列（出现在三月的查询中）在一月和二月中被填充为 “null” 值，因为 “Jan 2008” 的查询没有 “TranDate” 列。

另一方面，由于源文件中的列名改变了，“Mar 2008” 查询没有 “Date” 列，而是拥有 “TranDate” 列。“Date” 列为每个三月记录填充了 “null” 值，而 “TranDate” 列则保存了本应在 “Date” 列中出现的值。

解决这个问题的方法如下所示。

1.  编辑 “Mar 2008” 的查询，将 “TranDate” 列重命名为 “Date”。
    
2.  编辑 “Transaction” 查询。
    
3.  转到【主页】【刷新预览】。
    

公平地说，预览应该自己刷新，但上面的单击步骤强制执行了这一点。

> 【注意】
> 
> 想自己试试吗？【编辑】其中一个月度查询，并将其中任何一列重命名为不同的名称。返回到 “Transactions” 查询，此时将看到新命名的列。

## 8.3 在当前文件中追加表和区域

虽然从外部文件中检索和【追加】数据是很常见的，但 Excel 用户也会使用这种功能来【追加】同一工作簿中的数据表。

当【追并】少量的表时，只需要使用上面描述的方法即可。

1.  为每个数据源创建一个【暂存】（【仅限连接】）查询。
    
2.  【引用】表。
    
3.  追加其他的数据。
    

但是，如果用户想构建一个体系，其中 Excel 就像一个准数据库一样，用户按月创建一个新表，在工作簿中保存该月的交易，会发生什么情况？分析师真的想手动调整查询来每月【追加】一个新表吗？并非如此。能否设置一个解决方案，在刷新时自动包含所有新表？

这个问题的答案是肯定的，它涉及到利用在第 6 章中使用的 Excel.CurrentWorkbook 函数来读取动态命名范围。

来看一些具体的例子，从 “第 08 章 示例文件 \\Append Tables.xlsx” 开始。

这个特定的文件包含三个表，其业务表示某水疗中心每月发行的礼品券。每个工作表都以月和年命名，并用空格隔开，每个工作表都包含一个表格。虽然每个表格也是以年和月命名，但这些日期部分用 “\_” 字符分隔的（ Jan\_2008，Feb\_2008，等）因为表格名称中不允许有空格。

每个月，记账员都会勤奋地创建和命名一个新的工作表，并设置和命名该表作为他们月末工作的一部分。他们似乎忽略了一件事，就是把礼品券的发放日期或到期日期放在表中，如图 8-14 所示。

图 8-14 一月份礼品券信息的示例数据

那么，如何才能建立一个解决方案，使它自动包含记账员添加的所有新表，而不必教记账员如何编辑 Power Query。

### 8.3.1 合并表

不幸的是，Excel 中没有按钮可以对当前工作簿中的可见对象创建查询，所以需要去从头开始创建这整个查询，如下所示。

1.  创建一个新的查询【数据】【获取数据】【自其他源】【空白查询】。
    
2.  将查询重命名为 “Certificates”。
    
3.  在公式栏中输入以下内容：
    

```
=Excel.CurrentWorkbook()
```

此时可以看到表格列表，而且是利用在前几章学到的技巧，用户可以单击 “Content” 列中 “Table” 单词旁边的空白处来预览数据，如图 8-15 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMDVa47HScOlsXldabrQBNAC93AKDupibZwg2eVwWVogmppPJXvA2oBGKyibDQYr8o3SQFNFmtSKNnw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 8-15 预览 “Jan\_2008” 表内的记录

如果仔细观察 “Content” 列的右上角，会发现它有一个图标，看起来像两个指向不同方向的箭头。这是一个很酷的功能，本质上允许用户【展开】每一个表，所有的操作都是一次性完成的。这个功能被称为扩展操作，最有价值的地方是，因为 “Name” 适用于表 “Content” 列中的每一行，展开后它将与此前对应的每一行相关联。

按如下所示进行操作。

1.  单击 “展开” 箭头，展开 “Content” 列。
    
2.  取消勾选【使用原始列名作为前缀】的复选框【确定】。
    

数据很好地展开了，保持了 “Name” 列的细节，如图 8-16 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMDVa47HScOlsXldabrQBNAFicYr22USWVMxtfibFbb4XwAuI5z64zwOF5By3t3OqLXe9bToOc1kf2A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 8-16 子表已经被【展开】

> 【注意】
> 
> 请记住，列名和数据将根据上一节中所涉及的规则进行展开，所以，如果此时列命名不一致，则会看到一些列中有空值。

要做的下一件事是将 “Name” 列转换为有效的月末日期列。由于 “Jan\_2008” 不是一个有效的日期，需要要用一个小技巧把它变成一个有效的日期，然后再更改成月末日期。

1.  右击 “Name” 列【替换值】。
    
2.  将 “\_” 字符替换为 “ 1 ”（空格 1 空格）。（译者注：为了构成日期格式形态，为了后续转换。）
    
3.  选择所有列【转换】【检测数据类型】。
    
4.  选择 “Name” 列，转到【转换】标签【日期】【月份】【月份结束值】。
    
5.  右击 “Name” 列【重命名】“Month End”。
    

现在，完成的查询将看起来如图 8-17 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMDVa47HScOlsXldabrQBNAricu7wrv6DibzAeEO4xVTBhicg3PogWRL2ll6P2cTdfkdXyVa6zWEpNjQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 8-17 完成查询，准备就绪

这里一切看起来都很好，然而当选择【关闭并上载】时，会看到触发了一个错误，这很奇怪。单击查询旁边的刷新按钮，会看到错误的数量发生了变化，错误增加到了 63 个如图 8-18 所示，这是什么原因？

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMDVa47HScOlsXldabrQBNAnAUopicxkJcu8MiceIKic9micMzdI0kHibjlnibshbwhVUcu5jNJqgxVZ5nw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 8-18 “63 个错误”？但它看起来如此之好

那么发生了什么？回去检查这个查询。但在这之前，请确保将 “Certificates” 工作表移动到工作簿的最后，如图 8-19 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMDVa47HScOlsXldabrQBNADD1Zaia4v94hu0hDWEkrUvLFxOR3QaAP86hrwgxTPzHp5Z5utsibyU6A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 8-19 Certificates 工作表，现在是选项卡顺序中的最后一个

> 【注意】
> 
> 通常情况下，由于有点麻烦可以不用移动这个工作表，但这有助于确保用户与本书在这里相同位置看到错误。

移动工作表之后，右击 “Certificates” 查询【编辑】，选择 “Source” 步骤。

此时，将会注意到比之前多列出了一个表，作为这个查询的输出而创建的 “Certificates” 表，如图 8-20 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMDVa47HScOlsXldabrQBNArD5TM8icRVqMriakZSWOUIkpPP9adEhEibpvSUVjC0iciarnCyibBzUCHLRg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 8-20 新查询显示在所有工作簿查询的列表中

> 【注意】
> 
> 如果在选择 “Source” 步骤时没有看到 “Certificates” 表，那因为 Power Query 已经缓存了数据预览。可以通过进入【主页】【刷新预览】来解决这个问题，事实上，由于缓存的问题，在调试查询时，总是应该刷新。

> 【警告】
> 
> 当使用 “=Excel.CurrentWorkbook ()” 来列举表或范围时，输出的查询在刷新时也会被识别，为了处理这个问题，需要一些新的步骤，有不同的方式，这取决于用户如何构建查询。

现在应该逐步执行查询的每个步骤，查看发生了什么。

当进入 “Replaced Value（替换的值）” 步骤时，是否注意到这里有什么危险的事情发生，如图 8-21 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMDVa47HScOlsXldabrQBNAwouoONmTVY2stDZuoOFXWzmadqu1xO3NMa6ZaeqT7uZiaw9Yc88Riatw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 8-21 假设下一步是将 “Name” 列转换为日期

接下来是检查 “Changed Types” 步骤，它试图将 “Name” 列中的所有数据类型转换为【日期】类型，但这显然不能用于 “Certificates” 数据。相反，这导致每个包含该文本的单元格会产生一个 “Error” 值，如图 8-22 所示。

图 8-22 将无效日期转换为错误

这个问题实际上是有利的，因为合并后的礼品券全表中的所有数据都是重复的。对这些抛出错误的行，可以简单地把它们筛选掉。

1.  确保 “Changed Types” 步骤被选中。
    
2.  选择 “Name” 列【主页】【删除行】【删除错误】。
    
3.  弹出的对话框【插入步骤】，单击【插入】。
    
4.  转到【主页】【关闭并上载】。
    

完成筛选后，会从 Power Query 中得到一个正面的结果，只加载 62 行数据，没有任何错误，如图 8-23 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMDVa47HScOlsXldabrQBNADCYHXMaNK3WSkiciaWN6kh1Baeu5AWDeicEvFzVPw5cw1tQMbrGFSnOfw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 8-23 从 3 个合并的表中加载 62 行数据

这个解决方案现在应该工作得很好，因为它加入了表名遵循 “月\_年” 格式的任何新表，但筛选掉了任何其他表。唯一的挑战是什么？现在要依靠记账员来记住正确命名这些表。鉴于它不是最明显的元素，这可能是危险的。

### 8.3.2 合并区域或工作表

现在，如果工作表没有表，而是由职员命名工作表呢，会怎么样呢？可以合并所有的工作表吗？是可以的，但正如第 6 章所提到的，没有内置函数可以从活动工作簿中的工作表中读取数据。相反，必须利用与命名范围对话的能力。一个特定的命名范围。诀窍是定义一个 “打印区域”，因为它有一个动态名称，可以通 “Excel.CurrentWorkbook ()” 公式枚举到这个名称。

1.  选择 “Jan 2008” 工作表，进入【页面布局】选项卡【打印标题】。
    
2.  在【打印区域】框中输入：“A:D”【确定】。
    
3.  对 “Feb 2008” 和 “Mar 2008” 工作表重复这一过程。
    
4.  创建一个新的查询【自其他源】【空白查询】。
    
5.  将该查询重命名为 “FromWorksheets”。
    
6.  在公式栏中输入以下内容：
    

```
= Excel.CurrentWorkbook()
```

现在会看到所有的表格和命名范围的列表，包括 “打印区域”，如图 8-24 所示。

图 8-24 使用 Excel.CurrentWorkbook 函数显示 “打印区域”

由于目前有两个表格和打印区域，现在来筛选并展开它，看看可以得到什么。

1.  筛选 “Name” 列【文本筛选器】【结尾为】“Print\_Area”【确定】。
    
2.  将 “Name” 列中的 “'!Print\_Area” 文字替换为空白（【替换为】不输入任何东西）。
    
3.  将 “Name” 列中剩余的文本（“'”）替换为空。
    
4.  展开 “Content” 列（取消勾选【使用原始列名作为前缀】复选框）。
    

注意，这里的情况有所不同。此时已经成功地创建了一个从工作表中读取数据的 “黑科技”，在 “打印区域” 中读取每一列，如图 8-25 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMDVa47HScOlsXldabrQBNAIquXciaDrLzj1G97iawgVNbujvicKm5GyPbWSgWguYo4ry9Y3wmrgNz2g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 8-25 原始的工作表

这显然意味着需要进行更多的数据清理，以便汇总这些范围并将其转换成干净的表格，但好消息是可以做到这一点。

需要注意的是，在应用这种技巧的场景中，将第一行提升为标题是有风险的，因为如果有人不关心日期列，他们可能会删除 “Feb 2008” 这一列，这就会导致出错。出于这个原因，这里采用手动重命名列的方法，通过设置数据类型触发错误，然后再将这些错误筛选掉。

因此，清理这个特定数据集的步骤如下所示。

1.  删除 “Column4”（因为它是空的）。
    
2.  将列重命名为 “Certificate”、“Value”、“Service” 和 “Month End”。
    
3.  右击 “Month End” 列【替换值】，在【要查找的值】下面输入一个空格，【替换为】输入 “1,”。（译者注：没错，是 “1,”，而不是 1。）
    
4.  设置 “Certificate” 列的数据类型【整数】。
    
5.  设置 “Value” 列的数据类型【整数】。
    
6.  设置 “Service” 列的数据类型【文本】。
    
7.  设置 “Month End” 列的数据类型【日期】。
    
8.  选择所有列并转到【主页】【删除行】【删除错误】。
    
9.  筛选 “Certificate” 列，取消勾选 “(null)” 值。
    
10.  选择 “Month End” 列【转换】【日期】【月份】【月份结束值】。
    
11.  转到【主页】【关闭并上载】。
    

完成后，会发现它提供的行数（以及数据）与之前构建的 “Certificate” 查询结果完全相同，如图 8-26 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMDVa47HScOlsXldabrQBNAxIfM4ZgDMO8GHtVF3HJNgib75DIu5BkvCDbR0t4fKZv4hOeSPWVYhUA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 8-26 两种方法，同样的结果

在处理 “打印区域” 时，尽量将 “打印区域” 限制在所需要的行和列，这是一个很好的建议，原因有二：第一是更多的数据需要 Power Query 处理的时间更长；第二是每一列在处理后会自动形成一推形如 “Column#” 的列，导致很多无意义的空列会被纳入进来，还需要再删除。

### 8.3.3 Excel.CurrentWorkbook

在使用 Excel.CurrentWorkbook 函数构建解决方案时，需要记住的最重要的一点是这个函数会读取当前文件中的所有对象。由于这会影响计算链，所以会受到递归效应的影响，这意味着随着新表的构建，Power Query 会识别它们并将它们也作为潜在的内容来读取。

当查询试图加载自身时，这种情况会在刷新时出现，从而在输出中重复了数据。当使用这种方法时，重要的是记住这一点并加以防范。

在这里，防止出现问题的策略包括筛选关键列上的错误，以及为输入和输出列使用标准命名，从而筛选掉不需要的列。

> 【注意】
> 
> 无论用户选择哪种方法，请确保在将其发布到生产环境之前通过刷新进行多次测试。

## 8.4 关于追加查询的最后思考

本章讲述的功能意义重大，假设用户有三个独立的文件，导入并将它们合并到一个单一的 “Transactions” 表中，并基于这些数据建立一个【数据透视表】或 Power BI 可视化。这就是一个基于三个独立文件的商业智能解决方案。

而当用户想刷新这个解决方案时，只需要单击【全部刷新】按钮就可以更新它。Power Query 将启动对 “Transactions” 表的刷新，这将启动对三个单独的数据表的刷新，为它提供数据。

假设现在这个解决方案是建立在没有特定日期的文件上，而它们是 “Product 1、Product 2 和 Product 3”。用户已经通过加载 “CSV” 文件构建了解决方案，这些文件包含了相关的数据，并针对它们建立了商业智能报告。然后，下个月来了，IT 部门给分析师发送了替换文件，为每个产品提供新的交易数据。

用户把新的 “Product 1” 文件覆盖到旧的文件上，对 “Product 2” 和 “Product 3” 做同样的处理。然后单击【全部刷新】，此时就已经完成了。

没错，只需要点击刷新，一切就完成了。

另外，追加查询的功能不仅能用于处理外部文件，也可以将当前工作簿中的所有表格或打印区域结合起来合并，创建一个用于分析的表。

因为 Power Query 的纵向追加数据功能，原有的工作时间被大幅缩短，并且不存在用户意外地复制粘贴数据导致数据重复的风险，这里根本不需要复制粘贴，只需要将一组数据追加到另一组，删除重复的标题。这种方式，可以构建同时拥有了速度和一致性两重优点的解决方案。

至此，已经探索了用外部数据源的手动追加，以及如何为工作簿中的数据生成自动更新系统，有没有可能把这些合并起来，创建一个系统，可以推广到合并一个文件夹中的所有文件，而不必在 Power Query 中手动添加每个文件？答案是肯定的，将在第 9 章继续讨论这个问题。

正在学习 Power Query 吗？可以加入本主题的交流群一些交流分享。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNhia5Pc4XC1Um7IYgQhGEoEC1yK05ibUFoPBYpcoAMvibuZh2BZaibMzULeDwNfSeQ0KHRcDUdX3FzVA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**Power Query 真经连载**

往期推荐

[

开始学习 Power Query 真经



](https://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650791937&idx=1&sn=e4ed2f9edcc0048ded16b246a3f8c512&chksm=f18ce010c6fb69062075ee8b9e4e38072e12189a90095ab2d9b02877f870533ec8fb85cfbb95&scene=21#wechat_redirect)

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

[

Power Query 真经 - 第 4 章 - 在 Excel 和 Power BI 之间迁移查询



](https://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650792560&idx=1&sn=145876f89d990391f0f3ea63f4033e7f&chksm=f18ce261c6fb6b779ffc9f8708ce8a31d378f1a14b3467267e2555d081a0fc36596241ec2b0b&scene=21#wechat_redirect)

[

Power Query 真经 - 第 5 章 - 从平面文件导入数据



](https://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650792761&idx=1&sn=45659b398623de1b7e32d8c770da96fe&chksm=f18ce328c6fb6a3ec527118bae565f7ee63b2a707af610f47b15d81b0dcfa74d9d4ff09650af&scene=21#wechat_redirect)

[

Power Query 真经 - 第 6 章 - 从Excel导入数据



](https://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650792864&idx=1&sn=82a5eb90a31faa0516b3d31b6d390323&chksm=f18ce3b1c6fb6aa797a0fa28fccec0e070f8f2f30af3b476699a0fab8fec27b790bc6205e782&scene=21#wechat_redirect)

[

Power Query 真经 - 第 7 章 - 常用数据转换



](https://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650793036&idx=1&sn=c2e59ca667c5eaef5b990914f89d1a14&chksm=f18ce45dc6fb6d4b8eec2e2ed4bab896f4c90b6d2165be785ed57f13dd632906202c6ad73f78&scene=21#wechat_redirect)

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
