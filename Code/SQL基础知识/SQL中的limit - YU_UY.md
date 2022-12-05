---
create_date: 2022-12-04T16:23:19 (UTC +08:00)
tags: 博客园/sql
aliases: null
pagetitle: SQL中的limit - YU_UY - 博客园
source: https://www.cnblogs.com/yu011/p/13299702.html
author: YU_UY
status: 已完成 
category: 
notes: False
ZK: Origin
uid: 
---

##### 概述

1、主要用于提取前几条或者中间某几行数据。  
```sql
select * 
from table 
limit m,n;`  
```
其中m是指记录开始的index，从0开始，表示第一条记录；n是指从m+1条开始，取n条。  
```sql
select * 
from table 
limit 2, 4;`  
```
2、即取出第3条至第6条，4条记录。  

3、取前五个：  
`limit 0, 5;`等同于`limit 5;`  
4、==limit不通用，是mysql特有的==，其他数据库中没有。  
5、==limit是sql语句最后执行的一个环节==。

##### 例子

找出工资排名在第4到第9名的员工。

```
SELECT ename, sal 
from emp 
order by sal desc 
limit 3, 6;
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200714152506793.png)

##### 通用的标准分页SQL

1、每页显示3条记录：  
第1页: 0, 3  
第2页: 3, 3  
第3页: 6, 3  
第4页: 9, 3  
第5页: 12,3  
2、  
每页显示pageSize条记录：  
第pageNo页：`(pageNo-1) * pageSize, pageSize`  
3、  
pageSize：每页显示多少条记录  
pageNo：显示第几页  
4、java代码：

```
int pageNo = 2; //页码是2
int pageSize = 10; //每页显示10条
limit(pageNo - 1) * pageSize, pageSize
```
