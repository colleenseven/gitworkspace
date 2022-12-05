---
create_date: 2022-12-04T12:31:16 (UTC +08:00)
tags: 菜鸟教程/SQL
aliases: null
pagetitle: SQL DELETE 语句 | 菜鸟教程
source: https://www.runoob.com/sql/sql-delete.html
author: 
status: 已完成
category: 
notes: False
ZK: Origin
uid: 
---

___

DELETE 语句用于删除表中的记录。

___

## SQL DELETE 语句

DELETE 语句用于删除表中的行。

### SQL DELETE 语法

```sql
DELETE 
FROM _table_name_  
WHERE _some_column_=_some_value_;
```
  

<table><tbody><tr><th><img decoding="async" src="https://www.runoob.com/images/lamp.jpg" width="32" height="32" alt="lamp"></th><td><strong>请注意 SQL DELETE 语句中的 WHERE 子句！</strong><br>WHERE 子句规定哪条记录或者哪些记录需要删除。如果您省略了 WHERE 子句，所有的记录都将被删除！</td></tr></tbody></table>

  

___

## 演示数据库

在本教程中，我们将使用 RUNOOB 样本数据库。

下面是选自 "Websites" 表的数据：

```
+----+--------------+---------------------------+-------+---------+
| id | name         | url                       | alexa | country |
+----+--------------+---------------------------+-------+---------+
| 1  | Google       | https://www.google.cm/    | 1     | USA     |
| 2  | 淘宝       | https://www.taobao.com/   | 13    | CN      |
| 3  | 菜鸟教程 | http://www.runoob.com/    | 4689  | CN      |
| 4  | 微博       | http://weibo.com/         | 20    | CN      |
| 5  | Facebook     | https://www.facebook.com/ | 3     | USA     |
+----+--------------+---------------------------+-------+---------+
```

  

___

## SQL DELETE 实例

假设我们要从 "Websites" 表中删除网站名为 "Facebook" 且国家为 USA 的网站。

我们使用下面的 SQL 语句：

## 实例

```sql
DELETE 
FROM Websites 
WHERE name='Facebook' AND country='USA';
```



执行以上 SQL，再读取 "Websites" 表，数据如下所示：

![](https://www.runoob.com/wp-content/uploads/2013/09/BD5EFB9A-2A65-4AF8-81F3-022E051811DC.jpg)

___

## 删除所有数据

您可以在不删除表的情况下，删除表中所有的行。这意味着表结构、属性、索引将保持不变：

**注释：**在删除记录时要格外小心！因为您不能重来！
