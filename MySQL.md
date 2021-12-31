1、查看数据库

`show databases;`

2、创建数据库

`creat database name;`

3、使用数据库

`use name;`

4、删除数据库

`drop database name;`

数据类型

1、数值类型

int

2、浮点类型

double

decimal

varchar

test

表的操作

1、创建表

`create table [表名] ();`

2、查看表结构

`desc [表名];`

3、删除表

`drop table [表名];`

4、查看表

`show tables;`

CRUD

1、插入数据

全插入

`insert into [表名] values();`

对于的字段的数目和类型要与表结构一致

插入其中几列

`insert into [表名] (id,name) values(); `

一次多插入

`insert into [表名]  values(),(),(); `

2、查看数据

全列查找

`select *from [表名];`

指定列查找

`select* [列名] from [表名];`

查询字段为表达式



