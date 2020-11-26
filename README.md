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



## 连接 join

### inner join

INNER JOIN 与 JOIN 是相同的。

### left join

LEFT JOIN 关键字从左表（table1）返回所有的行，即使右表（table2）中没有匹配。如果右表中没有匹配，则结果为 NULL。

### RIGHT JOIN

RIGHT JOIN 关键字从右表（table2）返回所有的行，即使左表（table1）中没有匹配。如果左表中没有匹配，则结果为 NULL。

### FULL OUTER JOIN

FULL OUTER JOIN 关键字只要左表（table1）和右表（table2）其中一个表中存在匹配，则返回行.

FULL OUTER JOIN 关键字结合了 LEFT JOIN 和 RIGHT JOIN 的结果。

## UNION 

UNION 操作符用于合并两个或多个 SELECT 语句的结果集。

请注意，UNION 内部的每个 SELECT 语句必须拥有**相同数量**的列。列也必须拥有相似的数据类型。

同时，每个 SELECT 语句中的列的**顺序**必须相同...。

## SELECT INTO

SELECT INTO 语句从一个表复制数据，然后把数据插入到另一个新表中。

*MySQL 数据库不支持 SELECT ... INTO 语句，但支持 insert into.... select ...*  见 下一小结

## INSERT INTO SELECT

INSERT INTO SELECT 语句从一个表复制数据，然后把数据插入到一个已存在的表中。目标表中任何已存在的行都不会受影响。

## CREATE DATABASE

```
CREATE DATABASE dbname;
```

## CREATE TABLE

CREATE TABLE 语句用于创建数据库中的表。

```
CREATE TABLE table_name
(
column_name1 data_type(size),
column_name2 data_type(size),
column_name3 data_type(size),
....
);
```



## 约束

SQL 约束用于规定表中的数据规则。

如果存在违反约束的数据行为，行为会被约束终止。

约束可以在创建表时规定（通过 CREATE TABLE 语句），或者在表创建之后规定（通过 ALTER TABLE 语句）。



 SQL CREATE TABLE + CONSTRAINT 语法

```
CREATE TABLE table_name
(
column_name1 data_type(size) constraint_name,
column_name2 data_type(size) constraint_name,
column_name3 data_type(size) constraint_name,
....
);
```



有如下约束：

* **NOT NULL** - 指示某列不能存储 NULL 值。

* **UNIQUE** - 保证某列的每行必须有唯一的值。

  ```sqlserver
  CREATE TABLE Persons
  (
  P_Id int NOT NULL UNIQUE,
  LastName varchar(255) NOT NULL,
  FirstName varchar(255),
  Address varchar(255),
  City varchar(255)
  )
  ```

  alter 方式

  ```sqlserver
  ALTER TABLE Persons ADD UNIQUE (uc_PersonID)
  ```

  删除

  ```sql server
  ALTER TABLE Persons DROP CONSTRAINT uc_PersonID
  ```

  

* **PRIMARY KEY** - NOT NULL 和 UNIQUE 的结合。确保某列（或两个列多个列的结合）有唯一标识，有助于更容易更快速地找到表中的一个特定的记录。

  PRIMARY KEY 约束唯一标识数据库表中的每条记录。

  主键必须包含唯一的值。

  主键列不能包含 NULL 值。

  每个表都应该有一个主键，并且每个表只能有一个主键。

  ```sqlserver
  CREATE TABLE Persons
  (
  P_Id int NOT NULL PRIMARY KEY,
  LastName varchar(255) NOT NULL,
  FirstName varchar(255),
  Address varchar(255),
  City varchar(255)
  )
  ```

  alter

  ```
  ALTER TABLE Persons ADD CONSTRAINT pk_PersonID PRIMARY KEY (P_Id,LastName)
  ```

  drop

  ```
  ALTER TABLE Persons DROP CONSTRAINT pk_PersonID
  ```

  

