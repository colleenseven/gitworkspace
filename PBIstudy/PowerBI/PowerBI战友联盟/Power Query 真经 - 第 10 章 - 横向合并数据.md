---
create_date: 2022-09-29T11:34:16 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power Query 真经 - 第 10 章 - 横向合并数据
source: https://mp.weixin.qq.com/s/ra4u-WwR1sSbMhGW5PDUZg
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

导语：Power Query 是可证明的，在这个星球上性价比最高的数据处理工具，如果你的工作中需要处理数据，注意，是处理，不是分析，那么此工具必须掌握。对此，90%的鼠标点击，5%的猜测以及5%的公式能力足以。本文来自《Master Your Data》的第十章，非常重要，必须掌握。

___

用户经常需要将两个独立的数据表进行合并，以便后续制作透视表。虽然 SQL 专业人员可以很轻松地通过不同的方式实现，但如果仅用传统 Excel 公式，用户需要使用复杂的 VLOOKUP 或 INDEX + MATCH 组合函数，才能将数据从一个表中匹配到另一个表中。当 Power Query 出现后，用户可以不用学习 SQL 连接、Excel 复杂公式或者学习如何建立关系型数据库结构，就可以使用另一种轻松的方式将两个表合并在一起。

## 10.1 合并基础知识

在这个例子中：同一个 Excel 工作表中有两个独立的数据源，一个是销售交易表 “Sales”，另一个是包含产品细节的 “Inventory” 表。连接两个表的的重点在于选择两个表之间正确的连接字段。

这个案例的问题在于，“Sales” 表有 “Date” 列、“SKU” 列（最小存货单位）、“Brand” 列和 “Units” 列，但缺少有关于产品的 “Price” 或 “Cost” 等其他信息。然而这些以及更多的信息是包含在 “Inventory” 表中的，如图 10-1 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFBI2icIK0K9QIAdCrslvXUCpYneITBPZSN9qEBwHbgOhFLdxA1GgRaHDQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-1 在 Excel 中的 “Sales” 表和 “Inventory” 表

通常需要把这两个表合并在一起，来得到一个完整的产品清单以及相关详细信息。

### 10.1.1 创建暂存查询

无论是选择直接打开 “第 10 章 示例文件 / Merging Basics.xlsx” 文件在同一个 Excel 工作簿中执行这项任务，还是从 Excel 中创建一个外部链接数据源，或者使用 Power BI 从 Excel 表中读取数据，以下方法都是可以的。现在需要做的是先为这两个数据表各创建一个 “暂存” 查询。

1.  创建一个新的查询，连接到 “第 10 章 示例文件 / Merging Basics.xlsx” 文件中的两个表。
    
2.  将每个查询保存为 “暂存” 查询（【禁用加载】或设置为【仅限连接】）。
    

> 【注意】
> 
> 为了在 Excel 中【合并】或【追加】查询，查询必须存在。仅仅在 Excel 工作簿中放置最终合并好的表并不是最好的方式，应该分别放置暂存查询再进行显性的合并操作。

完成后，应该有两个简单的查询可以使用，如图 10-2 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFBHNevcIibrvLBsiavqXl47VzJcBjpJc4M3s31UrCp7q2HjVsH2ial058Dw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-2 现在 “Sales” 查询和 “Inventory” 查询可以进行合并

### 10.1.2 执行合并

和【追加】查询一样，Excel 用户可以通过右击【查询 & 连接】窗格中的 “Sales” 查询来【合并】查询。同样，与【追加】查询一样，这将导致在 Power Query 用户界面上出现一个名为 “Source” 的步骤，将两个查询【合并】。由于这很难被快速理解，请选择右击并【引用】查询，这样就可以把每个步骤看作是查询中的一个单独的行项目。

1.  右击 “Sales” 查询【引用】。
    
2.  【重命名】为 “Transaction”。
    
3.  进入【主页】选项卡【合并查询】【合并查询】（不是【将查询合并为新查询】）。
    

> 【注意】
> 
> 【将查询合并为新查询】命令将复制在 Excel 的【查询 & 连接】面板看到的过程，创建一个新的查询并在第一步中执行合并。

此时，会弹出【合并】窗口，在这里可以选择要与哪张表进行合并。

在这个对话框中，当前活动的查询（在这个例子中，“Transaction” 源于 “Sales” 查询）将显示在表格的顶部。在这个查询的数据预览下方，有一个下拉菜单，可以选择解决方案中的任何查询，就是用户希望与当前数据合并的表。

> 【注意】
> 
> 这个对话框也允许用户对查询本身进行合并，这是一种高级技术，将在第 14 章看到。

由于查询的当前状态是基于 “Sales” 表的查询数据，所以选择针对 “Inventory” 表进行合并。

1.  在下拉菜单中选择 “Inventory” 表。
    
2.  将默认的连接类型设为 【左外部 (第一个中的所有行，第二个中的匹配行)】。
    
3.  不勾选【使用模糊匹配执行合并】复选框。
    

奇怪的是，在做出所有的配置选择后，【确定】按钮并没有亮起，如图 10-3 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFBKc4XayClU2icsxSicicHd7ia2y9d9fYicvmX2TEA8kqbly5w6eBK04amp1Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-3 已经选择了表，但是为什么不能继续呢

因为 Power Query 不知道要用哪些字段来进行【合并】。

为了进行【合并】，最好有一个列，在一个表中包含唯一的值，在另一个表中可以有重复的记录，这被称为一对多关系结构，该结构是确保最终得到的结果与所期望的一致的最好方法。

> 【注意】
> 
> Power Query 还支持一对一和多对多的连接。

在本例中，“SKU” 列在 “Inventory” 表中包含唯一值，而在 “Sales” 表中有重复记录，使用这一列连接两边。

1.  分别单击 “Inventory” 表和 “Sales” 表中的 “SKU” 列标题。
    
2.  单击【确定】。
    

现在将进入 Power Query 编辑器，在 “Sales” 表的右边有一列新表列，如图 10-4 所示。

图 10-4 一个新的表列，包含匹配的 “Inventory” 录

