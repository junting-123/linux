##基础知识
###Mysql服务器启动和关闭
	net stop mysql80;
	net start mysql80;


###MySQL服务登录和退出
	登录：
	mysql -h localhost -P 3306 -u root -p
	mysql [-h主机名 -p端口名] -u用户名 -p密码
	退出：
	exit或quit

###SQL语言
	DBA数据库管理人员
	DBMS数据库管理系统
	DB数据库
	SQL是一种非过程化语言，只需提出“做什么”，而不需要指明“怎么做”；

###SQL语言分为五部分
	1.数据库查询语言(Data Query Language，DQL)
	DQL主要用于数据的查询，其基本结构是使用SELECT子句，from子句和where子句组合来查询一条或多条数据；

	2.数据操作语言（Data Manipulation Language,DML）
	DML主要用于对数据库中的数据进行增加、修改和删除：
	（1）Insert:增加数据
	（2）Update:修改数据
	（3）Delete:删除数据

	3.数据定义语言（Data Definition Language,DDL）
	DDL主要针对数据库对象
	（1）Create:创建数据库对象
	（2）Alter:修改数据库对象
	（3）Drop：删除数据库对象

	4.数据控制语言（Data Control Language,DCL）
	DCL用于授予或回收访问数据库的权限
	（1）Grant：授予用户某种权限
	（2）Revoke:回收授予的某种权限

	5.事务控制语言（Transaction Control Language,TCL）
	TCL用于数据库的事务管理
	（1）Start transaction:开启事务
	（2）Commit:提交事务
	（3）Rollback:回滚事务
	（4）Set transaction:设置事务的属性

###Mysql常见命令
	1.查看当前所有的数据库
	show databases;
	2.打开指定的库
	use 库名
	3.查看当前库的所有表
	show tables；
	4.查看其它库的所有表
	show tables from 库名；
	5.创建表
	show table 表名（
	列名 列类型，
	列名 列类型
	...
	）
	6.查看表结构
	desc 表名；

	7.查看服务器版本
	方式一：登录到mysql服务端
	select version();
	方式二：没有登录mysql服务端
	mysql --version 或 mysql --v

###Mysql语法规范
	1.不区分大小写，建议关键字大写，表名列名小写
	2.每条命令分号结尾
	3.根据需要可缩进换行
	4.注释
		单行注释：# 或 --
		多行注释：/*注释文字*/

##表操作、查询DQL
###学习select语句
	1.取出表里所有内容
	select*from emp(表名)
	2.取出名字、月薪的内容
	select ename,sal from emp

###Where子句
	1.去除薪水大于800
	select*from emp(表名) where sal >= 800
	2.在emo表中查询comm值为空
	select*from emp(表名) where comm is null

###order_by子句（排序）
	select*from dept order by deptno
	select*from dept order by deptno desc(逆序)

###算数运算符
	select empno,ename,sal,sal+1000 as '涨薪后',deptno from emp where sal < 2500;
	select empno,ename,sal,comm,sal+comm from emp;  -- ？？？后面再说

###去重操作
	select job from emp;
	select distinct job from emp;
	select job,deptno from emp;
	select distinct job,deptno from emp;对后面的所有列组合去重 ，而不是单独的某一列去重
	
###group用来分组，hanving分组后筛选
	1.
	select job,avg(sal) from emp group by job having job != 'MANAGER' ;
	2.select语句执行顺序
	from--where -- group  by–  select   -  having-   order  by 
	3.统计各部门的最高工资，排除最高工资小于3000的部门
	select deptno,max(sal)
	from emp 
	group by deptno
	having max(sal) < 3000;

###多表查询（连接）
	1.交叉连接：cross join
	select *
	from emp（表1）
	cross（可不写） join dept（表二）;----笛卡尔乘积
	2.自然连接:natural join
	select *
	from emp
	natural join dept--自动匹配同名列，同名列只展示一次
	3.内连接：using子句
	4.内连接：on子句

###外连接
	1.左外连接：left outer join
	select *
	from emp e
	left outer join dept d
	on e.deptno = d.deptno;
	2.右外连接：right outer join
	select *
	from emp e
	right outer join dept d
	on e.deptno = d.deptno;

###使用事务保证转账安全
	-- 创建账户表：create table account(        
	id int primary key auto_increment,        
	uname varchar(10) not null,        
	balance double);
	-- 查看账户表：
	select * from account;
	-- 在表中插入数据：
	insert into account values (null,'丽丽',2000),(null,'小刚',2000);

	-- 丽丽给小刚 转200元：
	update account set balance = balance - 200 where id = 1;
	update account set balance = balance + 200 where id = 2;
	-- 默认一个DML语句是一个事务，所以上面的操作执行了2个事务。update account set balance = balance - 200 where id = 1;
	update account set balance = balance2 + 200 where id = 2;
	
	-- 必须让上面的两个操作控制在一个事务中：
	-- 手动开启事务：
	start transaction;
	update account set balance = balance - 200 where id = 1;
	update account set balance = balance + 200 where id = 2;
	
	-- 手动回滚：刚才执行的操作全部取消：
	rollback;
	-- 手动提交：
	commit;-- 在回滚和提交之前，数据库中的数据都是操作的缓存中的数据，而不是数据库的真实数据

###分页
	取第6-10
	select ename,sal from emp order by sal desc limit 5,5

