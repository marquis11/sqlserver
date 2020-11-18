# sqlserver
sqlserver 学习笔记

# SQL语法

## select 

```

select   ...

select ... distinct ...

select ... where ...

select ... where  ... and (... or...)

select ... where ... order by colume

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













 