前面已经学习如何扩展表列，这里唯一的问题是要明确需要哪些列。由于 “SKU” 列和 “Brand” 列已经存在于 “Sales” 表中，所以在扩展时将这两列排除在外。

1.  单击 “扩展” 图标（“Inventory” 列标题的右侧）。
    
2.  取消勾选 “SKU” 列和 “Brand” 列的复选框。
    
3.  取消勾选【使用原始列名作为前缀】的复选框，单击【确定】。
    

现在，已经把产品细节合并到了 “Sales” 表中，如图 10-5 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFBHGj8HaQcJ5BMmOowRMOQsDic25H0dQHdlMyw9vUk4LU4gk6MCaXtRfg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-5 此时 “Inventory” 表的详细信息被合并到了 “Sales” 表中

一共有 20 条记录，在原来的 “Sales” 表中每笔交易都有一条记录，这样就完全实现了 Excel 的 VLOOKUP 精确匹配或 SQL 左外连接的相同功能。

## 10.2 连接类型

作为 SQL 专家们多年来知道的常识，连接数据实际上有多种不同的方法。遗憾的是，这一事实对 Excel 专业人员来说却并不熟悉，因为在 Excel 中通常只看到【左外部】连接（VLOOKUP）的例子。然而，在 Power Query 中，可以通过【合并】对话框支持多种不同的连接类型。这些连接类型不仅可以找到匹配的数据，还可以找到不匹配的数据，这对任何试图匹配或汇总记录的用户来说都是非常重要的。

考虑一下如图 10-6 所示的两个表格。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFB9exIOicu4OHCD4xIoFEa4kN1EzFcO8UXRLTIuRicRPhAe25hWibZUTxkQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-6 这些记录能匹配吗

这些表之间的数据是相关的，但其中有几个细微差别。

第一个细微差别是右边的 “Chart of Accounts” 表。这个列表提供了系统中所有 “Account” 的独立列表，但需要结合 “Account” 和 “Dept” 字段，生成唯一的标识符。仔细观察，会发现 “Account” 列前四行的数值在接下来的四行中重复，所以很明显存在重复的情况。同样地，“Dept” 列的前四行都包含 150 的值，而后四行包含 250 的值。如果用分隔符连接，就会得到每个都是唯一值如：“64010-150、64020-150、64010-250” 等。在左边的 “Transaction” 表中也可以看到这种相同的情况。

这意味着可以通过匹配 “Transaction” 表中的数据来获得 “Chart of Accounts” 表中的 “Name”，前提是可以根据两个表之间的 “复合键” 来进行匹配，如图 10-7 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFBXWQvtIofnka1hrj2lbVOYLQXRrYYK4DSMDrR9ViafibbYjeB0gHkibJEg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-7 此时目标是根据 “Account”+“Dept” 的组合来匹配 “Name” 列

第二个细微差别是阴影行。在上面的图片中，可以看到在 “Chart of Accounts” 表中没有 “64015-150” 或 “64010-350” 组合的条目。而在 “Transaction” 表中也没有 “Special” 或 “Pull Chart” 名字的账户。

就这一问题而言，又分为不同的情况，其问题严重性也不同。“Chart of Accounts” 表是一个包含 “Transaction” 可以被记入的账户的表格。因此，如果存在一个从未使用过的账户，这其实不是一个大问题。但在另一方面，如果一个交易被记入一个不存在的账户，或是帐户部门组合，这就是一个大问题了。

> 【注意】
> 
> 这个问题不仅限于会计数据。它存在于任何需要在两个列表之间进行匹配、比较或调整的场景。例如：客户与信用额度，销售人员与订单，零件与价格，有无数种可能出现该问题的场景。

现在看一下这两个表之间可以进行的七种具体的连接配置，可以用于合并数据，或提取感兴趣的部分。

> 【注意】
> 
> 在合并数据时，数据类型是非常重要的。在执行合并之前，始终确保用于连接的列已经使用正确的数据类型，并且与之连接的列的数据类型是一致的。

到现在为止，用户应该对创建【仅限连接】的 “暂存” 查询相当熟悉了，所以不再详细介绍这个过程。可以打开 “第 10 章 示例文件 / Join Types.xlsx” 文件，其中已经包含了 “Transactions” 表和 “COA” 表（即 “Chart of Accounts” 表）的 “暂存” 查询，如图 10-8 所示。

图 10-8 关于 “Transaction” 和 “COA” 的 “暂存” 查询

### 10.2.1 左外部连接

该功能在 Power Query 叫做：【左外部 (第一个中的所有行，第二个中的匹配行)】。

【左外部】连接如图 10-9 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFBZImb2ibBsDBQZ3d1XUy7XNicVdI56gtodq7vszFPfE71dl3TNkDhjTqA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-9 【左外部】连接：所有记录从左边开始，匹配从右边开始

第一个【连接种类】是默认的连接类型：【左外部】连接。这种连接的工作方式是返回左表（顶部）的所有记录，以及右表（底部）的匹配记录。右表（底表）中没有匹配的记录将被忽略。

创建步骤如下所示。

1.  确定哪个表是 “左” 表（此示例中使用 “Transaction” 表）。
    
2.  右击 “左” 表的查询，选择【引用】。
    
3.  将查询【重命名】为 “Left Outer”。
    
4.  转到【主页】选项卡【合并查询】。
    
5.  选择 “右” 表，即 “COA” 表。
    

此时，必须暂停并处理之前讨论的第一个细微差别。合并两个表的键是，需要以 “Account” 字段和 “Dept” 字段的组合为基础。虽然可以通过使用分隔符【合并】列，但实际上没有必要这样做。先单击 “Left Outer” 表的 “Account” 列，按住 Ctrl 键并选择 “Dept” 列。在 “COA” 表重复这个操作即可，如图 10-10 所示。

图 10-10 使用复合键连接【合并】表

连接列的顺序将按照用户选择它们的顺序用 “1”、“2”、…… 来表示。请记住，只要选择顺序一致，数据列在查询之间不需要相同的顺序。

