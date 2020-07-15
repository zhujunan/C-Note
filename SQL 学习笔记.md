
#[MySQL基本概念](#MySQL基本概念)

#[MySQL常用指令](#MySQL常用指令)

#[MySQL条件语句](#MySQL条件语句)

#[MySQL数据处理](#MySQL数据处理)

#[其它](#其它)

==============================================

#MySQL基本概念

	###自定义变量
一、用户变量

声明并初始化：

	SET @变量名=值;
	SET @变量名:=值;
	SELECT @变量名:=值;
赋值：

	方式一：一般用于赋简单的值
	SET 变量名=值;
	SET 变量名:=值;
	SELECT 变量名:=值;


	方式二：一般用于赋表 中的字段值
	SELECT 字段名或表达式 INTO 变量
	FROM 表;

使用：

	select @变量名;

二、局部变量

声明：

	declare 变量名 类型 【default 值】;
赋值：

	方式一：一般用于赋简单的值
	SET 变量名=值;
	SET 变量名:=值;
	SELECT 变量名:=值;


	方式二：一般用于赋表 中的字段值
	SELECT 字段名或表达式 INTO 变量
	FROM 表;

使用：

	select 变量名



二者的区别：

			作用域			定义位置		语法
用户变量	当前会话		会话的任何地方		加@符号，不用指定类型
局部变量	定义它的BEGIN END中 	BEGIN END的第一句话	一般不用加@,需要指定类型


	``着重号，区分同名命令和名称

	###常见约束

	NOT NULL
	DEFAULT
	UNIQUE
	CHECK
	PRIMARY KEY
	FOREIGN KEY


7、起别名
①as
②空格



#MySQL常用指令

	1、字符函数
		concat拼接
		substr截取子串
		upper转换成大写
		lower转换成小写
		trim去前后指定的空格和字符
		ltrim去左边空格
		rtrim去右边空格
		replace替换
		lpad左填充
		rpad右填充
		instr返回子串第一次出现的索引
		length 获取字节个数
		
	2、数学函数
		round 四舍五入
		rand 随机数
		floor向下取整
		ceil向上取整
		mod取余
		truncate截断

	3、日期函数
		now当前系统日期+时间
		curdate当前系统日期
		curtime当前系统时间
		str_to_date 将字符转换成日期
		date_format将日期转换成字符
		
	5、其他函数
		version版本
		database当前库
		user当前连接用户

	6.查看表结构
		desc(cribe) 表名;

	AVG();SUM() 必须数值型
	MIN();MAX() 任意数据类型
	
	COUNT
	COUNT(*) 返回记录总数
	COUNT(expr) 返回expr不为空总数

	表名.列名

	AS 别名


#MySQL条件语句

	where 
		条件 （>;&&;like；in（））;
	order by 
		排序的字段|表达式|函数|别名 【asc|desc】
	group by 
		分组字段		having 【分组后的筛选条件】
	like
		% 任意个字符	_一个字符

	分组前筛选：	原始表		group by的前面		where
	分组后筛选：	分组后的结果集	group by的后面		having

###分页

	limit 【起始的条目索引，】条目数;

特点：

	1.起始条目索引从0开始
	
	2.limit子句放在查询语句的最后
	
	3.公式：select * from  表 limit （page-1）*sizePerPage,sizePerPage
	假如:
	每页显示条目数sizePerPage
	要显示的页数 page


limit 【offset，】size;
注意：
offset代表的是起始的条目索引，默认从0卡死
size代表的是显示的条目数

公式：
假如要显示的页数为page，每一页条目数为size
select 查询列表
from 表
limit (page-1)*size,size;



###join
	等值连接、非等值连接 （内连接）
	外连接
	交叉连接
	
	内连接 [inner] join on

	外连接
	左外连接 left  [outer] join on
	右外连接 right [outer] join on


