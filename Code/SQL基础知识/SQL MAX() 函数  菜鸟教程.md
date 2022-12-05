---
create_date: 2022-12-04T16:18:48 (UTC +08:00)
tags: 菜鸟教程/SQL
aliases: null
pagetitle: SQL MAX() 函数 | 菜鸟教程
source: https://www.runoob.com/sql/sql-func-max.html
author: 
status: 已完成
category: 
notes: False
ZK: Origin
uid: 
---

___

## MAX() 函数

MAX() 函数返回==指定列的最大值==。

### SQL MAX() 语法

```sql
SELECT MAX(column_name) 
FROM table_name;
```


___

## 演示数据库

在本教程中，我们将使用 RUNOOB 样本数据库。

下面是选自 "Websites" 表的数据：

+----+--------------+---------------------------+-------+---------+
| id | name         | url                       | alexa | country |
+----+--------------+---------------------------+-------+---------+
| 1  | Google       | https://www.google.cm/    | 1     | USA     |
| 2  | 淘宝          | https://www.taobao.com/   | 13    | CN      |
| 3  | 菜鸟教程      | http://www.runoob.com/    | 5000  | CN      |
| 4  | 微博          | http://weibo.com/         | 20    | CN      |
| 5  | Facebook     | https://www.facebook.com/ | 3     | USA     |
|  6 | 百度         | https://www.baidu.com/    |     4 | CN      |
|  7 | stackoverflow | http://stackoverflow.com/ |     0 | IND     |
+----+---------------+---------------------------+-------+---------+


  

___

## SQL MAX() 实例

下面的 SQL 语句从 "Websites" 表的 "alexa" 列获取最大值：

## 实例

```sql
SELECT MAX(alexa) AS max_alexa 
FROM Websites;
```

执行以上 SQL 结果如下所示：

![](https://www.runoob.com/wp-content/uploads/2013/09/max1.jpg)
