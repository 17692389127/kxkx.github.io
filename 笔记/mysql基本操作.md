# mysql

## 一、基本操作

### 1.mysql中有四个系统数据库

information_schema、mysql、performance_schema、sys

### 2.连接mysql服务器

mysql -uroot -p

### 2.database()

数据库的名字

### 3.version（）

数据库版本号

## 一、information_schema数据库

用来记录mysql系统中所有的数据库名、表名、字段名等信息

### 1.查询数据库中的某一个数据表

(例：information_schema数据库中的schemata数据表)

select*from information_schema.schemata;

### 2.information_schema中的表

schemata：记录数据库中所有数据库的信息的表
tables：记录了数据库中所有表信息的表
columns：记录了数据库说的的列信息的表

### 3.information_schema中的列

information_shcema中的表：tables、columns
tables表中的字段：table_schema、table_name
columns表中的字段：column_name、table_name

## 二、数据库查询语言（DQL）

带有select的都是查询语句

### 1.select单独使用

mysql> select @@basedir;	#mysql安装目录
mysql> select @@port;		#mysql端口号
mysql> select @@innodb_flush_log_at_trx_commit;		#日志刷新策略
mysql> show variables like 'innodb%';	#模糊查看innodb开头的配置
mysql> select database();	#查看当前库名
mysql> select now();		#查看当前系统时间
mysql> select @@server_id;	#查看本实例id号，群集中不能重复

### 2.select通用语法

select {字段列表} from <表1>,<表2> [where 表达式] [group by] [having] [order by] [limit <>]

字段	作用
select	显示的列名（多列逗号分开）
from	表名（多个表逗号分开）
where	过滤条件的列
group by	分组的列
having	分组后的过滤聚合函数
order by	排序的列（desc降序 默认：asc升序）
limit	显示前几行 LIMIT M,N:跳过M行,显示一共N行 LIMIT Y OFFSET X: 跳过X行,显示一共Y行
like %_	模糊查询 %：任意字符 _：一个字符
union	多个结果集合并查询的功能
union all	多个结果集合并查询的功能，去重

通用符

| 选项          | 作用           |
| ------------- | -------------- |
| and           | 并且           |
| or            | 或者           |
| in            | 与or相同       |
| between …and… | 在什么范围之内 |
| is not        | 查询空值       |
| distinct      | 查询结果不重复 |

## 三.数据库定义语言（DDL）

### 1.DDL数据库操作

#### 1.1库操作

##### 1.1.1查询所有数据库 

show database；

##### 1.1.2创建数据库

create database [if not exists] 数据库名 [default charset 字符集] [collate 排序规则]

##### 1.1.3删除

drop database [is exists] 数据库名;

##### 1.1.4使用

use 数据库名;

#### 1.2表操作

##### 1.2.1查询当前数据库所有表

show table;

##### 1.2.2查询表结构

desc 表名；

##### 1.2.3查询指定表的建表语句

`show create table 表名(`
	`字段1 类型 [comment 注释],`
    `字段2 类型 [comment 注释],`
    `字段3 类型 [comment 注释]`
`)[comment 表注释];`

##### 1.2.4删除表

drop table 表名；

##### 1.2.5删除指定表，并重新创建表

truncate table 表名；

#### 1.3表管理

##### 1.3.1添加字段

alter table 表名 add 字段名 类型 [comment 注释] [约束];

##### 1.3.2修改数据类型

alter table 表名 modify 字段名 新类型;

##### 1.3.3修改字段名和字段类型

alter table 表名 change 旧字段 新字段 类型 [comment 注释] [约束];

##### 1.3.4删除字段

alter table 表名 drop 字段名;

##### 1.3.5修改表名

alter table 表名 rename to 新表名;

### 2、管理数据库

#### 2.1查看mysql创建格式

mysql> help create database;

#### 2.2查看系统支持的字符集

mysql> show charset;

#### 2.3创建数据库

mysql> create database if not exists test default character set=gb18030 collate=gb18030_bin;

创建一个字符集为gb18030排序规则gb18030_bin，名为test，如果存在将跳过创建，不出现报错信息，如果不存在进行创建

#### 2.4修改数据库字符集

mysql> alter database test default character set='utf8' ;

mysql> show create database test;

#### 2.5修改表存储引擎

mysql>show create table test;

mysql> alter table test engine=MyISAM;

#### 2.6删除数据库

表内删除库：mysql> drop database test;

表外删除库：mysql> mysqladmin -u root -p drop test

### 3、管理表

#### 3.1创建表

mysql> create table if not exists txt(id int,name varchar(10) not null,age int not null,primary key(id))engine=innodb default charset=utf8;

#### 3.2查看表的结构和类型

mysql> desc txt;

mysql> show create table txt;

#### 3.3插入数据

mysql> insert into txt (id,name,age) values(1,'zhangsan',12);

#### 3.4对表的字符集进行修改

mysql> alter table txt convert to character set gb18030;

#### 3.5对表重命名