A： UNION 运算符
UNION 运算符通过组合其他两个结果表（例如 TABLE1 和 TABLE2）并消去表中任何重复行而派生出一个结果表。当 ALL 随 UNION 一起使用时（即 UNION ALL），不消除重复行。两种情况下，派生表的每一行不是来自 TABLE1 就是来自 TABLE2。

三、意义
1、将一条比较复杂的查询语句拆分成多条语句
2、适用于查询多个表的时候，查询的列基本是一致

四、特点
1、要求多条查询语句的查询列数必须一致
2、要求多条查询语句的查询的各列类型、顺序最好一致
3、union 去重，union all包含重复项
B： EXCEPT 运算符
EXCEPT 运算符通过包括所有在 TABLE1 中但不在 TABLE2 中的行并消除所有重复行而派生出一个结果表。当 ALL 随 EXCEPT 一起使用时 (EXCEPT ALL)，不消除重复行。
C： INTERSECT 运算符
INTERSECT 运算符通过只包括 TABLE1 和 TABLE2 中都有的行并消除所有重复行而派生出一个结果表。当 ALL 随 INTERSECT 一起使用时 (INTERSECT ALL)，不消除重复行。

子查询
外面的语句可以是insert、update、delete、select等，一般select作为外面语句较多


#MySQL数据处理

##DQL语言

	select 
		要查询的字段|表达式|常量值|函数
	from 
		表




当查询中涉及到了多个表的字段，需要使用多表连接
select 字段1，字段2
from 表1，表2,...;

笛卡尔乘积：当查询多个表时，没有添加有效的连接条件，导致多个表所有行实现完全连接
###联合查询


引入：
	union 联合、合并

语法：

	select 字段|常量|表达式|函数 【from 表】 【where 条件】 union 【all】
	select 字段|常量|表达式|函数 【from 表】 【where 条件】 union 【all】
	select 字段|常量|表达式|函数 【from 表】 【where 条件】 union  【all】
	.....
	select 字段|常量|表达式|函数 【from 表】 【where 条件】

特点：

	1、多条查询语句的查询的列数必须是一致的
	2、多条查询语句的查询的列的类型几乎相同
	3、union代表去重，union all代表不去重


##DML语言

###插入

语法：
	insert into 表名(字段名，...)
	values(值1，...);

insert into 表名 set 字段=值,字段=值,...;

特点：

	1、字段类型和值类型一致或兼容，而且一一对应
	2、可以为空的字段，可以不用插入值，或用null填充
	3、不可以为空的字段，必须插入值
	4、字段个数和值的个数必须一致
	5、字段可以省略，但默认所有字段，并且顺序和表中的存储顺序一致

###修改

修改单表语法：

	update 表名 set 字段=新值,字段=新值
	【where 条件】
修改多表语法：

	update 表1 别名1,表2 别名2
	set 字段=新值，字段=新值
	where 连接条件
	and 筛选条件

###删除

方式1：delete语句 

单表的删除： ★
	delete from 表名 【where 筛选条件】【limit 条目数】

多表的删除：
	delete 别名1，别名2
	from 表1 别名1，表2 别名2
	where 连接条件
	and 筛选条件;


delete 别名1,别名2 from 表1 别名 
inner|left|right join 表2 别名 
on 连接条件
 【where 筛选条件】



方式2：truncate语句

	truncate table 表名


两种方式的区别【面试题】
	
	#1.truncate不能加where条件，而delete可以加where条件
	
	#2.truncate的效率高一丢丢
	
	#3.truncate 删除带自增长的列的表后，如果再插入数据，数据从1开始
	#delete 删除带自增长列的表后，如果再插入数据，数据从上一次的断点处开始
	
	#4.truncate删除不能回滚，delete删除可以回滚


1.truncate删除后，如果再插入，标识列从1开始
  delete删除后，如果再插入，标识列从断点开始
2.delete可以添加筛选条件
 truncate不可以添加筛选条件
