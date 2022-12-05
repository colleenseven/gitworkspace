---
create_date: 2022-12-04T15:05:11 (UTC +08:00)
tags: 菜鸟教程/SQL
aliases: null
pagetitle: SQL SELECT DISTINCT 语句 | 菜鸟教程
source: https://www.runoob.com/sql/sql-distinct.html
author: 
status: 已完成
category: 
notes: False
ZK: Origin
uid: 
---

___

SELECT DISTINCT 语句用于==返回唯一不同的值==。

___

## SQL SELECT DISTINCT 语句

在表中，一个列可能会包含多个重复值，有时您也许希望仅仅列出不同（distinct）的值。

DISTINCT 关键词用于返回唯一不同的值。

### SQL SELECT DISTINCT 语法

```sql
SELECT DISTINCT _column_name_,_column_name_  
FROM _table_name_;
```
  

___

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
+----+--------------+---------------------------+-------+---------+
```

  

___

## SELECT DISTINCT 实例

下面的 SQL 语句仅从 "Websites" 表的 "country" 列中选取唯一不同的值，也就是去掉 "country" 列重复值：

## 实例

```sql
SELECT DISTINCT country
FROM Websites;
```

输出结果：

![](https://www.runoob.com/wp-content/uploads/2013/09/E3012A35-35DF-4BBB-8657-8A312C5AEAB6.jpg)
