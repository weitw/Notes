### 1.DQL

#### 1.1 基础查询

##### 1.1.2 简单示例

```mysql
# 查询员工表数据
# 单列检索
select empno from emp;
# 多列检索
select empno,ename from emp;
# 检索所有列
select * from emp;

# 查询1005号员工信息
select * from emp where empno=1005;

# 查询员工的薪水和年薪(用as取别名)
select salary,salary*12 as year_salary from emp;

# 使用限定表名
select ename from emp_xms

# 查询员工的月薪salary+bonus
select salary+bonus as sb from emp;
# 优化
select salary+ifnull(bonus,0) as sb from emp;
```

**注意：使用通配符*查询会降低查询速度和影响程序的性能**

##### 1.1.3 条件判断

| 符号     | 描述     |
| -------- | -------- |
| =        | 等于     |
| !=或者<> | 不等于   |
| >        | 大于     |
| <        | 小于     |
| <=       | 小于等于 |

##### 1.1.4 NULL空值

- 任何数据类型都可以取空值（insert插入默认为空）

- 空值和任何数据类型参与算术运算，结果为NULL

- NULL和字符串类型作连接操作，结果也为空

- 空值处理函数

  ifnull(d1,d2)。如果第一个参数为空，则取第二个参数代替；反之，如果第一个参数不为空，则取第一个参数。

##### 1.1.5 查询空值

用IS NULL 或者 IS NOT NULL来找空值

##### 1.1.5 字符串连接

concat(x,y,z...)

##### 1.1.6 去重

distinct。只能跟在select后面

例如：`select distinct position from emp;`

// 查询每个部门不重复的职位（需要对两个字段进行联合去重，distinct表示全部列的唯一组合）

`select distinct deptno,position from emp;`

##### 1.1.7 大小写

MySQL默认查询不区分大小写，其他很多数据库，默认是区分大小写的（Oracle），如果需要区分，必须在建表的时候，通过binary标识敏感的数据

例如：

```mysql
create table temp(
name varchar(10) binary
);  # 此时name这一字段严格区分大小写
```

如果在建表的时候没有加binary，我们在查询的时候需要区分大小写，那么可以写成下面这种

`select * from emp where binary position='Analyst';`

##### 1.1.8 and和or

and表示逻辑并且，or表示或者

`select ename,salary from emp where salary>=5000 and salary<=10000;`

还可以用between 低值 and 高值，**闭区间 [低值，高值]**

`select * from emp where salary between 5000 and 10000;`

##### 1.1.9 in(列表项)

判断等于列表项中任意一项，满足一个即可

```mysql
# 选出工资为4000或者5000的记录
select * from emp where salary in(5000,4000);
# in等价于any，但是mysql不支持，Oracle可以
select * from emp where position=any('Analyst','Manager');
```

增加一个列表项（null）之后，对查询结果没有影响，例如

`select * from emp where salary in(5000,4000,null);`，那么salary为null的结果能出来（因为如果salary和in()里面值逐一比较，如果发现一样的，则匹配成功，如果和Null比较，继续和下一个值比较，即和null比较查询为空）。但是not in ()就会有影响（因为要保证salary和列表项里面的每一项都要不同，所以每次都要和null比较，结果自然全为空）。

因为当用表中的salary和in()里面的值比较时，和null是无法比较的，**即没有null等于null这种说法**。

##### 1.1.10 结论

- **空值不能用等于或者不等于跟任何数据进行比较**
- **使用in()时列表项中有空值对结果没有影响；not in()有影响，结果为空**

##### 1.1.11 模糊查询

使用like关键字并结合占位符使用

_表示1个字符

%表示0到多个字符

```mysql
# 查询员工姓名中包含'张'字的员工信息
select ename from emp where ename like '%张%';
```

**注意：通配符使用比较影响查询速度，花费时间比较长，不要过度使用**