3.truncate效率较高
4.truncate没有返回值
delete可以返回受影响的行数
5.truncate不可以回滚
delete可以回滚




##DDL语句

###库和表的管理

库的管理：

	一、创建库
	create database 库名
	二、删除库
	drop database 库名
	1.查看当前所有的数据库<br>
	show databases;
	2.打开指定的库
	use 库名
	3.查看当前库的所有表
	show tables;
	4.查看其它库的所有表
	show tables from 库名;

表的管理：

 
	6、说明：增加一个列
	Alter table tabname add column col type


8、说明：创建索引：create [unique] index idxname on tabname(col….)
删除索引：drop index idxname
注：索引是不可更改的，想更改必须删除重新建。
9、说明：创建视图：create view viewname as select statement
删除视图：drop view viewname


	#1.创建表

create table 【if not exists】 表名(
	字段名 字段类型 【约束】,
	字段名 字段类型 【约束】,
	。。。
	字段名 字段类型 【约束】 

)

	CREATE TABLE IF NOT EXISTS stuinfo(
		stuId INT,
		stuName VARCHAR(20),
		gender CHAR,
		bornDate DATETIME
		
	
	);

	DESC studentinfo;

	#2.修改表 alter
	语法：ALTER TABLE 表名 ADD|MODIFY|DROP|CHANGE COLUMN 字段名 【字段类型】;
	
	#①修改字段名
	ALTER TABLE studentinfo CHANGE  COLUMN sex gender CHAR;
	
	#②修改表名
	ALTER TABLE stuinfo RENAME [TO]  studentinfo;
	#③修改字段类型和列级约束
	ALTER TABLE studentinfo MODIFY COLUMN borndate DATE ;
	
	#④添加字段
	
	ALTER TABLE studentinfo ADD COLUMN email VARCHAR(20) first;
	#⑤删除字段
	ALTER TABLE studentinfo DROP COLUMN email;
	
	
	#3.删除表
	
	DROP TABLE [IF EXISTS] studentinfo;

	7、说明：添加主键： Alter table tabname add primary key(col)
	说明：删除主键： Alter table tabname drop primary key(col)

二、修改表

1.添加列
alter table 表名 add column 列名 类型 【first|after 字段名】;
2.修改列的类型或约束
alter table 表名 modify column 列名 新类型 【新约束】;
3.修改列名
alter table 表名 change column 旧列名 新列名 类型;
4 .删除列
alter table 表名 drop column 列名;
5.修改表名
alter table 表名 rename 【to】 新表名;

三、删除表
drop table【if exists】 表名;

四、复制表
1、复制表的结构
create table 表名 like 旧表;
2、复制表的结构+数据
create table 表名 
select 查询列表 from 旧表【where 筛选】;


一、常见的约束
NOT NULL：非空，该字段的值必填
UNIQUE：唯一，该字段的值不可重复
DEFAULT：默认，该字段的值不用手动插入有默认值
CHECK：检查，mysql不支持
PRIMARY KEY：主键，该字段的值不可重复并且非空  unique+not null
FOREIGN KEY：外键，该字段的值引用了另外的表的字段

外键：
1、用于限制两个表的关系，从表的字段值引用了主表的某字段值
2、外键列和主表的被引用列要求类型一致，意义一样，名称无要求
3、主表的被引用列要求是一个key（一般就是主键）
4、插入数据，先插入主表
删除数据，先删除从表
可以通过以下两种方式来删除主表的记录
#方式一：级联删除
ALTER TABLE stuinfo ADD CONSTRAINT fk_stu_major FOREIGN KEY(majorid) REFERENCES major(id) ON DELETE CASCADE;

#方式二：级联置空
ALTER TABLE stuinfo ADD CONSTRAINT fk_stu_major FOREIGN KEY(majorid) REFERENCES major(id) ON DELETE SET NULL;

