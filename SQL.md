# 1.SQL复习

## 1.创建和管理数据库

### 1.1创建和管理数据库

```sql
//创建和管理数据库
create database (IF NOT EXISTS) 数据库名;
//查看数据库
show database;
//选择数据库
use database;
//删除数据库
drop database 数据库名

```



## 2.数据表管理

### 创建数据表

````sql
create table 数据表tt(
  id int not null primary key,
  name char(8) not null,
  sex char(2) not null
)
````



### 修改数据表

```sql
alter table 数据表名(
  ///添加列
    add colunmn datatype
  ///修改列信息  
    |modify (column datatype)
  ///删除列
    |drop column column_name
  ///重命名列
    |rename column old_column to new_column
)

//例子
alter table tt add (列名 列数据类型 default '' not null);
alter table tt add sex char(1) not null;

//修改属性名
alter table tt change 原列名 修改后列名 数据类型
alter table tt change name to new_name char(8)

//修改列属性
alter table tt modify(列名 li);
alter table tt modify name varchar(20) not null;

alter table tt drop [column] (列名1,列名2...) [cascade constrains]; 删除约束

//部分删除
alter table tt set unused (列名) cascade constrains; //仅仅是逻辑删除，还需要进一步释放空间
alter table tt drop unused colunmns;

alter table 表1 rename to 表2;  //修改数据表名字

//删除所有记录 保留表结构 
delete from 表名 ;
truncate table 表名;

//删除表
drop table 表名 [cascade constrains] 


//查看表结构 
desc 表名;
show colunmns from 数据库名.表名

//复制数据表
create [temporary]table [if not exists]新建的数据表名字  like  要复制的数据库表名;
create table table1 as (statement 查询)
```



### 表约束

#### 主键约束(primary key)

1.一张表只能有一个主键，是一个字段或者字段组

设置主键常见的两种方式:

a.表级完整性约束

b.列级完整性约束

```sql
create table tt(
id int primary key;
)

create table tt(
id int not null,
name char(20) not null,
phone char(11) not null,
 primary key(id,name)  ////联合主键
)
```

####  外键约束(foreign key)

外键的有两种方式，

a.在表级完整性下定义外键约束

b.在列级完整性下定义外键约束

```sql
//将sc表的sno字段设置为外键，该字段的值参照(reference )学生student表的sno字段的取值. 
alter table sc add foreign key(sno) references student(sno)

//列级完整性约束
create table tt(
  id int not null,
  sno char(10) not null,
  cno char(10) not null,
  primary key (sno,cno),
  foreign key(sno) references student(sno)
)
```



####  非空约束(not null)

```sql
alter table tt modify name cahr(25) not null;
```



####  唯一性约束(unique)

```sql
create table tt (
id int  not null unique)
```



####  默认值约束(default)

```sql
create table tt(
 id int not null default 12)
```



####  自增约束(auto_increment) 

```
create table tt(
id int not null auto_increment)
```



#### 检查约束(check)

```sql
create  table  student
(    学号 	char(6) not null,
     性别 	   char(1) not null
         check(性别 in ('男', '女'))
);
```



#### 删除约束

```sql
alter table sc drop 约束 约束名
```



## 3.表记录操作



#### 插入

```sql
insert into 表名 [（字段列表）]  values (值列表)
//第一种写法
insert into user(id,name,sex) value(1,"zzr","nan");
//第二种写法
insert into user set name="zzr" ,sex="nan" ,age=14;

//批量插入
insert into 表名 values (值列表1)，（值列表2）....

//在insert语句中使用select子句可以将源表的查询结果添加到目标表中，语法格式如下。
insert into 目标表(字段列表1) select (字段列表2) from 源表 where 条件表达式


使用replace插入同理
replace into 表名(字段列表) values (值列表);
replace [into] 表名 set 字段1=值1,字段2=值2;
replace [into] 目标表名[(字段列表)] select (字段列表2) from 源表 where 条件表达式

replace 与insert的区别：
使用replace语句向表插入新记录时，如果新纪录的主键值或者唯一性约束的字段值与已有记录相同，则已有记录先被删除（注意：已有记录删除时也不能违背外键约束条件），然后再插入新记录。
```



更新

````sql
update 表名 set 字段1=值1，字段n=值n where 条件表达式
update user set name="zln" where id=2;

更新多个表
update 表1，表2 set 表1.字段=值，表2.字段=值 where 表1.主键=表2.主键 where 条件表达式
````



