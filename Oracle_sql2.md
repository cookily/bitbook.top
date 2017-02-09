# Oracle SQL 语句基本使用方法之建表

```
--创建员工表
create table employee
(
       id number(4),--员工id
       name varchar2(20),--员工的姓名
       gender char(1),--员工的性别
       birthday date,--员工的生日
       salary number(6,2),--员工的工资
       comm number(6,2),--员工的绩效
       job varchar2(30),--员工的职位
       manager number(4),--员工的上司id
       deptno number(2)--员工的所在部门的id
);

--删除表
drop table employee;

--表重命名
alter table emp rename to employee;

--列的重命名
alter table employee rename column empid to id;

--添加列
alter table employee add newcolumn varchar2(20);

--修改列
alter table employee modify id varchar2(20);

--删除列
alter table employee drop column newcolumn;

--约束
--创建对应的主键约束
alter table employee add constraint emp_primary_key primary key(id);

--删除主键
alter table employee drop primary key;

--复合主键
alter table employee add constraint emp_pk primary key(id,name);

--唯一约束
alter table employee add constraint emp_unique unique(name);

--删除唯一约束
alter table employee drop constraint emp_unique;

--添加非空约束
alter table employee modify gender not null;

--删除非空约束
alter table employee modify gender char(1) null;

--默认值
--创建表的时候创建对应的默认约束
create table emp
(
       id number(4),
       name varchar2(20) default 'empname',
       gender char(1)
);
--检查约束（条件约束，check约束）
alter table emp add constraint gender_ck check(gender in('F','M'));
alter table emp add constraint id_ck check(id between 1 and 10000);
alter table emp add constraint gender_ck check(name like 'T__');

--外键约束(引用完整性)
drop table emp;
create table emp(id number(4),name varchar2(20),deptno number(4));--部门编号);
create table dept(id number(4),deptname varchar2(20));--部门表

--外键在外键表中创建
alter table emp add constraint dept_emp_fk foreign key(deptno) references dept(id);

--注意点：主表的主键名必须设成主键，否则报错
--dept(主表，要被引用的表)
--emp(从表或子表)

--设置dept表的主键
alter table dept add constraint dept_pk primary key(id);

--建立引用关系后：主表的行如果被引用，则不允许删除，删除时，先删从表，再删主表，插入时，先插主表，再插入从表

--简单创建方法
create table stuinfo
(
       stuid int primary key,
       email varchar2(20) default('xxx.xx.com') not null,
       age int check(age>=10 and age<=40),
       sex varchar2(3),
       constraint pk_stuid primary key(stuid),
       constraint fk_id foreign key(age) references dept(id)
)
```