> 【注意】
> 
> 虽然在视觉上没有创建连接，但这些列是使用隐含的分隔符连接的。这一点很重要，因为如果有产品 1 到 11 和部门 1 到 11，Power Query 将正确连接数据。使用隐含的分隔符可以避免基于 111 键的模糊连接，而是将这些值视为 1-11 或 11-1。

> 【警告】
> 
> 预览底部的指示器提示根据 Power Query 的数据预览，会给出一个预估匹配情况。虽然这个数字在这个例子中是正确的：左表的 8 条记录中只有 6 条与右表相匹配，但要记住，预览可能被限制在每个表的 1,000（或更少）行。这意味着，完全有可能看到一个匹配度不高的预估数据，而实际上在完整执行时是完全匹配的。

单击【确定】确认连接，将生成名为 “COA” 的新列（“COA” 是作为连接的 “右侧” 的表的表名）。为了便于说明，将按如下方式展开列。

单击 “COA” 列上的扩展图标，勾选【使用原始列名作为前缀】的方框，单击【确定】。

结果将如图 10-11 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFBIkzRpnfFrfvxboLY5unM5lDIQU3xOhn2zHXYItymbj2BC0tRyTuCNQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-11 【左外部】连接的结果

这里需要注意的关键事情如下所示。

1.  前 6 行包含来自左边 “Transaction” 表的结果，以及来自右边 “COA” 表的匹配细节。
    
2.  第 7 行和第 8 行显示来自 “Transaction” 表的结果，但显示 “COA” 表的匹配结果为空。
    
3.  当数据被加载到工作表或数据模型时，所有的 “null” 值将被加载为空值（什么都不显示）。
    

在正常的情景中为了避免重复，不会在右边的表中展开 “Account” 列和 “Dept” 列。这里保留是为了演示这些列不包含值，因为在 “COA” 表中没有找到匹配的记录。

### 10.2.2 右外部连接

该功能在 Power Query 叫做：【右外部 (第二个中的所有行，第一个中的匹配行)】。

【右外部】连接如图 10-12 所示。

图 10-12 【右外部】连接，所有记录从右边开始，匹配从左边开始

如前所述，【左外部】连接是默认的。现在来看看【右外部】连接。

对于这个连接，将使用与【左外部】连接几乎完全相同的步骤如下所示。

1.  确定希望哪个表成为 “左” 表（本示例中使用 “Transaction” 表）。
    
2.  右击 “左” 表的查询【引用】。
    
3.  将查询重命名为 “Right Outer”。
    
4.  转到【主页】选项卡，单击【合并查询】。
    
5.  选择 “右” 表（即 “COA” 表）。
    
6.  按住 CTRL 键，依次选择每个表中的 “Account” 列和 “Dept” 列。
    
7.  将【连接种类】选择为【右外部】【确定】。
    

此时，可能会发生一件奇怪的事情：数据中的某一行可能会显示所有列的空值，除了包含匹配 “右” 表对象的那一列（即 “COA” 列），如图 10-13 所示。

图 10-13 第 5 行显示表格前有一堆空值

虽然它看起来很奇怪，但这是完全可以预测的。这只是意味着在右表中的条目在左边的表格中没有匹配。可以扩展这个表来查看。

1.  单击 “COA” 列上的【扩展】图标，勾选【使用原始列名作为前缀】的复选框，单击【确定】。
    
2.  结果看起来将如图 10-14 所示。
    

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFBumKOJ5Uhjo5A7dWkgTEDGqkkZgsUyHvavFYA8nSfPrSaC8UycVzdwQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-14 【右外部】连接的结果

这一次，“COA” 列都填入了数值，但是由于 “Special” 和 “Pull Cart”（显示在第 5 行和第 7 行）没有交易被匹配，所以这些列显示为空值。

### 10.2.3 完全外部连接

该功能在 Power Query 叫做：【完全外部 (两者中的所有行)】。

【完全外部】连接如图 10-15 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFBOzyibT7N7cmdrlzesz8NH4SibtZGdUcDzPLwrM7n3PnEOanPSTlfge2A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-15 【完全外部】连接：两个表中的所有记录

在相同的数据上使用【完全外部】的连接类型时会得到什么？再一次使用相同的步骤，只改变【连接种类】，如下所示。

1.  确定需要用哪个表作为 “左” 表（本案例中使用 “Transaction” 表）。
    
2.  右击 “左” 表查询【引用】。
    
3.  将该查询重命名为 “Full Outer”。
    
4.  进入【主页】选项卡【合并查询】。
    
5.  选择 “右” 表（即 “COA” 表）。
    
6.  按住 CTRL ，选择每个表中的 “Account” 列和 “Dept” 列。
    
7.  将【连接种类】选择为【完全外部】【确定】。
    
8.  单击 “COA” 列上的【扩展】图标，勾选【使用原始列名作为前缀】的复选框，单击【确定】。
    

【完全外部】连接完成后看起来如图 10-16 所示。

图 10-16 【完全外部】连接的结果

在这个例子中，注意不仅有表之间匹配的记录，还有通过【左外部】连接暴露的所有不匹配的结果（第 9 行和第 10 行），以及【右外部】连接不匹配的结果（第 5 行和第 7 行）。当试图了解两表的差异时，这种方式可以非常方便查看到数据不一致的地方。

> 【注意】
> 
> 这种【连接种类】还说明了为什么在比较两个表时，用户经常希望从连接所基于的右表展开列。如果与左表不匹配，则键只出现在连接右侧的结果中。。

### 10.2.4 内部连接

该功能在 Power Query 叫做：【内部 (仅限匹配行)】。

【内部】连接如图 10-17 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFBO4gcTMPKla0pBIUzkELT0csPhxZl9IiaZ38JibO9D6Mx3FW1SQbeQIjQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-17【内部】连接：只有在两个表中都有匹配的记录

对于这个连接，依然使用与前面的查询相同的步骤，当选择【内部】连接后，结果将如图 10-18 所示。

_图 10-18 【内部】连接的结果_

这个连接产生的数据显然比之前所有的连接要少得多。是因为它只返回两个表之间可以匹配的记录的结果。

### 10.2.5 左反连接

