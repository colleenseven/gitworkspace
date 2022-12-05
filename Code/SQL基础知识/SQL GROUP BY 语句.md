---
create_date: 2022-12-03T22:07:45 (UTC +08:00)
tags: 菜鸟教程/SQL
aliases: null
pagetitle: SQL GROUP BY 语句 | 菜鸟教程
source: https://www.runoob.com/sql/sql-groupby.html
author: 
status: 已完成
category: 
notes: False
ZK: Origin
uid: 
---

分类:: 分组统计


___

GROUP BY 语句可==结合一些聚合函数==来使用

___

## GROUP BY 语句

GROUP BY 语句用于结合聚合函数，根据一个或多个列对结果集进行分组。

### SQL GROUP BY 语法

```sql
SELECT column_name, aggregate_function(column_name)  
FROM table_name  
WHERE column_name operator value  
GROUP BY column_name;
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

## GROUP BY 简单应用

==统计 access\_log 各个 site\_id 的访问量==：

## 实例

```sql
SELECT site_id, SUM(access_log.count) AS nums  
FROM access_log 
GROUP BY site_id;
```


执行以上 SQL 输出结果如下：

![](https://www.runoob.com/wp-content/uploads/2013/09/groupby1.jpg)

  

___

## SQL GROUP BY 多表连接

下面的 SQL ==语句统计有记录的网站的记录数量==：

## 实例

```sql
SELECT Websites.name,COUNT(access_log.aid) AS nums 
FROM access_log  
LEFT JOIN Websites  
ON access_log.site_id=Websites.id  
GROUP BY Websites.name;
```


执行以上 SQL 输出结果如下：

![](https://www.runoob.com/wp-content/uploads/2013/09/groupby2.jpg)
