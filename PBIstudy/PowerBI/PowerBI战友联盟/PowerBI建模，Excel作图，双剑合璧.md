---
create_date: 2022-07-05T11:43:46 (UTC +08:00)
tags: 
aliases: null
pagetitle: PowerBI建模，Excel作图，双剑合璧
source: https://mp.weixin.qq.com/s/OqjftKpky9ngOihlEgT8zg
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

现场讲解，错过可惜

![](https://wx.qlogo.cn/finderhead/Q3auHgzwzM4Rz9mYvEFH2tuPTpv0svaghGlMxxNNbNjkwBJCRr1RFw/0)

**PowerBIMBA**

，

07月07日 20:00 直播

数据模型 + Excel可视化

视频号

Power BI，就起本质技术架构，包括：

-   PBI - Power Query - 数据混合
    
-   PBI - 数据模型（Data Model）- 数据模型，DAX 用于操作模型
    
-   PBI - 可视化（Visualization）
    

我们常说的可视化，其实在 Power BI 中是一个独立存在的部分。

这套架构在 Excel 中，也存在，包括：

-   Excel - Power Query - 数据混合
    
-   Excel - 数据模型（Data Model）- 数据模型，DAX 用于操作模型
    
-   Excel - 可视化（Visualization）
    

问题来了：

-   到底应该在哪里做数据模型？Excel 还是 Power BI？
    
-   到底应该在哪里做可视化？Excel 还是 Power BI？
    

大家好，我们今天来研究下这个问题应该怎么做出选择。

## Power BI 的精华

目前，Power BI 的精华在于数据模型，也就是用户拖拽关系构建的数据模型以及用 DAX 定义的度量值。

Power BI 的可视化仅仅是对 Power BI 数据模型发出的查询。

## Power Pivot

Power Pivot 就是 Excel 中的数据模型，为了宣传的目的，微软当年为其取名 Power Pivot，其实质是构建 “数据模型”。

由于历史的原因，微软的自助商业智能分析战略已经全部迁移到 Power BI 中。

Power Pivot 仅仅作为兼容过去的一种存在，因此，很多能力不再演化，基本还停留在 2015 年的阶段。

## 必然之选

数据模型，是数据分析的基础结构，因此，是必然之选。而由于数据模型的全部战线已经在 Power BI 中，因此，构建带有强大能力的数据模型，在 Power BI 中进行是全功能的。

因此，我们推荐：

**在 Power BI 中构建数据模型。**

这样就可以获得全功能的数据模型能力。接着就是需要数据可视化的能力了。

## 可视化的场景

乔布斯有次演讲说过，他在开会的时候，是不需要技术参加的。只做应该出现的需求对应的产品。

从可视化的角度，有两大场景：

-   第一种，Excel 可视化
    
-   第二种，BI 可视化
    

这里并没有说 Power BI，因为 Power BI 可以被归纳到 BI 可视化的范畴。所有 BI 可视化中又有一个通用需求，就是导出成 Excel。这点在 Power BI 教父的演讲中已经讲过。

## 模型与可视化架构

根据以上分析，不难得出一个实用的数据模型加可视化的通用架构，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM3frppfhP2yKkO9CafgJHmQRV1HohsWY8TRPF0Diajctq6Nme2YiaCDJAo6YWicoxwtsNk4r208SLibQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在这个架构下，我们要解决三大问题：

-   Power BI 数据建模
    
-   Power BI 数据可视化
    
-   Excel 数据可视化
    

其中，前两者属于 Power BI 的默认部分，不再探讨。

Excel 数据可视化，这部分，又要解决两个问题：

-   Excel 如何使用 Power BI 数据模型
    
-   Excel 如何更容易地出图
    

## Excel 数据可视化

这里用了一个非常重要的词，

是：出图

而不是：作图

出图，强调快速得到结果。

作图，强调出图经历的过程。

作图不是目的，图才是目的，一键快速出图是最佳实践。

在这方面，我们已经有过大量探讨。

大部分刚刚进入 Excel 领域的小白还在惊呼好强大啊的时候，很多更务实的业务分析者已经在考虑如何更高效地出图了。

这方面，有很多的 Excel 插件可以帮助完成。例如：国内的 tusimple BI 和国外的 Zebra BI 等。

我们这里投入精力测试和验证过的工具才会进一步推荐给大家，要确保：

-   稳定
    
-   可行
    
-   支持科学的作图方法论
    

目前，tusimple BI 和 Zebra BI 是我们测试过的产品，可以放心使用。

## tusimple BI 与 Zebra BI 的对比

这里并不准备对比它们的功能和技术细节，在宏观初衷上，它们略有差异。

-   tusimple BI 支持 Excel 各种通用作图及复杂作图。
    
-   Zebra BI 是完全按照 IBCS 推荐的模式进行作图。
    

也就是说，从一定意义上 tusimple BI 比 Zebra BI 支持的范围更广更全。但在作图的方法论下作图，可能导致有的功能不需要使用到，而由于场景的缩窄，导致用户体验上和细节差异上，Zebra BI 更符合某种标准化流程。

这里并不想去评述哪个工具比哪个工具更好，在具体实际操作下，可能是这样的一种需求：

我们只需要趋势分析，指标分析，结构分析，差异分析等场景来覆盖 80% 以上的业务分析场景。

那么，不管用哪套工具，都应该在这个业务需求下去探索最佳实践。

作为工具本身，它们可以继续开拓通用性或其专属方向。

因此，其架构是这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM3frppfhP2yKkO9CafgJHmv32PjnNllYZx8icA27Sjfle2OtAeklBPHKiae105JKicu60z2SyFfzTFw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里面就出现了三个问题：

-   精华需求有哪些？
    
-   Excel 如何获得数据模型的数据？
    
-   Excel 如何出图？
    

## 出图精华需要哪些

关于这方面，我们已经在之前的文章中探讨过。并给出了：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM3frppfhP2yKkO9CafgJHmO5iboRDWUa7JOddY04xetTz8NNhhRzWe9tmIkNCDnjRNRPMGLZlfx8g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

参考：http://excel120.com/go/find-chart/?f=wxp

关于这方面的教程也给出了基于 ZBI 的实现，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM3frppfhP2yKkO9CafgJHmX7whW1o0YFEr8grDaIApU7tibPfKx0IdkTpicvQnF2Q2tStjHuQEUYgw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

参考：http://excel120.com/go/zbi-basic/?f=wxp

教程参考：https://e.excel120.com/detail/p\_62411cd4e4b0812e17845f27/6?fromH5=true

## Excel 如何获得数据模型的数据

方法有很多，我们之前也给出过，用插件的方法以及原生的方法。

**DAX Studio 方法**

在 Power BI 中有很多第三方插件，但有实际意义以及需要学习的并不多，目前看来有三个是必须的，DAX Studio 是其中之一。

如果嫌网络不好，可以在这里下载：

https://excel120.com/#/p/daxstudio

下载后，在 Power BI 关闭下双击安装完成即可。

打开 Power BI 中可以看到：

这就是 DAX Studio。

确保当前 Power BI 打开了一个 .pbix 文件，并且有内容，至少包括一些模型和度量值。

点击【DAX Studio】如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM3frppfhP2yKkO9CafgJHmzntiaicyvBrSKhgPsauyRuzoIeB4NWwbZibawkBBXwqibodWibrA65HIacg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在右下角可以看到一个号码，就是：数据模型的连接信息。点击右边的【复制】小图标，将该信息复制。

打开一个空的 Excel 文件，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM3frppfhP2yKkO9CafgJHmYSOvVYpbPc187npZN0EDwKSYQyk5jNQT1URibYicrqvYCFbugxhicbXRw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

依次点击上述 1,2,3,4 后得到：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM3frppfhP2yKkO9CafgJHmGSH8khU8ibdicsPtHCibicLc0wynZtqmGp0JSZqltmSqNK3YPibAcGmC09w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

填写刚刚复制好的连接信息到上述【服务器名称】后点击【下一步】【完成】。可得：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM3frppfhP2yKkO9CafgJHmdib1xDg6j6tWBuiaCHibicxs6LJQYyXMKvSSe2VldMBoYqypTA8F5ZhDVw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这说明 Excel 已经连接到 Power BI 的数据模型上了。

> 💡小提示
> 
> 经典的商业智能中，透视表就是和 CUBE（也就是模型）配合使用的，现在常见的透视表反而不是透视表的最初形态。此处理解的用法才是原汁原味的经典方法。

## 数据模型 - 透视表

既然可以用透视表，可以使用数据，例如：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM3frppfhP2yKkO9CafgJHmicCaaLdUjp4NFyZYSehZke1CDDjcM2XKhIOe6d0Q3xicwfsfoZSwLzog/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

例如，要计算利润，需要这样一种简单的计算。这很强大了，但仍然有两个需求：

-   自定义计算。例如：希望不要 “总计”，而是要 “利润”，但 “利润” 没有。怎么办？
    
-   对透视表进行可视化。怎么做？
    

## 透视表 - 可视化

我们利用 tusimple BI 对透视表，进行可视化，如下：

我们不必追究这里的细节，我们想说明的是：

-   基于透视表的可视化往往需要额外数据，导致混合结构。
    
-   出图工具要前兼容透视表或混合数据进行出图，本身就增加了技术复杂度。
    

因此，基于透视表的直接出图，有时候，甚至大多数时候只能是基本的，而很难做到高级出图。

那怎么办呢？解决方法是：**透视表的平面化**。

## Cube 函数

这基本是一套鲜为人知的函数，也是 Excel 中最强大的函数，没有之一。它们构建里平面数据到数据模型的桥梁。大概只有不到 0.01% 的人知道且会用这套函数，学习 Cube 函数大约需要 60 分钟就可以学会一切需要的。

如果还不会 Cube 函数，也没有关系，可以这样：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM3frppfhP2yKkO9CafgJHmB9cW2QmjzP0X7UVqypibIrLJLb5B0YB3JB18GeSHEMlX74l5RRnYsiaQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以直接将基于数据模型的透视表，转换为 Cube 函数结构。这就实现了数据的平面化。

Cube 函数帮助用户获取维度信息，这样，数据模型中的维度就得以使用。如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM3frppfhP2yKkO9CafgJHmDjcNntZBJK5FhbFYSBML5qENNibEnAtryibaaxNwjibOWFZqfc713zstA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

Cube 函数帮助用户获取指标信息，这样，数据模型中的指标就得以使用。如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM3frppfhP2yKkO9CafgJHmL5eJarmp5JCoZDx1oBHlTVBTU7aJibjibicBcsRqDvBWJ5BibXRQmhC1jg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

从一定意义上来说，仅仅需要学习两个 Cube 函数即可。他们是：

-   CUBEMEMBER
    
-   CUBEVALUE
    

学习的方法就是观察下规律，记住即可。学习完毕。

至此，透视表的数据就被平面化了，也就是说，多维数据模型空间中的数据被业务人员根据需要提取了一个截面。

也就是说：

一个多维的宇宙空间，由于人类的视觉是二位平面的，因此，在人看数据的时候必须要将多维世界坍缩成二维平面后再观察。

Cube 函数帮助我们完成这个动作。

## 平面数据 - 可视化

在得到平面数据以后，就可以用任何出图工具来进行可视化了。现在用 tusimple BI 来作图看看，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/09hv4Xua0LM3frppfhP2yKkO9CafgJHmcHCY1IX5OGg7lVYe6TIYlM4jqgWWd8U2dg88y4m7WYF30Xl2d4XHlw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

当然了，tusimple BI 还支持水平瀑布，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM3frppfhP2yKkO9CafgJHmVCqByDbS6MM7zM3IpszQZ3DLlu4XgkWkrnACT4b0ZW18zsriaibk202Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这同样满足 “一键出图”。

## tusimple BI 的限制

tusimple BI 在 Excel 出图方面无疑是国内强大的产品。做图不知刘万祥，做出图来也枉然。tusimple BI 由刘老师设计打造，在作图全面性方面很好，但毕竟产品设计和作图不是一件事，我们看到了刘老师在这个方面的投入，也看到了很多小伙伴对 tusimple BI 基于透视表作图时的限制的抱怨。

如果你不具备透过产品看基因的本事，你永远只能看到静态的事物，你既看不到过去，也看不到未来。

举个例子，刘万祥老师在 Excel 原生作图方面研究了十多年（也许更久），这是历史；现在 tusimple BI 有了，刘老师原来的作图课程是收费的，现在产品收费，但课程免费，产品的价值在于你不需要学习作图而是一键出图。

除非，你上班的确有很多时间来研究作图，且老板也因此支付工资给你作图，很显然，不是这样。那么，一键出图才能让业务人员将精力聚焦到业务分析本身上。当然，很多人作图和抽烟喝酒是一样的，作为一个爱好存在，可以消磨时间。从商业意义上来看，有了一键出图的工具，此爱好只能是爱好了。

tusimple BI 实现的功能和限制，其实并不用大家吐槽，刘老师第一个就知道很多问题，但改是需要时间的，这就是未来。

如果你能看到一个人，一个公司可以做一件事数十年，你应该研究历史，现在，未来。这才是立体地，可发展地看待和选择事物的方法。

tusimple BI 会继续为小白用户优化和开发基于透视表的作图能力（相关进度可以关注 tusimple BI 的网站），但对我们这种高级用户来说，这是一种伪需求。

如果你看明白本文，就应该明白一个道理，真正的作图不是作图这一个环节，而是在一个流程里。这个流程是这样的：

如果是 BI 模式，那就是纯 Power BI；如果是 Excel 模式，那就是：

-   PBI 做模型
    
-   Excel 连数据模型
    
-   透视表转平面数据（Cube 函数）
    
-   平面数据出图
    

看到了吗？正确和专业高效使用 tusimple BI 的方式，不管它是否支持透视表，一个核心的模式是在这个流程中的。从这个意义来看，能出图的部位都应该是平面化的，透视表仅仅是一种特殊的平面形态而已。因此，对于我们来说，我们更关心 tusimple BI 是不是可以更简单，直接，高效，稳定，系统地基于平面数据一键出图。至于它能不能基于透视表出图，有了更好，没有也无所谓。

## 一键出图

我猜测 tusimple BI 当前的产品形态还是没有跟上刘万祥老师的全部作图经验总结。因此，当前状态的 tusimple BI 还有很大的成长空间，这是好事。我们对未来的 tusimple BI 很有期待。尤其在一点上，我们高度认可 tusimple BI 目前的定位，那就是：

一键出图。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM3frppfhP2yKkO9CafgJHmY5VHb8TzL2uhYjeKa1jDGg85JMvncUW3hTU7TDIIL8XHBOzaeEQaow/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以看出两点：

-   tusimple BI 目前设计在 V0.2 版本
    
-   tusimple BI 支持很多图表场景
    

从这些信息，应该可以看到 tusimple BI 的未来了。如果猜的没错，tusimple BI 目前的产品设计对于表达刘万祥老师多年作图经验来说，还是开始阶段。

大家可以利用 tusimple BI 来学习作图本身。

## 总结

这里定位于：**自助商业智能分析**本身。在这个流程中，涉及到两大作图场景：

-   Power BI 场景，由 Power BI 作图解决。
    
-   Excel 场景，由 Excel 出图工具解决。
    

而本文给出的是：

PBI 建模，Excel 作图的通用框架流程。在这里流程里的难点是获取数据以及 Excel 出图。这里用 Cube 函数完成数据获取；而用 tusimple BI 来实现一键出图。

## 福利

tusimple BI 是国内 Excel 作图插件中的优秀产品，我们积极反馈了 tusimple BI 的各种问题，作为回馈，tusimple BI 团队支持伙伴们更多的反馈以优化产品，因此，特别开设了本公众号的专属优惠码【BI6666】，如果未来你需要购买 tusimple BI，输入这个优惠码可以在原有所有活动基础上，再享受业界最大优惠。

也欢迎大家反馈和总结 tusimple BI 作图中的问题和最佳实践，我们也会在这方面给出相关研究。插件下载：http://www.tusimpleBI.com/

重要的说三次：

购买 tusimpleBI 输入优惠码：**BI6666** 专享BI佐罗优惠。

购买 tusimpleBI 输入优惠码：**BI6666** 专享BI佐罗优惠。

购买 tusimpleBI 输入优惠码：**BI6666** 专享BI佐罗优惠。

如果没有完全理解本文要点，没有关系，我们将提供直播讲解，欢迎关注。

现场讲解，错过可惜

![](https://wx.qlogo.cn/finderhead/Q3auHgzwzM4Rz9mYvEFH2tuPTpv0svaghGlMxxNNbNjkwBJCRr1RFw/0)

**PowerBIMBA**

，

07月07日 20:00 直播

数据模型 + Excel可视化

视频号

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNhia5Pc4XC1Um7IYgQhGEoEC1yK05ibUFoPBYpcoAMvibuZh2BZaibMzULeDwNfSeQ0KHRcDUdX3FzVA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**Power BI 终极系列课程《BI真经》**

[

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/09hv4Xua0LNBM1lxlQYHJBicic4CvPoRGLqHgdTZOr8goNRh0asDXA48mRDzc9zxW4UMQiayHwgDmx7mlt4cQxtjg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

BI真经 - 让数据真正成为你的力量





](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650788512&idx=1&sn=76972ff4b0cf265fe9479c6457b04b47&chksm=f18cd2b1c6fb5ba7386eb0bb835280bd8a651bfe0481cc78f20fc30b80c60d2d4cb7eb5b1e3e&scene=21#wechat_redirect)

扫码与精英一起讨论 Power BI，验证码：data2022

点击“阅读原文”进入学习中心

**↙**