该功能在 Power Query 叫做：【左反 (仅限第一个中的行)】。

【左反】连接如图 10-19 所示。

图 10-19 【左反】连接：左表的记录在右表中没有匹配值

到目前为止，所探讨的连接主要是针对匹配的数据。当对比两个数据列表的差异时，人们实际上更关心不匹配的数据而不是匹配的数据（具有讽刺意味的是，在会计领域花了大量的时间来识别匹配的数据，目的只是为了删除它们 ，人们真正关心的是那些不匹配的数据）。

图 10-20 显示的结果是按照与前面几种【连接种类】所使用的完全相同的步骤产生的，但【连接种类】选择的是【左反】。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFBj3VIR28PnVJtRSD0JGYcDUNLFuIoWHRiaN6xESWayGTfD8qXiarCs8ZQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-20 【左反】连接的结果

注意只有两条记录：两条交易在 “COA” 表中没有对应的 “Account” 列和 “Dept” 列的组合。

> 【注意】
> 
> 如果唯一的目标是识别左表中没有在右表中匹配的记录，就没有必要展开合并的结果。而且可以直接删除右边的列，因为无论如何每条记录都会返回空值。

### 10.2.6 右反连接

该功能在 Power Query 叫做：【右反 (仅限第二个中的行)】。

【右反】连接如图 10-21 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFBd8ht3De9OLziamjOxdDo32JQvVF9TRtC5sTkUObxaOJbywyLgDA7XAg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-21【右反】连接：右表中的记录在左表中没有匹配值

使用到目前为止一直使用的相同模式，但【连接种类】选择【右反】将产生如图 10-22 所示的结果。

图 10-22 【右反】连接的结果

如图所见，只有 “Special” 和 “Pull Cart” 账户存在，因为这是 “COA” 表中仅有的两个没有的交易项。

> 【注意】
> 
> 每次创建正确的【右反】连接时，连接的结果将显示一行空值，并在最后一列中显示一个嵌套表。这是意料之中的，因为左表中没有匹配项，导致每列的值为空。如果只查找不匹配的项，可以右击包含合并结果的列，然后选择【删除其他列】，再进行展开操作。

### 10.2.7 完全反连接

“完全反” 连接如图 10-23 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFBbRNRdMX6vNHAO6TH3t7Nxlw0hI7GdKoIZB9fqGr5RUXnZ1tfn8NPJQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-23 “完全反” 连接：所有记录均不匹配

另一种非常有用的连接类型是 “完全反” 连接，特别是试图识别两个列表之间不匹配的项时。坏消息是，这不是通过用户界面提供的默认连接类型来完成的。但好消息是，它很容易创建，如下所示。

1.  创建【左反】连接查询。
    
2.  创建【右反】连接查询。
    
3.  【引用】“Left Anti” 连接查询来创建新查询。
    
4.  转到【首页】选项卡，【追加查询】追加 “Right Anti” 连接查询【确定】。
    

结果与【内部】连接结果完全相反，因为完全反连接显示两个表之间不匹配的所有项，如图 10-24 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFBU9Dolup9Y13OHdXgraicf7G2giaDAsysPjdEGiaZsnxGJBXDGvD5uJgtw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-24 “完全反” 连接，显示无法匹配的数据

如图所见，第 1 行和第 2 行显示了【左反】连接查询的结果，表示左表中的记录在右表中没有匹配项。在它们下面的第 3 行和第 4 行中，可以看到【右反】连接中的项，这表示右表中的记录在左表中没有匹配项。此连接非常有用，因为它是所有未匹配项的完整列表。

> 【注意】
> 
> 【追加查询】时，主查询中不存在的列将被添加并用空值填充。如果删除了【左反】连接和【右反】连接中的空列，此模式仍然有效，前提是【右反】连接中的名称与【左反】连接生成的名称是一致的。

## 10.3 笛卡尔积（交叉连接）

无论将其称为 “交叉” 连接、“多对多” 连接或其正式名称 “笛卡尔积”，这种连接类型都包括从两个表中获取单个值并创建一组包含所有可能的组合。此处显示了此类连接的一个简单示例，需要一份所有产品的列表以及颜色，如图 10-25 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFBicOYicDiat6b1ClBDfk9HwAepBaxTslpMlsV2HsQQxczZ8iaUEjBhYbiblQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-25 “Color” 表和 “Product” 表之间 “笛卡尔” 连接的结果

### 10.3.1 方法

在 Power Query 中创建 “笛卡尔积” 可以通过一个简单的方法完成，如下所述。

1.  在每个要合并的表中。
    
2.  连接到数据源并执行任何所需的清洗步骤。
    
3.  转到【添加列】【自定义列】。
    
4.  使用 “MergeKey” 作为列名，公式输入 “=1”。
    
5.  右击其中一个表【引用】。
    
6.  使用基于 “MergeKey” 列的【左外部】连接与另一个表合并。
    
7.  删除 “MergeKey” 列。
    
8.  从新创建的列中展开除 “MergeKey” 之外的所有列。
    

> 【注意】
> 
> 可以使用不需要添加 “MergeKey” 列的方法，通过添加【自定义列】，公式等于另一个表的名称即可，虽然可以这样做，但使用 “MergeKey” 方法运行得更快（基于通过添加 “MergeKey” 列，大致可以减少 30% 的时间）。

### 10.3.2 实例

有了上面的方法，现在就使用 “第 10 章 示例文件 \\Cartesian Products.xlsx” 中的数据来学习这一点。本例的目标是获取一个包含固定每月费用的表，并为一年中的每个月创建一个预算表，如图 10-26 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFBkqyApPo2ibZd5ibGibkEPibF1x1lntdop8FBakVSBXrG2MTZiaibicjwkQJbQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-26 快速创建直线预算

使用上面的方法，从准备各自的数据开始。从 “Expenses” 表（如上图左侧所示）开始，进行如下操作，如图 10-27 所示。

1.  连接到数据源。
    
2.  转到【添加列】【自定义列】。
    
3.  将列名设置为 “MergeKey” 列，公式为 “= 1”【确定】。
    
