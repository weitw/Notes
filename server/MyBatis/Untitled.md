### 1. SqlSession

此组件包含所有执行sql语句操作的方法，用于执行已映射的sql语句

MyBatis配置文件

1. SqlMapConfig.xml（一个）

2. SqlMapper.xml(N个)

   映射文件，用于定义SQL语句的映射信息

### 2. MyBatis基本操作

#### 2.1 搭建MyBatis技术环境

为工程添加MyBatis的开发包和数据库驱动包

在src下添加MyBatis的主配置文件SqlMapConfig.xml

配置SqlMapConfig.xml，指定数据库连接参数与框架参数

利用MyBatis提供API，获取SqlSession对象

#### 2.2 获取SqlSession对象

```java
String path = "主配置文件URL";
Reader reader = Resources.getResourceAsReader(path);
// 构建SqlSessionFactory对象
SqlSessionFactoryBuilder ssfb  = new SqlSessionFactoryBuilder();
SqlSessionFactory ssf = ssfb.build(read);
//构建SqlSession对象
SqlSession ss = ssf.openSession();
```

#### 2.3 利用SqlSession实现CRUD操作

增加（Create），查询（Retrieve），更新（Update），删除（Delete）

根据数据库表编写实体类

编写SqlMapper.xml映射文件，定义SQL操作和映射信息

获取SqlSession对象，执行增删改查操作

提交事务（DML）

释放SqlSession对象资源





























































