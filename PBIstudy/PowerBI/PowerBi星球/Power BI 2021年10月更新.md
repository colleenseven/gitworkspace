---
ZK: Origin
create_date: 2021-10-17T13:00:09 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI 2021年10月更新
source: https://mp.weixin.qq.com/s/WRAkWTDOyIDlyY4mH8yDrQ
author: 
status: 未阅读
category: 
notes: False
uid: 
---

PowerBI 2021年10月的更新来了，本月的更新看起来依然很长的一个列表，主要是一些性能改进，没什么让人兴奋的新功能，这里就不再像之前的月份一样，单独挑几条实用的专门讲解，而是直接转载官方博客的内容，你可以快速浏览一遍，也许有你会用到的功能。

也可以在我的视频号中观看本月更新的官方视频讲解（已加中文字幕）:

下面是官方博客的文字讲解（机器翻译）：

https://powerbi.microsoft.com/zh-cn/blog/power-bi-october-2021-feature-summary/

___

更新列表

报告

-   热图图层 – Azure Maps Visual 
    
-   适用于 Power BI 数据集和 Azure 分析服务的 DirectQuery 
    
-   Bing 地图的租户级功能切换
    

数据建模

-   SWITCH性能优化
    
-   DAX 中的按位函数
    

数据连接和准备

-   Amazon Redshift
    
-   Dataverse
    
-   Google Analytics
    
-   Azure Cosmos DB V2
    
-   Azure Databricks
    
-   Amazon Athena
    
-   SIS-CC-SDMX
    
-   SumTotal
    
-   Usercube
    

服务

-   行政与治理
    
-   部署管道 API 
    
-   即将为 Microsoft Teams 自动安装 Power BI 应用
    

嵌入式分析

-   将 Power BI 报告导出到文件 API – 预览更新 
    
-   Power BI Embedded 现已普遍提供对象级安全性 (OLS)
    
-   调整嵌入式 Power BI 报表的缩放级别
    
-   更新了对 Power BI Embedded 的多地理位置支持
    
-   Power BI Embedded Playground 更新 – 使用您自己的嵌入令牌
    
-   Power BI Angular 组件
    

开发者

-   向您的自定义视觉对象添加现代工具提示
    
-   模态对话框 API 更新
    

可视化

-   Lollipop Bar Chart by Nova Silva
    
-   Drill Down TimeSeries PRO visual by ZoomCharts
    
-   Inforiver by Lumel
    
-   Hierarchical bar chart by Excelnaccess.com
    
-   New visuals in AppSource
    
-   Editor’s pick of the month
    

其他

-   对分页报告的 ODBC 支持 
    

正文

**报告**

**热图图层 – Azure Maps Visual** 

我们很高兴在此版本中将热图图层引入 Azure Maps Visual。

热图在地图上显示颜色模式以表示数据点的密度，使用一系列颜色并在地图上显示数据“热点”。热图是一种可视化具有大量点的数据集的好方法。

Azure Maps 处于预览状态，因此要打开它，请转到“文件”>“选项和设置”>“选项”>“预览功能”，然后将 Azure Maps Visual 切换为“开”。

热图的格式窗格允许用户自定义和设计热图可视化。格式窗格选项允许您：

-   使用像素或米为单位配置每个数据点的半径。
    
-   自定义热图图层的不透明度和强度。
    
-   指定大小字段中的值是否应用作每个数据点的权重。
    
-   从颜色选择器下拉列表中选择不同的颜色。
    
-   为要显示的热图图层设置最小和最大缩放级别。
    
-   确定不同层之间的热图层位置，例如3D条形图层和气泡层。
    

当用户想要可视化大量比较数据时，热图很有用：

-   比较不同地区或国家的客户满意度或店铺业绩。
    
-   测量客户访问不同地点的购物中心的频率。
    
-   可视化庞大的统计和地理数据集。
    

了解有关Microsoft Power BI 中 Azure Maps 热图的详细信息。 

**适用于 Power BI 数据集和 Azure 分析服务的 DirectQuery** 

我们针对 Power BI 数据集和 Azure 分析服务的 DirectQuery 的持续预览本月将获得一些更新。

**选择表格时更灵活**

以前，当你建立到数据集或 Azure Analysis Services 模型的 DirectQuery 连接时，你的模型包含所有表。在此版本中，我们为您提供了更多控制权！

首先，您可以使用字段列表从模型中删除表。通过这种方式，即使您连接到的数据集或模型中有更多表，您也可以保持模型整洁。请注意，如果连接到透视图，则无法从模型中删除表。

