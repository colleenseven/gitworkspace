---
create_date: 2023-02-22T23:31:03 (UTC +08:00)
tags: wx/pbi/可视化图表 
aliases: null
pagetitle: Power BI主题全面解析：你不能错过的精华指南
source: https://mp.weixin.qq.com/s/Avst2cPlILtLXoal1Lenig
author: Jacob Dong
status: 已完成
category: 浏览文章
notes: False
ZK: Origin
uid: 
---

> 作者：**Jacob Dong**，Power Platform资深用户，微软认证Power BI 数据分析师，任职于世界500强商务卓越部门

作为一名 Power BI 报告作者，在给受众提供有价值的分析同时，也不能忽略了报告的美观度。一份漂亮的 Power BI 报告更容易抓住用户的眼球，让用户认真听取你的分析，接受你的观点。但是 Power BI 中成百上千个视觉对象格式设置，操作起来费事费力，重复的操作让人抓狂。这时我们就需要 Power BI 主题来帮忙了。

Power BI 主题是整个报告中所有视觉对象格式的标准定义，包含了调色板，字体，字号及各种细节的格式定义。应用报告主题可以让你的 Power BI 报告所有的视觉对象立刻获得统一的格式设置，如果格式有需要改动的地方，只要在主题文件中改动再应用，就能即刻更新你的报告格式设置。

Power BI 主题可以让你的多份报告拥有视觉一致性，也可以跨部门甚至整个组织具有连贯一致的，严格标准化的风格。

**基本主题**

