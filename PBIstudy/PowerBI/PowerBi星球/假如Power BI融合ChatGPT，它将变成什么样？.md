---
create_date: 2023-02-19T23:31:27 (UTC +08:00)
tags: wx/pbi/数据处理功能 
aliases: null
pagetitle: 假如Power BI融合ChatGPT，它将变成什么样？
source: https://mp.weixin.qq.com/s/4STQ2a0qZFV0IOhOEr0fkw
author: 采悟
status: 已完成
category: 浏览文章
notes: False
ZK: Origin
uid: 
---

微软宣称未来旗下所有产品都将整合ChatGPT，搜索引擎bing、Teams等产品现在已经开始整合，PowerBI中嵌入ChatGPT应该也不会太遥远。

虽然现在来看，ChatGPT能做的有限（[体验ChatGPT，我和它聊聊Power BI](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484083606&idx=1&sn=cd9df4ce8bf217b41d0787bb48b043fc&chksm=8e13b141b964385757882edd5011447b43877a4156ced9dc248609074d93747da436c6cdee7b&scene=21#wechat_redirect)），但是未来一旦融合到一起，它能帮我们的事情立即就会发生重大颠覆。

现在可以畅想一下，如果PowerBI接入了ChatGPT，或者嵌入更通用更大的OpenAI模型，PoweBI会变成什么样？

我认为至少会直接影响到下面这些功能。

___

**1\. 快速度量建议**

这是去年10月份发布的新功能：[Power BI 2022年10月更新，自然语言生成DAX功能面世](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484082587&idx=1&sn=b8fb767030c4b204e52cbc11bd718818&chksm=8e13bd4cb964345a148b0f7d1cc1117088c5b5e3c1fa318687222318ada52e3f148b1062b92b&scene=21#wechat_redirect)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMgooUVUjmLDKLic34wib1wcEq3vlyBEQpiau4OyW4MJwkkwIiaQ0SfK2focCtKvPzhk2K4kdiaoh6iaorQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个功能宣称的自然语言生成DAX，先不说它生成DAX的质量怎么样，关键是问题理解能力十分有限，并且中文支持非常弱，与ChatGPT在对问题的理解上，完全不属于一个层次，之前想着这个功能需要继续迭代几年才有可能帮我们写DAX。

但是现在有了ChatGPT，原来对这个功能的迭代开发可以停止了，而是尽快想想怎么对接好ChatGPT，一旦它融合进来，马上就可以实现自然语言生成DAX。

虽然现在ChatGPT在DAX方面还很弱（参考：[ChatGPT一路狂飙，它的DAX水平怎么样？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484083645&idx=1&sn=d2d0da62240aaadcb200bb7c07dfbcae&chksm=8e13b16ab964387cf6169ceb2c994bc79db50fe21ba9cf19834f719bfc137e6cc8a40e295717&scene=21#wechat_redirect)），但是一旦嵌入进来，它写DAX的能力将会彻底改观。  

一方面是在具体的环境下，它可以自动捕获数据模型中的全部信息，能更有针对性的给出精准的DAX写法；

另一方面，嵌入后每天将有大量的用户使用这个功能来写DAX，给它提供大量的学习素材，它的进化速度将大大提升。

从智障到智能，也许只需要一两个月甚至一两周，有了ChatGPT，再也不需要写大量的DAX了，我们要做的只是提出需求，以及对结果的判断和调试。

**2\. 问答**

[PowerBI中的问答](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484069875&idx=1&sn=256223aa887ad9f90693772dd9f1dd0d&chksm=8e0c4f24b97bc6328bf5dd1d146218149a2ae51b7a96fd06df2f88b9bc1b84f489335dbd2c26&scene=21#wechat_redirect)功能已经推出几年了，用的人并不多，因为的确不好用。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMgooUVUjmLDKLic34wib1wcEibiav7QN24wehflicZF3iaBiaibplzm5IMLxDeLVex2RonQ3qXRkBs9JHk4w/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

但这个功能更适合AI，你只需提问，它直接给出结果。  

问答输出的不仅是文本，可以直接根据提问者的要求，生成可视化图表，如果未来嵌入的不仅仅是聊天的ChatGPT，而是直接嵌入更通用的OpenAI模型，这时候问答将真正变成一个智能工具，你想要用什么图表、展现什么数据，甚至用什么样的配色风格，都不需要你动手了，你要做的就是提出具体的需求。

问答将成为PowerBI中制作报告的日常用法。

**3\. 智能叙述**

[智能叙述](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073801&idx=1&sn=3a6dcd73ed52e77a4159612fe49af3e7&chksm=8e0c5f9eb97bd68889ce7e6ae0af81e62b7ed6b7ea7827deb5ca1ba097c14e4965889736baa4&scene=21#wechat_redirect)可以根据当前的报告内容，自动生成文字见解，不过现在这个功能还很弱，也称不上智能。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPhCx8TTiczKPThfA6zfF6rwX2uJ4sxYeo87svMoalrmnG4prz7ib7WbjgibibsluccUNF3gMDdDcJUEg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

而有了ChatGPT加持，这个功能将变得名副其实，你可以随时随地，点击某个图表或者报告，让它直接告诉你其中的关键信息。

**4\. 异常检测**

**![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPnlBZuYvQ2UKCxWJ81RPJKxJfH1j8451LcjRiaGXHibvlqcVyc2XGleEgqM9TYicMf6lWWRLqTKZbLg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)**

融入AI以后，[异常检测](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078632&idx=1&sn=234d9c75989a118e3cc8f748c3863e22&chksm=8e13a2ffb9642be927cf5adfdf800aeff6c36f9c8362107f7ed730b15b8869665c982ff46198&scene=21#wechat_redirect)的功能将会变得很通用，每个图表都将拥有这个功能，随时呈现异常信息，并进一步给出合理的解释和应对建议。  

**5\. 关键影响因素**

[关键影响因素](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068371&idx=1&sn=497a7574a9d1a8a69d7d5e90f3ac6d64&chksm=8e0c4ac4b97bc3d2bbde4d08927abf4a1f25ae5dcf0c8cf01ed9e45b63a21fe1d3ad7db3b2f7&scene=21#wechat_redirect)是一个可视化对象，可以解释某指标，主要是被哪些因素所影响，以及影响的程度，不过不太直观，用起来也比较麻烦。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPqY3eZjZlYuNajFq1IP8NW2mJOKRmKByCF2HXnAVpB4uoRcjFDgCqjibvhUTDXJWR9icZ082OrEibyA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

如果ChatGPT嵌入，这个视觉对象很可能没有存在的必要了，我们直接可以通过问答来让AI模型来解释某个指标并通过指定的图表呈现出来。  

___

上面就是目前PowerBI里和智能沾边的功能（其实都不智能），他们都将被ChatGPT优化或者取代。  

如果融入的不仅仅是这个聊天AI，而是直接嵌入更通用更强大的OpenAI模型，经过迭代以后，PowerBI中所有的功能都会被优化，比如：

-   数据清洗：自动分析数据结构中的规律，简单的清洗工作可以让AI一键完成。  
    
-   数据建模：自动分析表之间的业务逻辑关系，提供建模建议，自动生成维度表，自动建立星型模型，而不是现在将数据上载后，自动在表之间连乱七八糟的关系。  
    
-   数据可视化：甚至连拖拽生成图表的操作都不需要了，直接说出你想用什么图表分析什么数据，自动将精美的图表直接呈现出来。
    

届时PowerBI本身可能会变成组织数据的框架工具和AI分析的输出窗口，把散落在各处的数据导入到一起，根据业务需求建立模型（AI可以提供建模建议），然后AI就可以在这个框架中捕获数据模型的全部信息，自动输出业务见解。

而对个性化的分析需求，用户只需要用自然语言描述出来向它提问，PowerBI作出高效的有数据支持的解答，解答并不一定是文字，还可以是最合适的可视化图表，甚至直接生成一份可视化报告（就像现在它可以自动写出文本的分析报告一样）。

从GPT的能力和进化速度来看，这个可能并不会很遥远，让我们拭目以待吧。

到那个时候，PowerBI将彻底改头换面，它也不再是PowerBI，而是PowerAI了，一个真正的自助式智能分析工具。

在真正的智能分析工具面前，我们还需要做什么呢？基础的、机械性的操作，AI都可以完成，而我们能做的有价值的事情，就是去提出问题、判断输出结果、深入思考业务逻辑、寻找更多分析角度，然后，提出更好的问题。

以上只是我个人的畅想，大家还有什么补充的，欢迎留言分享~  
