---
create_date: 2021-08-12T22:51:25 (UTC +08:00)
tags: 
aliases: null
pagetitle: 这个Power BI可视化技巧，你学会了吗？
source: https://mp.weixin.qq.com/s/-ygI4sirkvhQZNYEvjdA_g
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

[上一篇](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076932&idx=1&sn=3cad8e68d76597590f60aeb9d067f4be&chksm=8e13ab53b9642245fee0ffb53095aaebe19b9729447cdc7209530b1ab993195f0956baba026d&scene=21#wechat_redirect)关于折线图突出显示的文章发出后，很多星友都觉得非常实用，有些同学马上就将这个技巧应用于自己的报告中了（不得不承认，行动能力太强了）。  

同时也遇到了一些朋友看完后，接着就找我问了很多问题，比如文章中的折线图只显示一条折线，如果切片器多选，高亮显示多条折线怎么做吗？

其实只要去动手做一下，就会发现非常简单，把切片产品表中的产品名称放到顶层折线图的图例中，就可以实现：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNhpYmseE3xoH8QNG6UPgKCTWHRLXYNXdP710SN4Cx7kTTiaQ8VId9RuO9E1s0ZgKMIf5fTMjW1Ryg/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

因为一个折线图显示多条折线的原理，就是在图例中放入字段，当你有这个疑惑时，只要稍微迈出一步，动手实践一下，就会发现你的问题，自己都可以轻易解决，而不是必须让别人告诉你一个答案。  

所以在学习时，一定要自信一点，大胆去摸索，摸索不出来再去提问。即使没有探索出来又能怎么样呢？你没有任何损失。

**并且在摸索的过程中，很可能对某个功能更加熟悉，理解更加深入，或者偶然接触到了以前没有注意到的一个知识点，这些经历都会让你更快速的精通。**

你看，如果遇到问题直接问，最多只能获得这个问题本身的答案，但通过自己摸索，是不是对个人知识体系的完善带来了更多的可能性呢？  

还以这个折线图为例，通过你的探索，可能还会收获更多的技巧，比如发现度量值的写法很巧妙、比如还可以通过切片器来选择多个产品，利用其他图表交叉筛选的效果同样精彩：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNhpYmseE3xoH8QNG6UPgKCnre5u5V75RkVV18F3xkne1tO4hRVnTI2ibib1NcchUjCTukBz9sNttpA/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

在探索的过程中，你可能还会发现新的问题，比如同时显示多条折线，都是同一个颜色，这几条折线就很难区分了，解决这个问题可以进行颜色设置，为折线设置不同的颜色。

还可以在折线尾部直接显示对应的产品名称，以前的文章也介绍过（[PowerBI可视化技巧：折线图上直接显示类别](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076437&idx=1&sn=8f9e3f84e7894246cf05fa8ca7166c81&chksm=8e0c5542b97bdc54f9ed24dbeb304d55e3bf9891b9271a87b1e309bfc84ad9b4d325c8e2426c&scene=21#wechat_redirect)）,利用计算组可以轻松实现下面的效果：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNhpYmseE3xoH8QNG6UPgKCzHgiagSAicn6a0oTsGPGWapicdBL75ibiaDItuHhyEibYjzhXEytlcfr0FVw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

这样是不是也很清晰，连图例都省了。  

这个技巧我也已经分享过很长一段时间了，你有没有去动手操作并学会应用呢？

当然这个可视化效果仍然有很多可以提升的细节，可视化的优化可以说永无止境，只有平时多练习、多动手、多积累，才能在需要时，有更多的技巧可以利用；遇到问题时，也有更多的解决方案可供选择。

所以，平时看文章或者看书，不要看完就觉得学会了，而不去动手应用；也不要遇到问题时，立即找别人问，而不去思考和摸索。

**能提出问题很重要，但解决问题的不一定是别人，思考、动手把问题解决掉会让你更快的提升，即使最后还是通过别人获得了答案，但经过深入思考后，这个答案已不仅仅是问题本身，而是一连串知识点的融会贯通。**  

本文算是上篇文章的一些反馈由感而发，我平时遇到过形形色色的问题和提问题的人，不少人的学习能力确实有非常大的提升空间。

希望大家在平时的学习中一定要自信、主动，敢于摸索善于摸索，只有主动学习获得的东西，才能内化为自己的技能和竞争力。

___

**[PowerBI商业数据分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)**

帮你从0到1，轻松上手PowerBI

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOojexubCy39PJZJic24XlI9IC8Fhx57SVYiciave3T7sAxeLXXZgrAzhAsUHXC3dxpU1fp72ChD8ibfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072351&idx=1&sn=fabb08c54790ac1225b470fd647c7a5e&chksm=8e0c4548b97bcc5e0450f1945a2c76039bbb42650bcb1edbc856820836d63d32af4c7780e31a&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtsEpp19Px9ucXia6Tb0wrweNUvqrKWQ6iaTeuTLOic9rAMGficXo8UnpwDA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484069406&idx=1&sn=5342b16eb810a803dea5d2472441b4e1&chksm=8e0c4ec9b97bc7df8d65d5bbfeeaa95695f7d68e989179a2eeab008a49e7e2351c561a20326e&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtVXYmWpicF9SVicdBBQYdaKG4icSfUTkS9dFIBW3NsL5ZrNpYH6icjgJaUA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 扫码加入，和 3k+ 学习者一起成长