#### 删除

```sql
delete from 表名 where 条件表达式
delete from user where name="zzr"; ///删除name=zzr的所有记录
truncate table 表名 //删除表的所有记录 注:删除表中的所有数据，且不能恢复 .

truncate  与 delete 的区别:
清空记录的表如果是父表，那么truncate命令将永远执行失败。如果使用truncate table成功清空表记录，那么会重新设置自增型字段的计数器。truncate table语句不支持事务的回滚，并且不会触发触发器程序的运行。
```



## 4.数据库查询

```sql
select 字段列表 from 表名
where 条件表达式  
group by 分组字段 having 条件表达式 
order by 排序字段 [desc|asc]

1、列别名
select old_name as new_name;

2、消除重复行
select distinct 字段 from 表名

3、空值查询
select 字段 from 表名 where 字段 is [not] null;

4.模式匹配
(1)like匹配
LIKE匹配可以使用特殊符号“_”和“%”进行模糊查询，
其中“_”代表任意一个字符，“%”代表0个或者多个字符。

select * from 表名 where 字段 like "条件"；

当要匹配的内容包含特殊字符时，可以使用escape定义转义字符

查询电话以“_”开头的考生姓名、电话。
select name,phone from student  where phone like'$_%' escape '$';

(2)regexp匹配
正则表达式:
^字符串开头
$字符串结尾
.任何单个字符
[...]在方括号中的任意字符列表
[^...]非列在方括号内的任意字符列表
p1|p2|p3 交替匹配任何模式p1,p2或p3；
*零个或多个前面的元素
+前面元素的一个或者多个实例
{n}前面元素的n个实例
{m,n}m到n个实例前面的元素

查询姓赵的同学的准考证号、姓名
select zkzh,name      from student where name regexp '^赵';

(3)范围比较
范围比较主要使用between和in关键字,其中in关键字还可以在子查询中使用。
select * from user where score between 70 and 90;

select  * from user where id in (1,3,5);

```



#### 子查询

当一个查询是另一个查询的条件是，称之为子查询。

子查询语法:

expression [NOT] IN (sqlstatement)
       comparison [ANY | ALL | SOME] (sqlstatement)
       [NOT] EXISTS (sqlstatement)



```sql
例子:
查找参加了计算机网络考试的学生准考证号、姓名
select zkzh,name  from student where zkzh in (select zkzh from examinfo where course='计算机网络');

查找比姓王的学生年龄都小的学生姓名，出生日期
select name,birth from student where birth>all(select birth from student where name like'王%');

查找参加了软件测试考试的学生姓名。
select name from student where exists (select * from examinfo where zkzh=student.zkzh and course='软件测试');

```



#### group by子句

GROUP BY 语句用于结合合计函数，根据一个或多个列对结果集进行分组。

语法：group by 字段列表       [ having条件表达式 ] [ with rollup ]

with rollup  对结果进行了汇总。汇总时，根据GROUP BY后的列名，先汇总靠后的列，再汇总靠前的列，最后汇总所有的列

#### having子句

HAVING子句和WHERE类似，都是对查询结果的筛选。不过where子句的作用是在对查询结果进行分组前，将不符合where条件的行去掉，即在<u>分组之前过滤数据</u>。HAVING子句的作用是筛选满足条件的组，即<u>在GROUP BY分组之后过滤数据</u>，条件中经常包含聚合函数。



```sql
查询各门课程参加考试的考生人数。
select course,count(*) as '考生人数' from examinfo  group by course;

查询各专业的男生人数、女生人数和专业总人数，以及学生总人数。
select major,sex,count(*) as '考生人数' from student group by major,sex  with rollup;

查询超过3人考试的课程和考生人数。
select course,count(*) as '考生人数' from examinfo group by course  having count(*)>3;

```

#### 

#### order by子句

ORDER BY 语句用于根据指定的列对结果集进行排序，默认按照升序（ASC）对记录进行排序。如果您希望按照降序对记录进行排序，可以使用DESC关键字。

注:可在ORDER BY 中使用子查询。对空值进行排序时，空值为最小值。

```sql
查询计算机专业的全部学生姓名、性别、出生日期，并按照出生日期排序。
select name,sex,birth from student where major='计算机'  order by birth;

查询所有考生的专业，姓名、性别，并按照各专业人数排序。
select major,name,sex from student order by  (select count(*) as '考生人数'
from student  group by major);

```