4.  将查询加载为【仅限连接】查询。
    

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/09hv4Xua0LNlEFkwR76cndr8xTfEYoFBqBAIRuSAzk6OkoA8rqqS28okLpxg48FFGVbdxiaRx5bZ9yCSa4Ed2pw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-27 在 “Expenses” 查询中创建 “MergeKey” 列

然后，执行相同的步骤来设置 “Months” 表，添加 “MergeKey” 列，然后还将其作为【限仅连接】查询加载，如图 10-28 所示。

图 10-28 此时 “Month” 表已正确准备好

此时，只需确认要将哪个表用作 “左” 表（希望输出中的左边有哪些列）并执行【合并】。本案例中把 “Expenses” 表作为 “左” 表，以便复制最初的目标。

1.  右击 “Expenses” 查询【引用】。
    
2.  转到【主页】选项卡【合并查询】。
    
3.  选择要合并的 “Months” 查询，在每个表中选择 “MergeKey” 列【确定】。
    
4.  删除 “MergeKey” 列。
    
5.  从 “Months” 列展开除合并键（取消勾选 “MergeKey” 的复选框）列以外的所有列，取消勾选【使用原始列名作为前缀】的复选框【确定】。
    

现在有了一个完整的表格，其中每个月的费用类别都被记录在 “Months” 表格中，如图 10-29 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFBqfXzMF4letHGdIBJOXGUU3ecQjzIPvZia1CMTvGXuFRhn48BWZwjm0w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-29 一个线性预算表现在已经完成

此后，向 “Month” 表添加新月份，或向 “Expenses” 表添加新预算类别和金额，都可以通过一次刷新进行更新。

> 【注意】
> 
> 如果 “Expenses” 表中的值在每个月都保持一致，则此方法非常有效。在实际编制预算时，会有许多不符合这种结构的费用，但这不是问题。可以创建一个或多个单独的查询，并规范化为相同的列结构，然后【追加】到一个主表中。

### 10.3.3 意外问题

上一个例子显示了使用笛卡尔积可能非常有用的地方。不幸的是，实际操作中可能由于意外创建出一个不希望存在的笛卡尔积。考虑这样一个场景，其中有人将 2021 年 1 月添加到月份表中两次。在【刷新】后，将得到两个 2021 年 1 月的 “Property Tax” 结果、两个 “Insurance” 结果和两个 “Telephony” 结果，因为每个日期都将与 “Expenses” 表中的每个项目组合。

在这种情况下，解决这个问题的方法非常简单：在 “Months” 表中，右击 “Month” 列并选择【删除重复项】。这样做应该是安全的，因为不应该两次预测同一个月。

但是，在【合并】之前【删除重复项】也应谨慎。在本章的第一个示例中，尝试基于 “Brand” 列（存在于两个表中）合并 “Sales” 和 “Inventory” 表将创建笛卡尔 “Product”，从而在输出中产生重复的 “Sales” 表中的数据行。原因是虽然希望 “Sales” 表中有重复的行，但 “Inventory” 表中的 “Brand” 列中也有重复的项目，如图 10-30 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFBGT4INctCvAz75nBGD7N1R5QiacheJw7DGSdmonZYVZ4oD5zhSNr2NiaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-30 与 “SKU” 列不同，“Brand” 列将在【合并】时创建笛卡尔积

如图所示，在 “Inventory” 表中删除 “Brand” 列的重复项是不可取的，因为这样做会导致失去该供应商提供的两种产品中的一种。如果对 “Sales” 表的 “Brand” 列去重也会导致类似的问题。

为了避免意外产生的笛卡尔积，最好使用列分析工具来检查 “非重复值” 和 “唯一值” 的统计数据是否匹配如果 “非重复值” 和 “唯一值” 两个统计数据匹配，像本案例中 “SKU” 列一样（都是 “12”），那么该列可以安全的用作连接中 “右” 表的键，而不会产生问题，如果 “非重复值” 和 “唯一值” 两个统计数据不匹配，如本案例中 “Brand” 列一样，那么就会存在 “左” 表列中的值与 “右” 表列中的值多次匹配的现象，将会面临产生笛卡尔积的风险。

## 10.4 近似匹配

虽然 Power Query 提供了多种可以复制 “精确匹配” 连接的场景，但一种不存在的【连接种类】是执行近似匹配的功能。请记住，这不是一个 “模糊” 匹配（在后面会讨论这个问题），而是要查找并返回等于或介于两个数据点之间的值。Excel 用户知道此处是 VLOOKUP 近似匹配的场景，如图 10-31 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFBrGx3MC7p9opgep3kvyGd0KIuQMbDZ3RewhKRHic4HB1NhlxDIPlmspQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-31 查找最接近的 “Unit Price” 的值，但不超过某个值

在上面所示的情况下，购买者下的订单越多，价格就越优惠。问题是，查找表中没有 2,755 件的数据点，因此需要该订单数量的适当价格，即数量介于 2,500 到 5,000 件之间。由于客户尚未达到 5,000 件单价点，因此单价需要退回达到 2,500 单价层的 5.65 美元价格。

> 【注意】
> 
> 用户还会注意到，在上面的图片中，作者仔细地标记了数据下方的每一列。识别 “Key” 和 “Return” 列通常相当简单，因为它们通常是查找表中唯一的列。但另一个问题是，由于源表宽度不同，可能有多个列作为 ID 列。

### 10.4.1 方法

大多数用户会立即尝试利用 Power Query 的一种连接算法将这些表【合并】在一起。然而，这并不是这个案例中解决问题的方式。解决 Power Query 中近似匹配的方法如下。

-   步骤 1 ：连接到 “Source Table” 表和 “Lookup Table” 表。
    
    正常连接并清洗数据。
    
-   步骤 2 ：准备 “Lookup Table” 表。
    
    重命名 “Key” 列，以确保它们在两个表中匹配。
    
-   步骤 3 ：执行匹配。
    

1.  【引用】“Source Table”。
    
2.  转到【主页】选项卡，【追加查询】“Lookup Table”。
    
3.  筛选 “Key” 列，【升序排序】。
    
