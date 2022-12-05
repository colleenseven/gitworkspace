---
create_date: 2022-12-04T12:50:15 (UTC +08:00)
tags: CSDN/sql
aliases: null
pagetitle: sql using_云闲不收的博客-CSDN博客_sql using
source: https://blog.csdn.net/S_ZaiJiangHu/article/details/121611891
author: 
status: 已完成
category: 
notes: False
ZK: Origin
uid: 
---

mysql中using的用法为：

using()==用于两张表的join查询，要求using()指定的列在两个表中均存在，并使用之用于join的条件==。

示例：

复制代码代码如下:

```sql
  select a.*, b.* from a left join b using(colA);
```

等同于：

复制代码代码如下:

```sql
  select a.*, b.* from a left join b on a.colA = b.colA;
```

