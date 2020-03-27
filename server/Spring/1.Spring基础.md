### 1. Spring概述
Spring是一个开源的轻量级应用开发框架，其目的是用于简化企业应用程序的开发，降低侵入
性。

Spring提供的IOC和AOP功能，可以将组件类的耦合度降至最低，即解耦，便于系统的升级和
维护。

Spring的本质是管理应用中的对象，即创建对象和维护对象之间的关系。

### 2. Spring容器
在Spring中，任何的Java类和JavaBean都被当成Bean处理，这些Bean通过容器管理和使用。

Spring容器有BeanFactory和ApplicationContext两种类型。

#### 2.1 Spring容器的实例化
ApplicationContext继承自BeanFactory接口，拥有更多的企业级方法

加载工程classpath下的配置文件实例化。
`String xml = "配置文件路径";
ApplicationContext ac = new ClassPathXmlApplicationContext(xml);`

#### 2.2 Spring容器的使用
首先在容器配置文件applicationContext.xml中添加Bean定义。
`<bean id="标识符" class="Bean类型"></bean>	`
然后在创建容器对象后，调用getBean方法获取实例对象：`ac.getBean("标识符")`

### 3. Bean的作用域
Spring容器在实例化Bean时，可以创建以下作用域的Bean。

1. singleton：在Spring容器中一个Bean定义对应一个实例对象，**默认创建的就是单例的。**
2. prototype：一个Bean定义对应多个实例对象
3. request：在一次HTTP请求中，一个Bean定义对应一个实例对象
4. session：在一次HTTP Session中，一个Bean定义对应一个实例对象

Bean的作用域可以通过\<bean>定义的scope属性指定

### 4. Bean的生命周期

指定初始化回调方法：`<bean init-method=""/>`

指定销毁回调方法，仅适用于singleton模式的Bean：`<bean destroy-method=""/>`

在\<beans>标签中的default-init-method属性，可以为容器中的\<bean>指定初始化回调方法，也可以通过default-destroy-method属性为容器中的\<bean>指定销毁回调方法

### 5. Bean的延迟实例化
**默认是在容器实例化的同时将单例模式的Bean提前进行实例化**。

延迟实例化操作：在\<bean>声明时指定其属性lazy-init为true，一个延迟实例化的Bean将在第一次被用到时实例化。

注意：**Bean的延迟实例化仅适用于单例模式**（因为非单例的都是在用到时才会创建，所以也不需要被延迟）

在\<beans>标签中的default-lazy-init属性，可以为容器中的\<bean>指定延迟实例化特性

### 6. 基于注解的组件扫描
#### 6.1 什么是组件扫描
指定一个包路径，Spring会自动扫描此包及其子包中所有的组件类，当发现组件类定义前有特定的注解标记时，就将此组件纳入到Spring容器中管理，等价于原有的XML配置中的\<bean>定义。

组件扫描可以替代大量XML配置的\<bean>定义。

指定扫描包路径，组件扫描需要在XML配置文件中指定扫描父级package路径：
`<context:component-scan base-package="com.xms"/>`。

Spring容器会自动扫描指定包及其子包下所有的组件类，如果此组件类定义前有特定的注解标记，则会将此组件类实例化。

#### 6.2 自动扫描的注解标记

| 注解标记    | 描述           |
| ----------- | -------------- |
| @Component  | 通用注解       |
| @Repository | 持久层组件注解 |
| @Service    | 业务层组件注解 |
| @Controller | 控制层组件注解 |

#### 6.3 自动扫描组件的命名
当一个组件在扫描过程中被检测到时，会生成一个默认的ID值，默认ID值为小写开头的类名，也可以在注解标记中定义。

```java
@Repository("user")
public class Admin {}
```

#### 6.4 指定组件的作用域
Spring容器管理的组件默认作用域是"singleton"，如果需要其他的作用域可以使用@Scope注解，只需要在注解中提供作用域的名称即可。

```java
@Repository("emp")
@Scope("request")
public class Emp {}
```

#### 6.5 指定初始化和销毁回调方法
@PostConstruct和@PreDestroy注解分别用于指定初始化和销毁回调方法

```java
public class Emp {
    @PostConstruct
    public void init(){
        System.out.println("初始化方法执行");
    }
    @PreDestroy
    public void destroy(){
        System.out.println("销毁方法执行");
    }
}
```

#### 6.6 指定延迟实例化
默认是非延迟，如果需要指定延迟实例化操作，只需要将@Lazy注解的值指定为true即可

```java
@Lazy(true)
public class Emp{}
```

