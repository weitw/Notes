### 2. Spring+SpringMVC+SpringJdbc应用

#### 2.1 窗创建工程，搭建SpringMVC和SpringJDBC技术环境

创建一个WEB工程，添加JDBC相关技术环境

引入数据库驱动包

引入DBCP连接池开发包

添加Spring相关技术环境

引入SpringIOC，web, webmvc, jdbc, tx开发包

在src下添加applicationContext.xml配置文件

在web.xml中配置DispatcherServlet主控制器

在web.xml中配置中文乱码过滤器CharacterEncodingFilter

#### 2.2 基于SpringJDBC实现DAO组件

根据数据表编写实体类

编写DAO组件

在Spring配置文件中配置JDBCTemplate组件

在DAO组件中注入JDBCTemplate对象

#### 2.3 编写和配置SpringMVC主要组件

编写Controller和请求处理方法

配置`<mvc:annotation-driven>`支持@RequestMapping

配置Controller

开启注解扫描，讲Controller组件扫描到容器中

需要DAO组件采用注入方式注入

在请求处理方法上使用@RequestMapping指定对应请求

配置ViewResoler

#### 2.4 编写JSP视图组件，利用JSTL标签和EL表达式显示数据



























