其次，当连接到数据集或模型时，您现在可以准确指定首先加载哪些表。如果您只是在寻找特定的表子集，则无需加载所有内容。

请注意，您还可以选择在与模型建立连接后自动添加任何可能添加到数据集或模型的表。请注意，当您连接到透视图时，您的模型将包含数据集或模型中的所有表，并且任何未包含在透视图中的表都将被隐藏。此外，任何可能添加到透视图中的表都将自动添加。

只有在将 DirectQuery 连接添加到 Power BI 数据集或将 Azure Analysis Services 模型添加到现有模型时，才会显示此对话框。您还可以通过在创建数据源设置后更改与 Power BI 数据集或 Azure 分析服务模型的 DirectQuery 连接来打开此对话框。

**性能改进**

模型查询和智能缓存的并行执行可全面提高性能。

阅读更多：在文档中阅读有关此功能的更多信息。

**Bing 地图的租户级功能切换**

本月晚些时候，我们将推出租户级功能开关来启用或禁用 Bing 地图视觉效果。您可以在管理门户中找到这个新选项。展望未来，必应地图将要求新租户明确选择加入，这意味着默认情况下它将被禁用。现有租户不应受到影响，但请注意，现在将存在禁用视觉效果的选项。在已禁用的上下文中加载 Bing 地图视觉对象将导致仅影响该视觉对象的错误，这会通知用户联系其管理员选择加入。我们预计此更改将在本月晚些时候在 Power BI 服务中推出，并在下一版本的桌面中。

**数据建模**

**SWITCH性能优化**

我们优化了 DAX 中SWITCH 函数的性能 。如果 SWITCH 函数具有大量值（数百个或更多）或者值表达式包含度量引用，您应该会看到改进的性能。

**DAX 中的按位函数**

我们为 DAX 添加了新的按位函数！现在您可以执行常见的按位运算，例如在 DAX 中移位。我们添加了以下功能：

-   BITLSHIFT和BITRSHIFT允许您分别将数字向左或向右移动指定的位数。
    
-   BITAND、BITOR和BITXOR 分别返回两个数字的按位 AND、OR 或 XOR。
    

**数据连接和准备**

本节中的功能在某些地区可能会延迟发布。我们正在努力确保它们尽快在所有公共区域可用。

**Amazon Redshift（连接器更新）**

我们很高兴地宣布支持 Amazon Redshift 连接器的本机数据库查询。

与 SQL 和 Snowflake 连接器类似，这将允许您输入 Amazon Redshift 本机查询并在其上构建报告。

**Dataverse（连接器更新）**

我们更新了 Dataverse 连接器以支持环境发现。用户将能够查看他们有权访问的环境列表，而无需指定环境 URL。

**Google Analytics（连接器更新）**

Google Analytics Connector 已更新为使用 V4 API。此更新中的其他功能包括更好的 API 可靠性以及公开 V3 中不可用的其他维度和度量。

**Azure Cosmos DB V2（新连接器）** 

我们很高兴地宣布在即将到来的 2021 年 11 月更新中发布 Azure Cosmos DB V2 连接器！

为了查询存储在 Azure Cosmos DB 容器的事务存储中的数据，我们之前发布了一个本机 Power BI 连接器（以下称为 Azure Cosmos DB V1 连接器），该连接器通常可用且仅支持导入模式。我们现在发布了一个新的本机 Power BI 连接器（以下称为 Azure Cosmos DB V2 连接器），它将支持在 DirectQuery 和导入模式下查询事务存储。除了支持 DirectQuery 模式，V2 连接器还包括与查询下推和数据序列化相关的性能优化。

**Azure Databricks（连接器更新）**

Azure Databricks 连接器已更新。以下是 Databricks 团队的笔记。

通过 Unity Catalog 支持添加了对工作区中目录层次结构导航的支持,默认情况下启用“快速评估”，提供更快的大型导入处理，并启用直接 SQL 直通，为 Databricks SQL 和 Databricks Runtime 8.3 及更高版本提供更低的延迟。

**Amazon Athena**

此连接器现已普遍可用。

**SIS-CC-SDMX（新连接器）** 

我们很高兴地宣布发布新的 SIS-CC SDMX 连接器。以下是来自 SIS-CC-SDMX 团队的描述。

