#   数据的增删改
##  一、	数据的插入

```sql
语法：
insert into 表名(列名) values(值)
```

### *注意点：写入的值必须和列数量要匹配，列名和值的顺序必须一致*
1. 主键必须写在指定列中

2. 写入值和列的数据类型必须匹配

3. 表中数据如果想使用默认值，则使用default关键字代替

4. 写入的值必须要符合check约束

5. 如果不能为null的略没有插入数据值，报错

### *为每一列写入数据*
```sql
语法：
insert into 表名 values(值)
```
*注意点：如果想呈现默认值使用default关键字替入，如果某列为空使用null替入*

*如果不能为null的列插入了null值，报错（就算有默认值也报错）*

*事务DML提交commit*

### 2.数据表的复制  
```sql
-- 1. 建表时写入数据
-- 语法:
	Create table 表名 as select * from 原表名
	Create table 表名 as select 具体列名 from 原表名
```
```sql
-- 1. 向已经存在的表复制数据
-- 语法：
insert into 新表 select * from 原表

```
*前提：必须先将新表创建，新表的列结构要和原表一致*

表复制语句是否可以反复执行？

### 3.新增日期类型数据
1. 获取当前系统时间
```sql
select sysdate from dual;
```
2. 使用to_date()对字符型时间转换为date类型时间进行插入

### 4.序列
	#作用：用来生成唯一数字值的数据库对象#

序列的值由oracle数据库按照递增或递减的顺序自动生成，通常用来自动生产主键值

注意点：序列是独立的数据库对象。不依赖与表，一般一个序列就作为一个表的主键

语法：
```
Create sequence 序列名
start with 起始数 默认1
increment by 增长数 默认1
maxvalue m 最大值
minvalue n 最小值
cycle|nocycle 表示到达最大值或最小值以后是否继续生成序列号，默认是nocycle
cache p|nocache 表示指定p个数据在缓存中，nocache表示不缓存，默认是20
```

## 二、数据的修改
语法：update 表名 set 列=值 [where 条件]

## 三、数据的删除
语法：
```
delete from 表 [where 条件]
Truncate table 表
```
#面试题：delete和truncate的区别#
1. Delete可以有条件的删除，truncate只能将表的全部数据删除，
2. Delete是DML语句，可以回滚，truncate是DDL语句，立即生效，不可回滚，
3. 如果删除全部表的记录，且数据量比较大，delete效率比truncate低。
