```sql
-- 1.创建表student
create table student
(
   stuid int primary key,
   stuname varchar2(20) not null,
   age int check(age>=10 and age<40),
   sex varchar2(4),
   email varchar2(20) default('xx@niit.com'),
   tel varchar2(20)
);
```
```sql
-- 查询表中所有内容
  select * from student;
```
```sql
-- 向student表中添加数据
-- 根据指定列新增数据
insert into student
(stuid,stuname,age,sex,email,tel)
values
(1006,'jack',25,'男',default,'13585468547');

insert into student
(stuid,stuname,age,sex)
values
(1005,'marry',28,'女','sdf');

insert into student(stuid) values(1002);
```
```sql
-- 为每一列写入值,值的数量必须要和当前表的总列数匹配
insert into student values
(1008,'jerry',null,null,null,null);
```

```sql
-- 建表时插入数据
create table newstudent
as select * from student;

select * from newstudent;
```

```sql
--只选择复制原表的指定列
create table newstu
as select stuname
from student;

select * from newstu;
```
```sql
-- 创建新表newstudent，结构和sutdent一致
drop table newstudent;
create table newstudent
(
   stuid int ,
   stuname varchar2(2), --如果比原表小，会放不下
   age int ,
   sex varchar2(4),
   email varchar2(20) ,
   tel varchar2(20)
);
```

```sql
-- 修改列的数据类型
alter table newstudent modify stuname varchar2(20);
```
```sql
-- 复制数据到新表中
insert into newstudent select * from student;
```

```sql
-- 日期类型
-- 系统当前时间
select sysdate from dual;

-- 向student表中添加生日列，类型为date
alter table student
add birthday date;
```
```sql
-- 插入生日
insert into student values
(
  1009,
  'mingzi',
  30,
  '男',
  default,
  '1234567895',
  to_date('1988-01-20','YYYY-MM-DD')
);
```
```sql
insert into student values
(
  1010,
  'mingzi',
  30,
  '男',
  default,
  '1234567895',
  to_date('19880220','YYYYMMDD')
);
```
```sql
--插入系统当前时间
insert into student values
(
  1012,
  'mingzi',
  30,
  '男',
  default,
  '1234567895',
  sysdate+1 -- 天数加1
);
```

```sql
insert into student values(1013,'mingzi',30,'男',default,'1234567895',sysdate+1/24/60/60*3);
```

```sql
insert into student values(1014,'mingzi',30,'男',default,'1234567895',sysdate);
```
--将日期型转换为字符类型
select to_char(birthday,'YYYY-MM-DD') from student;

--序列
create sequence my_seq
start with 1
increment by 1
maxvalue 9999
minvalue 1
nocache

--使用序列
--获取当前序列号
select my_seq.currval from dual;
--当序列创建后，必须先执行一次nextval之后才能使用currval
select my_seq.nextval from dual;

--创建表test使用序列
create table test
(
       stuid int,
       stuname varchar2(20)
);
--添加数据
insert into test values(my_seq.nextval,'jack');

select * from test;

--删除序列
drop sequence my_seq;

--修改数据
select * from student;
--如果不加where条件，表示将该列所有行都修改（慎用）
update student set sex='女';
--where条件（筛选）
update student set email='fff@niit.com' where stuid=1005;
--将年龄在25-29之间的学生生日都改成当前时间
update student set birthday=sysdate where age between 25 and 29;
update student set birthday=sysdate where age in(25,26,27,28,29);


--修改多个列(set关键字出现一次就可以)
update student set age=35,sex='男' where stuid=1001;
--修改没有填写过tel的改成00000000
update student set tel='0000000' where tel is null;

--删除数据
delete from student
rollback;

--删除主外键关系表（先删从表，再删主表）
create table dep as select * from scott.dept;
create table emp as select * from scott.emp;
drop table emp;

select * from dep;
select * from emp;

--删除truncate
truncate table student

--删除部门20的数据
--先删子表，再删主表
delete from emp where deptno=20;
delete from dep where deptno=20;
