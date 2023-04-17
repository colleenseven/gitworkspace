---
create_date: 2020-09-03T20:41:08 (UTC +08:00)
tags:
aliases:
pagetitle: 利用PowerBI Report Builder打造像素级完美报告
source: https://mp.weixin.qq.com/s/sfR69GRd48w-2TR59gqY2w
author: 大脸猫
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

> 文/大脸猫
> 
> 8年汽车行业数据分析经验，擅长跨行业快速理解业务并搭建模型，利用Power BI，Python等工具实现业务及报表自动化，相比技术更关注如何落实实际业务场景的解决方案。

上一期聊到如何搭建个人数据模型（[如何打造并复用属于自己的 BI 数据模型？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072732&idx=1&sn=9e35dd498a32f681b6ce428cdc564f50&chksm=8e0c5bcbb97bd2dd715d56bf4545ece6f2af517ee276cc4cae41dd131eddb1215b999eedf789&scene=21#wechat_redirect)），在这个基础上可以有哪些衍生呢？今天来聊一聊Power BI Report Builder。

众所周知Power BI很强，但是在企业内推广还是存在一些障碍，其核心的原因在于喜欢Power BI的更多的是报表设计者，而报表使用者的阅读习惯却很难改变。

我们来模拟一下企业内Power BI数据分析师和老板的对话：

___

**BI分析师**：老板，给您推荐一个数字化工具，微软的Power BI，商务智能软件，它的可视化及交互能力很强！ 

**老板**：嗯，不错，很好，符合我们公司的数字化战略！搞！ 

**BI分析师**：好的，老板，我们打算替换掉我们日常的业务报表，以后不再发送PDF和邮件了，也不用打印报表了，无纸化办公！ 

**老板**：啥，先不要这么激进，Power BI你先搞着，日常业务报表照常发送，手机看PDF多方便！

**BI分析师**：… 

___

Power BI无法满足日常业务中那些高频率，初始设计灵活，后续格式固定并且可打印的报表需求。很多时候，老板需要的是一些中国式组合报表，可能组合时并不一定存在强逻辑，但老板就是习惯这些报表。

作为报表阅读者的老板，是不会关心制作者花费多久时间的，你很难去改变他的阅读习惯，因为在他看来就是一个PDF，发邮件给他就行。所以今天我来推荐这样一款大杀器：**Power BI ReportBuilder**，帮助你在不改变原报表阅读者习惯的前提下，又能不浪费超级高效的Power BI数据模型。

Power BI Report Builder这款软件发布时间在2019年4月，在市场上普及度还是很低的。他的前身其实是Paginated Reports，早期熟悉SSRS的童鞋可能接触过，算是一个分页报表制作工具，但是说实话技术门槛略高，对于普通用户就没有Power BI Desktop那么友好。

**我们不是为了技术而去学习技术，而是为了解决业务的实际问题。我一直觉得能快速理解业务并落实解决方案才是王道。**

所以今天给大家介绍PowerBI Report Builder也不是讲它的技术，细节的操作可能写三十篇也写不完，今天想教大家如何快速复用自己的模型。

**千万不要想一下子完全掌握这款软件的方方面面，和Power BI Desktop一样，先用最低的时间成本和认知负担用起来，围绕业务需求去解决实际问题，慢慢地你自然会越来越熟练。**

在开始之前先安装软件，官网下载地址：

https://www.microsoft.com/zh-CN/download/confirmation.aspx?id=58158

或者后台发送关键字“Report Builder”，获取安装包。

安装完毕后，先熟悉一下这个软件的用户界面，最上面是微软Office标准的Ribbon风格菜单栏，和Office风格非常接近，这点大家摸索一下就能搞清楚。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzhiboLdYM1BkgkjO76lKmj2883kG7CE35d1KDZXg3NconTqib9VlKzVQic39KtnLKyLEC15pCn27MQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

最左侧空白区是报表数据，其中分为：  

**1.内置字段**

可以理解为动态参数，最常用的就是报表生成时间和页码标记。

**2.参数**

用来调整报表显示参数的，例如你可以选择显示2019还是2020年的报表

**3.图像**

可以导入图片，如公司LOGO之类的

**4.数据源**

可以添加多种数据源

**5.数据集**

利用数据源生成用于报告的数据字段

菜单栏下方首先是参数界面，说实话，参数不是必选，作为快速入门可以缓一缓再研究。

然后正中间白色区域就是正文报表设计，可以想象为画布，最右侧是属性设置，涉及几乎报表的全部属性。

从属性设置的项目之多你就可以看出微软设计这款软件就是为了弥补Power BI的短板，实现像素级别完全的自定义。

初学的时候很容易被这些属性搅乱，我一般习惯只观察这些属性，而不轻易去调整他们，需要调整属性的时候，可以在对应的对象区域点击鼠标右键，跳出设置框设置，这可能更加符合我们平时办公软件的使用习惯。

好了，快速了解完界面后我们开始进入Power BI Report Builder速成三步曲啦！

**第一步：连接Power BI数据源**

看过上期文章的童鞋一定已经有了自己的数据模型了，现在就是连接并利用它的时候。

（记住登录自己的国际版Power BI Service账号）

**添加数据源**

右击数据源，添加Power BI数据集连接：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzhiboLdYM1BkgkjO76lKmjKv8vT6IxyMwxWeIh3ve14icU7wsIRuPIecM1SdGNCjU8p0zTw2RJz7A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在你的工作区选择自己搭建好的Power BI数据模型：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzhiboLdYM1BkgkjO76lKmjGGr82ficoqE4XzfBHzFk9DaOABk2pkicBbRicYwugIDibicmOoeGn236X8g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**添加数据集**

点击确定添加完数据源后开始添加数据集。

这里很多人会望而生畏，不要慌，我们全程可以用傻瓜式的操作来完成数据集字段选择，不用会编程语言，一样可以玩转。

右键点击数据集，选择你刚刚添加的数据源，然后点击查询设计器：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzhiboLdYM1BkgkjO76lKmjYicr0EK128b94LtaAoBlLDZA2sAxdpGlADMB8MCazRNgIxiaDVs4YfLg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzhiboLdYM1BkgkjO76lKmjJsTBcYkxHicgK7VsgHL49JtIOrtMg08I6HVQG1AgphNiciczoRyr78CJw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

最上面圈出来的那部分你可以理解为筛选器，用于筛选你要的数据范围，比如我这里就预先过滤了数据集，只到2020年。

然后下面圈出来的是需要用于分析的字段，你可以从左侧的数据模型直接拖过来，完全鼠标操作就可以完成数据集设计啦!

添加成功后，数据集就出现在这里了。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzhiboLdYM1BkgkjO76lKmjecWpxSGtZchN0Kg25ahOwicj5xuFwnTibgTC9uicaygUYyFy9Kr48oqbw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**第二步：报表设计**

由于在这个场景下我们主要是想设计可供打印的报表格式，所以强烈建议先按照自己的习惯设置好一个报表基础模板，这样就不用以后每次都要进行繁琐的设置啦。

**1.页面设置**

一个报表首先要进行的一定是页面设置，先想好你的报表是要横向还是纵向？A4大小还是A3大小？

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzhiboLdYM1BkgkjO76lKmjHc10SxgdyIYlmiameLq44icMl3a7ArV52P8L614ohWpPbiaEf0IRm9rIA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

右键报表区，点击报表属性，调整纸张方向和纸张大小。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzhiboLdYM1BkgkjO76lKmjp630trRrv4nKic5EWISzcIwgos0Z4SmBziaQ7XHuV1cDn9SmjYb94kAA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以看到红框处的宽度和高度，你可以想象成这就是你的纸张最大值。

你的正文区是可以通过拖拉或者添加新的元素自动扩展的，但记得不要超过这个宽度哦，正文超过了纸张的高度可以换页显示，一旦超过了纸张的宽度显示出来就会非常的奇怪，这点在初始设计的时候一定要记住。

**Tips**:

很多人到这里设置完毕后,设计报表的时候一直出现行列显示不完整的情况，强烈建议你在右侧的属性框将这个ConsumeContainerWhitespace设置为True。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzhiboLdYM1BkgkjO76lKmjLqZrT9lxSdzRRNQ3UjXqcDDnDDXeqZtR9tpd9nIge4AB7O4jBnk86w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**2.设置页眉和页脚** 

右键报表区，可以选择添加页眉和页脚，这点大家用过WORD应该很熟悉了。

在页眉处右键插入文本框，添加你所需要的报表标题，右键插入图片，添加你们公司的LOGO。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzhiboLdYM1BkgkjO76lKmjRtaCgQuRoVzEQ8DMjXLbnNgngicdap96hUOrunVggtPDLfEngdDpCXA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在页脚处添加页码，这里要稍微研究一下，还记得一开始我们说的内置字段吗？这里就要用到表达式了，表达式是Power BI Report Builder非常核心的一块，虽不如DAX那么强大，但是他可以帮你实现一切可调整的内容和格式。

同样的右键页脚处，添加文本框，右键文本框，选择表达式。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzhiboLdYM1BkgkjO76lKmj1MHgdAISJ27PqZkbrt03bibg6CicdyelL3ZqkNnd1dsYqdGmd16ib2RwQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

同样用拖拉拽的方式把你需要的字段拖进来，再手工加几个&和字符串，这个应该不难，而且在下面的公式都自带提示和示例，稍微摸索一下即可快速掌握。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzhiboLdYM1BkgkjO76lKmj0bMFfpBGEpMEIH3iaiboUwQAZKTlR2IiaQpwuG4J26UMFL57lO4xW0mxA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**3.报表设计及格式设置**

你在设计的时候看到的是这样的界面：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzhiboLdYM1BkgkjO76lKmjLLdykGQmqOttEmhamZ8jsA3DgZdS9B6RZ79UibwbSopCaKktzLx8Tug/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

表格的上方和左边各有一个类似中括号的符号，这代表这个字段是从Power BI数据集里面添加的字段，这个又称之为行组或者列组。这个字段是从模型中取出来，随着模型数据的变化而动态变化的，你在设计的时候要考虑清楚它的分布，尤其要慎重使用列组的字段，避免影响最终报表格式。

**这里重点讲一个条件格式的调整，如果我想实现某些小计或者总计行变粗或者加底色的设置该如何实现？如果行是静态的，你只需要和EXCEL里面一样的简单设置即可，但是我们面对的是动态变化的行标题数据该怎么处理呢？提示：辅助列数据。**

选中你需要设置格式的区域，右键点击文本框属性，选择填充颜色右侧的FX表达式：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzhiboLdYM1BkgkjO76lKmjRMuLAgBb119wucgbGGBErrqOIqtONIJEQSVHJ3ajkUW0tEB2bpg4Fw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzhiboLdYM1BkgkjO76lKmj3DKLQFibrPmZXMe9qNic2PAiaK1tc6ibywFyEMxaMbFEFpTtd1g6SJDYhw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

输入条件格式的表达式，其实很简单，借助辅助数据L0 Order Value，用条件判断就可以啦！

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzhiboLdYM1BkgkjO76lKmjxwhibsZicILUIjPTFK6J37Fm3B4w7FE6zNAUhM03FVbojOPXTUcPEWCQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里的L0 Order Value就是我为了实现行标题排序而建立的字段（注意它是在Power BI Desktop建模的时候就考虑好的，因此直接调用即可），我只是重复利用他来实现了行数据的条件格式功能。

**第三步：报表运行及导出**

**报表运行调试：**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzhiboLdYM1BkgkjO76lKmjwz5FedqeVQ5DT5ZPKNWiaria58clNvjYmke5ZcoibHNNDUefuSWWoToQg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

看到标出红框的地方了吗，这些就是老板经常要你加的那些标题备注。包括你要新加一列计算其他数据，新加一行计算subtotal这些需求都可以实现，当然你可能还需要多学习一下上面提到的表达式。

总之在Power BI Report Builder里面，表格是可以任意添加行和列的，单元格里面是可以任意填写表达式的，格式也可以任意设置的，所以是不是实现了完全自定义的灵活设计？这点在Power BI Desktop里怎么也搞不出来呀。

最后保存一份，以后在这个基础上可以继续开发设计新的报表啦！

**报表导出：**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzhiboLdYM1BkgkjO76lKmjLQ4hsyXN9OeX38eBhYIQDBbMefWtJ3GX1iakerCkmGp7wLhEszHib6xQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

你也可以随意导出各种格式的报表，PDF,EXCEL都不在话下。

好啦，今天我们只是通过Power BI Report Builder三步曲（添加数据源，设计报表并调整格式，运行报表并导出）实现了一次Power BI模型复用。

核心难点在报表设计过程（页面设置，页眉页脚设计，正文设计），你可能需要反复运行和返回设计界面不断调整，记住保存自己的常用格式，这样才可以做到Report模板的复用哦！

当然很多人会质疑，他只能做表格吗？当然不是，几乎所有你在EXCEL中能制作的表格、图表，包括近期流行的插入的小多图，都可以实现哦。

给大家分享一个Power BI社区官方制作的示例，我们的报告当然是从基础开始，向这个方向进发啦！

**示例1：**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzhiboLdYM1BkgkjO76lKmjK819LCpGznTOTDvyh80wMic7lucu4DJjSw1icSv6VqdDFBIjBia7R8ia1Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**示例2：**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzhiboLdYM1BkgkjO76lKmjIJ8PO0ItzL8T0QgtUJliaAKxr6MjseichGrEibbHHVzTREZxKiacYuz9KA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**示例3：**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzhiboLdYM1BkgkjO76lKmjmD2WrYgGULmc58TS37ibLE3yVjOFbCHC3huRuRcDpyR8D4gsLmbxpQA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

Power BI Report Builder适用于有PDF打印需求的固定格式报表，它兼具了EXCEL的超强自定义灵活性，Power BI数据模型和DAX度量值的便利性，又能做到含交互的像素级别完美的可打印报告。

如果你是Power BI Report Server或者Power BI Service高级用户，甚至可以通过订阅功能每天自动发送PDF报告至订阅者的邮箱中，是不是很方便？

**接下来是不是可以考虑将日常业务工作中很多报表做一次老板都意识不到的变革设计呢？**

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和2.3k+ 学习者一起成长
