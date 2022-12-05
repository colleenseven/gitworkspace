---
create_date: 2022-12-04T12:06:12 (UTC +08:00)
tags: 菜鸟教程/SQL
aliases: null
pagetitle: SQL UPDATE 语句 | 菜鸟教程
source: https://www.runoob.com/sql/sql-update.html
author: 
status: 已完成
category: 
notes: False
ZK: Origin
uid: 
---

___

UPDATE 语句用于==更新表中的记录==。

___

## SQL UPDATE 语句

UPDATE 语句用于更新表中已存在的记录。

### SQL UPDATE 语法

```sql
UPDATE _table_name_  
SET _column1_=_value1_,_column2_=_value2_,...  
WHERE _some_column_=_some_value_;
```


<table><tbody><tr><th><img decoding="async" src="https://www.runoob.com/images/lamp.jpg" width="32" height="32" alt="lamp"></th><td><strong>请注意 SQL UPDATE 语句中的 WHERE 子句！</strong><br>WHERE 子句规定哪条记录或者哪些记录需要更新。如果您省略了 WHERE 子句，所有的记录都将被更新！</td></tr></tbody></table>

  

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
+----+--------------+---------------------------+-------+---------+
```

  

___

## SQL UPDATE 实例

假设我们要==把 "菜鸟教程" 的 alexa 排名更新为 5000，country 改为 USA==。

我们使用下面的 SQL 语句：

## 实例

```sql
UPDATE Websites 
SET alexa='5000', country='USA' WHERE name='菜鸟教程';
```



执行以上 SQL，再读取 "Websites" 表，数据如下所示：

![](https://www.runoob.com/wp-content/uploads/2013/09/update1.jpg)

  

___

## Update 警告！

在更新记录时要格外小心！在上面的实例中，如果我们省略了 WHERE 子句，如下所示：

```sql
UPDATE Websites
SET alexa='5000', country='USA'
```

执行以上代码会将 Websites 表中所有数据的 alexa 改为 5000，country 改为 USA。

执行没有 WHERE 子句的 UPDATE 要慎重，再慎重。