可以使用escape 来指定转义字符进行转义。转义字符后面的%或者下划线，使其不作为通配符。

例如：`select ename from emp where ename like '张\%' escape '\';`

转义字符\可以转义特殊字符

##### 1.1.12 查询中否定形式

```mysql
# 查询哪些员工有奖金
select ename,bonus from emp where bonus is not null;

# 查询薪水不在5000到10000之间的员工姓名和薪水
select ename,salary from emp where salary not between 5000 and 10000;

# 查询不是20号部门和30号部门的员工信息
select * from emp where deptno not in(20,30);
# 如果写成not in(20,30,null)，那么查询的结果就是空。
```

**注：int(列表项)，表示肯定，判断等于列表项中任意一项，如果列表项中有空值，对结果没有影响。not in(列表项)，表示否定，判断不等于列表项中任意一项，如果列表项中有空值，查询到的结果为空。**

#### 1.2常用函数

##### 1.2.1 单行函数

每一行数据处理后返回一个结果。

1. 数字函数

   | 函数                                     | 描述                                                         |
   | ---------------------------------------- | ------------------------------------------------------------ |
   | round(数字，保留小数点后指定的位数)      | 对数字进行四舍五入，如果保留到整数位，第二个<br />第二个参数可以用0表示，或者不写 |
   | truncate(数字，截取到小数点后指定的位数) | 注意是截取，round是四舍五入，如果截取到整数位，<br />第二个参数只能用0，不能省略 |

2. 拼接函数

   | 函数          | 描述                 |
   | ------------- | -------------------- |
   | concat(a,b,c) | 用于多个字符串的连接 |

3. 去除空格函数

   | 函数            | 描述               |
   | --------------- | ------------------ |
   | trim(字符数据)  | 去掉左右两边的空格 |
   | ltrim(字符数据) | 去掉左边的空格     |
   | rtrim(字符数据) | 去掉右边的空格     |

4. 文本处理函数

   | 函数            | 描述   |
   | --------------- | ------ |
   | upper(字符数据) | 转大写 |
   | lower(字符数据) | 转小写 |

5. 数据处理函数

   | 函数       | 描述                |
   | ---------- | ------------------- |
   | abs(数据)  | 返回数据的绝对值    |
   | rand()     | 返回0-1之间的随机数 |
   | sqrt(数据) | 返回数据的平方根    |
   | pow(x,y)   | 返回x的y次方        |
   | mod(x,y)   | 返回x除以y的余数    |

6. 处理日期和时间的函数

   | 函数                               | 描述                                                         |
   | ---------------------------------- | ------------------------------------------------------------ |
   | now()                              | 当前日期                                                     |
   | date(日期时间)                     | 返回该日期时间的日期                                         |
   | time(日期时间)                     | 返回时间（时：分：秒）                                       |
   | year(日期)，month(日期)，day(日期) | 年，月，日                                                   |
   | adddate(给定的日期，增加的日期)    | 增加一个日期（可以增加天，周，月，年）<br />例如（注：interval表示间隔）<br />select add(now(),2)，加2天<br />select add(now(), interval 3 week)，加三周<br />select add(now(), interval 1 month)，加一月 |
   | date_format(日期，格式)            | 格式化日期格式<br />select date_format(now(), '%X年%m月%d日 %H时%i分%s秒') |

7. 其他

   | 函数                                      | 描述                                                         |
   | ----------------------------------------- | ------------------------------------------------------------ |
   | length(字符串)                            | 字符串长度。数据库默认使用utf8编码，一个<br />中文占三个字节 |
   | substring(字符串，起始位置，最大字符数量) | 截取字符串，从起始位置开始，最多截取n个字符<br />注意，下标从1开始，不是0。 |
   | case....whren                             | 分支条件语句<br />语法结构：<br />select 字段名,case 字段<br />when 条件1 then 值1 <br />when 条件2 then 值2<br />else 其他值 end 别名<br />form 表名； |

