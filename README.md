# sqlserver
sqlserver 学习笔记

# SQL语法

## select 

```

select   ...

select ... distinct ...

select ... where ...

select ... where  ... and (... or...)

select ... where ... order by columeName

```

## Insert into

第一种形式无需指定要插入数据的列名，只需提供被插入的值即可

```
INSERT INTO table_name
VALUES (value1,value2,value3,...);
```

第二种形式需要指定列名及被插入的值：
```
INSERT INTO table_name (column1,column2,column3,...)
VALUES (value1,value2,value3,...);
```

## update

## delete 

# 高级语法

## select ...  top ...

不同数据库使用的方式不一样

```sql server
SELECT TOP number|percent column_name(s)
FROM table_name;
```



```mysql
SELECT column_name(s)
FROM table_name
LIMIT number;
```



```oracle
SELECT column_name(s)
FROM table_name
WHERE ROWNUM <= number;
```

## count

cont（） 求个数

count（*）求个数

count（字段名）： 返回字段非空记录的个数，重复的记录也会被当有效

cout（distinct 字段名）： 返回字段不重复并且非空的记录的个数



## like

通配符 %  ， 单一字符 _

 %cc%  包含cc的所有的字符

%c  以c结尾的

c% 以c开头的

## in

IN 操作符允许您在 WHERE 子句中规定多个值。

## between 

BETWEEN 操作符选取介于两个值之间的数据范围内的值。这些值可以是数值、文本或者日期。

```
SELECT column_name(s)
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```

## 别名



### 函数

### avg()

### count()

### first() last()

不同数据库不一样

### max() MIN() SUM()

聚合函数

### group by

```
select  column(group by 的) ，(其余字段要是聚合函数) from table  where 条件  group by  column
```

### having

在 SQL 中增加 HAVING 子句原因是，WHERE 关键字无法与聚合函数一起使用。

HAVING 子句可以让我们筛选分组后的各组数据。

```
SELECT 
       count([Volume20GP])
      ,count([Volume40GP])
      ,count([Volume40HQ])
      ,count([Income20GP])
      ,count([Income40GP])
      ,count([Income40HQ])
      ,[blFileID]
  FROM [IndexTest20201113].[dbo].[Future_BLData] where id between 1 and 1000 group by blfileId having count([Volume20GP]) > 400
```



### EXISTS

EXISTS 运算符用于判断查询子句是否有记录，如果有一条或多条记录存在返回 True，否则返回 False。

### UCASE() LCASE() 

大小写

### Mid（）

sql server  使用的是 SUBSTRING（）

```
SELECT MID(column_name,start[,length]) FROM table_name;
```

|    参数     |                            描述                             |
| :---------: | :---------------------------------------------------------: |
| column_name |                  必需。要提取字符的字段。                   |
|    start    |             必需。规定开始位置（起始值是 1）。              |
|   length    | 可选。要返回的字符数。如果省略，则 MID() 函数返回剩余文本。 |

### len

### ROUND

ROUND() 函数用于把数值字段舍入为指定的小数位数。

```
SELECT ROUND(column_name,decimals) FROM table_name;
```

### NOW()

NOW() 函数返回当前系统的日期和时间。

## ### FORMAT() 函数

FORMAT() 函数用于对字段的显示进行格式化。



# 其他

## 指定时间与延时

### 指定时间 

```
 WAITFOR TIME '22:20';  指定在 '00:00:00.000' 执行
```

### 延时

```
WAITFOR DELAY '02:00';  '00:00:00.000' 指定时分秒毫秒后执行
```

### 查询隔离级别

```sql server
DBCC USEROPTIONS
```













 