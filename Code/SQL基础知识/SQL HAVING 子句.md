---
create_date: 2022-12-03T22:43:35 (UTC +08:00)
tags: 菜鸟教程/SQL
aliases: null
pagetitle: SQL HAVING 子句 | 菜鸟教程
source: https://www.runoob.com/sql/sql-having.html
author: 
status: 已完成
category: 
notes: False
ZK: Origin
uid: 
---

___

## HAVING 子句

在 SQL 中增加 HAVING 子句原因是，==WHERE 关键字无法与聚合函数一起使用==。

HAVING 子句可以让我们==筛选分组后的各组数据==。

### SQL HAVING 语法

## SQL HAVING 语法

```sql
SELECT column_name, aggregate_function(column_name) 
FROM table_name 
WHERE column_name operator value %列名的表达式%
GROUP BY column_name 
HAVING aggregate_function(column_name) operator value;
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

## SQL HAVING 实例

现在我们想要==查找总访问量大于 200 的网站==。

我们使用下面的 SQL 语句：

## 实例

```sql
SELECT Websites.name, Websites.url, SUM(access_log.count) AS nums 
FROM (access_log INNER JOIN Websites 
	  ON access_log.site_id=Websites.id) 
GROUP BY Websites.name 
HAVING SUM(access_log.count) > 200;
```



执行以上 SQL 输出结果如下：

![](https://www.runoob.com/wp-content/uploads/2013/09/having1.jpg)

现在我们想要查找总访问量大于 200 的网站，并且 alexa 排名小于 200。

我们在 SQL 语句中增加一个普通的 WHERE 子句：

## 实例

SELECT Websites.name, SUM(access\_log.count) AS nums FROM Websites INNER JOIN access\_log ON Websites.id\=access\_log.site\_id WHERE Websites.alexa < 200 GROUP BY Websites.name HAVING SUM(access\_log.count) > 200;

执行以上 SQL 输出结果如下：

![](https://www.runoob.com/wp-content/uploads/2013/09/having2.jpg)
