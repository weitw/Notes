## 1. JDBC 概念

1. 概念：Java DataBase Connectivity，Java数据库连接

2. JDBC本质：sun公司定义的一套操作所有关系型数据库的规则，即接口。各个数据库厂商去实现这套接口，提供数据库驱动jar包。我们可以使用这套接口(JDBC)编程，真正执行的代码是驱动jar包中的实现类

## 2. JDBC执行步骤

实例

   ```java
		// 1. 导入驱动jar包
        // 2. 注册驱动
		//        Class.forName("com.mysql.jdbc.Driver");
        // 3. 获取数据库连接对象
        Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/test", "root", 	"passwd");
        // 4. 定义sql语句
        String sql = "insert into P (Pno, Pname, Color, Weight, City) values ('1', 'exile', 'red', 4.5, '南京')";
        // 5. 获取执行sql的对象Statement
        Statement stmt = conn.createStatement();
        // 6.　执行sql
        int count = stmt.executeUpdate(sql);
        // 7. 处理结果
        System.out.println(count);
        // 8. 释放资源
        stmt.close();
        conn.close();
   ```

注意上面代码中的注册驱动那一句。如果写那句的话，程序运行没有问题，但是会有一个警告，提示灭有必要导入，警告如下。所以导入驱动可以省略。

```java
Loading class `com.mysql.jdbc.Driver'. This is deprecated. The new driver class is `com.mysql.cj.jdbc.Driver'. The driver is automatically registered via the SPI and manual loading of the driver class is generally unnecessary.

```

## 3. 各个类介绍

### 3.1 DriverManager类

1. 注册驱动

2. 获取数据库连接

   方法：static Connection getConnection(String url, String user, String password)

   参数：

   > 1. url: 指定连接的路径
   >
   >    语法: jdbc:mysql://ip地址(域名):端口号/数据库名称
   >
   >    例子: jdbc:mysql://localhost:3306/test
   >
   >    注：如果连接的是本机的数据库，那么可以简写为jdbc:mysql:///数据库名称
   >
   >    例如：jdbc:mysql:///test
   >
   > 2. user: 用户名
   >
   > 3. password: 密码



















































