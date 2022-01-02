# 数据库基础

## 数据库操作

1、查看数据库

`show databases;`

![Snipaste_2022-01-01_11-02-47](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011152533.png)

2、创建数据库

```sql
CREATE DATABASE [IF NOT EXISTS] db_name [create_specification [,
create_specification] ...]

create_specification:
	[DEFAULT] CHARACTER SET charset_name
	[DEFAULT] COLLATE collation_name
```

![Snipaste_2022-01-01_11-09-27](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011152534.png)

3、使用数据库

```sql
use name;
```

![Snipaste_2022-01-01_11-11-06](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011152536.png)

4、删除数据库

```sql
DROP DATABASE [IF EXISTS] db_name;
```

![Snipaste_2022-01-01_11-06-21](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011152537.png)

## 数据类型

1、数值类型

| 数据类型     | 大小               | 说明                                             | 对应java数据类型                                |
| ------------ | ------------------ | ------------------------------------------------ | ----------------------------------------------- |
| bit[(M)]     | M指定位数，默认为1 | 二进制数，M范围从1到64，存储数值范围从0到2^M-1   | 常用Boolean对应BIT，此时默认是1位，即只能存0和1 |
| tinyint      | 1字节              |                                                  | Byte                                            |
| smallint     | 2字节              |                                                  | Short                                           |
| int          | 4字节              |                                                  | Integer                                         |
| bigint       | 8字节              |                                                  | Long                                            |
| float(M,D)   | 4字节              | 单精度，M指定长度，D指定小数位数。会发生精度丢失 | Float                                           |
| double(M,D)  | 8字节              |                                                  | Double                                          |
| decimal(M,D) | M/D最大值+2        | 双精度，M指定长度，D表示小数点位数。             | BigDecimal                                      |
| numeric(M,D) | M/D最大值+2        | 精确数值和DECIMAL一杨                            | BigDecimal                                      |

| 数据类型      | 大小             | 说明                   | 对应java类型 |
| ------------- | ---------------- | ---------------------- | ------------ |
| varchar(size) | 0-655535字节     | 可变字符串             | String       |
| text          | 0-655535字节     | 长文本数据             | String       |
| mediumtext    | 0-16 777 215字节 | 中等长度文本数据       | String       |
| blob          | 0-65,535字节     | 二进制形式的长文本数据 | byte[]       |

3、时间类型

| 数据类型  | 大小  | 说明                                             | 对应java类型                            |
| --------- | ----- | ------------------------------------------------ | --------------------------------------- |
| datetime  | 8字节 | 范围从1000到9999年，不会进行时区的检索及转换。   | java.util.Date、<br/>java.sql.Timestamp |
| timestamp | 4字节 | 范围从1970到2038年，自动检索当前时区并进行转换。 | java.util.Date、<br/>java.sql.Timestamp |

## 表的操作

1、创建表

```sql
CREATE TABLE table_name (
	field1 datatype,
	field2 datatype,
	field3 datatype
);
```

![Snipaste_2022-01-01_11-33-52](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011152538.png)

可以使用comment增加字段说明。

```sql
create table stu_test (
	id int,
	name varchar(20) comment '姓名',
	password varchar(50) comment '密码',
	age int,
	sex varchar(1),
	birthday timestamp,
	amout decimal(13,2),
	resume text
);
```

![Snipaste_2022-01-01_11-36-51](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011152539.png)

2、查看表结构

`desc [表名];`

![Snipaste_2022-01-01_11-37-53](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011152540.png)

3、查看表

`show tables;`

![](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011152541.png)

4、删除表

`drop table [表名];`

![Snipaste_2022-01-01_11-41-54](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011152542.png)

# CRUD

## Create

使用上文的students表

1、单行数据全列插入

`insert into [表名] values();`

对于的字段的数目和类型要与表结构一致

插入其中几列

`insert into [表名] (id,chinese) values(); `

一次多插入

`insert into [表名]  values(),(),(); `

![Snipaste_2022-01-01_11-49-57](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011152543.png)

## R

全列查找

`select *from [表名];`

![Snipaste_2022-01-01_11-51-43](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011152544.png)

指定列查找

`select* [列名] from [表名];`

![Snipaste_2022-01-01_11-54-52](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011231309.png)

查询字段为表达式

`select [列名0], [列名1] +[列名2]+[列名3] from [表名];`

![Snipaste_2022-01-01_12-15-09](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011231310.png)

`select [列名0], [列名1] +10 from [表名];`

![Snipaste_2022-01-01_12-16-26](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011231311.png)

