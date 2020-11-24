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



## 函数

### group by

select  column(group by 的) ，(其余字段要是聚合函数) from table  where 条件  group by  column





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













 