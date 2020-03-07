SpringMVC

### 1. MVC模型

#### 1.1 M-Model模型层。
模型（Model）的职责是负责业务逻辑，包含两层：业务数据和业务处理，比如实体类，Dao，
Service都属于模型层

#### 1.2 V-View视图
视图（View）的职责是负责显示页面和用户交互（收集用户信息），属于视图层的组件是不包
含业务逻辑和控制逻辑的JSP	

#### 1.3 C-Controller
控制器是模型层与视图层之间的桥梁，用于流程控制，比如Servlet中单一控制器ActionServlet

### 2. 什么是SpringMVC
SpringMVC是Spring框架中的一个功能模块，实现MVC结构，便于简单，快速开发MVC结构
的WEB程序，MVC提供的API封装WEB开发中常用的功能，简化WEB开发过程

### 3. SpringMVC核心组件
SpringMVC提供M，V和C相关的主要组件，具体如下：

DispatcherServlet（控制器，请求入口）
HandlerMapping（控制器，请求派发）
Controller（控制器，请求处理流程）
ModelAndView（模型，封装业务数据和视图）
ViewResolver（视图，视图显示处理器）

### 4. SpringMVC的处理流程
浏览器向服务器发送请求，请求交给前端控制器DispatcherServlet处理，前端控制器通过
HandlerMapping找到相对应的Controller组件来处理请求，执行Controller组件的约定方法，	
在约定方法中调用模型层组件来完成业务处理，约定方法返回一个ModelAndView对象，此
对象封装处理结果和跳转的视图名称信息，前端控制器接收到ModelAndView对象之后，调
用ViewResolver组件定位View（JSP），传递数据信息，生成响应页面

### 5. 基于XML配置的MVC应用

#### 5.1 搭建SpringMVC环境
创建WEB工程，导入SpringMVC相关开发包
Spring ioc，web，webmvc开发包
在src下添加Spring核心配置文件applicationContext.xml
名称可以自定义，例如spring-mvc.xml
#### 5.2 配置前端控制器

在web.xml中配置DispatcherServlet控制器组件

配置DispatcherServlet时，指定Spring核心配置文件

#### 5.3 定义Controller

Controller组件负责执行具体业务处理，编写时需要实现Controller接口及约定方法handleRequest

handleRequest方法返回一个ModelAndView对象，此对象封装模型数据和视图名称

ModelAndView(String viewName)
ModelAndView(String viewName,Model model)

viewName是视图名称，model是业务处理的数据

#### 5.4 定义请求映射HandlerMapping

通过HandlerMapping组件，DispatcherServlet控制器可以将客户端的HTTP请求映射到对应
的Controller

SimpleUrlHandlerMapping维护一个个HTTP请求和Controller映射关系列表（Map），根
据列表对应关系调用Controller

#### 5.5 定义视图解析器ViewResolver

ViewResolver组件，Controller组件返回一个ModelAndView对象，Spring中的视图名称以
名字为标识，视图解析器ViewResolver通过名字来解析视图

InternalResourceViewResolver：
UrlBasedViewResolver的子类，它支持InternalResourceView（对Servlet和JSP包装）以及
子类JstlView和TitleView响应类型

#### 5.6 示例

web.xml中

```xml
<!-- 请求入口 -->
<servlet>
    <servlet-name>dispatcherServlet</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath:applicationContext.xml</param-value>
    </init-param>
    <load-on-startup>1</load-on-startup>
</servlet>
<servlet-mapping>
    <servlet-name>dispatcherServlet</servlet-name>
    <url-pattern>*.do</url-pattern>
</servlet-mapping>
```

com.xms.controller.HelloController.java中的代码

```java
public class HelloController implements Controller {
	@Override
	public ModelAndView handleRequest(HttpServletRequest arg0, HttpServletResponse arg1) throws Exception {
		System.out.println("hello,spring mvc");
		return new ModelAndView("hello");
	}
}
```

applicationContext.xml中

```xml
<bean id="helloController" class="com.xms.controller.HelloController"></bean>
<!-- 定义HandlerMapping -->
<bean class="org.springframework.web.servlet.handler.SimpleUrlHandlerMapping">
    <!-- 定义URL关系映射 -->
    <property name="mappings">
        <props>
            <prop key="/hello/hello.do">helloController</prop>
        </props>
    </property>
</bean>
<!-- 定义视图解析器 -->	
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
    <property name="prefix" value="/WEB-INF/jsp/"></property>
    <property name="suffix" value=".jsp"></property>
</bean>
```

### 6. 基于注解配置的MVC应用

#### 6.1 Controller注解应用

推荐使用@Controller注解声明Controller组件，可以使得Controller控制器定义更加灵活，可以不用实现Controller接口，请求处理方法也可以灵活定义。

为了使@Controller注解生效，需要在Spring的XML配置文件中开启组件扫描定义：`<context:component-scan base-package="" />`

#### 6.2 RequestMapping注解应用

@RequestMapping注解可以用在类定义和方法定义上，表明此组件类和方法与哪一个请求对应。

为了使@RequestMapping注解生效，需要在Spring的XML配置中开启MVC注解扫描：`<mvc:annotation-driven />`

#### 6.3 示例

web.xml中的代码同上5.6

com.xms.controller.HelloController.java类中的代码

```java
@Controller
@RequestMapping("/hello")  // 命名空间为/hello的请求都交给这个类处理
public class HelloController {
    @RequestMapping("/hello.do")  // hello命名空间下的hello.do请求交给这个方法处理
    public ModelAndView hello() {
        System.out.println("hello");
        return new ModelAndView("jsp/hello");
    }
}
```

applicationContext.xml中的配置如下：

```xml
<!-- 指定扫描包路径 -->
<context:component-scan base-package="com.xms"></context:component-scan>
<!-- 开启RequestMapping注解 -->
<mvc:annotation-driven />
<!-- 定义视图解析器 -->
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
    <property name="prefix" value="/WEB-INF/"></property>
    <property name="suffix" value=".jsp"></property>
</bean>
```





















































































​	