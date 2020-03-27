### 1. MyBatis

#### 1.1 什么是MyBatis

MyBatis最早源自Apache基金会的一个开源项目iBatis，2010年项目由Apache sorfware foundation迁移到Google Code，改名为MyBatis。

MyBatis是支持普通SQL查询，存储过程和高级映射的优秀持久层框架。其使用简单的XML配置或注解配置定义映射关系，将实体类对象映射成数据库记录。

#### 1.2 MyBatis工作原理

1. 加载配置

   MaBatis将SQL的映射加载为一个个的MappedStatement对象（包括传入的参数映射配置，执行的sql语句，结果映射配置），将其存储在内存中

2. SQL解析

   当API接口层收到调用请求时，会接收到传入的SQL的ID和传入的参数对象（可以是Map，实体类或者基本数据类型），MaBatis会根据SQL的ID找到相应的MappedStatement，然后根据传入的参数对象对MappedStatement进行解析，解析后可以得到最终要执行的sql语句和参数

3. SQL执行

   将最终得到的sql语句和参数拿到数据库进行执行，得到执行结果

4. 结果映射

   将操作数据库的结果按照映射配置进行转换，可以转换为Map，实体类或者基本数据类型，将转换结果返回。

### 2. MyBatis框架API

#### 2.1 SqlSessionFactoryBuilder

此组件负责根据MyBatis主配置文件构建SqlSessionFactory

#### 2.2 SqlSessionFactory

每一个MyBatis的应用程序都以一个SqlSessionFactory对象为核心，此组件负责创建SqlSession对象

#### 2.3 SqlSession

此组件包含所有执行sql语句操作的方法，用于执行已映射的sql语句

### 3. MyBatis配置文件

#### 3.1 SqlMapConfig.xml

主配置文件，用于指定数据库连接参数信息和框架信息，项目中只有1个该文件。

#### 3.2 SqlMapper.xml

映射文件，用于定义SQL语句的映射信息。有N个

### 4. MyBatis基本操作

#### 4.1 搭建MyBatis技术环境

为工程添加MyBatis的开发包和数据库驱动包

在src下添加MyBatis的主配置文件SqlMapConfig.xml

配置SqlMapConfig.xml，指定数据库连接参数与框架参数

利用MyBatis提供API，获取SqlSession对象

#### 4.2 获取SqlSession对象

```java
String path = "主配置文件URL";
Reader reader = Resources.getResourceAsReader(path);
// 构建SqlSessionFactory对象
SqlSessionFactoryBuilder ssfb  = new SqlSessionFactoryBuilder();
SqlSessionFactory ssf = ssfb.build(read);
//构建SqlSession对象
SqlSession ss = ssf.openSession();
```

#### 4.3 利用SqlSession实现CRUD操作

增加（Create），查询（Retrieve），更新（Update），删除（Delete）

根据数据库表编写实体类

编写SqlMapper.xml映射文件，定义SQL操作和映射信息

获取SqlSession对象，执行增删改查操作

提交事务（DML）

释放SqlSession对象资源













































































