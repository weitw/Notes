### 1. 中文乱码解决方案

在表单提交时，如果遇到中文字符会出现乱码现象，Spring提供一个CharacterEncodingFilter
​过滤器，可以用于解决乱码问题。

CharacterEncodingFilter使用时需要注意以下问题

> 表单数据以POST方式提交
> 在web.xml中配置CharacterEncodingFilter过滤器
> 页面编码和过滤器指定的编码保持一致	

### 2. 异常处理
Spring处理异常方式有以下三种

1. 使用Spring提供的简单异常处理器SimpleMappingExceptionResolver
   只需要在Spring的配置文件中定义异常处理器即可

2. 实现HandlerExceptionResolver接口（自定义异常处理器）
   自定义异常处理器需要在Spring的配置文件中定义才可以使用，适合全局处理有"处理过程"
   的异常	

3. 使用@ExceptionHandler注解实现异常处理
   适合局部处理有"处理过程"的异常	

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