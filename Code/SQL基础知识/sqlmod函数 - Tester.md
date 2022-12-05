---
create_date: 2022-12-04T11:52:12 (UTC +08:00)
tags: 博客园/sql
aliases: null
pagetitle: sql:mod函数 - Tester - 博客园
source: https://www.cnblogs.com/lhTest/p/15401530.html
author: Tester
status: 已完成
category: 
notes: False
ZK: Origin
uid: 
---

## mod 的作用

求余数，和%一样

## mod的语法格式

```sql
mod(n,m)
n mod m
n % m
```

#### 语法格式说明

返回n除以m的余数，当然推荐直接%，方便快捷

#### 例子

```sql
SELECT MOD(234, 10); # 4
SELECT 253 % 7; # 1
SELECT MOD(29,9); # 2
SELECT 29 MOD 9; #2
```