SIS-CC SDMX 连接器允许轻松查询任何支持 SDMX-CSV 输出格式的公共 SDMX REST Web 服务端点，以分析、可视化和共享来自 Power BI 的数据。统计数据和元数据交换 (SDMX) 是一项 ISO 国际开放标准，被统计组织（国家、次国家、区域和国际）采用和使用，用于制作和传播官方统计数据。

SIS-CC SDMX 连接器是由统计信息系统协作社区 ( SIS-CC )提供的开源项目。

访问 SDMX 连接器文档页面了解更多信息和如何开始，访问 SDMX 官方网站了解更多关于 SDMX 标准的信息。

**SumTotal（连接器更新）** 

SumTotal 连接器已更新，现已普遍可用。以下是来自 SumTotal 团队的更新。

-   删除了 OData 实体的硬编码列表；现在动态拉取所有 OData API
    
-   添加了允许通过查询字符串参数绕过 SSO 登录的逻辑
    

**Usercube（新连接器）** 

我们很高兴发布新的 Usercube 连接器。以下是 Usercube 团队的笔记：

Usercube 是第一个用于身份治理和管理 (IGA) 的无代码全功能解决方案，可针对您独特的组织、流程和策略进行配置。

身份生命周期管理变得无缝：所有用户，包括内部员工、合作伙伴、RPA 机器人和物联网设备，都会自动获得必要的访问权限——仅此而已——执行您的安全策略和职责分离 (SoD) 基于你独特的榜样。

通过 Usercube 的 Power BI 集成，业务报告可以从用户身份、权利详细信息（帐户和细粒度权限）和批准工作流跟踪（谁做了什么和什么时候做）等数据中受益。

这些报告易于创建和共享。它们集成了来自多个应用程序的数据，并为整个公司提供了清晰的信息：

\- 密切监控和分析权利管理和安全性能。

– 业务团队受益于用于数据驱动决策的简单且一流的报告。

请随时联系 Usercube 进行演示。

**服务** 

**行政与治理**

**Premium Gen2** 

全新的第二代Premium容量平台（称为 Premium Gen2）现已全面上市。

新平台提供了更高的弹性和性能稳定性、更大的使用规模以及更少的内存利用率和并发刷新限制、现代化的容量指标监控以及通过 Autoscale 容量调整的可选调整灵活性。它可以自动增加您的容量大小，以解决对容量处理能力需求的意外高峰。

所有新的Premium容量将创建为 Gen2 容量，并鼓励所有现有容量切换到 Gen2。几周后，我们将自动将传统的第一代容量移植到第二代（与容量管理员的公告和通信将单独进行）。

阅读有关Power BI Premium Gen2 平台的更多信息，如果您还没有，请立即将现有容量切换到新平台！

**用于确定谁有权访问哪些 Power BI 资产的新 API** 

上个月，我们发布了一组 API 以预览用户权限（有关详细信息，请参阅此博客文章）。本月，另一个 API 可帮助你更好地管理 Power BI 资产清单。所述GetUserArtifactAccessAsAdmin API需要用户具有访问资产的用户，并返回列表的图表ID。结果由 continuationToken 分页，每页结果包含一种类型的资产。作为 Power BI 服务管理员，此 API 对您有何用处？考虑员工离开公司时的情景。通常，需要转移该员工资产的所有权。API可以帮助确定员工拥有哪些资产，从而顺利转移所有权。

了解有关用户 GetUserArtifactAccessAsAdmin API 的更多信息。

**部署管道 API** 

几个月前，我们宣布了部署管道 API 的公共预览版。部署 API 使专业 BI 开发人员能够将 Power BI 版本作为他们选择的 DevOps 工具的一部分进行管理。

今天，我们宣布所有部署管道 API全面可用。作为公告的一部分，我们还发布了一组新的 API，用于从头到尾创建和管理管道，因此使用 Power BI 部署管道进行迁移和扩展比以往任何时候都更快、更容易。

借助新的 API 集，专业 BI 开发人员将能够：

-   自动添加新工作区以使用管道 - 设置一个自动化流程，将新的生产工作区分配给管道，并且所有相关团队成员都获得适当的权限。
    
-   标准化组织中的发布流程 - 大规模迁移内容以使用管道，以便您的发布流程达到最高标准。
    
-   在您选择的 DevOps 工具中集中管理 Power BI 内容，无需打开 Power BI - 从管道创建到部署到生产，所有操作都可以通过自动化完成。
    

您可以使用PowerShell 示例轻松入门。

新 API 将包含哪些内容：

-   创建/更新/删除部署管道。
    
-   为部署管道分配/取消分配工作区。
    
