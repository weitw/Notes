## 事务

事务处理语言：TPL

commit：提交

rollback：回滚

savepoint：保存点

事务是一组DML操作的逻辑单元，用来保存数据的一致性，在事务内组成的DML操作，要么一起成功提交，要么一起撤销。

### 1. 事务处理

#### 1.1 事务的开始和结束

##### 1.1.1 开始

1. 事务开始于上一个事务的结束
2. 事务开始于一条DML操作，insert，update，delete。

##### 1.1.2 结束

事务终止于显示操作，commit，rollback。

#### 1.2 事务中的数据状态

如果有多个会话操作同一张表数据，当用户和服务器连接成功后，服务器和客户端会建立起一个会话（session），客户端和服务器的交互都在此会话中进行。 

演示（两个窗口A,B）

步骤一：打开A会话，创建表，插入数据不提交

```mysql
create table temp(
id int
);
```

`set autocommit = 0;`

`insert into temp values(1);`

步骤二：A会话更新不提交

`update temp set id=2;`

步骤三：A会话更新数据不提交，B会话删除数据不提交

`update temp set id=3;`  A会话，不提交或者不会滚，那么该事务就没有结束，下一个事务就无法执行

`delete from temp;`   B会话会等待，超时之后会报错。

步骤四：A会话更新数据不提交，更新以后回滚

`update temp set id=4;`

`rollback;`

总结：

1. 事务内部数据的改变，如果没有提交，只有在自己的会话（缓存）可以看到数据的改变，其他会话看不到数据的改变的。
2. 事务会对操作的数据进行加锁，不允许其他事务进行操作。（A会话更新数据，B会话删除数据会发生阻塞，当超过阻塞时间，会释放锁，回滚到更新之前）
3. 如果提交，数据的改变得到确认，其他回话可以看到数据的改变。数据上的锁也会被释放，保存数据的临时空间（缓存）被释放
4. 如果回滚，数据的改变会取消，数据上的锁会被释放掉。保存数据的临时空间被释放

补充：

`show variables like 'innodb_local_wait_timeout';`，查看事务锁超时时间

#### 1.3 保存点

可以回滚到指定的保存点

```mysql
set autocommit=0;
insert into temp values(1);
savepoint A;  # 保存点A

insert into temp values(2);
savepoint B;  # 保存点A

insert into temp values(2);
savepoint C;  # 保存点A
```

`rollback to B;`，回到保存点B，那么B之后的保存点会被全部取消。如果进行commit提交，那么回滚无效。

### 2. 数据库常用对象

#### 2.1 表(Table)

表是关系型数据库的基本存储结构。表示一个二维结构，由行（记录）和列（字段）组成。

表就相当于实体的对象类，记录就相当于具体的实例对象，字段就相当于实例对象的属性。

创建表

```mysql
create table tb_name(字段 类型);
```

#### 2.2 视图(View)

视图是虚表（没有数据），其内容由查询定义。视图对应一条select语句，此语句得到的结果赋予一个名字，即为视图的名字。因此，可以像操作表一样，操作视图。

// 查询20号部门的员工信息

```mysql
select empno,ename
from emp
where deptno=20;
```

1. 创建视图

   ```mysql
   # 语法
   create view 视图名 as 查询语句;
   # 举例
   create view view_emp as 
   select empno,ename
   from emp
   where deptno=20;
   ```

2. 说明

   视图的使用和表相同，视图的好处能够简化查询，还可以隐藏数据表中部分列，视图中本身是不包含任何数据的。视图是基表的投影。

3. 基表和视图示例

   // 更新基表数据，查看视图

   `update emp set ename='郭靖2' where ename='郭靖';`

   `select * from view_emp;`

   // 更新视图数据，查看基表

   `update view_emp set ename='郭靖' where ename='郭靖2';`

   `select ename from emp where empno=1004;`

4. 基表和视图进行DML操作

   基表进行DML操作会改变视图的显示，对视图进行DML操作，同样会该表基表的显示，视图只是基表的投影。

5. 删除视图

   `drop view 视图;`

#### 2.3 索引(Index)

索引用于在数据库中加速表查询的数据库对象。通过快速访问路径的方式，定位数据，可以减少磁盘的IO操作，提高查询效率。

用空间换时间。使用索引会占用额外的空间，索引的结构是数据+地址。

##### 2.3.1 索引分类

1. 聚簇索引

   按照数据存放的物理地址为顺序，可以提高多行的检索速度

2. 非聚簇索引

   可以提高单行的检索速度，需要通过多个地址查询。

##### 2.3.2 索引的类型

唯一索引，主键索引，聚集索引，全文索引，普通索引

##### 2.3.3 索引的创建

1. 自动创建索引

   主键约束，唯一约束....

2. 手动创建索引

   语法
   `create index 索引名 on 表名(列名);`

   // 根据员工号查询信息
   
   `select ename from emp where empno=1004;`
   
   // 给empno员工号加索引
   
   `create index index_empno on emp(empno);`
   
   // 查看语句执行时间
   
   // 显示SQL语句执行时间
   
   `show variables like '%pro%';`
   
   `set profiling=1;`
   
   // 显示执行时间
   
   `show profiles;`
   
   说明：通过前后时间对比，加索引时间查询更少。

#### 2.4 存储过程(Procedure)

存储过程是在大型数据库系统中，一组为完成特定功能的SQL语句集。

存储过程存储在数据库中，经过一次编译后，再次调用，不需要再次编译，用户通过制定的存储过程名字，并给参数（如果有参数就给参数，没有就是无参）

1. 好处

   - 可以把复杂的操作存放在存储过程中，简化用户的操作
   - 简化变动时的修改
   - 保证数据的完整性
   - 提高性能

2. 创建存储过程

   语法

   ```mysql
   create procedure 存储过程名([参数])
   begin
   SQL语句...
   end
   ```

   // 创建存储过程，查询员工表中员工的最高薪水

   ```mysql
   delimiter //
   
   create procedure maxSalary()
   begin
   select max(salary) from emp;
   end //
   
   delimiter ;
   ```

   delimiter //，即临时将分隔符改成//，

3. 调用存储过程

   `call 存储过程名([参数]);`

4. 说明

   先声明分隔符，创建完存储过程之后，再次将分隔符声明为`‘;’`
   
5. 删除存储过程

   `drop procedure 存储过程名;`，注意，这个地方不要加括号

6. 创建存储过程，带有输出参数，参数用out修饰

   // 查询员工表中最高薪水、最低薪水、平均薪水。

   ```mysql
   delimiter //
   
   create procedure getEmp(
   out max_salary double(7,2),
   out min_salary double(7,2),
   out avg_salary double(7,2)
   )
   begin 
   select max(salary) into max_salary from emp;
   select min(salary) into min_salary from emp;
   select avg(ifnull(salary,0)) into avg_salary from emp;
   end //
   
   delimiter ;
   ```

   调用

    `call getEmp(@max_salary,@min_salary,@avg_salary);`

   查看数据

   `select @max_salary,@min_salary,@avg_salary;`

#### 2.5 序列(Sequence)

Oracle才有的，MySQL没有