4.  筛选 “ID” 列，【升序排序】。
    
5.  右击 “Return” 列，【填充】【向下】。
    
6.  筛选 “ID” 列，取消勾选 “null” 值。
    

总的来说，这是一个简洁的方法，但请相信，这就是在 Power Query 中执行近似匹配所需的全部步骤。

### 10.4.2 示例

此示例的数据可在 “第 10 章 示例文件 \\Approximate Match.xlsx” 中找到，如图 10-32 所示。示例的目标是通过上述方法，即使用近似匹配来创建最右边显示的表。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFBytS92W3t8xMYwrc0CBYicnfGSpnuMKbPVH29dib0QB0CiamNLTMAXCGxw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-32 源数据和输出目标

该过程的步骤 1 是创建单个查询，来连接到 “Prices” 表和 “Orders” 表。这里的真正目标是将数据转换成干净的表格格式，确保列的名称正确且完整。这里已经准备好，只需连接到数据就足够了。

查询就绪后，可以转到步骤 2，其中包括确保两个表之间的 “Key” 列的名称一致。为此，请仔细确定所有方案组件。

1.  源表：这里是 “Orders” 表（如上图中所示），因为它包含了丰富的信息。此模式 “Source” 的 “ID” 列将是 “Order ID” 列，“Source” 的 “Key” 列将是 “Quantity” 列。
    
2.  查找表：这里是 “Price” 表（如左图所示），因为它包含返回（或合并）到源表中的值。具体来说，希望返回每列的价格，为此，在查找匹配项时，需要通过比较源键（“Quantity” 列）和查找键（“Units” 列）来计算出正确的值。
    

由于 “Key” 列的名称不一致，所以需要先来解决这个问题。由于不想破坏源数据，所以将在 Power Query 中进行更改，如图 10-33 所示。

1.  编辑 “Price” 查询。
    
2.  右击 “Units” 列【重命名】输入 “Quantity”。
    

图 10-33 更新的查找表（“Prices” 查询）

> 【注意】
> 
> 虽然选择重命名查找表中的 “Key” 列，但如果愿意，可以重命名源表中的 “Key” 列。最终目标只是确保每个表中的列名相同。

现在数据已经准备好，可以进入步骤 2，在这里实际创建匹配。

1.  右击 “源” 表（“Order” 表）【引用】。
    
2.  【首页】【追加查询】，追加 “Price” 查询。
    

如果滚动到预览的底部，结果现在应该如图 10-34 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFBaiad1LVhoTFX3ryyUsfMAGnUyUju0LqYUh0QRRpxaS4JWMX3wVjsCIA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-34 【追加】源表和查找表

正如已经知道的，在【追加】两个表时，具有相同名称的列被堆叠起来，具有新名称的列被添加到表中。这就是为什么确保键列在两个表之间保持一致非常重要的原因。用户还将注意到，对于 “Order” 表中的每个订单，当前 “Price Per” 显示为 “null”，而 “Price” 表中所有行的 “Order ID” 也显示为 “null”。

> 【注意】
> 
> 这里从 “源” 表开始的原因仅仅是因为通常希望在完成时将这些列放在输出的左侧，这样可以避免以后对列进行重新排序。如果用户想从 “查找” 表开始并【追加】“源” 表，那么这个方法仍然有效。

> 【警告】
> 
> 如果 “源” 表长度超过 1000 行，用户甚至可能无法在数据预览中看到 “查找” 表。不用担心，只需按照方法步骤操作即可。尽管它可能无法通过预览正确显示，但在加载时将对整个数据集执行这些步骤，并且方法将起作用。

现在，将采取以下步骤（是见证奇迹的时刻）。

1.  “Quantity” 列【升序排序】。
    
2.  “Order ID” 列【升序排序】。
    

此时，数据将如图 10-35 所示，“Price” 表的每一行显示在 “Order” 表的相关行上方。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFBFK3IvibRtcgXEyibGDWEf69giau9RDichSANLdcZCqZ8Jufh1ORIibTqYow/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-35 近似匹配几乎完成了

这个方法最巧妙的地方是对 “Key” 列（也就是 “Quantity” 列）的排序，因为这会以升序顺序将所有定价表的行与原始数据的行混合。然后对 “Order ID” 列进行第二次排序（如果有多个排序条件，则需要对多个 ID 列进行排序），这样做可以确保 “Price” 表中的行始终位于 “Order” 表中的行之前。（如果价格表中的 “Quantity” 值恰好于订单表中的订单数量一样，（比如在例子中的第 7 行和第 8 行中显示的 1000 行），那么对 ID 列的排序可以确保 “Price” 表中的行始终位于源表的数据行的上方。）。

1.  右击 “Price Per”【填充】【向下】。
    
2.  【筛选】“Order ID” 列，取消勾选 “null” 值。
    
3.  选择 “Quantity” 和 “Price” 列，转到【添加列】选项卡下的【标准】【乘】。
    
4.  将乘法列重命名为 “Revenue”。
    

就这样，“Price” 表中的行不再存在，但订单数量的价格以及作为所需输出表一部分的收入都存在，如图 10-36 所示。

图 10-36 成功复制了 Excel 的 VLOOKUP 函数的功能，并正确获得了近似匹配值

## 10.5 模糊匹配

到目前为止，本章中介绍的每个连接都要求两个表之间的数据具有某种一致性。数据点要么需要精确匹配，要么需要遵循有序逻辑。只要是使用计算机生成的数据，都能做到数据准确。但是，当试图将人工输入的数据与计算机生成的数据进行匹配时，会发生什么情况？

拼写错误、大小写、缩写、符号和替换术语只是导致匹配的数据集之间不一致的原因之一。由于 Power Query 的默认连接仅连接完全匹配的连接数据，因此它会显著影响比较两个列表的能力，如图 10-37 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFBM6y0fRiaqMpNJe8ase97avdJbuibZQl9YfhG1z8JY8FibV2KicMs95A55A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-37 手动填写 “Procuct” 表（左）并与 “Price” 表（右）进行比较

