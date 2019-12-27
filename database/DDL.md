### 1. DDL

#### 1.1 创建表结构

1. 创建表结构

   ```mysql
   create talbe 表名(
   字段名 类型,
   字段名 类型
   );
   ```

   注意：

   - 关键字：`create table`

   - 表名不能重复（同一个库里）

   - 最后一个字段后面不能加逗号

   - 字段有默认值，用default

2. 创建部门表(dept_wtw)

   分析：

   - 部门号：10 20 30-->deptno-->int
   - 部门名称：'研发部、市场部等-->deptname-->varchar(10)
   - 部门地址：'南京'，，，，-->location-->varchar(10)

   代码：

   ```mysql
   create table dept_wtw(
   deptno int,
   deptname varchar(10),
   location varchar(10)
   );
   ```

   表重命名：`rename table 原表名 to 新表名;`

#### 1.2 修改表结构

1. 增加字段

   ```mysql
   alter table 表名 add 字段 类型;
   # 往部门表中增加字段(des varchar(20))
   alter table dept_wtw add des varchar(20); 
   ```

2. 修改（字段类型，长度，字段名）

   ```mysql
   #modify
   alter table 表名 modify 字段名 新数据类型;
   # 注意，modify不能修改字段名
   # 修改部门表中des字段（varchar(20) --> char(10)）
   alter table dept_wtw modify des char(20);
   ```

   ```mysql
   # change
   alter table 表名 change 原字段名 新字段名 新数据类型;
   # 例如
   alter table dept_wtw change des des varchar(20);
   ```

3. 删除字段

   ```mysql
   alter table 表名 drop 字段名;
   # 例如
   alter table dept_wtw drop des;
   ```

4. 删除表结构

   ```mysql
   # 删除表
   drop table 表名;
   ```

5. 清空表数据

   ```mysql
   truncate table 表名;
   ```

6. 总结

   ```mysql
   create:创建表结构
   alter:修改表结构(
   	add:增加字段
       modify:修改字段类型，不能修改字段名
       change:修改字段类型和字段名
       drop:删除字段或者删除表
       truncate:清空表数据
   )
   ```

#### 1.3 约束条件

##### 1.3.1 主键约束

主键（Primary Key，简称PK）。

主键约束=不能为空+不能重复。一张表里只能有一个主键，主键可以是一列或者多列的组合。

1. 定义主键的方式

   列级

   primary key auto_increment，主键并设置自增。

   ```mysql
   create table stu(
   	id int primary key auto_increment,
       name varchar(10)
   );
   ```

   表级。语法是：`constraint 约束名primary key(字段)`。约束名的命名规则：`表名_字段名_约束简称名`

   ```mysql
   create table stu(
   	id int,
   	name varchar(10),
       constraint stu_id_pk primary key(id)
   );
   ```

   修改：`alter table 表名 add constraint 约束名 primary key(字段1,字段2)`
   
##### 1.3.2 非空约束

   非空约束（not null 简称NN）

   非空约束的方式只有一种列级

   ```mysql
   create table stu(
   	id int primary key auto_increment,
       name varchar(10) not null
   );
   ```

##### 1.3.3 唯一约束

   唯一约束（unique 简称uk），可以插入空值，而且多个记录的该字段都可以为空（因为空不能做比较，所以就不能判定两个null是一样的）

   - 列级

     ```mysql
     create table stu(
         id int primary key auto_increment,
         name varchar(10) not null,
         email varchar(18) unique
     );
     ```

   - 表级

     ```mysql
     create table stu(
     	id int,
     	name varchar(10),
         email varchar(20),
         constraint stu_id_pk primary key(id),
         constraint stu_email_uk unique(email)
     );
     ```

##### 1.3.4 外键约束

外键约束（foreign key 简称jk）

外键约束定义在两张表的两个字段上，用来保证这两个字段的关系

// 创建部门表

```mysql
create table temp_dept(
	deptno int primary key,
    dname varchar(10) not null
);
```

// 创建员工表

```mysql
create table temp_emp(
	empno int primary key,
    ename varchar(20) not null,
    deptno int,
    constraint temp_emp_deptno_fk foreign key(deptno) 
    references temp_dept(deptno)
);
```

// 往员工表插入数据

```mysql
insert into temp_emp
values(1001,'张三',100);
```

// 往部门表中插入一条数据

```mysql
insert into temp_dept values(100,'研发部');
```

注：外键主要用于保证数据的完整性和一致性。如果添加外键约束，两张表在创建和插入数据时，都有一定的顺序（先有部门，然后才能将员工分配给该部门，员工表中部门号依赖于部门表中的部门号）

























