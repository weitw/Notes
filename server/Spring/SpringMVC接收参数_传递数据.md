### 1. 实战技巧

#### 1.1 接收请求参数

SpringMVC请求提交数据到控制器有以下方式

1. 使用HttpServletRequest获取

   可以在方法中定义参数

   `public void method(HttpServletRequest request, HttpServletResponse response)`

   Spring自动参数注入到HttpServletRequest中，所以我们才能利用这个参数获取请求信息。

   这种方法比较直接，有缺点（需要自己处理数据类型转换）

2. 使用@RequestParam注解

   Spring会自动参数注入到方法参数（名称一致）

   使用@RequestParam注解映射不一致的名称

   优点：参数类型自动转换，但可能出现类型转换异常

 3. 使用自动封装成Bean对象

    定义实体类，属性名必须与请求参数名相同

注意，在jsp中，`${ request.contextPath }`得到的是类似：`localhost:8080/Spring05/`，而`${ pageContext.reqquest.contextPath }`得到的是类似：`localhost:8080/Spring05`，区别就是后面是否有一个/，这个需要在表单提交地址时拼接url注意。

#### 1.2 向页面传值
当Controller组件处理后，需要向JSP页面传值时的方式

1. 直接使用HttpServletRequest或HttpSession

2. 使用ModelAndView对象
   在Controller处理方法完成后返回一个ModelAndView，包含显示视图名称和模型数据

3. 使用ModelMap参数对象
   在Controller处理方法中追加一个ModelMap类型参数

   注意：数据会利用HttpServletRequest的attribute传递到JSP页面

4. 使用@ModelAttribute注解
   在Controller方法的参数部分或属性的get方法上。这个注解标记不要理解为单纯的传递数据，更确切的说是绑定数据。

   比如，请求参数中有一个username，那么我们在定义方法时可以这样

   ```java
   public ModelAndView method(@ModelAttribute("username") String username){
       // 此时就已经绑定了，那么在响应页面中，可以使用${username}来获取这个username了，也就是说，这个注解既可以接收参数，也可以传递参数
       return new ModelAndView("hello");
   }
   // 案例演变，假如我们绑定的名字不是username，即@ModelAttribute("name") String username，此时的这个username并不是请求参数中的username，而是方法调用者（前端控制器）传递的一个空字符串""
   ```

#### 1.3 重定向	
SpringMVC默认采用转发方式定位视图，如果需要重定向方式，可以采用以下方式：

1. 使用RedirectView

   如果Controller的请求处理方法返回的是ModelAndView对象，可以使用RedirectView方式
   重定向，实例代码

   ```java
   public ModelAndView checkLogin(){
   	RedirectView view = new RedirectView("重定向URL");
   	return new ModelAndView(view);
   }	
   ```

2. 使用redirect:前缀

   如果Controller请求处理方法返回的是String类型，可以使用"redirect:前缀"方式重定向，实
   例代码

   ```java
   public String checkLogin(){
   	return "redirect:重定向URL";
   }
   ```

![image-20200306001820933](/home/exile/.config/Typora/typora-user-images/image-20200306001820933.png)







































































