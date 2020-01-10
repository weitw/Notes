## JDBC分页
###  Oracle分页:
​			利用Oracle中的rownum(伪列),传入SQL语句,以获取分页查询结果	
Oracle中SQL核心语句:

```sql
 select * from( select e.* , rowmum rn
 from emp_xu e ) where rn between ?(开始行默认从1开始) and ?(结束行);
```
#### **计算公式** 
 pagesize: 每页记录条数 
 page 指定页数 -->1  2 3....
 起始:  beginValue: (page-1)\*pageSize+1;
 结束:   endvalue: page\*pagesize;

##### java实现核心代码:
```java
String sql="select * from(select e.* , rowmum rn from emp_xu e ) where rn between ? and ?";
 pStatement=conn.prepareStatement(sql);
 //计算
 int beginValue: (page-1)\*pageSize+1;	
 int  endvalue: page\*pagesize;
 pStatement.setInt(1,beginValue); //起始行
 pStatement.setInt(2,endvalue);	//结束行
 ResultSet result=pStatement.executeQuery();
```
### Mysql分页：
​			利用 limit 关键字 用来限制查询记录数的检索语句
 核心SQL语句:
```sql
 select * from emp_xu limit ?(起始行默认从0开始),?(每页显示的记录数);
```
####  **计算公式:**
 pagesize: 每页记录条数 
 page 指定页数 -->1  2 3....
 起始记录: beginValue: (page-1)*pageSize;

#####  java实现核心代码:
```java
 String sql="select * from emp_xu limit ?,?";
 pStatement=conn.prepareStatement(sql);
 // 计算起始页下标
 int beginValue = ((beginPage<=0?1:beginPage) - 1) *  pageSize;
 pStatement.setInt(1,beginValue); //起始行
 pStatement.setInt(2,pageSize);  //每页显示的记录数
 ResultSet result=pStatement.executeQuery();
```

 

 

 

 

 

 

 

 