```mysql
select ename,position,salary,
case position 
when 'Analyst' then salary*1.2
when 'Progrmmer' then salary*1.05
when 'Clerk' then salary*1.02
else salary end new_salary
from emp;
```

##### 1.2.2 组函数（聚合函数）

多行数据处理后返回一个结果

| 函数           | 描述     |
| -------------- | -------- |
| count(列明\|*) | 求记录数 |
| sum(列明)      | 求和     |
| avg(列名)      | 求平均   |
| max(列名)      | 求最大值 |
| min(列名)      | 求最小值 |

计算会忽略空值，*不忽略。

```mysql
// 查询员工的人数总和，薪水总和，平均薪水
select count(*),sum(salary),avg(salary) from emp;
# 注意，avg会忽略空值，所以应该进行空值处理
select count(*),sum(salary),avg(ifnull(salary,0) from emp;
                                
select ename,max(salary),min(salary) from emp;
# 该写法在MySQL中不会报错，其他数据库里会报错
```

总结

- count,sum,avg,max,min如果函数中写列名，默认忽略空值，count(*)不忽略空值，sum,avg只能处理数值类型

- 尽量不要将列名与组函数在一起使用，例如

  `select ename,max(salary),min(salary) from emp;`

##### 1.2.3 自定义函数

1. 创建一个不带参数的自定义函数

   ```mysql
   create function f1() returns varchar(30)
   return 'hello world';
   ```

   使用

   `select f1();`

2. 创建带有参数的自定义函数

   ```mysql
   create function f2(num1 int,num2 int) returns int
   return num1+num2;
   ```

3. 删除自定义的函数

   `drop function f1;`，注意没有()。

#### 1.3 正则表达式

MySQL支持的正则表达式只是正则表达式的一个很小的子集。

// 查询员工表中姓名包含张字的所有记录

`select ename from emp where ename regexp '张';`

// 查询员工表中姓名包含“张”或者“郭”的记录

`select ename from emp where ename regexp '张|郭';`

// 再放三条数据

```mysql
insert into emp(empno,ename)
values
(1014,'1张三'),
(1015,'2张三'),
(1016,'3张三'));
```

// 查询员工表中包含1张三，2张三，3张三的记录

`select ename from emp where ename regexp '[123]张三';`

特殊字符需要转义

| 元字符 | 描述                 |
| ------ | -------------------- |
| *      | 0-多个               |
| +      | 1-多个               |
| ?      | -或1个               |
| {n}    | 匹配n个              |
| {m,n}  | 匹配m到n个           |
| {m,}   | 不小于指定数量的匹配 |
| ^      | 以指定的文本开头     |
| $      | 以指定的文本结尾     |

// 查询员工表中姓名起始字符包含.或者1或2，3的所有记录

`select ename from emp where ename regexp '^[123\\.];'`

#### 1.4 排序子句

对查询结果集进行排序，先有结果集再排序。

排序子句：`order by 列名`

排序规则：asc(升序，默认)，desc(降序)

// 按照薪水升序排序

`select ename,salary from emp order by salary asc;`

**注：MySQL中，空值参与排序被看作是最小值**

// 按照部门号升序排序，同一部门按照薪水降序排序，没有部门号的不算在内

` select ename,salary,deptno from emp where deptno is not null order by deptno asc,sa lary desc;`

还可以写成：` select ename,salary,deptno from emp where deptno is not null order by 1 asc,2 desc;`，这儿的1和2会根据select后面的字段序号来确定

注意：排序语句的执行在select之后，因此排序可以用列名，列别名，表达式，函数，还可以使用数字（数字表示查询结果集对应字段顺序，第一列用1表示，以此类推）

// 根据员工的名字排序

`select ename from emp order by ename;`

// 按照gbk汉字首字母排序

convert(字段 using 字符集)，表示字符集转换