二、创建表时添加约束
create table 表名(
	字段名 字段类型 not null,#非空
	字段名 字段类型 primary key,#主键
	字段名 字段类型 unique,#唯一
	字段名 字段类型 default 值,#默认
	constraint 约束名 foreign key(字段名) references 主表（被引用列）

)
注意：
			支持类型		可以起约束名			
列级约束		除了外键		不可以
表级约束		除了非空和默认	可以，但对主键无效

列级约束可以在一个字段上追加多个，中间用空格隔开，没有顺序要求

三、修改表时添加或删除约束
1、非空
添加非空
alter table 表名 modify column 字段名 字段类型 not null;
删除非空
alter table 表名 modify column 字段名 字段类型 ;

2、默认
添加默认
alter table 表名 modify column 字段名 字段类型 default 值;
删除默认
alter table 表名 modify column 字段名 字段类型 ;
3、主键
添加主键
alter table 表名 add【 constraint 约束名】 primary key(字段名);
删除主键
alter table 表名 drop primary key;

4、唯一
添加唯一
alter table 表名 add【 constraint 约束名】 unique(字段名);
删除唯一
alter table 表名 drop index 索引名;
5、外键
添加外键
alter table 表名 add【 constraint 约束名】 foreign key(字段名) references 主表（被引用列）;
删除外键
alter table 表名 drop foreign key 约束名;


四、自增长列
特点：
1、不用手动插入值，可以自动提供序列值，默认从1开始，步长为1
auto_increment_increment
如果要更改起始值：手动插入值
如果要更改步长：更改系统变量
set auto_increment_increment=值;
2、一个表至多有一个自增长列
3、自增长列只能支持数值型
4、自增长列必须为一个key

一、创建表时设置自增长列
create table 表(
	字段名 字段类型 约束 auto_increment
)
二、修改表时设置自增长列
alter table 表 modify column 字段名 字段类型 约束 auto_increment
三、删除自增长列
alter table 表 modify column 字段名 字段类型 约束 






#数据库事务(TCL语言)




一、含义
事务：一条或多条sql语句组成一个执行单位，一组sql语句要么都执行要么都不执行
二、特点（ACID）
A 原子性：一个事务是不可再分割的整体，要么都执行要么都不执行
C 一致性：一个事务可以使数据从一个一致状态切换到另外一个一致的状态
I 隔离性：一个事务不受其他事务的干扰，多个事务互相隔离的
D 持久性：一个事务一旦提交了，则永久的持久化到本地

三、事务的使用步骤 ★
了解：
隐式（自动）事务：没有明显的开启和结束，本身就是一条事务可以自动提交，比如insert、update、delete
显式事务：具有明显的开启和结束

使用显式事务：
①开启事务
set autocommit=0;
start transaction;#可以省略

②编写一组逻辑sql语句
注意：sql语句支持的是insert、update、delete

设置回滚点：
savepoint 回滚点名;

③结束事务
提交：commit;
回滚：rollback;
回滚到指定的地方：rollback to 回滚点名;
四、并发事务
1、事务的并发问题是如何发生的？
多个事务 同时 操作 同一个数据库的相同数据时
2、并发问题都有哪些？
脏读：一个事务读取了其他事务还没有提交的数据，读到的是其他事务“更新”的数据
不可重复读：一个事务多次读取，结果不一样
幻读：一个事务读取了其他事务还没有提交的数据，只是读到的是 其他事务“插入”的数据
3、如何解决并发问题
通过设置隔离级别来解决并发问题
4、隔离级别
				  	        脏读	  	      不可重复读  		幻读
read uncommitted:读未提交     ×                ×              ×        
read committed：读已提交      √                ×              ×
repeatable read：可重复读     √                √              ×
serializable：串行化          √                √              √



###含义
	通过一组逻辑操作单元（一组DML——sql语句），将数据从一种状态切换到另外一种状态