#### limit子句

LIMIT 子句可以被用于强制 SELECT 语句返回指定的记录数。LIMIT 接受一个或两个数字参数。参数必须是一个整数常量。
	如果给定两个参数，第一个参数指定第一个返回记录行的偏移量，第二个参数指定返回记录行的最大数目。

注:LIMIT统计起始位时，0作为第一位，

```sql
查找准考证号排在最3-7位的学生准考证号、姓名、出生日期。
select zkzh,name,sex   from student order by zkzh  limit 2,5;
```



#### 全连接

多表查询的数据来源于多个表格，查询复杂度高，代码难度大。我们可以通过全连接或者JOIN连接来进行多表查询。

注：可以在全连接里附加更具体的限制条件以缩小查询范围，快速查找特定目标。

```sql
查询在校本部的全部考场的考场号、考试时间和考试科目。
select exam.testid,testtime,course from exam,examinfo where exam.testid=examinfo.testid and exam.school='校本部';

```



#### join连接

**mysql不支持Full join**

SQL标准中的连接类型主要分为inner连接（内连接）和outer连接（外连接），而外连接又分为left（左外连接，简称为左连接）、right（右外连接，简称为右连接）以及full（完全外连接，简称完全连接）。

语法：

from 表名1  [ 连接类型 ]  join  表名2  on  表1和表2之间的连接条件



**INNER JOIN**（内连接,或等值连接）：取得两个表中存在连接匹配关系的记录。

**LEFT JOIN**：左外连接指的是将JOIN关键字左边表的全部内容查询出来，并将JOIN关键字右边表中符合查询条件的内容也查询出来，形成新的查询结果表。如果右边表中没有符合条件的匹配信息，则设置为NULL。

**RIGHT JOIN**：右外连接和左外连接刚好相反，指的是将JOIN关键字右边表的全部内容查询出来，并将JOIN关键字左边表中符合查询条件的内容也查询出来，形成新的查询结果表。如果左边表中没有符合条件的匹配信息，则设置为NULL。

```sql
1.如果没有特殊声明，则默认内连接，可以省略语法里看到的INNER关键字。
select exam.testid,testtime,course from exam join examinfo on exam.testid=examinfo.testid where exam.school='校本部';

2.Left join 取得左表完全记录，取右表满足条件的记录
select user.id,user.name,user.sex,tt.phone from user left join tt on user.id=tt.id ;

```

![1557734361331](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1557734361331.png)

```sql
3.Right join取得右表完全记录，取左表满足条件的记录
select user.name,tt.phone,user.sex from user right join tt on user.id=tt.id;
```



![1557734603878](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1557734603878.png)

```sql
如果要连接的表中列名相同，可以使用USING子句。
select user.id,user.name,tt.phone,user.sex from user join tt using(id);
```

![1557734717456](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1557734717456.png)

## 5.视图

视图是从一个或多个表（或视图）导出的表。
       视图是数据库的用户使用数据库的观点。
       视图中的数据并不像表、索引那样需要占用存储空间。
       视图中保存的仅仅是一条SELECT语句，其源数据都来自于数据库表，数据库表称为基本表或基表，视图称为虚表。
      基表的数据发生变化时，虚表的数据也会随之变化。

视图的特点：1.使操作变得简单   2.避免数据冗余     3.增强数据安全性	  4.提高数据的逻辑独立性



#### 创建视图

创建视图需要有CREATE VIEW的权限，并且对于查询涉及的列有SELECT权限。



语法:create view 视图名 [ (视图字段列表) ] as    select语句

完整语法：

CREATE [OR REPLACE] [ALGORITHM = {UNDEFINED | MERGE | TEMPTABLE}]
          VIEW view_name [(column_list)]
          AS select_statement
         [WITH [CASCADED | LOCAL] CHECK OPTION]



**注意**

使用视图查询时，若其关联的基本表中添加了新字段，则该视图将不包含新字段。

如果与视图相关联的表或视图被删除，则该视图将不能再使用。

```sql
create view userInfo as select user.id,user.name,age,phone from user join tt using(id);;

select * from userInfo;
```



#### 查看视图

查看视图是查看数据库中已存在的视图的定义，查看视图必须要有SHOW VIEW的权限。查看视图的方法包括：

DESCRIBE
SHOW TABLE STATUS
SHOW CREATE VIEW

#### 更新视图