`select ename from emp order by convert(ename using gbk);`

#### 1.5 分组子句

**分组：group by 列名**

[案例](./案例.md)

#### 1.6 总结

1. 写法顺序：select0->from->where->group by->order by

2. 执行顺序：

   from：检索的表

   where：行记录的过滤

   group by：分组

   having：分组后再过滤

   select：结果集

   order by：排序。

#### 1.7 子查询（高级查询）

##### 1.7.1 非关联子查询

子查询：一条SQL语句中嵌套select查询语句

嵌套的子查询是独立语句，不依赖主查询。

[案例](./案例.md)

总结

1. 清楚非关联子查询的执行过程
2. 比较符的选择（单值和多值）
3. 多值多列的情况。比较规则要相同，返回了多少列，就用()将要比较的内容括起来，然后再和返回的结果比较。

##### 1.7.2 关联子查询

嵌套的子查询不是独立语句，依赖主查询。

查询哪些员工的薪水比本部门的平均薪水值低 (**该例子引出关联子查询**)

两者的比较规则不相同，非关联子查询不能使用

```mysql
select ename,salary
from emp e
where salary<(
    select avg(ifnull(salary,0))
	from emp
    where deptno=e.deptno
);
```

嵌套子查询中的e.deptno动态数据依赖主查询传递过来的参数

1. 特点：关联子查询中嵌套的子查询执行多次

2. 执行过程
   - 先执行主查询
   - 将参数传递给子查询
   - 再执行子查询
   - 子查询返回的结果给主查询，再执行主查询（作为主查询的条件）
3. exists关键字用来判断子查询有没有数据返回，满足某种关系，有数据返回则为true。反之，不满足某种关系，没有数据返回，则为false。exists不关心子查询返回的结果，所以子查询中select后面写什么都行。通常直接用1来表示。

##### 1.7.3 组合查询

组合查询的规则

- 组合查询是由两条以上的select语句组成，并以union分割
- 被union连接起来的不同的查询的结果必须包含相同的列、表达式或者组函数（结果集的机构必须相同）
- union会自动去重
- 可以使用union all取消去重

1. 查询10号部门的员工姓名和薪水

   ```mysql
   select ename,salary
   from emp
   where deptno=10;
   ```

2. 查询薪水大于6000的员工姓名和薪水

   ```mysql
   select ename,salary
   from emp
   where salary>6000;
   ```




#### 1.8 分页实现

分页实现使用limit关键字，用来限制查询记录数的检索语句。

语法：

```mysql
# 第一种方式，只能得到表的前n个，后面的没法查询
select 字段
from 表名
limit 数量;
# 第二种方式，常用
select 字段
from 表名
limit 开始行，数量; # 行的下标从0开始
```

1. 从第一行记录开始查找，找5条记录
   `select empno,ename from emp limit 0,5;`

2. 从第二行开始找，找五条

   `select empno,ename from emp limit 1,5;`

分页数据是由前台动态获取的，并不是写死的。

pageSize:每页显示记录  ->5

page:指定页数(该数据由前台传过来)               -> 0,1,2,3,.....

公式(获得数据库中分页的开始行)：int begin = (page-1)*pageSize

#### 1.9 表间关联查询

##### 1.9.1 内连接

1. 语法

   ```mysql
   表1 [inner] join 表2 on 条件 # inner可以省略
   ```

2. 查询员工的姓名和其部门的名字

   ```mysql
   select ename,dname
   from emp e inner join dept d
   on e.deptno=d.deptno; 
   ```

   内连接的结果集中数据一定是在两张表中能够找到的匹配记录，由于deptno在两张表中都有，所以必须指明是哪张表的字段。

