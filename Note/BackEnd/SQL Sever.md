# `MySQL`



# `SQL Sever`

## `SQL Server安装`

**[SQL SERVER 下载与安装](https://www.bilibili.com/video/BV1XT4y1C7Gc?spm_id_from=333.1007.top_right_bar_window_history.content.click)**

**安装问题：安装Sql Server:以前的某个安装需要重新引导计算机以便使其更改生效。若要继续，请重启计算机，然后再次运行安装程序。**

**解决方案：[大佬的博客](https://blog.csdn.net/weixin_43897590/article/details/115624607)**

## `MySQL和SQL Server的区别`

**01.MySQL需要写分号结束语句，而SQLServer不需要**

**02.MySQL里面的database和schema 一样，可以相互替换，而SQL Server里面的schema是database的一个模式，可以看成一个子数据库，二者不可以替换**

**03.MySQL的注释可以是 -- or # ，而SQL Server只能是 --**

**附：[MySQL和SQL Server的区别](https://www.php.cn/mysql-tutorials-414005.html)**

## `基本语法`

### `创建`

```sql
-- 创建数据库db1
create database db1				
-- 创建模式，作者是jack
create schema sch1 authorization jack 
-- 创建表t1、含三列（num、name、mark）
create table t1 (num int, name char(50), mark int)
-- 和c语言不同，变量的类型在变量名后面、变量类型必须给出
```
### `查询`

```sql
select sName postName from ...
-- sName ——> postName
```

## `进阶语法`

略

****

## `高阶语法`

### `视图`

**Note：由几个基本表的查询 or 视图的查询导出一个虚表，就像一个窗口**

#### `创建视图`

```sql
-- 基本语法
create view 
	<视图名> [列名...] 	 -- 列名要么全写，要么不写
as						-- 当
[with check option] 	-- 更新限制 select
```

```sql
-- 例一
create view stuView(num, name, age)
	as select num, sname, 2022 - year(birth) from stu
	-- 从表stu中导出num， sname， age（由计算得到）
```

```sql
-- 例二
create view isStuView
as select sno, sname, sex ssex from stu
	where dept = 'IS'
```
#### `视图中插入数据`
```sql
insert into <视图名>
	values(1、2、3...)
```

```sql
insert into stuView
 values('200912047', 'jack', 18)
```



**Note：对视图进行任何修改都要满足视图建立时的条件**

#### `视图查询`

```sql
-- 续上
select * from stuView -- 获取视图stuView全部列
```

****

## `练习一`

**题目：**

**创建数据库EXE，创建模式Stu_SC2、根据课本内容创建学生表student、课程表course、选课表sc**

**代码如下：**

```sql
	drop database if exists exe
	create database exe --创建数据库
go
	use exe
	drop schema if exists Stu_SC
go 
	create schema  Stu_SC authorization dbo
		create table student
		(
			学号Sno char(100),
			姓名Sname text,
			性别Ssex char(100),
			年龄Sage int,
			所在系Sdept char(100)
		)
		create table course
		(
			课程号Cno int, 
			课程名Cname char(100),
			先行课Cpno int,
			学分Ccredit int
		)
		create table sc
		(
			学号Sno char(100),
			课程号Cno int,
			成绩Grade int
		)
go 
	insert into Stu_SC.student values ('201215121','李勇','男',20,'CS');
	insert into Stu_SC.student values ('201215122','刘晨','女',19,'CS');
	insert into Stu_SC.student values ('201215123','王敏','女',18,'MA');
	insert into Stu_SC.student values ('201215124','张立','男',19,'IS');
	select * from Stu_SC.student
go
	insert into Stu_SC.course values (1,'数据库',5,4);
	insert into Stu_SC.course values (2,'数学',null,2);
	insert into Stu_SC.course values (3,'信息系统',1,4);
	insert into Stu_SC.course values (4,'操作系统',6,3);
	insert into Stu_SC.course values (5,'数据结构',7,4);
	insert into Stu_SC.course values (6,'数据处理',null,2);
	insert into Stu_SC.course values (7,'PASCAL预言',6,4);
	select * from Stu_SC.course
go
	insert into Stu_SC.sc values ('201215121',1,92);
	insert into Stu_SC.sc values ('201215121',2,85);
	insert into Stu_SC.sc values ('201215121',3,88);
	insert into Stu_SC.sc values ('201215122',2,90);
	insert into Stu_SC.sc values ('201215122',3,80);
	select * from Stu_SC.sc
```















