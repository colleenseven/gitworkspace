---
create_date: 2022-12-03T23:23:42 (UTC +08:00)
tags: 博客园/sql
aliases: null
pagetitle: Mysql 中is null 和 =null 的区别 - 手撕高达的村长 - 博客园
source: https://www.cnblogs.com/sunxun/p/4335108.html
author: 手撕高达的村长
status: 已完成
category: 
notes: False
ZK: Origin
uid: 
---

在mysql中，筛选非空的时候经常会用到is not null和!=null，这两种方法单从字面上来看感觉是差不多的，其实如果去运行一下试试的话差别会很大！

为什么会出现这种情况呢？

==null 表示什么也不是， 不能=、>、< … 所有的判断，结果都是false，所有只能用 is null进行判断。  ==
默认情况下，推荐使用 IS NOT NULL去判断，因为==SQL默认情况下对！= Null的判断会永远返回0行，但没有语法错误==。  
如果你一定想要使用！= Null来判断，需要加上这个语句：

set ANSI\_NULLS off

这时你会发现IS NOT NULL 和 != null 是等效的

  
个字段如果设为“NULL”，表示如果这个字段的值为空时，自动插入一个“NULL”值。

一个字段如果设为“NOT NULL”，表示如果这个字段的值为空时，不自动插入“NULL”值（任其无值）。

所以，设为“NULL”的意思反而是“不能无值”（由MYSQL自动赋“NULL”值），而设为“NOT NULL”是“可以无值”。

其实要证明这一点很简单，建一个测试表，两个字段（VC型），一个设为“NULL”，一个设为“NOT NULL”，两个都

插入空值，看看结果就明白了。

==NULL 不是 '' 也不是 0。==

你的字段定义为 not null，但是却赋值了一个 null，那么数据库系统会按照该字段类型选择一个默认的值放进去，

比如 char 就是用空字符串。  
但注意，空字符串其实已经是一个确定的值了，就是一个长度为 0 的字符串！

==至于 NULL 值，给你一个正确的理解：把 NULL 理解为 UNKNOWN。  ==
主要意思是'不知道'，就是它可能是任何值；  
另外一层意思是'信息缺失'，比如某个存储姓名信息的字段值是 NULL，代表姓名信息缺失。  
所以 NULL 值不是任意一个确定的值！

举例来说，逻辑 与/或 运算会的吧？  
与运算：true and true = true， true and false = false， false and true = false， false and false =

false  
第一个 true and null，它的结果完全靠 null 确定。如果它是 true 结果就是 true，如果它是 false，结果就是

false。因为 null 代表不知道，所以结果也是不知道，所以是 null。

第二个 false and null，它的结果不需要靠 null 确定，因为 and 运算的特性，有 false 出 false，所以结果是false。

第三个 null and null，就好理解了吧，它完全就是空对空了，两个操作数都是不知道，结果自然也是不知道，所以是 null。