-   从部署管道中添加/删除用户。
    

阅读有关部署管道自动化的更多信息。

**即将为 Microsoft Teams 自动安装 Power BI 应用**

许多组织在 Microsoft Teams 中使用现代协作来实现更快的决策和行动。现在，Power BI 使组织可以更轻松地在 Teams 中推出 Power BI 体验，因此用户可以在他们工作的地方发现和使用数据。这有助于人们更快地收到通知，获得更丰富的链接共享体验，并在不离开 Microsoft Teams 的情况下访问他们的所有数据。

为了使组织能够更轻松地在 Teams 中推出 Power BI，我们进行了一些改进：

-   当用户访问 Power BI 服务时，Power BI 将开始自动为 Teams 安装 Power BI 应用程序。
    
-   Power BI 管理员可以选择不通过新的 Power BI 租户设置自动安装。
    
-   租户设置现已开始推出，让管理员有时间根据需要选择退出。
    
-   对于启用了该设置的组织，自动安装将于 2021 年 11 月开始生效。
    

在微软团队自动安装Power BI应用 租户设定被添加到Power BI管理门户。Power BI 管理员可以控制自动安装行为。默认情况下，启用自动安装。

Power BI 租户设置，用于控制用户为 Microsoft Teams 自动安装 Power BI 应用。

在以下条件下为用户进行自动安装：

-   适用于 Microsoft Teams 的 Power BI 应用在 Microsoft Teams 管理门户中设置为允许。
    
-   Power BI 租户设置为 Microsoft Teams 自动安装 Power BI 应用已启用。
    
-   用户拥有 Microsoft Teams 许可证。
    
-   用户在 Web 浏览器中打开 Power BI 服务（例如 app.powerbi.com）。
    

最初，自动安装适用于新用户首次在 Web 浏览器中访问 Power BI 服务时。将来，符合条件的 Power BI 服务的所有活动用户都将进行自动安装。

发生自动安装时，Power BI 服务通知窗格中会显示以下通知。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPibDqMHcoMeA7QJutKB5tj3U3rm29lxVYhFF3txrjm4lz6MMkrjcz7raSKMcQ0fVXWJKC4KVQDbYg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

了解有关Microsoft Teams 的 Power BI 应用自动安装的详细信息。

**嵌入式分析**

**将 Power BI 报告导出到文件 API – 预览更新** 

将 Power BI 报告导出到文件 API（预览版）允许您使用 REST 调用将 Power BI 报告导出为以下文件格式：PDF、PPTX (PowerPoint) 和 PNG。自此 API 推出以来，我们不得不强加一些限制，我们现在正在为 Premium/Embedded Gen2 容量删除这些限制。以下修改适用：

-   每小时 Power BI 导出的数量不限于每个容量每小时50个，而是每个容量每分钟仅 50 个报表页。
    
-   有没有最大并发报表页的限制。
    
-   导出 API 操作负载被评估为慢速运行/后台操作，如Premium Gen2 容量负载评估中所述。出现导出 API 操作的工作负载称为“InteractiveReportExports”。
    

我们预计这份 Export Power BI 报告将在 2021 年 11 月底提交 API。

**Power BI Embedded 现已普遍提供对象级安全性 (OLS)**

与 Power BI Premium 和 Pro 保持一致，我们也在 Power BI Embedded 中将对象级安全功能从公共预览版转移到通用版。对象级安全 (OLS) 使模型作者能够对报表查看者隐藏敏感的表或列。从没有适当访问权限的用户的角度来看，受保护的表或列不存在。此外，对象名称和元数据也受到保护，以防止恶意用户发现此类对象的存在。这一附加的安全层可防止没有适当访问级别的用户发现业务关键或敏感的个人信息。可以使用利用 XMLA 端点的工具在 Power BI 数据集中编写 OLS 规则。请务必查看公共预览对象级安全公告以获取更多详细信息以及如何启用此功能。

**调整嵌入式 Power BI 报表的缩放级别**

现在，您可以通过向嵌入设置添加单个参数或在报告加载后使用 setZoom API 调整缩放级别，以编程方式设置嵌入报告的缩放级别。这使您可以将报告的缩放级别调整为与默认缩放级别不同，并确保所有用户都可以完全看到和使用您的报告，而不管任何视觉或身体障碍。

**更新了对 Power BI Embedded 的多地理位置支持**

