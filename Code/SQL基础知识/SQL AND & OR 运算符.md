---
create_date: 2022-12-03T21:59:10 (UTC +08:00)
tags: 菜鸟教程/SQL
aliases: null
pagetitle: SQL AND & OR 运算符 | 菜鸟教程
source: https://www.runoob.com/sql/sql-and-or.html
author: 
status: 已完成
category: 
notes: False
ZK: Origin
uid: 
---
归类:: 逻辑运算符
___

AND & OR 运算符用于基于一个以上的条件对记录进行过滤。

___

## SQL AND & OR 运算符

如果==第一个条件和第二个条件都成立，则 AND 运算符显示一条记录==。

如果==第一个条件和第二个条件中只要有一个成立，则 OR 运算符显示一条记录==。

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

## AND 运算符实例

下面的 SQL 语句从 "Websites" 表中==选取国家为 "CN" 且alexa排名大于 "50" 的所有网站==：

## 实例

```sql
SELECT * 
FROM Websites 
WHERE country='CN' AND alexa > 50;
```

执行输出结果：

![](https://www.runoob.com/wp-content/uploads/2013/09/and-or1.jpg)

  

___

## OR 运算符实例

下面的 SQL 语句从 "Websites" 表中选取国家为 "USA" 或者 "CN" 的所有客户：

## 实例

```sql
SELECT * 
FROM Websites 
WHERE country='USA' OR country='CN';
```

执行输出结果：

![](https://www.runoob.com/wp-content/uploads/2013/09/and-or2.jpg)

  

___

## 结合 AND & OR

您也可以==把 AND 和 OR 结合起来==（使用圆括号来组成复杂的表达式）。

下面的 SQL 语句从 "Websites" 表中选取 alexa 排名大于 "15" 且国家为 "CN" 或 "USA" 的所有网站：

## 实例

```sql
SELECT * 
FROM Websites 
WHERE alexa > 15 AND (country='CN' OR country='USA');
```


执行输出结果：

![](https://www.runoob.com/wp-content/uploads/2013/09/and-or3.jpg)
