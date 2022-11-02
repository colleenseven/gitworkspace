---
create_date: 2022-07-12T12:28:26 (UTC +08:00)
tags: 建模技巧
pagetitle: 如何在Power BI报告中插入链接？
source: https://mp.weixin.qq.com/s/vAPo6AeDF4IuPino0pdNuA
author: 采悟
status: 已完成
category: 浏览文章
uid: 
---

经常有人问如何在PowerBI报告中插入链接，点击即可跳转到一个网页，这是很常见的需求，这里就介绍几种插入链接的方式。

#### **1、利用文本框插入链接**

<mark style="background: #FF5582A6;">插入文本框，就会在格式栏看到“插入链接”的按钮</mark>，这里以PowerBI官网为例：https://powerbi.microsoft.com

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNZXcVP7HTZZpvtQm6lyS3ickPZqN8YX22NCnKE1b3GBLVOgicQoSaIMzTfhYrWicmOROFh0MNWIHElQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以在这里直接输入网址，文本框中会出现网址链接；或者先选中文本后，再输入网址，这样不会直接显示网址，而是作为文本的超链接。

在编辑状态下不能直接点击打开链接，发布后在阅读状态可以直接点击跳转到对应的网页。

#### **2、利用按钮插入链接**

<mark style="background: #FF5582A6;">按钮经常与书签结合用于导航，它其实也可以用于网页的跳转</mark>。插入按钮后，可以在按钮的操作属性中，选择类型为“Web URL”，然后在下面输入网址即可：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNZXcVP7HTZZpvtQm6lyS3icEQ2ICEfhCqK9Mga6UjjlGuGGJu5mfcrQdQ9GAVYuj1PfBricdYiaTubA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

对于按钮的点击，在编辑状态下同样需要按住Ctrl才能点击进入，阅读状态下可直接点击。

上面两种方式都是单独插入一个链接，如果在数据表中有个链接字段，需要批量插入多个链接，可以使用下面的方式。  

#### **3、利用表格/矩阵插入链接**

以之前介绍的豆瓣图书信息为例（[Power BI如何获取网页中的链接](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070458&idx=1&sn=c4c2f4de681ef66524b91209e83dd769&chksm=8e0c42edb97bcbfb525a923d9d7378095f91ae9e3d592e28b7918ee1ea8a991b49ed4017fee0&scene=21#wechat_redirect)），已经从网页获取了每本书的链接，如果把这个字段直接放到表格里展示：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNZXcVP7HTZZpvtQm6lyS3icib7pbxHNBiaJeFxjwsUs3Pn77GQ9Gjib0xw7mFNPdia6OV9JcBv1eHBkaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样的网址是无法点击跳转的。

对于网址字段，需要先选中它，然后设置它的数据类别，调整为“Web URL”:

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNZXcVP7HTZZpvtQm6lyS3ic8cHULKicxcBI4UEmcCGVYwqyFfIInibKibxA1GKR29wxR7qFSdUCFOjAA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后表格中的网址就变成了链接的样式，点击就可以跳转了：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNZXcVP7HTZZpvtQm6lyS3icKaaTLiaeLWe16h7B05woNd9Va0Qu8Qgdsrib1RlmTPDncZ1TTy0OvCpg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果觉得网址太长不够美观，还可以<mark style="background: #FF5582A6;">不显示网址，直接显示一个链接图标</mark>，在表格的格式面板中，打开“URL 图标”。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNZXcVP7HTZZpvtQm6lyS3icS9J87e6xw1oGZVwBUC60YSElsNXVIGYHpJmaHgpkiaqD4zWEpKxXibbg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

设置后链接的效果是这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNZXcVP7HTZZpvtQm6lyS3ic1L08AwJa8YQFIM4rwCK0liaJh2WZDNYOicECteLAyCgwjxdvD6foYhzw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样看起来就比一大串的网址简洁多了。

不过还可以进一步设置，<mark style="background: #FF5582A6;">不单独把链接的字段放到表格中，而是把它作为书名的超链接</mark>。  

在单元格元素中，找到“书名”列，打开"Web URL":

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNZXcVP7HTZZpvtQm6lyS3icR4sSkBTn8RcN0Up5OibibFicGlmrlkYH1jcHrn7SRT6Rm147ubH0qWcLw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后在弹出的窗口中，格式样式选择“字段值”，基于哪个字段选择“链接”  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNZXcVP7HTZZpvtQm6lyS3icGkCabLT0GMZaIVLgqJzxPG5hRnThzXO6YryDQtAeibm1XcvxscVCcNg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后书名就自动带有超链接。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNZXcVP7HTZZpvtQm6lyS3ic0dfyGdBsBJKRobGd0vP9wXVFUVDJtfX80xVI94GY9SePq5ytuejCYg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击某个书名即可跳转到对应的网页，而不需要在表格中单独放一列网址。

以上就是PowerBI报告中插入网址链接的几种常用方式，基本可以满足日常需要。
