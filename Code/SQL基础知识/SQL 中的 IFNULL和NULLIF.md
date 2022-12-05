---
create_date: 2022-12-03T23:04:13 (UTC +08:00)
tags: 博客园/sql
aliases: null
pagetitle: SQL 中的 IFNULL和NULLIF - 翔云123456 - 博客园
source: https://www.cnblogs.com/lanyangsh/p/10055389.html
author: 翔云123456
status: 已完成
category: 
notes: False
ZK: Origin
uid: 
---
归类:: sql函数

sql 中的IFNULL和NULLIF很容易混淆，在此记录一下。

## IFNULL

```
IFNULL(expression1, expression2)
```

==如果expression1为null, 在函数返回expression2，否则将返回expression1==。%用于数据清洗很有用%

**例如**

```
mysql> select IFNULL(0,"a");
+---------------+
| IFNULL(0,"a") |
+---------------+
| 0             |
+---------------+
1 row in set (0.00 sec)
```

第一个参数是0，不是NULL，所以结果是0.

再例如，

```
mysql> select IFNULL(NULL,"a");
+------------------+
| IFNULL(NULL,"a") |
+------------------+
| a                |
+------------------+
1 row in set (0.00 sec)

mysql>
```

第一个参数是NULL，所以结果是第二个参数"a"。

## NULLIF

```
NULLIF(expression1, expression2)
```

==如果两个参数等价，则返回NULL ；否则，返回第一个参数==。

**例如**

```
mysql> select NULLIF(1,2);
+-------------+
| NULLIF(1,2) |
+-------------+
|           1 |
+-------------+
1 row in set (0.00 sec)
```

两个参数不相等，所以结果是第一个参数1。

再例如，

```
mysql> select NULLIF(1,1);
+-------------+
| NULLIF(1,1) |
+-------------+
|        NULL |
+-------------+
1 row in set (0.00 sec)
```

两个参数相等，所以结果是NULL。

