---
create_date: 2020-09-07T20:39:55 (UTC +08:00)
tags:
aliases:
pagetitle: Power BI导航设计：多级下拉菜单
source: https://mp.weixin.qq.com/s/dJ4RrZep1yg9WsYpHB0WLQ
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

经常有人问Power BI报表的下拉菜单是怎么设计的，这篇文章就来带你轻松在PowerBI中制作下拉菜单式导航。  

以这个财务分析报告为例，改成下单菜单导航以后，效果是这样的：

在导航区，点击财务报表和指标分析，会弹出下拉菜单，显示下一级的导航，点击子菜单可以进入具体的报表页，这种设计主要是利用了PowerBI的书签功能，下面以**公司概况页**为例，来介绍一下制作步骤。

**1、在每个页面上添加导航需要的按钮和文本框。**

这个报告的页面分为三个类别：公司概况、财务报表和指标分析，这三个作为一级菜单。

其中财务报表可以细分为资产负债表、利润表和现金流量表，那么这三大报表就可以作为财务报表的二级菜单；而运营分析和杜邦分析作为指标分析的二级菜单。  

将一级菜单和二级菜单用按钮全部添加上去，并在二级菜单下面套一个文本框，模拟下拉框的效果：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMcz0rd1FWBAib5DHEJ5H9DhbgduIxP9fn0QPxmd5UcCNUlBWe8zQoRAY0QDmkBSGJWnQqiceC21soA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

为了识别每个按钮和文本框，可以单独为他们重命名，以便后面的快速操作。  

点击 视图>选择，在选择窗格中可以看到上面添加的按钮和文本框，双击即可重命名。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMcz0rd1FWBAib5DHEJ5H9DhGMM7sA9KrX0w8MOKtqZGRXFm0eOoAm8RhO5ZumR7ibjhLRiaFOMtbJvQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

还可以拖动组件，让他们按照菜单的顺序和包含关系来排序。  

这样操作完成以后，全选这些组件，复制，然后粘贴到其他需要下拉菜单的页面中。  

**2、修改组件的显示/隐藏属性，并生成各级菜单的书签。**

下拉菜单导航的设计，每一页至少应该有一级菜单页面，和每个二级菜单页面。  

在一级菜单页面，所有的二级菜单上的按钮和文本框隐藏，然后添加书签（如果对书签还不熟悉，请先阅读这篇文章：[PowerBI中的书签，真的非常有用！](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068219&idx=1&sn=b74e0d16ac61413a90fb5f7837dea112&chksm=8e0c75acb97bfcba745fe9ba7eb4ca2aa83d0af34a17668284170b97c68b2d3dc909dc9eb936&scene=21#wechat_redirect)），并重命名为“公司概况”，这个名称可以是任意的，按自己的需要即可：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMcz0rd1FWBAib5DHEJ5H9DhcOqowDyBA8Vib7RiaqOxFqQlvYwwPpONibZn7Y4tAme78bvR8NqVTrJZQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

页面显示如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMcz0rd1FWBAib5DHEJ5H9DhEK3dGZFTicDyfSN8Z8k8m0H1If2l902sicYl07mcA3zMk5Jf6CGxlllg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后，将财务报表的二级菜单包含的组件显示出来，添加书签，命名为“公司概况-报表下拉”：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMcz0rd1FWBAib5DHEJ5H9DhL5h7wpPlXn8lT1icOzkbmYibtlEs9ic9E1jQeicDib4uER1k5D36p1Y8pPw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

页面显示如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMcz0rd1FWBAib5DHEJ5H9DhYmTiby6ZY0NjSSqy2genGZZibVcC74hZ7Q4tZKguYpJmovib1xUVIsNZA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这就是财务报表的下拉二级菜单效果。

同样的方式制作指标分析的二级菜单书签。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMcz0rd1FWBAib5DHEJ5H9Dh1myEAEmwXWA84btK8jSicVbmbhpyWUSG2apSvX00Q0NbsPnwxq2E3xg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样，公司概况页的一级菜单书签和二级菜单书签制作完毕。  

在其他页面，按照上面的操作步骤，分别生成每个页面的各级菜单书签。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMcz0rd1FWBAib5DHEJ5H9DhOsfWdvGp5vZgXicDFLkUg7XaqM4cyd89D0OSCHaFjWl95UhdBY1Nbng/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**3，设置每个按钮的操作属性。**

比如公司概况页的一级菜单按钮“财务报表”，设置其操作属性为书签>公司概况-报表下拉：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMcz0rd1FWBAib5DHEJ5H9Dh78tuYt6Ep6u3uDuibNhkibYEMWp9PfWibPMLI9bnOdia8iaMn9mdebUFsJA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后点击这个按钮，就会有弹出下拉框的效果：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMcz0rd1FWBAib5DHEJ5H9Dhfr8QBG4CkjhpUT5eGpMKMaicgiceiauOgabBDd9bPbCiaEibHmpyejOG67w/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

在弹出的二级菜单中，设置每个按钮的操作属性为该页一级菜单的书签，比如资产负债表，直接选择书签“资产负债表”即可，点击就可以跳转到资产负债表的页面。

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMcz0rd1FWBAib5DHEJ5H9Dhn8aaDy8YGuSib50kBtUng076V7PlfwHlXUk7FOH7zS6uNUe0ib4AF5uQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

熟悉了这个跳转的逻辑和思路以后，把其他的按钮都一一设置为对应的书签即可完成下拉菜单的效果，并且在任意一个页面均可以自由切换到其他页面。

最后提醒一下，添加完书签以后，在本例中，还需要修改书签的属性，右键，将"数据"的勾选去掉:

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMcz0rd1FWBAib5DHEJ5H9Dhozbfh0QIJ5mggwrhcibME4ru6hkWZtwjfdYgA3C0ULhZm5iafgibl7jgw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**这样书签才不会把页面的数据锁定，当同步切片器修改公司名称或者年度以后，跳转到某个页面，该页面同样是最新的筛选数据。**

关于下拉菜单导航的技巧就介绍到这里，步骤并不复杂，但比较繁琐，每一步都需要细致的设置，以免出错。

本例的效果是两级菜单，如果想设置更多层级的菜单，也可以同样操作，只是需要更多的操作步骤，以及需要添加更多的书签。

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和2.3k+ 学习者一起成长