更新视图是指通过视图来插入、更新、删除表中的数据，因为视图是一个虚拟表，其中没有数据。通过视图更新的时候都是转到基本表上进行更新的，如果对视图增加或删除记录，实际上是对其基本表增加或删除记录。

三种方法：  INSERT、UPDATE和DELETE。



```s
将 xsks_st1视图中所有学生的成绩增加5分。
UPDATE  xsks_st1 SET score =score + 5;
若一个视图依赖于多个基本表，则一次修改该视图只能变动一个基本表的数据。

删除视图xsks_st2中女同学的记录。
DELETE FROM  xsks_st2  WHERE sex=0;
对依赖于多个基本表的视图，不能使用DELETE语句。

```



#### 修改视图

修改视图的语句和创建视图的语句是完全一样的。当视图已经存在时，修改语句对视图进行修改;当视图不存在时，创建视图。

语法：

ALTER [ALGORITHM = {UNDEFINED | MERGE | TEMPTABLE}]   	   VIEW view_name [(column_list)]
   	AS select_statement
   	[WITH [CASCADED | LOCAL] CHECK OPTION]



```sql
将视图xsks_st2修改为只包含计算机专业学生的准考证号、姓名和成绩。
ALTER VIEW xsks_st2  AS	SELECT zkzh,name,score FROM student WHERE major='计算机';
```



#### 删除视图

view_name是视图名，声明了IF EXISTS，若视图不存在的话，也不会出现错误信息。也可以声明RESTRICT和CASCADE，但它们没什么影响。

语法:

DROP VIEW [IF EXISTS]
	view_name [, view_name] ...
	[RESTRICT | CASCADE]



```sql
使用DROP VIEW一次可删除多个视图。
DROP VIEW xsks_st1, xsks_st2;
```



## 6.索引

本质上，索引其实是数据库表中字段值的复制，该字段称为索引的关键字。

对于数据库表而言，一个数据库表可以创建多个索引。



**索引的种类：**
	1.主索引、聚簇索引             2.唯一性索引
	3.普通索引                            4.复合索引 
	5.全文索引（fulltext）



索引关键字的选取原则:

原则1：表的某个字段值离散度越高，该字段越适合选作索引的关键字。
        原则2：占用储存空间少的字段更适合选作索引的关键字。

原则3：较频繁地作为where查询条件的字段应该创建索引，分组字段或者排序字段应该创建索引，两个表的连接字段应该创建索引。
       原则4：更新频繁的字段不适合创建索引，不会出现在where子句中的字段不应该创建索引。
       原则5．最左前缀原则
       原则6．尽量使用前缀索引



#### 索引与约束

约束主要用于保证业务逻辑操作数据库时数据的完整性；约束是逻辑层面的概念。

索引则是将关键字数据以某种数据结构的方式存储到外存，用于提升数据的检索性能；索引既有逻辑上的概念，更是一种物理存储方式，且事实存在、需要耗费一定的储存空间。



#### 创建索引

方法1:创建表的同时创建索引

create table 表名(字段名1 数据类型 [约束条件],
…
[其他约束条件],
…
**[ unique | fulltext ]  index  [索引名] ( 字段名 [(长度)]  [ asc | desc ] )**
) engine=存储引擎类型 default charset=字符集类型



```sql
创建学生学籍表（表名为：xsxj），xsxj表带有学号和身份证号的联合主键，并在成绩列上创建索引。
CREATE TABLE xsxj(
	学号   CHAR(8) NOT NULL,
	身份证号 CHAR(18) NOT NULL,
	成绩   TINYINT(1),
	学分    TINYINT(1),
	PRIMARY KEY(学号,身份证号),
	INDEX  CJ(成绩)    );

```



方法2:在已有表上创建索引

a.语法格式1:

create [ unique | fulltext ] index 索引名 on 表名 ( 字段名 [(长度)]  [ asc | desc ] )

b.语法格式2:

alter table 表名 add [ unique | fulltext ] index 索引名 ( 字段名 [(长度)]  [ asc | desc ] )



```sql
假设student表已经创建，要求在成绩列上创建索引
 create index cj on student(成绩  asc );
 Alter table student add index cj (成绩  desc);

```



#### 删除索引



如果从表中删除了列，则索引可能会受到影响。如果所删除的列为索引的组成部分，则该列也会从索引中删除。如果组成索引的所有列都被删除，则整个索引将被删除。



