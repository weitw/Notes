## JDBC-------Oracle数据库的连接及操作

java database connectivity (jdbc): java连接数据库的技术(负责连接数据库 与数据库类别无关)
JDBC定义了一套标准的接口,即访问数据库的通用API

#### 常用接口:    

 DriverManager 驱动管理类  java.sql.DriverManager;

 Connection; 连接(实现由厂商提供的驱动包完成)   java.sql.Connection;

 Statement; 语句对象 PreparedStatement; 语句对象  java.sql.Statement;

 ResultSet;  结果集    java.sql.ResultSet;

#### JDBC执行过程:

#####  1,加载驱动,创建连接

```java
Class.forName("oracle.jdbc.driver.OracleDriver");
String url = "jdbc:oracle:thin:@127.0.0.1:1521:xe";
String user = "system";
String password = "123456";
Connection conn=
	DriverManager.getConnection(url,user,password);
```
#####  2,创建语句对象

```java
Statement statement = conn.createStatement();
```
#####  3,执行SQL语句

```java
// 查询需要处理结果集
 ResultSet result= statement.executeQuery(sql); //查询
 	statement.executeUpdate();  //增删改 返回值为0,1 不需要处理结果集
```
#####  4,处理结果集
 	ResultSet result; //存放执行SQL语句之后的结果,初始指针位于行首
###### 		常用方法
 		next(); 	移动指针 (查找下一个记录) 返回值boolean
​		getXXX(字段名或字段顺序值(数字)); 	根据给定字段获取字段对应类型的数据 

```java
//将查询结果保存在结果集中
 	ResultSet result=statement.executeQuery(sql); 
```
#####  5,关闭连接
  遵循一个原则:  先打开的后关闭,后打开的先关闭
```java
   finally{
   if (result != null)
	{
	result.close(); //最后打开的先关闭
	}
	if (statement != null)
	{
	statement.close();
	}
	if (conn != null)
	{
	conn.close(); //最先打开的后关闭
	}
   }
```
#### 注意:

Class.forName("oracle.jdbc.driver,OracleDriver"); //jdk1.2以后不需要显示调用
当调用getConnection方法时会自动加载合适的驱动

String url= "jdbc : oracle : thin : @localhost : 1521 : xe";
@localhost:	本机ip 等于127.0.0.1		
1521:	 端口号
xe: 	数据库应用名