###特点
	（ACID）
	原子性：要么都执行，要么都回滚
	一致性：保证数据的状态操作前和操作后保持一致
	隔离性：多个事务同时操作相同数据库的同一个数据时，一个事务的执行不受另外一个事务的干扰
	持久性：一个事务一旦提交，则数据将持久化到本地，除非其他事务对其进行修改

相关步骤：

	1、开启事务
	2、编写事务的一组逻辑操作单元（多条sql语句）
	3、提交事务或回滚事务

###事务的分类：

隐式事务，没有明显的开启和结束事务的标志

	比如
	insert、update、delete语句本身就是一个事务


显式事务，具有明显的开启和结束事务的标志

		1、开启事务
		取消自动提交事务的功能
		
		2、编写事务的一组逻辑操作单元（多条sql语句）
		insert
		update
		delete
		
		3、提交事务或回滚事务
###使用到的关键字

	set autocommit=0;
	start transaction;
	commit;
	rollback;
	
	savepoint  断点
	commit to 断点
	rollback to 断点


###事务的隔离级别:

事务并发问题如何发生？

	当多个事务同时操作同一个数据库的相同数据时
事务的并发问题有哪些？

	脏读：一个事务读取到了另外一个事务未提交的数据
	不可重复读：同一个事务中，多次读取到的数据不一致
	幻读：一个事务读取数据时，另外一个事务进行更新，导致第一个事务读取到了没有更新的数据
	
如何避免事务的并发问题？

	通过设置事务的隔离级别
	1、READ UNCOMMITTED
	2、READ COMMITTED 可以避免脏读
	3、REPEATABLE READ 可以避免脏读、不可重复读和一部分幻读
	4、SERIALIZABLE可以避免脏读、不可重复读和幻读
	
设置隔离级别：

	set session|global  transaction isolation level 隔离级别名;
查看隔离级别：

	select @@tx_isolation;
	

#其它
##视图
含义：理解成一张虚拟的表

视图和表的区别：
	
		使用方式	占用物理空间
	
	视图	完全相同	不占用，仅仅保存的是sql逻辑
	
	表	完全相同	占用

视图的好处：


	1、sql语句提高重用性，效率高
	2、和表实现了分离，提高了安全性

###视图的创建

create view 视图名
as
查询语句;

	语法：
	CREATE VIEW  视图名
	AS
	查询语句;
###视图的增删改查
	1、查看视图的数据 ★
	
	SELECT * FROM my_v4;
	SELECT * FROM my_v1 WHERE last_name='Partners';
	
	2、插入视图的数据
	INSERT INTO my_v4(last_name,department_id) VALUES('虚竹',90);
	
	3、修改视图的数据
	
	UPDATE my_v4 SET last_name ='梦姑' WHERE last_name='虚竹';
	
	
	4、删除视图的数据
	DELETE FROM my_v4;

三、修改
方式一：
create or replace view 视图名
as
查询语句;
方式二：
alter view 视图名
as
查询语句

四、删除
drop view 视图1，视图2,...;
五、查看
desc 视图名;
show create view 视图名;
六、使用
1.插入
insert
2.修改
update
3.删除
delete
4.查看
select
注意：视图一般用于查询的，而不是更新的，所以具备以下特点的视图都不允许更新
①包含分组函数、group by、distinct、having、union、
②join
③常量视图
④where后的子查询用到了from中的表
⑤用到了不可更新的视图


###某些视图不能更新
	包含以下关键字的sql语句：分组函数、distinct、group  by、having、union或者union all
	常量视图
	Select中包含子查询
	join
	from一个不能更新的视图
	where子句的子查询引用了from子句中的表
###视图逻辑的更新
	#方式一：
	CREATE OR REPLACE VIEW test_v7
	AS
	SELECT last_name FROM employees
	WHERE employee_id>100;
	
	#方式二:
	ALTER VIEW test_v7
	AS
	SELECT employee_id FROM employees;
	
	SELECT * FROM test_v7;
