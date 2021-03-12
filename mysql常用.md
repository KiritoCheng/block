Mysql最常用的命令
1、显示数据库列表：
show databases;

2、显示库中的数据表：
show tables;

3、显示数据表的结构：
describe 表名;

4、建库：
create database 库名;

5、建表：
create table 表名 (字段设定列表);

6、删库和删表:
drop database 库名;
drop table 表名;

7、将表中记录清空：
delete from 表名;(内容清空，自增id不会被清掉，自增id会保留)
mysql> truncate table users;
数据库返回：“Query OK, 0 rows affected (0.04 sec)”
（成功返回0）（自增id也一同会被清掉）

8、显示表中的记录：
select * from 表名
库的基本操作
让我们一起开始学习吧

1.创建数据库：
mysql> create database ceshi;

2.连接数据库
mysql> use ceshi;

3.查看当前使用的数据库
mysql> select database();

4.当前数据库包含的表信息
mysql> show tables; 

5.删除数据库
mysql> drop database ceshi;
表的基本操作
一、建表

1.命令:create table <表名> (<字段名 1> <类型 1> [,..<字段名 n> <类型 n>]);

1.1例子：
mysql> create table Class(
id int(4) not null(不能为空) primary key（主键） auto_increment（自增长）, 
name varchar(25) not null, 
age int (4) not null default'0');    （default'0' 设置默认值为0）

二、获取表结构
2命令: desc 表名，或者show columns from 表名

2.1例子：
mysql> desc Class;
mysql> describe Class;
mysql> show columns from Class;

三、插入数据
3.命令:insert into <表名> [( <字段名 1>[,..<字段名 n > ])] values ( 值 1 )[, ( 值 n )]

3.1例子：
mysql> insert into Class values(1,'Wrry',26),(2,'ZJW',28);

四、查询表中的数据

4.查询所有行

mysql> select * from Class;

4.1查询前几行数据

4.1.1例如:查看表 Class 中前 3 行数据
mysql> select * from Class limit 0,3;

4.1.2或者
mysql> select * from Class order by id limit 0,3;    （order by id  ：以id排序）

五、删除表中数据

5.1命令:
delete from 表名 where 表达式

5.2例如:删除表 Class 中编号为 6 的记录
mysql> delete from MyClass where id=1;

六、修改表中数据

6.命令:
update 表名 set 字段=新值,... where 条件
6.1例如:
mysql> update Class set name='AI' where id=1;

七、在表中增加字段

7命令:alter table 表名 add 字段 类型 其他;

7.1例如:在表 Class 中添加了一个字段 sex,类型为 varchar(25),默认值为 0
mysql> alter table Class add sex varchar(25) default '0'

八、更改表名

8.命令:rename table 原表名 to 新表名;

8.1例如:在表 Class 名字更改为 MClass
mysql> rename table Class to MClass;

九、删除表

9.命令:drop table <表名>

9.1例如:删除表名为 MClass 的表

mysql> drop table MClass;