对 Power BI Embedded 的多地域支持意味着使用 Power BI Embedded 构建应用程序以将分析嵌入其应用程序的 ISV 和组织可以在全球不同地区部署其数据。到目前为止，Multi-Geo 并未为 Power BI Embedded 部署带来更好的性能，因为加载报告和仪表板仍然涉及向主区域请求元数据。现在我们已经设法克服了这个限制，从而获得了更好的性能！

**Power BI Embedded Playground 更新 – 使用您自己的嵌入令牌**

您现在可以使用自己的嵌入令牌将报告嵌入到Playground 开发人员沙箱中。这是嵌入示例报表或选择可用 Power BI 报表之一的现有选项的补充。

如果你使用“为客户嵌入”解决方案，你将使用 REST API 生成嵌入令牌，让你的应用知道其用户可以访问哪些 Power BI 内容以及他们的访问级别。

生成嵌入令牌后，您可以将其输入到 Playground 中以测试报告并确保设置了正确的内容和访问级别。然后，您可以继续探索我们的 API 并在您的报告中对其进行测试。

如果您使用行级安全性 (RLS) 来限制用户对数据的访问，您可以通过插入为您要测试的相关身份生成的嵌入令牌在开发人员沙箱中对其进行测试。请详细了解Power BI Embedded的行级安全性。

要了解有关 Power BI 嵌入式的更多信息，请前往我们的嵌入式分析游乐场。

**Power BI Angular 组件**

Angular 的 Power BI 组件最近发布。此组件可让您轻松地将 Power BI 报告、仪表板等嵌入到 Angular Web 应用程序中。

在过去的几年里，Angular 的受欢迎程度大大提高，它是目前专业开发人员使用最多的 Web 框架之一。通过提供将 Power BI 分析集成到 Angular 应用程序所需的框架，Angular 的新 Power BI 组件可以让你快速轻松地从洞察到行动。

使用此库，您可以嵌入 Power BI 报告、仪表板、磁贴、视觉对象、问答和分页报告。您还可以使用可用的引导程序集成或分阶段嵌入来优化报告的性能，设置和编辑事件处理程序，并利用可用的客户端 API。

Angular 组件在npm和GitHub 上可用。

**开发**

**向您的自定义视觉对象添加现代工具提示**

现在，您可以使用 API V3.8.3 或更高版本将现代工具提示添加到您的自定义视觉对象中，方法是将 supportEnhancedTooltips 属性添加到 capabilities.json 文件中的工具提示对象。

查找有关如何向报告页面添加现代工具提示支持的更多信息。

**模态对话框 API 更新**

新的模型对话框 API 使开发人员能够确定对话框相对于原始视觉的大小和位置。这在 API 4.0 版本中可用。

详细了解如何为 Power BI 视觉对象创建对话框。

**可视化**

**Lollipop Bar Chart by Nova Silva**

标准条形图非常适合显示每个类别的单个度量。您可以轻松地将每个类别与其他类别进行比较。但是，如果条形图中的类别数量较多 (>10)，则图表本身可能会变得“重”。彩色条将填充图表表面的很大一部分。为了避免这种混乱，可以使用 Power BI 的棒棒糖条形图作为替代方案。

棒棒糖条形图为每个类别显示一个标记（主要是一个点）。一条细线将标记连接到测量轴原点。标记与线条相结合，使其成为棒棒糖条形图。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPibDqMHcoMeA7QJutKB5tj3LsAm2ZzxuJ5MR5U9IYicKD9RsXA2icWB9FVSZRfQnMgKBAibpbKsrQCNw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

棒棒糖条形图还包含一个附加图表：点图。只需隐藏将标记连接到轴的线。

此图表的最新版本包含几个令人兴奋的增强功能：

-   条件格式（标记和行）
    
-   部分突出显示
    
-   数据标签
    
-   标记形状
    

不要犹豫，立即从AppSource下载棒棒糖条形图。所有功能均可免费用于在 Power BI Desktop 中评估此视觉对象。

**Drill Down TimeSeries PRO visual by Zoo****mCharts**

可视化 Power BI 时间线现在比以往任何时候都容易。ZoomCharts 的 Drill Down TimeSeries PRO 可让您探索精确到毫秒的基于时间的数据。具有丰富的交互选项和流畅的动画，结合多种图表类型以获得终极 Power BI 时间线体验。从几个月到几周，再到几天轻松地深入数据，并在平移和选择之间进行选择作为您的过滤方法。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPibDqMHcoMeA7QJutKB5tj3AJXuibRT4Jxqz6RVjN5LUGDd2d4bKEaQicMibGichY6e00wnicJzR3Utl4A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在 Drill Down TimeSeries PRO 的主要功能中，您会发现：