3. 补充：其他写法

   ```mysql
   select ename,dname
   from emp e,dept d
   where e.deptno=d.deptno;  # 先笛卡尔积再筛选
   ```

   笛卡尔积如果不加where条件的连接，得到的是笛卡尔积的结果，检索的结果的行数=第一张表行数x第二张表的行数。

   等价于数据里的交叉连接（cross join）,`select ename,dname from emp e cross join dept d;`

   其中emp（前面的）叫做驱动表，后面的dept叫匹配表。在内连接中，驱动表和匹配表的顺序可以交换。

4. 查询员工姓名和领导的名字(同一张表用两次)

   ```mysql
   select e.ename,m.ename
   from emp e join emp m
   on e.leader=m.empno;
   ```

5. 说明。

   - 内连接执行顺序，遍历驱动表，在匹配表中匹配记录
   - 等值连接时（条件中用的是等于号），驱动表和匹配表可以互换。
   - 内连接的结果集特点：能够在两张表中找到的匹配记录会被保留，匹配不到的记录会丢掉

6. 查询员工的姓名和其部门的名字，要求没有部门的员工也要被查询出来

   ```mysql
   select ename,dname
   from emp e inner join dept d
   on e.deptno=d.deptno
   union
   select ename,'No Dept'
   from emp
   where deptno is null;
   ```

##### 1.9.2 外连接

1. 语法

   ```mysql
   # 左外连接（左边的表是驱动表）
   tb1 left [outer] join tb2 on 条件
   # 右外连接（右边的表是驱动表）
   tb1 right [outer] join tb2 on 条件
   ```

2. 查询员工的姓名和其部门的名字，要求没有部门的员工也要被查询出来

   ```mysql
   # 分析：查询全部的员工，员工表中的数据全部出现外连接的结果集中，那么员工表应该作为驱动表
   select ename,ifnull(dname,'No Dept')
   from emp e left join dept d 
   on e.deptno=d.deptno;
   ```

   **左外连接和右外连接可以互换，但是必须要明确哪个表是驱动表。**

3. 查询员工的姓名和其部门的名字，要求没有员工的部门也要查出来

   ```mysql
   select dename,ifnull(ename,'No Emp')
   from emp e right join dept d 
   on e.deptno=d.deptno;
   ```

4. 外连接的特点

   如果驱动表在匹配表中找不到匹配记录，则匹配一行空值，但是保证驱动表中数据全部出现在外连接的结果集中

   外连接的结果集=内连接的结果集+驱动表在匹配表中皮配不上的记录

5. 查询哪些部门没有员工

   ```mysql
   # 非关联子查询
   select dname,deptno
   from dept
   where deptno not in(
       select deptno
   	from emp
       where deptno is not null
   );
   # 关联子查询
   select d.dname,d.deptno
   from dept d
   where not exists(
       select 1
   	from emp
       where deptno=d.deptno
   );
   # 外连接
   select dname,ename
   from dept d left join emp e
   on d.deptno=e.deptno
   where ename is null;
   ```

6. 总结

   外连接的本质：驱动表中的数据全部出现在外连接的结果集中

   分析：如果需要查询全部数据，考虑外连接。**内连接查出来的是两个表共有的一部分，外连接至少会将驱动表中的数据全部查出来，一一和匹配表进行匹配，匹配不上的为NULL**

   注意。

   - 不要关联不必要的表，关联处理非常消耗资源
   - 关联的表越多，可能导致性能下降
   - 获取同样的结果，可能存在很多SQL实现方式，找最优的方式。

##### 1.9.3 全外连接（了解）

full join on，MySQL不支持（会报错），Oracle可以

1. 查询全部员工和全部的部门

   ```mysql
   select empno,ename,d.deptno,dname
   from emp e full join dept d
   on e.deptno=d.deptno;
   ```

2. 用MySQL实现上面的例子

   ```mysql
   select empno,ename,d.deptno,dname
   from emp e left join dept d
   on e.deptno=d.deptno
   union
   select empno,ename,d.deptno,dname
   from emp e right join dept d
   on e.deptno=d.deptno;
   ```

   

