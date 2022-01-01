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

