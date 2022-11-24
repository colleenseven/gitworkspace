---
create_date: 2021-09-07T22:43:17 (UTC +08:00)
tags: 
aliases: null
pagetitle: 这个Power BI报告加密技巧，看完你就可以用上！
source: https://mp.weixin.qq.com/s/Rso-X7nVSrJqi7cQG3lDdg
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

有小伙伴问为了让PowerBI报告安全一些，能不能给报告加密，让其他人输入正确的密码才能查看，对于免费用户，其实并没有这种分享方式，但可以通过变通的方式实现，比如我上周做的一个示例报告，你可以在视频号中查看效果：  

也可以点击**阅读原文**，进入这个报告的web页亲自动手体验_（测试密码:383218）_。

很多人问是怎么实现的，这里就把报告打开让你一探究竟。

如果你熟悉PowerBI中按钮和导航功能，再看到这个报告的完整页面，应该就已经猜到其中的秘密了：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMOia023XBoSPkZdeXmROUQKDSXI6SldE6dYG4U9zKRIyayT8hTGNsia1vRUbyic5HYzk4B94UGEdRUw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

**首页上的密码输入框，以及其他页面密码键盘上每个数字，其实都是按钮，按钮属性设置为“页导航”，每点击一次，就跳转到下一页。**

生成密码的这些按键上的数字，其实只是分辨位置的按钮文本，用任何字符替代都可以，而密码输入框中用于隐藏密码的“\*”，真的就是一个星号而已。

每次输入密码，都必然面临正确和错误两种情况，这里设置的是6位密码，所以涉及密码输入的页面，做了6正、6错12个，如果你点击正确的密码按钮，就在正确的页面上按顺序跳转，也**只有全部输入正确的密码，才能按指定顺序跳转到报告页。**

但只要其中有任何一个密码按钮点击错误，就会跳转到错误的页面，但并不会立即提示你，**在错误的页面上，点击任何按钮，都只能跳转到下一个错误页**，再也不可能跳转到正确的页面，直到点击完6次密码按钮，才会提示输入错误，请重新输入。

以上就是按钮跳转设计的原则，也是这个密码验证的整体思路。

剩下的就是细节的处理，其中密码键盘，可以先在一个页面上设计好，先添加一个按钮，然后复制生成其他按钮，多个按钮的排列，可以一次框选多个，灵活使用对齐功能，快速排列。  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMOia023XBoSPkZdeXmROUQKEMlzkp7RvNS5coesnbuEGGOozOTXSiaiaokNK0xVjkdBfB25LHyk8hJQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

一个页面上排列好数字键盘后，将该页面复制多个，并了避免混乱，做好命名，以便设计每一个步骤要跳转的目标页。  

而对每个按钮设置操作属性，也可以用鼠标框选一次性设置，比如错误页面的按钮属性全部设置为了下一个错误页的导航：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMOia023XBoSPkZdeXmROUQKIAiaPJqfbU1w3FewBsQFCbs1PuQPupy2odvgrvqtPFBs10RPNhVnztQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

运用这些批量设置的技巧，其实很快就能做出这样的报告，关键是多动手，各种功能熟练应用。

当然这种密码验证的报告不止这一种做法，但可以算是最简洁的一种，不需要技术背景、不需要DAX，也不需要繁琐的设置，初学者就可以做到。

介绍到这里也许你的思路就打开了，灵活运用PowerBI中的按钮、书签、页导航等功能，你还可以再继续探索，比如加个用户识别，让不同的用户跳转到不同的密码页，输入不同的密码，最后查看不同的报告，实现密码验证的页面级权限控制。

学习PowerBI，不需要在各种奇奇怪怪的小技巧上面花太多功夫，只需用心把基本功做扎实，就能充分享受PowerBI的强大功能，至于各种吸引眼球的小技巧，想用也难不到你，万变不离其宗。

最后提醒一下，这种方式必须发布到web才有这个效果，虽然有密码验证，但发布到web本身是存在安全隐患的，内部敏感数据不建议使用。

___

**[PowerBI商业数据分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)**

帮你从0到1，轻松上手PowerBI

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNuVIqc0mzbKDNPmI0mwcTkvUibMVjf4z1bY0MYFh7lAkqrcHiaEHE4UicvjJjibpmkxJjc4TDlVO04qg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPUabZXugXKNdmeUzxwJM4OyUpTibBJjoq1jk8CzVZJz6s4nJRW1ViammT4ecqAJ7iapDccKNNrwtLYQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077212&idx=1&sn=bb3dac9becf80b5d929e5dc8405158dd&chksm=8e13a84bb964215d6362f78768cdefa18def4dfc8cd5c14f075442431604ed9c9729e4051a4b&scene=21#wechat_redirect)

[](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077048&idx=1&sn=b3da0a4079ed8366c67982912e795d59&chksm=8e13ab2fb964223978c16d5647e4a28eaeb50bc7338c4e82f4e14f2cddc8bb844b956f09beb6&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

↑ 扫码加入，和 3k+ 学习者一起成长