###视图的删除
	DROP VIEW test_v1,test_v2,test_v3;
###视图结构的查看	
	DESC test_v7;
	SHOW CREATE VIEW test_v7;



#存储过程

含义：一组经过预先编译的sql语句的集合
好处：

	1、提高了sql语句的重用性，减少了开发程序员的压力
	2、提高了效率
	3、减少了传输次数

分类：

	1、无返回无参
	2、仅仅带in类型，无返回有参
	3、仅仅带out类型，有返回无参
	4、既带in又带out，有返回有参
	5、带inout，有返回有参
	注意：in、out、inout都可以在一个存储过程中带多个
###创建存储过程
语法：

	create procedure 存储过程名(in|out|inout 参数名  参数类型,...)
	begin
		存储过程体

	end

类似于方法：

	修饰符 返回类型 方法名(参数类型 参数名,...){

		方法体;
	}

注意

	1、需要设置新的结束标记
	delimiter 新的结束标记
	示例：
	delimiter $

	CREATE PROCEDURE 存储过程名(IN|OUT|INOUT 参数名  参数类型,...)
	BEGIN
		sql语句1;
		sql语句2;

	END $

	2、存储过程体中可以有多条sql语句，如果仅仅一条sql语句，则可以省略begin end

	3、参数前面的符号的意思
	in:该参数只能作为输入 （该参数不能做返回值）
	out：该参数只能作为输出（该参数只能做返回值）
	inout：既能做输入又能做输出


#调用存储过程
	call 存储过程名(实参列表)


一、创建 ★
create procedure 存储过程名(参数模式 参数名 参数类型)
begin
		存储过程体
end
注意：
1.参数模式：in、out、inout，其中in可以省略
2.存储过程体的每一条sql语句都需要用分号结尾

二、调用
call 存储过程名(实参列表)
举例：
调用in模式的参数：call sp1（‘值’）;
调用out模式的参数：set @name; call sp1(@name);select @name;
调用inout模式的参数：set @name=值; call sp1(@name); select @name;
三、查看
show create procedure 存储过程名;
四、删除
drop procedure 存储过程名;



#变量
一、全局变量

作用域：针对于所有会话（连接）有效，但不能跨重启

	查看所有全局变量
	SHOW GLOBAL VARIABLES;
	查看满足条件的部分系统变量
	SHOW GLOBAL VARIABLES LIKE '%char%';
	查看指定的系统变量的值
	SELECT @@global.autocommit;
	为某个系统变量赋值
	SET @@global.autocommit=0;
	SET GLOBAL autocommit=0;

二、会话变量

作用域：针对于当前会话（连接）有效

	查看所有会话变量
	SHOW SESSION VARIABLES;
	查看满足条件的部分会话变量
	SHOW SESSION VARIABLES LIKE '%char%';
	查看指定的会话变量的值
	SELECT @@autocommit;
	SELECT @@session.tx_isolation;
	为某个会话变量赋值
	SET @@session.tx_isolation='read-uncommitted';
	SET SESSION tx_isolation='read-committed';


二、自定义变量
说明：
1、用户变量
作用域：针对于当前连接（会话）生效
位置：begin end里面，也可以放在外面
使用：

①声明并赋值：
set @变量名=值;或
set @变量名:=值;或
select @变量名:=值;

②更新值
方式一：
	set @变量名=值;或
	set @变量名:=值;或
	select @变量名:=值;
方式二：
	select xx into @变量名 from 表;

③使用
select @变量名;



2、局部变量
作用域：仅仅在定义它的begin end中有效
位置：只能放在begin end中，而且只能放在第一句
使用：
①声明
declare 变量名 类型 【default 值】;
②赋值或更新
方式一：
	set 变量名=值;或
	set 变量名:=值;或
	select @变量名:=值;
方式二：
	select xx into 变量名 from 表;
③使用
select 变量名;



#函数

###创建函数