`select [列名0], [列名1] +[列名2]+[列名3] as total from [表名];`

![Snipaste_2022-01-01_12-17-17](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011231312.png)

去重查询

`select distinct [列名] from [表名];`

![Snipaste_2022-01-01_12-21-05](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011231313.png)

`select distinct [列名1],[列名2] from [表名];`

![Snipaste_2022-01-01_12-22-31](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011231314.png)

排序

`select*from [表名] order by [列名] asc;`

desc为降序排列

![Snipaste_2022-01-01_12-25-18](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011231315.png)

`select [列名0], [列名1]+[列名2] from [表名]  order by [列名1]+[列名2] desc;`

![Snipaste_2022-01-01_12-28-49](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011231316.png)

`select [列名0], [列名1]+[列名2] as newName  from [表名]  order by newName desc;`

![Snipaste_2022-01-01_12-29-51](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011231317.png)

`select *from [表名] order by [列名1] desc,[列名2] desc;`

![Snipaste_2022-01-01_12-31-21](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011231318.png)

条件查询

| 运算符            | 说明                                                         |
| ----------------- | ------------------------------------------------------------ |
| >,>=,<,<=         |                                                              |
| =                 | 等于，NULL 不安全，例如 NULL = NULL 的结果是 NULL            |
| <=>               | 等于，NULL 安全，例如 NULL <=> NULL 的结果是 TRUE(1)         |
| !=, <>            |                                                              |
| BETWEEN a0 AND a1 | [a0,a1]                                                      |
| IN (option, ...)  | 如果是 option 中的任意一个，返回 TRUE(1)                     |
| IS NULL           | 不是 NULL                                                    |
| LIKE              | 模糊匹配。% 表示任意多个（包括 0 个）任意字符；_ 表示任意一个字<br/>符 |

![Snipaste_2022-01-01_15-53-50](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011618387.png)

![Snipaste_2022-01-01_15-54-35](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011618388.png)

![Snipaste_2022-01-01_15-55-46](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011618389.png)

![Snipaste_2022-01-01_15-57-17](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011618390.png)

分页查询

![Snipaste_2022-01-01_16-03-33](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011618391.png)

![Snipaste_2022-01-01_16-00-20](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011618392.png)

![Snipaste_2022-01-01_16-02-59](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011618393.png)

## Updata

```sql
```



![Snipaste_2022-01-01_15-41-32](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011618394.png)

## Del

![Snipaste_2022-01-01_16-16-18](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011618396.png)

