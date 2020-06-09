### 1. JSP基本语法
#### 1.1 JSP由来
为什么有JSP规范
Servlet技术产生以后，在使用时最麻烦的是使用大量的pw.print语句输出页面，这样形式
在系统变更，维护，预览效果时都不能方便快捷的完成任务，于是推出JSP这种技术，用来
将Servlet中负责显示的语句抽取出来

```java
class XxxServlet{
    ...service(){
        ......
        pw.println("<html>");
        ......
        pw.println("</html>");
        ......
    }
}	
```

#### 1.2 什么是JSP	
Sun公司制定的一种服务器端动态页面技术的组件规范，JSP是一个以".jsp"为后缀的文件
在该文件中，主要是HTML和少量的Java代码，JSP文件会被容器转换为一个Servlet类，
然后执行	

#### 1.3 JSP编写规范
1) 如何编写JSP

- 写一个以".jsp"为后缀的文件
- 在该文件中，可以包含如下的内容：
  -HTML（CSS，JavaScript）
  -注释
  -Java代码
  -指令
  -隐含对象	

2) JSP代码的书写规则
JSP页面中的HTML代码
-HTML标记
-CSS
-JavaScript
像编写HTML页面一样编写即可
作用：控制页面在浏览器中显示的效果
转译成Servlet时的规则：
转译成Servlet中service()方法的pw.write语句

3) JSP页面中的注释
语法：

- <!-- 注释内容 -->
  HTML注释，注释中的内容如果包含Java代码，这些Java代码会被执行
- <%-- 注释内容 --%>
  JSP特有的注释，如果注释的内容中出现Java代码，会忽略	

JSP页面中的Java代码
JSP页面中的Java代码，包含以下三种：

- JSP表达式
  语法规则：<%= ...... %>
  合法内容：变量，变量加运算符组合的表达式，有返回值的方法
  转译成Servlet时的规则：在service()方法中用pw.print语句输出该变量，表达式，
  方法的值	

  例如：

  \<p>The square root of 5 is <%=Math.sqrt(5)%>\</p>	

  转译成

  ```java
  pw.write("\<p>The square root of 5 is");
  pw.print(Math.sqrt(5));
  pw.write("\</p>");	
  ```

- JSP小脚本
  语法规则：<% ...... %>
  合法内容：能够写在方法里的Java代码片段都可以作为小脚本
  转译成Servlet时的规则：原封不动转译成为Servlet类的service()方法里面的一段
  代码

  例如：

  ```jsp
  <%
      String name = request.getParamater("name");
      if(name != null && !name.equals("")){
          %>
          <p>Your name is <%=name%></p>
          <%	
      }	
  %>
  ```

  转译成如下代码插入到service方法中

  ```java
  String name = request.getParamater("name");
  if(name != null && !name.equals("")){	
      pw.write("<p>Your name is ");
      pw.print(name);
      pw.write("</p>");
  }
  ```

- JSP声明
  语法规则：<%! ..... %>
  合法内容：成员属性或成员方法的声明
  转译成Servlet时的规则：转译成Servlet中成员属性或成员方法

  例如：

  ```jsp
  <%!
      public String getResult(){
      //......
      }
  %>	
  ```

  转译成

  ```java
  public class Index_JSP extends JSPBase{
      public String getResult(){
      //......
  }
  
  public void service(){
      //......
      }
  }
  ```

  编写位置：页面的任意位置
  作用：控制页面中可变内容的产生	

### 2. JSP页面中的指令	
语法规则：<%@指令名 属性=值%>
常用指令：
#### 2.1 page指令
- 作用：用于导包，设置页面属性

- 例如：

  ```jsp
  <%-- 导包 --%>
  <%@ page import="java.util.*"%>
  <%@ page import="java.util.*,java.sql.*"%>	
  
  <%-- 设置response.setContentType()方法的参数值 --%>
  <%@ page contentType="image/gif"%>
  
  <%-- 设置容器读取该文件时的解码 --%>
  <%@ page pageEncoding="UTF-8"%>	
  ```

#### 2.2 include指令

- 作用：在JSP页面转换成Servlet时，能够将其他文件包含进来，可以包含JSP文
  件，也可以是静态的HTML文件，通过此指令能方便的在每个JSP页面中包含导
  航栏，版权声明，logo等
- 语法：
  <%@ include file="url"%>
- 例如：
  <%@ include file="header.html"%>
  <%@ include file="footer.html"%>

#### 2.3 taglib指令

- 作用：定义一个标签库以及其自定义标签的前缀，需要导入standard.jar，jstl.jar
  两个包，控制JSP在转译成Servlet类时生成的内容

- 语法：

  <%@ taglib uri="" prefix=""%>

- 例如：
  <%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>

### 3. JSP页面中的隐含对象
#### 3.1 什么是隐含对象？
容器自动创建，在JSP文件中可以直接使用的对象。
作用：
JSP预先创建的这些对象可以简化对HTTP请求，响应信息的访问。

#### 3.2 按类型划分：

- 输入输出对象
  out（JSPWriter->输出的数据流）
  request（HttpServletRequest->请求信息）
  response（HttpServletResponse->响应信息）
- 作用域通信对象
  session（HttpSession->会话）
  application（ServletContext->全局的上下文对象）
  pageContext（PageContext->JSP页面上下文）
- Servlet对象
  page（Object->JSP页面本身）
  config（ServletConfig->Servlet配置对象）
- 异常对象
  exception（Throwable->捕获网页异常）				

#### 3.3 JSP运行原理
JSP是如何运行的。

JSP如何转换为Java。

静态页面转换为动态页面	

- 拷贝静态页面代码至JSP页面
- 添加page指令pageEncoding和contentType
- 修改页面内容与目标页面一致
- 将需要动态生成的内容删除，替换为Java代码		
  ​		
  ​		
  ​		
  ​		
  ​		
  ​		
  ​		
  ​		
  ​		
  ​	

​		