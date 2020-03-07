## Spring对JDBC整合支持
### 1. Spring对DAO提供哪些支持

1. Spring对DAO异常提供统一处理
2. Spring对DAO编写提供支持的抽象类
3. 减少DAO编码量，提高编程效率

### 2. Spring对DAO异常支持
Spring把特定某种技术的异常，如SQLException，统一转换为自己的异常，异常以
DataAccessException为父类，它封装原始的异常对象，不会丢失原始错误信息

DataAccessException继承于RuntimeException，是非检查异常，不会因为没有处理异常
而出现编译错误，异常必须要处理可以用拦截器统一处理

### 3. Spring对DAO编写支持
Spring为了便于以一种一致的方式使用各种数据库访问技术，如JDBC，SpringJDBC，
MyBatis，Hibernate，Spring提供一套抽象的DAO类，通过DAO类提供的方法可以获得数据
库访问技术相关的数据源和其他配置信息

JdbcTemplate：封装常用JDBC操作方法

JdbcDaoSupport：JDBC数据库访问对象的基类

HibernateTemplate：封装常用Hibernate方法

HibernateDaoSupport：Hibernate数据库访问对象的基类

JdbcDaoSupport
利用JDBC技术编写DAO的父类，通过此类提供的方法可便于获取Connection和JdbcTemplate

JdbcDaoSupport使用时需要注入一个DataSource

JdbcTemplate
封装了连接获取以及连接释放等工作，从而简化我们对JDBC的使用避免忘记关闭连接等错误

### 4. 如何编写DAO组件
基于SpringJdbc技术编写DAO组件可以采用以下两种方式：
1）DAO继承JdbcDaoSupport，通过getJdbcTemplate方法获取JdbcTemplate对象，需要
在DAO实现类中注入一个DataSource对象来完成JdbcTemplate的实例化

2）DAO不继承JdbcDaoSupport，在Spring的容器中配置一个JdbcTemplate的Bean，然后
注入给DAO组件