---
create_date: 2022-12-04T15:01:43 (UTC +08:00)
tags: 
aliases: null
pagetitle: SQL-自链接的用法 - Fancy[love] - 博客园
source: https://www.cnblogs.com/fancy2022/p/15885176.html
author: Fancy[love]
status: 已完成
category: 
notes: False
ZK: Origin
uid: 
---

2022.02.11SQL-自连接

自连接：针对相同的表进行的连接，叫“自连接（self join）”

自连接获得**笛卡尔积**


```sql
CREATE TABLE Products
(name VARCHAR(16) PRIMARY KEY,
 price INTEGER NOT NULL);

--可重排列·排列·组合
INSERT INTO Products VALUES('苹果',    50);
INSERT INTO Products VALUES('橘子',    100);
INSERT INTO Products VALUES('香蕉',    80);
```


此时行数组合3^2 = 9；

```sql
/* 用于获取可重排列的SQL语句 */
SELECT P1.name AS name_1, P2.name AS name_2
  FROM Products P1, Products P2;
```

接下来排除（苹果，苹果）这种相同元素组合，需要用到**非等值自连接**的方式：

```sql
/* 用于获取排列的SQL语句 */
SELECT P1.name AS name_1, P2.name AS name_2
  FROM Products P1, Products P2
 WHERE P1.name <> P2.name;
```

相同表的自连接和不同表之间的普通连接并没有什么区别！

___

非等值自连接排序

ROW（）
```sql
\--排序  
DELETE FROM Products;  
INSERT INTO Products VALUES('苹果', 50);  
INSERT INTO Products VALUES('橘子', 100);  
INSERT INTO Products VALUES('葡萄', 50);  
INSERT INTO Products VALUES('西瓜', 80);  
INSERT INTO Products VALUES('柠檬', 30);  
INSERT INTO Products VALUES('香蕉', 50);
```


```sql
SELECT P1.`name`,
             P1.`price`,
             (SELECT COUNT(P2.price)
                FROM products AS P2
                    WHERE P2.price > P1.price) + 1 AS rank1
FROM products AS P1
ORDER BY rank1;

/*
等同于窗口函数：
SELECT name,price,
             RANK() OVER (ORDER BY price DESC) AS rank1
  FROM products;
*/
```

![](https://img2022.cnblogs.com/blog/2710767/202202/2710767-20220211224835861-435036158.png)

DENSE\_ROW（）

```sql
SELECT P1.`name`,
             P1.`price`,
             (SELECT COUNT(DISTINCT P2.price)
                FROM products AS P2
                    WHERE P2.price > P1.price) + 1 AS rank1
FROM products AS P1
ORDER BY rank1;

/*
等同于窗口函数：
SELECT name,price,
             DENSE_RANK() OVER (ORDER BY price DESC) AS rank1
  FROM products;
*/
```

![](https://img2022.cnblogs.com/blog/2710767/202202/2710767-20220211224924976-1992750147.png)

按自连接的写法改写：

```sql
SELECT P1.name,
       MAX(P1.price) AS price,
       COUNT(P2.name) +1 AS rank_1
  FROM Products P1 LEFT OUTER JOIN Products P2
    ON P1.price < P2.price
 GROUP BY P1.name
 ORDER BY rank_1;
```

此时去掉MAX（）结果相同，因为每种水果就一个。本质就是==先按自己的name分组，然后挨个去连比自己price大的P2，返回连了多少行（P2中有0个比自己price大，那就返回0，再加1，就表示排第一名了）==，可以自己去再细细体会，下面这个例子会看的更明白：

去掉价格重复的行

```sql
 --不聚合，查看集合的包含关系
DELETE FROM Products;
INSERT INTO Products VALUES('橘子',    100);
INSERT INTO Products VALUES('葡萄',    50);
INSERT INTO Products VALUES('西瓜',    80);
INSERT INTO Products VALUES('柠檬',    30);

SELECT P1.name AS name1, P2.name AS name2
FROM products P1 LEFT OUTER JOIN products P2
ON P1.price < P2.price;
```

![](https://img2022.cnblogs.com/blog/2710767/202202/2710767-20220211230809130-1132522893.png)

为什么此时用外连接不用内连接？

```sql
/* 排序：改为内连接 */
SELECT P1.name,
       MAX(P1.price) AS price,
       COUNT(P2.name) +1 AS rank_1
  FROM Products P1 INNER JOIN Products P2
    ON P1.price < P2.price
 GROUP BY P1.name
 ORDER BY rank_1;
```

![](https://img2022.cnblogs.com/blog/2710767/202202/2710767-20220211231142501-856915509.png)

没有price大于橘子的price，所以橘子在内连接时被排除掉了。外连接可以将第1名也存储在结果里。
