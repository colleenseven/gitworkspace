---
create_date: 2022-12-03T23:53:01 (UTC +08:00)
tags: 菜鸟教程/SQL
aliases: null
pagetitle: SQL ORDER BY 关键字 | 菜鸟教程
source: https://www.runoob.com/sql/sql-orderby.html
author: 
status: 已完成
category: 
notes: False
ZK: Origin
uid: 
---

___

ORDER BY 关键字用于==对结果集进行排序==。

___

## SQL ORDER BY 关键字

ORDER BY 关键字用于对结果集按照一个列或者多个列进行排序。

ORDER BY 关键字==默认按照升序对记录进行排序==。如果需要按照降序对记录进行排序，您可以使用 DESC 关键字。

### SQL ORDER BY 语法

```sql
SELECT _column_name_,_column_name_  
FROM _table_name_  
ORDER BY _column_name_,_column_name_ ASC|DESC;
```
  
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

## ORDER BY 实例

下面的 SQL 语句从 "Websites" 表中选取所有网站，并按照 "alexa" 列排序：

## 实例

```sql
SELECT * 
FROM Websites 
ORDER BY alexa;
```


执行输出结果：

![](https://www.runoob.com/wp-content/uploads/2013/09/orderby1.jpg)

  

___

## ORDER BY DESC 实例

下面的 SQL 语句从 "Websites" 表中选取所有网站，并按照 "alexa" 列==降序排序==：

## 实例

```sql
SELECT * 
FROM Websites 
ORDER BY alexa DESC;
```

执行输出结果：

![](https://www.runoob.com/wp-content/uploads/2013/09/orderby2.jpg)

  

___

## ORDER BY 多列

下面的 SQL 语句从 "Websites" 表中选取所有网站，并==按照 "country" 和 "alexa" 列排序==：

## 实例

```sql
SELECT * 
FROM Websites 
ORDER BY country,alexa;
```


执行输出结果：

![](https://www.runoob.com/wp-content/uploads/2013/09/orderby3.jpg)