mysql> alter table a2 rename a3;

#### 3.6删除表

mysql> drop table txt;

### 4.对表内数据进行更改

#### 4.1查看表内字符集

mysql> show full columns from txt;

#### 4.2对表内字段进行修改字符集

格式：alter table 表名 modify 字段 属性 character set 字符集 collate 校验集;

#### 4.3对字段属性进行更改

mysql> alter table txt modify age int;

#### 4.4创建字段的属性

##### 4.4.1字段属性

| 数据类型： | 类型                                  |
| ---------- | ------------------------------------- |
| int：      | 整型                                  |
| float      | 浮点型（单精度）                      |
| double     | 浮点型（双精度）                      |
| date       | 日期值（YYYY-MM-DD）                  |
| time       | 时间值（HH:MM:SS）                    |
| datetime   | 混合日期和时间（YYYY-MM-DD hh:mm:ss） |
| char       | 定义长字符串                          |
| varchar    | 变长字符字符串                        |

##### 4.4.2其他选项

选项	解释
null	数据可以包含为空的内容
not null	数据列不能为空
default	默认值
[constraint <约束名>] primary key	主键（唯一，不能为空）
primary key (字段1,字段2)	多字段联合主键
foreign key(字段) references 表(字段)	外键
auto_increment	自动递增，适用于整形
unsigned	无符号
character set 字符集	指定字符集
comment	注释

#### 4.5修改字段内容

mysql> update txt set name='zhaoliu' where name='zhangsan';

#### 4.6删除字段内容

mysql> delete from txt where name='zhaoliu';

## 四、数据库操作语言（DML）

对表中的数据进行增删改

### 1.增

#### 1.1给指定字段添加数据

insert into 表名 (字段名1,字段名2) values (值1，值2);

#### 1.2给全部字段添加数据

insert into 表名 values(值1,值2);

#### 1.3批量添加数据

insert into 表名 (字段名1,字段名2) values (值1,值2),(值1,值2),(值1,值2); 

insert into 表名 values (值1,值2),(值1,值2),(值1,值2); 

### 2.删

delete from 表名 [where 条件]

delete语句的条件可以有，也可以没有，如果没有条件，则会删除整张表的所有数据。

delete语句不能删除某一个字段的值（可以使用update）

### 3.改

update 表名 set 字段=值1,字段2=值2 [where 条件];

### 五、函数

#### 1.条件判断函数

(1) IF() IF(expr, v1, v2) 如果表达式 expr 为 TRUE ，则返回值为 v1 ，否则返回 v2

(2) IFNULL() IFNULL(v1, v2) ，如果 v1 不为 NULL ，则返回值为 v1 ；如果 v1 为 NULL ，则返回值为 v2

(3) CASE 语法：CASE expr WHEN v1 THEN r1 [WHEN v2 THEN r2] [ELSE rn] END 含义：如果 expr 等于某个 vn ，则返回对应位置 THEN 后面的结果，如果与所有值都不相等，则返回 ELSE 后面的 rn

#### 2.substr()

从字符串中提取子串

#### 3.系统信息函数

(1) 获取 MySQL 版本号的函数：VERSION() VERSION() 用于获取 MySQL 版本号

(2) 查看当前用户的连接数的ID函数：CONNECTION_ID() CONNECTION_ID() 用于查看当前用户的连接数
1. Id ：用户登录 MySQL 时，系统分配的连接 id 
2. User ：当前连接的用户 
3. Host ：显示这个语句是从哪个 IP 的哪个端口上发出的，可以用来追踪出现问题语句的用户 
3. db ：显示这个进程目前连接的是哪个数据库 
4. Command ：显示当前连接执行的命令，一般取值为休眠(Sleep)、查询(Query)、连接(Connect) 
5. Time ：显示这个状态持续的时间，单位是秒 
6. State ：显示使用当前连接的 SQL 语句的状态 
7. info ：显示这个 SQL 语句

(3) 查看当前使用的数据库的函数：DATABASE() 、SCHEMA() DATABASE() 用于查看当前使用的数据库
SCHEMA() 用于查看当前使用的数据库

(4) 查看当前登录的用户名的函数：USER() 、CURRENT_USER() 、SYSTEM_USER() USER() 返回当前登录的用户
及主机名
CURRENT_USER() 用于返回当前登录的用户及主机名
SYSTEM_USER() 用于返回当前登录的用户及主机名

(5) 查看指定字符串的字符集的函数：CHARSET(str) CHARSET(str) 用于查看字符串 str 的字符集
(6) 查看指定字符串的排列方式的函数：COLLATION(str) COLLATION(str) 用于查看字符串 str 的字符排列方式
(7) 获取最后一个自动生成的 ID 值得函数：LAST_INSERT_ID() LAST_INSERT_ID() 用于获取最后一个自动生成的
ID 值

#### 4.group_concat（）

将某一字段的所有数据生成在一行

group_concat([distinct] 字段名 [order by 排序字段 asc/desc] [separator '分隔符'])