-   多点触控设备友好 - 在任何设备上获得相同的体验。
    
-   多种图表类型和组合——柱状图、面积图和折线图。包括所有图表类型的堆叠和聚类。
    
-   跨图表过滤——不使用切片器，而是选择多个图表上的数据点。
    
-   静态和动态阈值 - 设置多个阈值以展示目标或基准。
    
-   完全自定义 – 使用丰富的自定义选项组合多种图表类型、设置阈值并将 GMT 数据转换为当地时间。
    

要免费评估 Drill Down TimeSeries PRO 的 Power BI 时间线功能，请立即开始 30 天试用期。从AppSource下载 Drill Down TimeSeries PRO 。

了解有关 Drill Down TimeSeries PRO 的更多信息。

**Inforiver by Lumel**

Inforiver是一种用于 Microsoft Power BI 的创新低代码/无代码报告和分析解决方案。借助我们内置的可视化公式引擎，最终用户可以使用 Inforiver 快速构建复杂的财务报表、损益报告、管理和差异报告，无需 IT 或 DAX 知识。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPibDqMHcoMeA7QJutKB5tj39z82QPC0BxuM69Rq46aexBbgodVgDpLSE8kvQRF8DNjCuKKcSCZ1icA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

Inforiver 专业版还支持数据透视表类型分析、嵌套过滤和 Top N 排名功能。内置工具栏提供单击样式、对齐和多个格式选项，并提供无与伦比的最终用户自助服务、交互性和协作体验。

Inforive专业版功能亮点：

财务和管理报告：

-   类似 Excel 的快速格式化（单元格、行和列）
    
-   分页
    
-   行/列动态重新排序和分组
    
-   自动数字格式
    
-   总计和小计定位（顶部或底部）以及拆分总计
    
-   插入视觉公式行/公式以及静态手动输入行
    
-   参差不齐的层次结构处理
    

合作：

-   细胞级注释和注释
    
-   审计 - 捕获变更日志的视觉级别变化
    
-   单元格编辑和单元格级公式
    

分析用例：

-   展开/折叠单个列以进行数据透视分析
    
-   能够使用管理列（非对称表）隐藏/显示
    
-   高级条件格式（总计、值）
    
-   冻结和固定 - 同时跨页多行
    

从AppSource下载此视觉效果 。

**Hierarchical bar chart by Excelnaccess.com**

分层条形图以条形图/柱形图的形式显示分层数据（具有父/子关系的不同字段），带有 +/- 符号以查看/隐藏详细信息或子元素。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPibDqMHcoMeA7QJutKB5tj38FCVibTMl5ac33uibcUQ9Tlk3LQGTDEAHDDYkibuPjyJIia5Gkwvu0essQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

此视觉对象具有以下主要功能。

-   使用 (+/-) 按钮展开/折叠栏
    
-   显示条形之间的差异
    
-   拖动条以进行自定义排序
    
-   单击图例向下/向上钻取到任何级别
    
-   显示目标
    

从APPSOURCE下载此视觉效果。

**AppSource 中的新视觉效果**

-   Acterys Reporting by Managility
    
-   PmBI – Process Mining by ProcessM
    

**本月编辑精选**

-   Drill Down Pie PRO by ZoomCharts
    
-   Floor Plan Visual by Simpson Associates
    
-   Ultimate Waterfall by dataviz.boutique
    
-   Phrazor by vPhrase Analytics Solutions Pvt. Ltd.
    
-   Journey Chart by MAQ Software
    

**其他**

**对分页报告的 ODBC 支持** 

我们很高兴地宣布对 Power BI 分页报表的 ODBC 支持全面可用！在 Power BI 报表生成器中创建分页报表时，您现在可以使用 ODBC 选项连接到任何数据源。分页报表现在可以连接到 ODBC 驱动程序，例如 SAP Hana、Redshift、Snowflake、Oracle、DB2、Vertica 等。要了解更多信息，请查看有关Power BI 网关和报表生成器支持 ODBC 数据源的文档。

以上就是10月的更新内容，你也可以点击阅读原文去看官方博客中查看。

___

PowerBI每月更新后，如果不能自动更新或者不方便下载，可以在公众号后台发送"**软件下载**",获取最新的PowerBI Desktop安装包；

如果要下载历史安装包，也可以发送**6位年月编号**获取，比如发送“202102”获取2021年2月的安装包（2021年2月是支持win7的最后一个安装包）。

___