此示例的源数据可在 “第 10 章 示例数据 \\Fuzzy Match.xlsx” 中找到。

乍一看一切都很好，但在 Power Query 中执行标准的【左外部】连接后，基于 “Product \[Item\]” 和 “Price \[Item\]” 列的匹配，只有一条数据会生成正确的价格，如图 10-38 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFBw41ojmx3NgTgdzia7zHNnZ6l8F2iaswvt4YLEBjeqqJib96fy1uQNTiaew/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-38 这是一个灾难，因为只有 “Monitor” 的显示器有价格

从上图中可以看出，这是行不通的。从末尾带有额外 “s” 的条目（表示它们是复数），到小写的 “laptop” 与定价表中正确的大小写 “Laptop” 不匹配，再到 “Screen”，它是 “Monitor” 的替代，几乎没有匹配项。

在许多工具中，唯一的方法是返回并手动清理 “Products” 表。但对于 Power Query，有一种方法能够处理一些这种模糊性：即【使用模糊匹配执行合并】。

> 【注意】
> 
> 如果根据用户输入收集数据，那么最好先设置数据验证规则，以阻止用户输入不匹配的数据，而不是尝试通过模糊匹配来修复它。不幸的是，并不总是有这样的控制，这就是这个工具可以变得非常有用的地方。

### 10.5.1 基本模糊匹配

创建一个基本的模糊匹配实际上相当容易。在创建常规连接时，只需勾选【使用模糊匹配执行合并】旁边的复选框，如图 10-39 所示。

图 10-39 将常规匹配转换为 “模糊” 匹配

这一步骤会大幅改变输出，从而在合并 “Product \[Item\]” 和 “Price \[Item\]” 时产生以下结果，如图 10-40 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFBcVPC3vXia1lsu3NY5zeeXWmaPD4g0xILbhWBWQq5TqL9ibooVic8YsJmw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-40 利用 Power Query 的基本【使用模糊匹配执行合并】

在这里显示的这个例子中，Power Query 通过勾选【使用模糊匹配执行合并】复选框，将匹配项增加到了六个条目中的四个。但这是为什么呢？

Power Query 利用 Jaccard 相似性算法来度量实例对之间的相似性，并将得分为 80% 或以上的任何内容标记为匹配项。在这种情况下，该算法对 “Laptops” 和 “laptop” 的评分与 “Laptop” 相当，尽管其中一个有一个额外的字符，另一个使用小写和大写的字符。在标准连接无法匹配的情况下，诸如颠倒位置的字符（ friend vs freind ）和标点符号差异（ mrs vs mrs. ）也将匹配。

一般来说，在使用模糊匹配时，单词越长，拥有的字符越相似，返回精确匹配的可能性就越大。要理解这一点，请考虑以下两个词是相同的。

1.“Dogs” 与 “Cogs”。

2.“Bookkeeperz” 与 “Bookkeepers”。

这两个词只有一个字母不同，但由于字符较少，无法确定它们是错误的。

> 【注意】
> 
> 【使用模糊匹配执行合并】功能仅在文本列上的操作上受支持。如果出于任何原因需要对使用不同数据类型的列执行模糊匹配，则需要首先将数据类型转换为【文本】。

### 10.5.2 转换表

虽然基本的模糊匹配解决了一些问题，但也可以从前面的图示中看到，有两个记录仍然无法生成匹配：“Mice”（希望与 “Mouse” 匹配）和 “Screen”（需要与 “Monitor” 匹配）。根据 Jaccard 相似性算法，这些单词不够接近，无法标记为匹配。那么如何解决这个问题呢？

秘诀是创建一个特殊表，将一个术语从另一个术语转换为另一个术语，如图 10-41 所示。

图 10-41 简单的转换表

> 【注意】
> 
> 虽然此表的名称并不重要，但它必须包含 “From” 列和 “To” 列，以便正确映射和转换术语。

在这个示例文件中，这个表称为 “Translations”，将把它作为【仅限连接】查询加载到 Power Query。执行此操作后，创建利用此表的模糊匹配的过程将采取以下步骤。

1.  创建连接数据的查询。
    
2.  勾选【使用模糊匹配执行合并】的复选框。
    
3.  单击三角形展开【模糊匹配选项】。
    
4.  向下滚动并选择 “Transformation” 表作为【转换表】。
    

正如所见，在扩展合并结果后，现在所有的数据点都匹配得很好，如图 10-42 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFBd1HgpicbW2xftqPNhaicbxIAmic2eB3dkouLLwMsQc3poMNNibmDR4fhnA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-42 终于匹配了所有的数据

> 【注意】
> 
> 再次强调，通过设置数据验证规则，来确保终端用户输入信息的有效性是更好的解决方案。但至少现在有了一种方法来应对用户没有规范化输入的情况，就是把初始的输入信息输入 “From” 列，然后把正确的规范化的值输入 “To” 列。

### 10.5.3 降低相似度阈值

如前所述，Power Query 利用 Jaccard 相似性算法来度量实例对之间的相似性，并将得分为 80% 或以上的任何内容标记为匹配项。它还提供了收紧或放松相似性分数的选项。数字越高，匹配就越准确。换句话说，将其设置为 1（ 100% ）将显示所选连接类型的精确匹配要求。

虽然从未将模糊匹配的相似性阈值设置为 1，但可能会倾向于采用另一种方式并放宽限制。然而，在这样做之前，需要确保熟悉潜在的不利因素。

假设需要在此处显示的 “Product” 表 “Dept” 表之间匹配员工，如图 10-43 所示。

图 10-43 “Product” 表（左）和 “Dept” 表（右）

这里的挑战是：记录销售的职员使用 “Donald A” 的全名，人力资源部则称他为 “Don A”（不是 “Donald”）。这此匹配进行得怎么样？事实证明，即使使用基本的模糊匹配，也不太好，如图 10-44 所示。

图 10-44 等等 “Donald” 是谁

事实证明，“Don A” 和 “Donald A” 之间的相似性得分在 50% 到 59% 之间。鉴于这低于 80% 的默认值，它们无法匹配。

