### 1. DML

#### 1.1 增加数据

- 方式一

  全部字段（按照表结构一一给值）

  ```mysql
  insert into 表名 values(值1，值2，值3);
  # 例如插入一条记录
  insert into dept_wtw values(10,'研发部','南京');
  # 运行时报错，报错信息如下
  # ERROR 1366 (HY000): Incorrect string value: '\xD1\xD0\xB7\xA2\xB2\xBF' for colum
  # n 'deptname' at row 1
  # 这是一个编码错误，此时我的数据默认的编码是utf8的，但是在Windows下的这些客户端的默认编码是gbk，所以应该将写入和读取都设置成gbk;使用命令
  set names gbk;
  ```

  **注意：mysql客户端默认自动提交。设置不自动提交，必须手动提交（执行commit）**

  `set autocommit = 0;`

  **设置了不自动提交的话，语句回车之后数据库里是没有这条数据的，但是缓存里面有这条数据，所以此时的窗口中可以查到这条语句。该窗口关闭重启之后，这条数据就查不到了。**

- 方式二

  指定字段插入（按照指定字段一一给值）

  ```mysql
  insert into 表名(字段一,字段2) values(值1,值2);
  # 例如
  insert into dept_wtw(deptno,deptname) values(20,"销售部");
  ```

#### 1.2 更新数据

语法：

```mysql
update 表名 set 字段名=新值 where 条件;
# 更新部门表中40号部门，将地址改为上海
update dept_wtw set location='上海' where dno=40;
```

#### 1.3 删除数据

```mysql
delete from 表名 where 条件;
# 删除第50号元素
delete from dept_wtw where dno=50;
```

删除的区别

delete。需要确认提交，没有提交的话，可以回滚的，可以带where条件删除，序号还是从删除的地方开始

truncate。立即生效，不能回滚，不能带where条件，序号从1开始