![Snipaste_2022-01-01_16-16-40](https://gitee.com/wang-fuming/dawning/raw/master/img/202201011618397.png)



# 进阶

## 数据库的约束

1、not null-指示某列不能存储null值

2、unique -保证某列的每行必须有唯一的值

3、defau -规定没有给列赋值时的默认值

4、PRIMARY KEY - NOT NULL 和 UNIQUE 的结合。确保某列（或两个列多个列的结合）有唯一标
识，有助于更容易更快速地找到表中的一个特定的记录。

5、FOREIGN KEY - 保证一个表中的数据匹配另一个表中的值的参照完整性。

6、CHECK - 保证列中的值符合指定的条件。对于MySQL数据库，对CHECK子句进行分析，但是忽略
CHECK子句。

```sql
-- 重新设置学生表结构
-- 对not null的测试
DROP TABLE IF EXISTS student;
CREATE TABLE student (
	id INT NOT NULL,
	sn INT,
	name VARCHAR(20),
	qq_mail VARCHAR(20)
);
```

![Snipaste_2022-01-01_20-44-02](https://gitee.com/wang-fuming/dawning/raw/master/img/202201012143894.png)

```sql
-- 重新设置学生表结构
-- 测试unique
DROP TABLE IF EXISTS student;
CREATE TABLE student (
	id INT NOT NULL,
	sn INT UNIQUE,
	name VARCHAR(20),
	qq_mail VARCHAR(20)
);
```

![Snipaste_2022-01-01_20-46-33](https://gitee.com/wang-fuming/dawning/raw/master/img/202201012143895.png)

```sql
-- 重新设置学生表结构
-- 测试default
DROP TABLE IF EXISTS student;
CREATE TABLE student (
	id INT NOT NULL,
	sn INT UNIQUE,
	name VARCHAR(20) DEFAULT 'unkown',
	qq_mail VARCHAR(20)
);
```

![Snipaste_2022-01-01_20-50-30](https://gitee.com/wang-fuming/dawning/raw/master/img/202201012143897.png)

```sql
-- 重新设置学生表结构
-- 测试主键值
DROP TABLE IF EXISTS student;
CREATE TABLE student (
	id INT NOT NULL PRIMARY KEY,
	sn INT UNIQUE,
	name VARCHAR(20) DEFAULT 'unkown',
	qq_mail VARCHAR(20)
);
```

```sql
-- 主键是 NOT NULL 和 UNIQUE 的结合，可以不用 NOT NULL
id INT PRIMARY KEY auto_increment,
```

```sql
foreign key (字段名) references 主表(列)、
```

![Snipaste_2022-01-01_21-12-13](https://gitee.com/wang-fuming/dawning/raw/master/img/202201012143898.png)

![Snipaste_2022-01-01_21-11-38](https://gitee.com/wang-fuming/dawning/raw/master/img/202201012143899.png)

```sql
drop table if exists test_user;
create table test_user (
	id int,
	name varchar(20),
	sex varchar(1),
	check (sex ='男' or sex='女')
);
```

## 表的设计

一对一

![Snipaste_2022-01-01_21-13-49](https://gitee.com/wang-fuming/dawning/raw/master/img/202201012143900.png)

一对多

![Snipaste_2022-01-01_21-14-15](https://gitee.com/wang-fuming/dawning/raw/master/img/202201012143901.png)

多对多

![Snipaste_2022-01-01_21-14-43](https://gitee.com/wang-fuming/dawning/raw/master/img/202201012143902.png)

## 新增

```sql
INSERT INTO table_name [(column [, column ...])] SELECT ...
```

![Snipaste_2022-01-01_21-42-44](https://gitee.com/wang-fuming/dawning/raw/master/img/202201012143903.png)

## 查询

聚合查询

1、聚合函数

| 函数                   |                    说明                     |
| ---------------------- | :-----------------------------------------: |
| COUNT([DISTINCT] expr) |           返回查询到的数据的 数量           |
| SUM([DISTINCT] expr)   |  返回查询到的数据的 总和，不是数字没有意义  |
| AVG([DISTINCT] expr)   | 返回查询到的数据的 平均值，不是数字没有意义 |
| MAX([DISTINCT] expr)   | 返回查询到的数据的 最大值，不是数字没有意义 |
| MIN([DISTINCT] expr)   | 返回查询到的数据的 最小值，不是数字没有意义 |

count

![Snipaste_2022-01-02_13-46-05](https://gitee.com/wang-fuming/dawning/raw/master/img/202201021517430.png)

sum![Snipaste_2022-01-02_13-47-54](https://gitee.com/wang-fuming/dawning/raw/master/img/202201021517432.png)

avg、max、min就是求平均值、最大值、最小值

![Snipaste_2022-01-02_13-49-43](https://gitee.com/wang-fuming/dawning/raw/master/img/202201021517433.png)

![Snipaste_2022-01-02_13-53-08](https://gitee.com/wang-fuming/dawning/raw/master/img/202201021517434.png)

2、group by

![Snipaste_2022-01-02_13-58-34](https://gitee.com/wang-fuming/dawning/raw/master/img/202201021517435.png)

3、having

![Snipaste_2022-01-02_14-00-34](https://gitee.com/wang-fuming/dawning/raw/master/img/202201021517436.png)

联合操作

```sql
select 字段 from 表1 别名1 [inner] join 表2 别名2 on 连接条件 and 其他条件;
select 字段 from 表1 别名1,表2 别名2 where 连接条件 and 其他条件;
```

1、查询某个人的成绩

![Snipaste_2022-01-02_20-23-36](https://gitee.com/wang-fuming/dawning/raw/master/img/202201022025039.png)

![](https://gitee.com/wang-fuming/dawning/raw/master/img/202201022025041.png)

![Snipaste_2022-01-02_20-24-55](https://gitee.com/wang-fuming/dawning/raw/master/img/202201022025042.png)

2、查找所有同学的总成绩

（1）按照学生id筛选，删除无意义的数据

（2）按照学生id进行group by操作

![Snipaste_2022-01-02_20-18-55](https://gitee.com/wang-fuming/dawning/raw/master/img/202201022025043.png)

![Snipaste_2022-01-02_20-18-25](https://gitee.com/wang-fuming/dawning/raw/master/img/202201022025044.png)

![Snipaste_2022-01-02_20-17-33](https://gitee.com/wang-fuming/dawning/raw/master/img/202201022025045.png)

![Snipaste_2022-01-02_20-33-02](https://gitee.com/wang-fuming/dawning/raw/master/img/202201022033658.png)