一、创建
create function 函数名(参数名 参数类型) returns  返回类型
begin
	函数体
end

注意：函数体中肯定需要有return语句
二、调用
select 函数名(实参列表);
三、查看
show create function 函数名;
四、删除
drop function 函数名；



学过的函数：LENGTH、SUBSTR、CONCAT等
语法：

	CREATE FUNCTION 函数名(参数名 参数类型,...) RETURNS 返回类型
	BEGIN
		函数体
	
	END

###调用函数
	SELECT 函数名（实参列表）


###函数和存储过程的区别

			关键字		调用语法	返回值			应用场景
	函数		FUNCTION	SELECT 函数()	只能是一个		一般用于查询结果为一个值并返回时，当有返回值而且仅仅一个
	存储过程	PROCEDURE	CALL 存储过程()	可以有0个或多个		一般用于更新



#流程控制结构

###分支结构
特点：
1、if函数
功能：实现简单双分支
语法：
if(条件，值1，值2)
位置：
可以作为表达式放在任何位置
2、case结构
功能：实现多分支
语法1：
case 表达式或字段
when 值1 then 语句1;
when 值2 then 语句2；
..
else 语句n;
end [case];

语法2：
case 
when 条件1 then 语句1;
when 条件2 then 语句2；
..
else 语句n;
end [case];


位置：
可以放在任何位置，
如果放在begin end 外面，作为表达式结合着其他语句使用
如果放在begin end 里面，一般作为独立的语句使用
3、if结构
功能：实现多分支
语法：
if 条件1 then 语句1;
elseif 条件2 then 语句2;
...
else 语句n;
end if;
位置：
只能放在begin end中


###循环结构
位置：
只能放在begin end中

特点：都能实现循环结构

对比：

①这三种循环都可以省略名称，但如果循环中添加了循环控制语句（leave或iterate）则必须添加名称
②
loop 一般用于实现简单的死循环
while 先判断后执行
repeat 先执行后判断，无条件至少执行一次


1、while
语法：
【名称:】while 循环条件 do
		循环体
end while 【名称】;
2、loop
语法：
【名称：】loop
		循环体
end loop 【名称】;

3、repeat
语法：
【名称:】repeat
		循环体
until 结束条件 
end repeat 【名称】;

二、循环控制语句
leave：类似于break，用于跳出所在的循环
iterate：类似于continue，用于结束本次循环，继续下一次

###分支
一、if函数
	语法：if(条件，值1，值2)
	特点：可以用在任何位置

二、case语句

语法：

	情况一：类似于switch
	case 表达式
	when 值1 then 结果1或语句1(如果是语句，需要加分号) 
	when 值2 then 结果2或语句2(如果是语句，需要加分号)
	...
	else 结果n或语句n(如果是语句，需要加分号)
	end 【case】（如果是放在begin end中需要加上case，如果放在select后面不需要）

	情况二：类似于多重if
	case 
	when 条件1 then 结果1或语句1(如果是语句，需要加分号) 
	when 条件2 then 结果2或语句2(如果是语句，需要加分号)
	...
	else 结果n或语句n(如果是语句，需要加分号)
	end 【case】（如果是放在begin end中需要加上case，如果放在select后面不需要）


特点：
	可以用在任何位置

三、if elseif语句

语法：

	if 情况1 then 语句1;
	elseif 情况2 then 语句2;
	...
	else 语句n;
	end if;

特点：
	只能用在begin end中！！！！！！！！！！！！！！！


三者比较：
			应用场合
	if函数		简单双分支
	case结构	等值判断 的多分支
	if结构		区间判断 的多分支


###循环

语法：


	【标签：】WHILE 循环条件  DO
		循环体
	END WHILE 【标签】;
	
特点：

	只能放在BEGIN END里面

	如果要搭配leave跳转语句，需要使用标签，否则可以不用标签

	leave类似于java中的break语句，跳出所在循环！！！
	



