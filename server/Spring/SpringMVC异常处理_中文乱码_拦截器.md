### 1. 中文乱码解决方案

在表单提交时，如果遇到中文字符会出现乱码现象，Spring提供一个CharacterEncodingFilter
​过滤器，可以用于解决乱码问题。

CharacterEncodingFilter使用时需要注意以下问题

- 表单数据以POST方式提交
- 在web.xml中配置CharacterEncodingFilter过滤器
- 页面编码和过滤器指定的编码保持一致	

### 2. 异常处理
Spring处理异常方式有以下三种

1. 使用Spring提供的简单异常处理器SimpleMappingExceptionResolver
   只需要在Spring的配置文件中定义异常处理器即可

   例如在applicationContext.xml中配置
   
   ```xml
   <bean class="org.springframework.web.servlet.handler.SimpleMappingExceptionResolver">
       <property name="ExceptionMappings">
           <props>
               <prop key="java.lang.NumberFormatException">error</prop>
           </props>
       </property>
   </bean>
   ```
   
   在上面的例子中，该异常表示的是全局变量，一旦程序中出现了NumberFormatException异常，那么就会转到error.jsp页面，而不是出现一个显示代码具体错误的页面。当然可以其他的异常类来进行处理
   
2. 实现HandlerExceptionResolver接口（自定义异常处理器）。自定义异常处理器需要在Spring的配置文件中定义才可以使用，适合全局处理有"处理过程"的异常	

   例如自定义一个异常类MyExceptionResolver

   ```java
   public class MyExceptionResolver implements HandlerExceptionResolver {
   	@Override
   	public ModelAndView resolveException(HttpServletRequest request, HttpServletResponse response,
   			Object obj, Exception ex) {
           // 该方法中的obj是程序中出现异常的方法对象，ex是出现的异常类型
   		System.out.println(obj);
   		System.out.println(ex);
   		String message;
   		if (ex instanceof NumberFormatException) {
   			System.out.println("数据转换异常");
   			message = "数据转换异常";
   		} else if (ex instanceof IndexOutOfBoundsException) {
   			System.out.println("下标越界异常");
   			message = "下标越界异常";
   		} else {
   			System.out.println("其他异常");
   			message = "其他异常";
   		}
   		request.setAttribute("error", message);
   		return new ModelAndView("error");
   	}
   }
   ```

   在applicationContext.xml中配置

   ```xml
   <bean class="com.xms.exception.MyExceptionResolver"></bean>
   ```

3. 使用@ExceptionHandler注解实现异常处理。适合局部处理有"处理过程"的异常

   ```java
   @ExceptionHandler
   public String test3(Exception ex, HttpServletRequest request) throws Exception {
       System.out.println(ex);
       if (ex instanceof ClassNotFoundException) {
           System.out.println("类找不到");
           request.setAttribute("error", "类找不到异常");
       } else {
           throw ex;
       }
       return "error";
   }
   ```

   注意，这种异常处理方法只作用于该方法所在的类中，所以只能处理局部的异常。这种方式可以在applicationContext.xml中配置

### 3. 拦截器

拦截器接口，拦截器必须实现HandlerInterceptor接口

1. preHandle()
   处理器执行前调用，方法返回true表示会继续调用其他拦截器或处理器，返回false表示中断流
   程，不会执行后续拦截器和处理器

2. postHandle()
   处理器方法执行后，视图处理器调用前，此时可以通过ModelAndView对象对模型数据或视
   图进行处理

3. afterCompletion()
   整个请求处理完毕后调用，如性能监控中可以在此记录结束时间，输出消耗时间，可以进行资
   源清理

注意：只有preHandle返回true时才会执行postHandle()和afterCompletion()

拦截器的配置

```xml
<mvc:interceptors>
    <mvc:interceptor>
        <!-- 需要经过拦截器的URL -->
        <mvc:mapping path=""/>
        <!-- 不需要经过拦截器的URL -->
        <mvc:exclude-mapping path=""/>
        注意：URL不可以写相对路径，绝对路径是从应用名之后开始
        <!-- 拦截器组件 -->
        <bean class=""/>
    </mvc:interceptor>
</mvc:interceptors>	
```

提示：定义拦截器，实现HandlerInterceptor接口，需要实现定义的全部抽象方法，如果只需
要某一个方法，可以继承HandlerInterceptorAdapter