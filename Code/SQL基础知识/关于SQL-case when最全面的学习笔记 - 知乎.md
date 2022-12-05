---
create_date: 2022-12-04T11:23:49 (UTC +08:00)
tags: 知乎/SQL
aliases: null
pagetitle: 关于SQL-case when最全面的学习笔记 - 知乎
source: https://zhuanlan.zhihu.com/p/110198759
author: 
status: 已完成
category: 
notes: False
ZK: Origin
uid: 
---

**推荐学习书籍：**  
**1、SQL基础教程 6-3**  
**2、SQL进阶教程 1-1**

![](https://pic2.zhimg.com/v2-23641118032f95186b4fce26321d14d1_b.jpg)

case when 是SQL语法中提供的标准的条件分支。  
条件分支在MYSQL中即为IF函数，不同的数据库都会提供自己的一些函数，但是==CASE WHEN 更加通用==。

## CASE语句的两种写法

### 1、搜索CASE表达式

（只会这一种方式即可）

```sql
CASE 
WHEN <求值表达式> THEN <表达式1>
WHEN <求值表达式> THEN <表达式2>
ELSE <表达式>
END
```

<求值表达式> ：一般为字段 【=、>、<、in、等】如 字段 = "1"  
<表达式1> : 一般为字段或者字符串或者数值等。  

### 2、简单CASE表达式

```sql
CASE <表达式>
WHEN <表达式> THEN <表达式>
WHEN <表达式> THEN <表达式>
ELSE <表达式>
END
```

注：

1.  ==ELSE 可以不写，默认返回null==
2.  end 不可以忘记
3.  当一个case子句中有多个判断逻辑时、字段类型需要一致
4.  ==当一个case子句中有多个判断逻辑时、第一个为真的结果会被输出==
5.  ==每一个case子句只输出一个结果==

## case 执行逻辑

## case 应用

### 1、添加列

现有学生表一张

![](https://pic3.zhimg.com/v2-2cd445ecb0f57b7042c589c3d0ca32a2_b.jpg)

先在需要根据生日列 `**生成新的一列 **`：显示90后，00后，10后

代码：

```sql
SELECT 
s_name
,s_birthday 
,CASE 
        WHEN YEAR(s_birthday)>=1990 and YEAR(s_birthday)<2000 THEN "90后"
        WHEN YEAR(s_birthday)>=2000 and YEAR(s_birthday)<2010 THEN "00后"
        WHEN YEAR(s_birthday)>=2010 and YEAR(s_birthday)<2020 THEN "10后"
    ELSE "未知"
    END 
    AS "阶段"
from student ;
```

显示结果：

![](https://pic4.zhimg.com/v2-74bc2f8dc4045bc9df8d42d020573237_b.jpg)

### 2、行转为列

现统计了学生的总成绩

![](https://pic4.zhimg.com/v2-b677198242e99f834910e17a56225daf_b.jpg)

。  
现在想将赵雷和李云的总成绩展示成：

![](https://pic4.zhimg.com/v2-742267bf976fb1ad1d7e4c474c341763_b.jpg)

可以输入以下代码：

```sql
SELECT 
 SUM(CASE WHEN s_name = "李云" THEN score ELSE 0 END) as "李云"
,SUM(CASE   WHEN s_name = "赵雷" THEN score ELSE 0 END) as "赵雷"
FROM
 score a INNER JOIN student b   on a.s_id=b.s_id;
```

### 3、实现分组统计

一般我们都==使用group by来实现分组统计，但是有的时候需要对字段先分组再统计==。

比如我们想知道成绩表现为不及格、良、优秀的课程数分别是多少

### 3.1 实现人次的分组统计

```sql
SELECT 
CASE 
        WHEN score<60 THEN "不及格"
        WHEN score>=60 and score<85 THEN "良"
        WHEN score>=85 THEN "优秀"
    ELSE "未知"   
    END     AS "阶段"
  ,count(*) as "人次"
from  score a INNER JOIN student b  on a.s_id=b.s_id
GROUP BY CASE 
        WHEN score<60 THEN "不及格"
        WHEN score>=60 and score<85 THEN "良"
        WHEN score>=85 THEN "优秀"
    ELSE "未知"
    END ;
```

![](https://pic3.zhimg.com/v2-0ee92bfdf25bc86fb6b103b4d609b2c6_b.jpg)

因为每个人会参加多门课程，所以==当使用`count(*)`的时候，就是对于人次计算==的，学生是没有去重的。

### 3.2 实现人数的分组统计

```sql
SELECT 
CASE 
        WHEN score<60 THEN "不及格"
        WHEN score>=60 and score<85 THEN "良"
        WHEN score>=85 THEN "优秀"
    ELSE "未知"
    END 
    AS "阶段"
,count(DISTINCT a.s_id) as "包含人数"

from  score a INNER JOIN student b  on a.s_id=b.s_id
GROUP BY CASE 
        WHEN score<60 THEN "不及格"
        WHEN score>=60 and score<85 THEN "良"
        WHEN score>=85 THEN "优秀"
    ELSE "未知"
    END ;
```

![](https://pic3.zhimg.com/v2-ca835405aefe668134c9e5a2cc25b81e_b.jpg)

  
这里==使用`count(DISTINCT a.s_id)` 对学生进行了去重==。

### 3.3 group by分组中使用别名

```sql
SELECT 
CASE 
        WHEN score<60 THEN "不及格"
        WHEN score>=60 and score<85 THEN "良"
        WHEN score>=85 THEN "优秀"
    ELSE "未知"
    END 
    AS type
,count(*)
from  score a INNER JOIN student b  on a.s_id=b.s_id
GROUP BY type;
```

更加SQL执行顺序，是==不应该使用别名的，但是在某些，比如MYSQL中执行时会先扫描select后的字段，所以实际执行是可以实现的。==

![](https://pic4.zhimg.com/v2-5a9a594fcc324bdb7a4650ff8da7fc1f_b.jpg)

### 4、透视表方式展示

case 表达式可以==实现sql像excel透视表类似的功能==。

比如我想知道每门课程，学生成绩的分别情况

![](https://pic2.zhimg.com/v2-644c1b1b43d0bd0d0826243dca5ba94d_b.jpg)

可以使用下方代码进行完成

```sql
SELECT 
c_id,
sum(CASE WHEN score<60 THEN 1   ELSE 0  END )   AS "不及格"
,sum(CASE WHEN score>=60 and score<85 THEN 1    ELSE 0 END) as "良"
,sum(CASE WHEN score>=85 THEN 1 ELSE 0 END) as "优秀"
from  score a LEFT JOIN student b   on a.s_id=b.s_id
where c_id is not null
GROUP BY a.c_id;
```

## case 执行逻辑

### 1、没有group by 的聚合

上面知识点 行转为列。  
代码如下：

```sql
SELECT 
 SUM(CASE WHEN s_name = "李云" THEN score ELSE 0 END) as "李云"
,SUM(CASE   WHEN s_name = "赵雷" THEN score ELSE 0 END) as "赵雷"
FROM
 score a INNER JOIN student b   on a.s_id=b.s_id;
```

结果为

![](https://pic4.zhimg.com/v2-742267bf976fb1ad1d7e4c474c341763_b.jpg)

我们在语句中使用了聚合函数，这个聚合函数使得数据展示为一行。如果不使用会如何？  

![](https://pic2.zhimg.com/v2-f2d733caf046fe16335851603dc996dd_b.jpg)

  
数据会以每一行的形式展示。  
因为==SQL在执行完语句后会逐行对数据进行计算==。

### 2、有group by 的汇总数据

接着上面来讲。  
这里有个问题，既然用group by了，为何还要使用SUM.。（这里主要是在mysql5.7以下会遇到这样的问题）  
我就在实际的统计中，遇到了这样的问题。  
因为自己的库装的是mysql,5.8 所以这样不符合规范的代码是运行不了的，因为要修改配置比较麻烦，我这里就手动写出他的

| c\_id | 不及格 | 良 | 优秀 | | --- | --- | --- | --- | | 01 | 1 | 0 | 0 | | 02 | 0 | 1 | 0 | | 03 | 1 | 0 | 0 |

这里就会出现每行只有一个结果。

```sql
SELECT 
c_id,
CASE WHEN score<60 THEN 1   ELSE 0  END     AS "不及格"
,CASE WHEN score>=60 and score<85 THEN 1    ELSE 0 END as "良"
,CASE WHEN score>=85 THEN 1 ELSE 0 END as "优秀"
from  score a LEFT JOIN student b   on a.s_id=b.s_id
where c_id is not null
GROUP BY a.c_id;
```

因为有groupby的存在，很容易导致计算错误还，看不错来，这为一个小坑。

这里关于SQL的执行顺序还需要单独再进行一章。
