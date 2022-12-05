---
create_date: 2022-12-04T12:40:34 (UTC +08:00)
tags: 菜鸟教程/SQL
aliases: null
pagetitle: SQL LEFT JOIN 关键字 | 菜鸟教程
source: https://www.runoob.com/sql/sql-join-left.html
author: 
status: 已完成
category: 
notes: False
ZK: Origin
uid: 
---

___

## SQL LEFT JOIN 关键字

LEFT JOIN 关键字从左表（table1）返回所有的行，即使右表（table2）中没有匹配。如果右表中没有匹配，则结果为 NULL。

### SQL LEFT JOIN 语法

```sql
SELECT _column_name(s)_  
FROM _table1_  
LEFT JOIN _table2_  
ON _table1.column_name_=_table2.column_name_;
```


或：
```sql
SELECT _column_name(s)_  
FROM _table1_  
LEFT OUTER JOIN _table2_  
ON _table1.column_name_=_table2.column_name_;
```


**注释：**在某些数据库中，==LEFT JOIN 称为 LEFT OUTER JOIN==。

![SQL LEFT JOIN](https://www.runoob.com/wp-content/uploads/2013/09/img_leftjoin.gif)

___

## 演示数据库

在本教程中，我们将使用 RUNOOB 样本数据库。

下面是选自 "Websites" 表的数据：

```
+----+--------------+---------------------------+-------+---------+
| id | name         | url                       | alexa | country |
+----+--------------+---------------------------+-------+---------+
| 1  | Google       | https://www.google.cm/    | 1     | USA     |
| 2  | 淘宝          | https://www.taobao.com/   | 13    | CN      |
| 3  | 菜鸟教程      | http://www.runoob.com/    | 4689  | CN      |
| 4  | 微博          | http://weibo.com/         | 20    | CN      |
| 5  | Facebook     | https://www.facebook.com/ | 3     | USA     |
| 7  | stackoverflow | http://stackoverflow.com/ |   0 | IND     |
+----+---------------+---------------------------+-------+---------+
```

下面是 "access\_log" 网站访问记录表的数据：

```
mysql> SELECT * FROM access_log;
+-----+---------+-------+------------+
| aid | site_id | count | date       |
+-----+---------+-------+------------+
|   1 |       1 |    45 | 2016-05-10 |
|   2 |       3 |   100 | 2016-05-13 |
|   3 |       1 |   230 | 2016-05-14 |
|   4 |       2 |    10 | 2016-05-14 |
|   5 |       5 |   205 | 2016-05-14 |
|   6 |       4 |    13 | 2016-05-15 |
|   7 |       3 |   220 | 2016-05-15 |
|   8 |       5 |   545 | 2016-05-16 |
|   9 |       3 |   201 | 2016-05-17 |
+-----+---------+-------+------------+
9 rows in set (0.00 sec)
```

___

## SQL LEFT JOIN 实例

下面的 SQL 语句将返回所有网站及他们的访问量（如果有的话）。

以下实例中我们把 Websites 作为左表，access\_log 作为右表：

## 实例

```sql
SELECT Websites.name, access_log.count, access_log.date  
FROM Websites  
LEFT JOIN access_log  
ON Websites.id=access_log.site_id  
ORDER BY access_log.count DESC;
```


执行以上 SQL 输出结果如下：

![](https://www.runoob.com/wp-content/uploads/2013/09/left-join1.jpg)

**注释：**LEFT JOIN 关键字从左表（Websites）返回所有的行，即使右表（access\_log）中没有匹配。
