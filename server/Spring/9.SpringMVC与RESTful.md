### 1. SpringMVC对Ajax支持
为了便于接收和处理Ajax请求，SpringMVC提供JSON响应支持，可以很方便地将数据自动转换成JSON格式字符串给客户端。

SpringMVC中通过@RequetBody注解实现将JSON数据转换成Java对象，通过@ResponseBody注解实现将Java对象转换成JSON数据输出。

@ResponseBody注解的作用是将Controller的方法返回的对象通过适当的转换器转换为指定的格式，写入response对象的body区，通常用来返回JSON数据或者是XML数据。

注意：**使用注解之后不会再走视图解析器，而是直接将数据写入到输出流，它的效果等同于通过response对象输出指定格式的数据。**

@ResponseBody注解主要用于Controller组件的处理方法前，具体操作如下：

1. 引入jackson开发包，实例代码采用的是
   jackson-annotation-2.9.8.jar
   jackson-core-2.9.8.jar
   jackson-databind-2.9.8.jar

2. 在Spring的配置文件中定义`<mvc:annotation-driven/>`开启对注解的支持，在Controller处理方法前定义@ResponseBody注解

### 2. RESTful

#### 2.1 什么是RESTful
REST是英文Representational State Transfer的缩写，中文翻译为"表述性状态转移"，REST本身只是为分布式超媒体系统设计的一种架构风格，适合开发Web Service服务，没有任何技术或语言上的限制，REST软件架构之所以适合超媒体系统，是因为它可以把网络上所有的资源进行唯一的URL定位，资源类型没有限制，例如图片，Word文件，视频，文本，XML，HTML等。

REST架构是一个抽象的概念，目前主要基于HTTP协议实现，其目的是为了提高系统的可伸缩性，降低应用之间的耦合度，便于架构分布式处理程序。

#### 2.2 REST主要对以下两方面进行规范

1. 定位资源的URL风格，例如：http://baidu.com/image/12

2. 如何对资源操作
   采用HTTP协议规定GET，POST，PUT，DELETE动作处理资源的增删改查操作

   | Method | CRUD                   |
   | ------ | ---------------------- |
   | POST   | create, update, delete |
   | GET    | read                   |
   | PUT    | update, create         |
   | DELETE | delete                 |

符合REST约束风格和原则的应用程序或设计就是RESTful。

例如

| url    | method | 描述          |
| ------ | ------ | ------------- |
| /emp/1 | GET    | 查询id=1的emp |
| /emp/1 | DELETE | 删除id=1的emp |
| /emp/1 | PUT    | 更新id=1的emp |
| /emp   | POST   | 新增员工      |

#### 2.3 REST架构的主要原则

1. 网络上的所有数据都可以抽象为资源
2. 每个资源都有一个唯一的资源标识符
3. 同一资源具有多种表现形式（xml，json等）
4. 对资源的各种操作不会改变资源标识符
5. 所有的操作都是无状态

需求：
1.查询
URI：emps
请求方式：GET	

2.添加
2.1显示添加页面
URI：emp
请求方式：GET
2.2添加员工
URI：emp
请求方式：POST
添加完成后，重定向到list页面

3.删除
URI：emp/{id}
请求方式：DELETE

4.修改
4.1显示修改页面
URI：emp/{id}
请求方式：GET
4.2修改员工信息
URI：emp
请求方式：PUT
修改完成后，重定向到list页面

### 3. SpringMVC对RESTful的支持
利用@RequestMapping指定要处理请求的URI模板和HTTP请求的动作类型，利用@PathVariable将URI请求模板中的变量映射到处理器方法的参数上，利用Ajax，在客户端发出PUT，DELETE动作的请求。

@RequestMapping可以定义在Controller类前和处理方法前，主要用于指定Controller的方法处理那些请求
在RESTful应用中，@RequestMapping可以采用以下格式：
@RequestMapping(value="/emp/{id}",method=RequestMethod.GET)	

@PathVariable作用是将URI请求模板中的变量解析出来，映射到处理方法的参数上

@RequestMapping(value="/emp/{empno}",method=RequestMethod.GET)	
public String execute(@PathVariable("empno") int id){
//操作处理
return "";
}	

上述URI请求模板匹配/emp/1，/emp/1002等格式请求

静态资源访问处理
采用REST架构后，需要将web.xml中DispatcherServlet控制器拦截的请求设置为/，这样
会将css，js，image等静态资源进行拦截，发生404错误
解决上述问题的方法如下：
1）配置<mvc:resources/>
<mvc:resources mapping="请求URI" location="资源位置"/>
2）配置<mvc:default-servlet-handler/>	