Power BI 预设了十多种基本主题，2023年2月，Power BI 又新增了5个无障碍基本主题来帮助视力障碍人士。依照WCAG标准，形状图形与相邻颜色的对比度至少为3:1。新的无障碍主题符合这一要求。
![https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM8ricNNDW9OGhPAH6UoYHmU2LcdHj5dmthW7CCqVU3rVESsenuvVGES3dlujbib5jiceerQh0Ghqewg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM8ricNNDW9OGhPAH6UoYHmU2LcdHj5dmthW7CCqVU3rVESsenuvVGES3dlujbib5jiceerQh0Ghqewg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
**自定义主题**

自定义主题可以很简单，也可以很复杂，简单的自定义主题只需要在 Power BI Desktop 中设置即可。复杂的自定义主题可能要写几百行 JSON 文件。

**简单自定义主题**

Power BI Desktop 的自定义主题功能可以在“视图”，“自定义当前主题”菜单中找到。

**名称和颜色**：主题名称和颜色设置包括“主题颜色”、“情绪颜色”、“差异颜色”和"高级"（结构化颜色）。

**主题颜色**是用于报告中的主要颜色，设置8种或更多颜色构建报告的调色板。在使用完调色板中的所有颜色后，如果视觉对象仍需要更多颜色，则会使用 Power BI 的默认调色板。

**情绪颜色**是用于 KPI 和瀑布图用于表达“好”，“坏”，“中立”的状态。

**差异颜色**是用于“条件格式”设置中的表示”最大“，”中间“，”最小“的渐变色，还有空值。

**结构化颜色**可以将其中的6种颜色应用到大量视觉对象的格式上，每个颜色对应的视觉对象的格式

**主要文本类格式设置**：文本设置包括字体系列、字号和颜色，可为标签、标题、卡和 KPI 以及选项卡标题设置。

**视觉对象**：视觉对象通用的格式设置，包括背景、边框、标头和工具提示等。

**页面**：页面元素设置包括壁纸和背景。

**筛选器侧边栏**：筛选器侧边栏设置包括背景色、透明度、字体和图标颜色、大小、筛选器卡。

具体细节请参考：https://learn.microsoft.com/zh-cn/power-bi/create-reports/desktop-report-themes

**自定义主题的变化**

2023年2月，Power BI Desktop 对主题进行了大量更新。

默认基本主题对许多视觉对象和报告进行了更改，如果不更新报告主题，这些更改不会自动应用到某些目前已有自定义主题的报告里，如果你使用的是过时的主题，在”视图”选项卡，“自定义当前主题”菜单中会看到如下提示：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM8ricNNDW9OGhPAH6UoYHmU1Fvs5JQEZcUoyJ7K2bJlwlZC1cUuzBZsMicynlh5lITqyTEaytFg2nw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

不过要注意应用更新主题后某些视觉对象的可能会有变化，请检查以确保报告在更新基本主题后仍按预期方式显示。

**自定义主题导入时的报告主题验证**

创建自定义主题是一个艰巨的任务，尤其是有那么多的视觉对象和格式设置。多余或者错误的字符都会导致导入 JSON 主题无效或者错误。2023年2月，Power BI 在自定义主题导入时会进行验证，以确保可以读取其中全部内容。如果有发现无法识别的内容，会显示一条错误提示，告诉你主题文件无效。而且 Power BI 还在 GitHub 发布了主题文件的 JSON 架构，随着时间主题文件的属性可能会发生变更，使用 JSON 架构以确保你的主题文件始终是最新的。

主题文件json架构：

https://github.com/microsoft/powerbi-desktop-samples/tree/main/Report%20Theme%20JSON%20Schema

**高级自定义主题**

高级自定义主题需要编辑 JSON 文件。

一个Power BI 自定义主题文件就是一个 JSON 对象，其中只有name属性是必须的。

最简单的 JSON 自定义主题文件可以是：

```
{
  "name": "我是一个主题文件"
}
```

在自定义主题文件中添加主题颜色：

```

{
    "name": "我是一个主题文件",
    "dataColors":[···代码省略···]
}
```

可以在 Power BI Desktop 中将基本的自定义主题设置完毕后导出，然后对视觉对象进行额外设置。

在JSON文件中有visualStyles属性，在其中添加视觉对象来进行单独的格式设置：

```
"visualStyles": {
        "<visualName>": {
            "<styleName>": {
                "<cardName>": [{
                    "<propertyName>": <propertyValue>
                }]
            }
        }
}
```

-   **visualName**是视觉对象的名称，具体名称可参考：https://learn.microsoft.com/zh-cn/power-bi/create-reports/desktop-report-themes#visualstyles-definition-list  
    
-   **st****yleName**为样式名称，目前始终为星号"\*"。
    
-   **cardName**是视觉对象中的格式卡，参考同上；
    
-   **propertyName**是格式卡中的视觉对象属性。参考：https://learn.microsoft.com/zh-cn/power-bi/create-reports/desktop-report-themes#properties-within-each-card
    

**全局视觉对象定义**

对于 visualName 和 cardName，若要将此设置应用于包含属性的所有视觉对象或卡片，请使用星号并使用引号括起来（“\*”）。如果视觉对象和卡片名称使用星号，则可以高效地在报表中全局应用设置，如所有视觉对象中所有文本的字号或特定字体系列。

视觉对象的格式定义优先级是，单个视觉对象定义>全局视觉对象定义>文本类设置＞结构化颜色。如果一个视觉对象的格式在以上3处都被定义过，那么应用的格式是单个视觉对象的定义。

例如：

我希望所有视觉对象的所有格式卡的文本自动换行关闭，可以这样写：

```
{
    "name": "所有格式卡的文本自动换行关闭",
    "visualStyles": {
        "*": {
            "*": {
                "*": [
                    {
                        "wordWrap": false
                    }
                ]
            }
        }
    }
}
```

我希望表格视觉对象中的所有格式卡的文本自动换行关闭，可以这样写：

```
{
    "name": "表视觉对象所有文本自动换行关闭",
    "visualStyles": {
        "tableEx": {
            "*": {
                "*": [
                    {
                        "wordWrap": false
                    }
                ]
            }
        }
    }
}
```

我希望所有视觉对象的标题开启，格式卡的文本自动换行关闭，可以这样写：

```
{
    "name": "视觉对象标题开启且标题文本自动换行关闭",
    "visualStyles": {
        "*": {
            "*": {
                "title": [
                    {
                        "show": true,
                        "titleWrap": false
                    }
                ]
            }
        }
    }
}
```

这里请注意，虽然在 Power BI Desktop 中，格式设置都叫”文本自动换行“，但是在 JSON 文件中的属性名称却是不一样的，而且属性对应的值类型也必须是一样才可以全局设置。

例如卡片视觉对象标注值格式卡中也有文本自动换行，但是这个文本自动换行的全局设置要这样写：

```
{
    "name": "不同的自动换行",
    "visualStyles": {
        "*": {
            "*": {
                "*": [
                    {
                        "wordWrap": false
                    }
                ],
                "wordWrap": [
                    {
                        "show": false
                    }
                ]
            }
        }
    }
}
```

或者这样写，单独设置在卡片视觉对象上：

```
{
    "name": "卡片视觉对象文本自动换行关闭",
    "visualStyles": {
        "*": {
            "*": {
                "*": [
                    {
                        "wordWrap": false
                    }
                ]
            }
        },
        "card": {
            "*": {
                "wordWrap": [
                    {
                        "show": false
                    }
                ]
            }
        }
    }
}
```

**在自定义主题中添加图标**

如果有一些标准化的图标想在不同文件中复用，可以将这些图标添加在主题文件中。

```
{
    "name": "图标",
    "icons": [
        {
            "description": "svg",
            "url": "data:image/svg+xml;utf8,<代码省略>"
        },
        {
            "description": "png",
            "url": "data:image/png;base64,<代码省略>"
        },
        {
            "description": "gif",
            "url": "data:image/gif;base64,<代码省略>"
        },
        {
            "description":"网络图片",
            "url":"https://代码省略"
        }
    ]
}
```

他们会出现在条件格式的图标选项里。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM8ricNNDW9OGhPAH6UoYHmU1mibQU6aeC4LroZGOAIPhJ7ibYFAeIeqLGgBflu52PiceIVvV0oSQA1qw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**高级自定义主题制作捷径**

2023年2月，微软公布了 Power BI 主题文件 JSON 架构，所有的定义都可以在架构文件中找到，不过制作复杂的自定义主题文件仍然是困难的事情。

网络上有==Power BI 大神制作了自定义主题生成器，可以帮助生成复杂主题，也能帮助学习 Power BI JSON 主题文件架构==：

https://themegenerator.point-gmbh.com/en/Home

https://themes.powerbi.tips/themes/palette

鉴于 JSON 主题架构的公布，以上2个网站预计不久就会有更新，会有更多的格式可以自定义。

**自定义主题的应用**

使用自定义主题，报表可以快速地在不同主题间切换以面对不同场景。

我们以Power BI Service网站的案例为例，在导入自制的自定义主题后，再进行微调，报告外观发生了显著变化：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJM8ricNNDW9OGhPAH6UoYHmUUpI7fJa3LLRWDbPSiauXlK2cQJjVEichiaJDOI1p3k3hYr1MVuT0AiaeJw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

如果你的手上有多份 Power BI 模板，为了将他们的主题调整为个人风格或者符合组织要求的风格。那么自定义主题是必不可少的。

对于Power BI 格式设置研究较深的同学，可能发现了，部分视觉对象的格式设置无法在 Power BI Desktop 中通过格式侧边栏调整实现，而 JSON 主题文件中却有该属性可以调整。使用深色主题的同学必定深有感触，白色背景的切片器搜索框与报告外观主题格格不入。通过 JSON 主题文件则可以设置搜索框的字体系列，字号，搜索框背景色等等。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJM8ricNNDW9OGhPAH6UoYHmUsHZichxaFFT15mia253oaW3nvxDT2bpjiaFsdwuvoOqKBDmSfsbnTajaw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**自定义主题学习资源**

虽然现在网上能找到的资源都是基于微软公布主题 JSON 架构前的，但是仍有学习价值，新的主题 JSON 架构应该只是公布了更多的可设置属性以及架构的微调（例如icons属性）。

推荐有兴趣的同学阅读这本书：

Pro Power BI Theme Creation:

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM8ricNNDW9OGhPAH6UoYHmUuIxrkd3ueAKatTrAGmIYNrNGU8p69brReEFaibhbOrKk9BYBEq6qqfA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

以及关注以下GitHub库：

https://github.com/Apress/pro-power-bi-theme-creation

https://github.com/deldersveld/PowerBI-ThemeTemplates

https://github.com/MattRudy/PowerBIThemeSolutions

\-end-
