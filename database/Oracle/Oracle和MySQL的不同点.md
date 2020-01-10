## Oracle和MySQL的不同点

| 比较点         | MySQL                                                    | Oracle                                                       | 描述                         |
| -------------- | -------------------------------------------------------- | ------------------------------------------------------------ | ---------------------------- |
| 查看系统时间   | `select now();`<br />或者`select now() from dual;`       | `select sysdate from dual;`<br />日期格式默认为"10-1月-20"，即日-月-年 |                              |
| 查看有哪些表   | 在指定了某个库的前提下(use database)<br />`show tables;` | `select table_name  from user_tables;`                       |                              |
| 数据类型       | 常用的int, double, char, varchar, date                   | number, char, varchar2, date                                 | Oracle中整数和小数统称number |
| 空值处理       | ifnull(d1, d2)                                           | nvl(d1, d2)                                                  | 如果d1为空值，则用d2代替     |
| 连接操作       | concat(d1, d2)                                           | \|\|                                                         |                              |
| 大小写         | 不区分大小写                                             | SQL语句的字段名不区分大小写，数据区分大小写<br />upper(data)，小转大<br />lower(data)，大转小 |                              |
| 数字的截取函数 | truncate(d, n)                                           | trunc(d, n)                                                  |                              |
|                |                                                          |                                                              |                              |