```sql
drop index 索引名 on 表名

DROP INDEX子句可以删除各种类型的索引。使用DROP PRIMARY KEY子句时不需要提供索引名称，因为一个表中只有一个主键。
删除student表上的主键和mark索引。
ALTER TABLE student DROP PRIMARY KEY,DROP INDEX mark;


```





## 7.存储过程与存储函数



#### 存储过程

存储过程（Stored Procedure）是一组为了完成特定功能的SQL语句集，经编译后存储在数据库中，用户通过指定存储过程的名字并给定参数（如果该存储过程带有参数）来调用执行它。

优点:

存储过程增强了SQL语言的功能和灵活性。
	    存储过程允许标准组件是编程。
	    存储过程能实现较快的执行速度。
        存储过程能过减少网络流量。
    	存储过程可被作为一种安全机制来充分利用。



语法:

##### 创建存储过程

create procedure 存储过程名（参数1，参数2，…）
       [存储过程选项]
       begin
       存储过程语句块;
       end;



```sql
创建一个存储过程，实现根据考生准号证号查询考生详细信息的功能。
drop  procedure if exists sele;
delimiter $$
create procedure sele(in zk char(20))
begin
select * from student where zkzh=zk;
end $$
delimiter;

调用方法：
call sele(120101101);

注释:因为存储过程sele需要一个输入参数，所以在调用时给了参数值为120101101，也就是查询准号证号为120101101的学生基本信息。

创建一个存储过程，计算a+b+c的值。
delimiter $$
create procedure bian(out num int(4))
begin
declare a int default 1;
declare b,c  int;
set b=2,c=3;
set num=a+b+c;
end $$

调用方法：
call bian(@d);
select @d;

```



##### 修改存储过程

ALTER {PROCEDURE | FUNCTION} sp_name [characteristic ...]
characteristic:
    { CONTAINS SQL | NO SQL | READS SQL DATA | MODIFIES SQL DATA }
  | SQL SECURITY { DEFINER | INVOKER }
  | COMMENT 'string'

```sql
将读写权限改为MODIFIES SQL DATA。
alter  procedure bian modifies sql data ; 
```



##### 删除存储过程

DROP {PROCEDURE | FUNCTION} [IF EXISTS] sp_name

```sql
drop  procedure if exists bian;
```



#### 存储函数

##### 创建存储函数

CREATE FUNCTION sp_name ([func_parameter[,...]])
    RETURNS type //存储函数返回值的数据类型
    [characteristic ...] routine_body //存储函数的过程体



存储函数使用SELECT语句调用，调用语法格式为：
SELECT sp_name ([func_parameter[,...]])



```sql
创建一个存储函数，返回一个学生的姓名
delimiter $$
create function fanname(zk char(12))
returns char(8)
begin      
declare newname char(12);
select name into newname from student where zkzh=zk;
RETURN newname;
end$$
delimiter;

调用方法：
select fanname(120101101);


调用前面的存储函数，根据输入的学号判断是否是赵宁宁，如果是则删除此学生信息，不是则返回flase
delimiter $$
create function delname(zk char(12))
returns boolean
begin
        declare stuname char(8);
	set stuname=fanname(zk);
        if stuname='赵宁宁' then
               delete from student where name=stuname;
              return true;
        else
             return false;
        end if;
end$$
delimiter;
```



##### 存储函数的删除和修改

修改存储函数语法为：
 ALTER FUNCTION sp_name [characteristic ...]

删除存储函数语法为：
DROP  FUNCTION [IF EXISTS] sp_name





##### 函数和存储过程的比较:

共同点:

1.应用程序调用存储过程或者函数时，只需要提供存储过程名或者函数名，以及参数信息，无需将若干条MySQL命令或SQL语句发送到MySQL服务器，节省了网络开销。
      2.存储过程或者函数可以重复使用，可以减少数据库开发人员，尤其是应用程序开发人员的工作量。 
      3.使用存储过程或者函数可以增强数据的安全访问控制。可以设定只有某些数据库用户才具有某些存储过程或者函数的执行权



不同点:

1.函数必须有且仅有一个返回值，且必须指定返回值数据类型（返回值类型目前仅仅支持字符串、数值类型）。

2.存储过程可以没有返回值，也可以有返回值，甚至可以有多个返回值，所有的返回值需要使用out或者inout参数定义。 
      3.函数体内可以使用select…into语句为某个变量赋值，但不能使用select语句返回结果（或者结果集）。存储过程则没有这方面的限制，存储过程甚至可以返回多个结果集。