现在已经知道，可以通过创建一个单独的表来保存 “Don” 的别名来解决这个问题。不过，任何人都喜欢有选项，所以是否可以通过调整相似度阈值来解决这个问题，并避免添加另一个表。

执行此操作的选项（如提供翻译表）包含在隐藏【模糊匹配选项】的小三角形下，如图 10-45 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFBxXD9rYOJWzqNc4Cp3ex64ic8DXwwibXzj6UhWC19Ef0BMbzbp3RPMLEg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-45 放宽 Jaccard 相似性阈值

对于示例数据，将该值放宽到 0.6（60% 相似性）不会对输出产生影响。但将其降低到 50% 会发现 Donald 与之匹配，如图 10-46 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNlEFkwR76cndr8xTfEYoFB2iaqQRTjF07n1ak4Z8HOiaIwErlHc7MciclcIjIupibe8ODrkV1bkETiaUQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图 10-46 终于把 “Donald” 与另一张表配对了

乍一看，这真是太棒了。已经成功地将 “Donald” 与 “Don” 匹配，而无需向解决方案中添加另一个表。但仔细观察会发现有些地方不太对劲。

在放宽相似性阈值之前，将六个销售记录与六名员工进行匹配，并返回六行。为什么现在有七个？

如果仔细查看第 4 行和第 5 行，可以看到 “Ron” 和 “Don B” 已与 “Depts” 表中的正确员工代码匹配。但是，在第 6 排，“Don B” 也被标记为 “Ron”。

在这里看到的是一个设置得太低的匹配容差，并显示为假阳性。此外，它还创建了一个意外（模糊）笛卡尔积。

> 【警告】
> 
> 除非绝对必要，否则避免依赖降低相似性阈值。这是一个危险的工具，可能导致数据不匹配和意外的笛卡尔积。

虽然基本模糊匹配可能会导致匹配中出现误报（毕竟匹配到 80% 的相似性），但 Power Query 团队提供了一个默认值，该值限制了误报的数量，同时仍提供了模糊匹配功能。只有在知道其含义并且在更改后应始终查看匹配结果的情况下，才应更改此阈值。

### 10.5.4 保持模糊匹配的策略

当然，这里的大问题是 “如何维护依赖于模糊匹配的解决方案？” 这看起来很吓人，尤其是刷新一个相对较新的解决方案并不断提出问题时。

为了建立一个依赖于模糊匹配的可维护系统，建议采取以下措施。

1.  在合并数据之前，替换已知需要修复的频繁出现的字符术语或模式。也就是说，如果知道计算机生成的查找表在地址前从不包含 “#” 符号，但源表可能包含以这种方式写入的地址，只需右击该列并将该列上的所有 “#” 符号替换为空即可。
    
2.  利用本章前面讨论的一种完全反连接模式，在每次刷新后获得一个异常表（未知项），供查看。
    
3.  创建 Excel 或 DAX 公式，以计算异常表中未知项目（行）的数量，并将其返回到报表页面，以便于查看（每次刷新时，将能够看到未知项的计数是否为 0 ，或者转换表是否需要添加其他项）。刷新后，将拥有一种检验机制，不仅可以提醒是否存在任何未知项，同样的解决方案还可以准确列出未知项。
    

在有未知项的情况下，可以将它们连同它们映射到的术语一起输入到转换表中（强烈建议尽可能使用 “例外” 表中的 “复制 / 粘贴” 到 “翻译” 表中，以确保拼写正确）。如果正确输入了所有缺少的术语，则应进行完整刷新，以正确匹配所有内容。

根据数据的干净程度和刷新频率，每次刷新时不匹配的数量都会减少。原因很简单：正在构建的是一个术语词典，每当遇到问题时，这个词典就会变得越来越强大。

> 【注意】
> 
> 模糊匹配算法不仅存在于合并操作中，而且也在其他特性中出现，例如分组特征和最近的新特征（称为聚类值）。虽然在此书出版前，这些体验仅在 Power Query 在线版体验中可用，但 Power Query 团队的目标是在所有版本的 Power Query 之间实现一致性，因此希望在不久的将来，将在最喜爱的 Power Query 产品集成中看到这些功能。

正在学习 Power Query 吗？本系列足以。可以加入本主题的交流群一些交流分享。

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

[

Power Query 真经 - 第 8 章 - 纵向追加数据



](https://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650793474&idx=1&sn=23cf9792cc040c03d8a74183454aeff2&chksm=f18ce613c6fb6f0579ec6004dcea4206b7b92b8873bc1ba818fc90b7ecae60bedcefd0756274&scene=21#wechat_redirect)

[

Power Query 真经 - 第 9 章 - 批量合并文件



](https://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650793756&idx=1&sn=fdc0278cd820933235eee96370988f29&chksm=f18ce70dc6fb6e1b40aebe67eb94fabd076144625e26453a3e076d500bf9313d7b231d5b9314&scene=21#wechat_redirect)

[

Power Query 真经 - 第 10 章 - 横向合并数据



](https://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650794776&idx=1&sn=e5d7a9c53941938a09b72553096f9f01&chksm=f18ceb09c6fb621f11bbc5d0cb90aa823357efea934fd4c9db79c5124cfbd59848e8c9fc49ef&scene=21#wechat_redirect)

**Power BI 终极系列课程《BI真经》**

[

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/09hv4Xua0LNBM1lxlQYHJBicic4CvPoRGLqHgdTZOr8goNRh0asDXA48mRDzc9zxW4UMQiayHwgDmx7mlt4cQxtjg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

BI真经 - 让数据真正成为你的力量





](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650788512&idx=1&sn=76972ff4b0cf265fe9479c6457b04b47&chksm=f18cd2b1c6fb5ba7386eb0bb835280bd8a651bfe0481cc78f20fc30b80c60d2d4cb7eb5b1e3e&scene=21#wechat_redirect)

扫码与精英一起讨论 Power BI，验证码：data2022

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOiad5BOrdQTKpB733esKiaxZa53LXWIPlQicMjxntaRr3a2hnMmuibTib8QacXeiakucDr7lSNGkuV2MXw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击“阅读原文”进入学习中心

**↙**