* **FOREIGN KEY** - 保证一个表中的数据匹配另一个表中的值的参照完整性。

  一个表中的 FOREIGN KEY 指向另一个表中的 UNIQUE KEY(唯一约束的键)。

  ```
  CREATE TABLE Orders
  (
  O_Id int NOT NULL PRIMARY KEY,
  OrderNo int NOT NULL,
  P_Id int FOREIGN KEY REFERENCES Persons(P_Id)
  )
  ```

  如需命名 FOREIGN KEY 约束，并定义多个列的 FOREIGN KEY 约束，请使用下面的 SQL 语法：

  alter

  ```
  ALTER TABLE Orders ADD CONSTRAINT fk_PerOrders FOREIGN KEY (P_Id) REFERENCES Persons(P_Id)
  ```

  drop

  ```
  ALTER TABLE Orders DROP CONSTRAINT fk_PerOrders
  ```

  

* **CHECK** - 保证列中的值符合指定的条件。

  ```
  CREATE TABLE Persons
  (
  P_Id int NOT NULL CHECK (P_Id>0),
  LastName varchar(255) NOT NULL,
  FirstName varchar(255),
  Address varchar(255),
  City varchar(255)
  )
  ```

  如需命名 CHECK 约束，并定义多个列的 CHECK 约束，请使用下面的 SQL 语法：

  ```
  CREATE TABLE Persons
  (
  P_Id int NOT NULL,
  LastName varchar(255) NOT NULL,
  FirstName varchar(255),
  Address varchar(255),
  City varchar(255),
  CONSTRAINT chk_Person CHECK (P_Id>0 AND City='Sandnes')
  )
  ```

  alter

  ```
  ALTER TABLE Persons
  ADD CONSTRAINT chk_Person CHECK (P_Id>0 AND City='Sandnes')
  ```

  drop

  ```
  ALTER TABLE Persons
  DROP CONSTRAINT chk_Person
  ```

  

* **DEFAULT** - 规定没有给列赋值时的默认值。

```
CREATE TABLE Persons
(
    P_Id int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255) DEFAULT 'Sandnes'
)
```

alter

```
ALTER TABLE Persons
ADD CONSTRAINT ab_c DEFAULT 'SANDNES' for City
```

drop

```
ALTER TABLE Persons
ALTER COLUMN City DROP DEFAULT
```

## 索引

您可以在表中创建索引，以便更加快速高效地查询数据。

用户无法看到索引，它们只能被用来加速搜索/查询。

**注释：**更新一个包含索引的表需要比更新一个没有索引的表花费更多的时间，这是由于索引本身也需要更新。因此，理想的做法是仅仅在常常被搜索的列（以及表）上面创建索引。

* ### SQL CREATE INDEX 语法

  在表上创建一个简单的索引。允许使用重复的值：

  ```
  CREATE INDEX index_name
  ON table_name (column_name
  )
  ```

* ### SQL CREATE UNIQUE INDEX 语法

  在表上创建一个唯一的索引。不允许使用重复的值：唯一的索引意味着两个行不能拥有相同的索引值

  ```
  CREATE UNIQUE INDEX index_name
  ON table_name (column_name
  )
  ```

## 视图

视图是可视化的表。

视图包含行和列，就像一个真实的表。视图中的字段就是来自一个或多个数据库中的真实的表中的字段。

您可以向视图添加 SQL 函数、WHERE 以及 JOIN 语句，也可以呈现数据，就像这些数据来自于某个单一的表一样。

Create 语法

```
CREATE VIEW view_name AS
SELECT column_name(s)
FROM table_name
WHERE condition
```

**注释：**视图总是显示最新的数据！每当用户查询视图时，数据库引擎通过使用视图的 SQL 语句重建数据。

更新

```
待了解
```



 SQL 撤销视图

```
DROP VIEW view_name
```







## 函数

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

### FORMAT() 函数

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













 