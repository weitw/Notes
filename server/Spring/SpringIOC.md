## SpringIOC

### 1. 基础概念

IOC全称Inversion Of Control，被翻译成控制翻转，IOC是指程序中对象的获取方式发生转变，由最初的new方式创建，转变为由第三方框架创建，注入（DI）它降低对象之间的耦合度。

Spring容器采用DI方式实现IOC控制，IOC是Spring框架的基础和核心。

DI全称是Dependency Injection，被翻译成依赖注入，DI的基本原理是将一起工作具有关系的对象，通过方法参数传入，建立关系，因此容器的工作就是创建Bean对象时注入依赖关系。

IOC是一种思想，而DI是实现IOC的主要技术途径。
DI主要有两种注入方式，即**Setter注入和构造器注入**。

例如：现有com.xms.entity.Emp类

```java
public class Emp {
	private Integer id;
	private String name;
	// 省略getter和setter
}
```

#### 1.1 Setter注入

```xml
<bean id="emp" class="com.xms.entity.Emp">
    <!--以下两个值的注入是一样的效果-->
    <property name="id">
        <value>1001</value>
    </property>
    <property name="name" value="张三"/>
</bean>
```

#### 1.2 构造器注入

```xml
<bean id="dept" class="com.xms.entity.Emp">
    <!-- type属性是指定参数的类型 -->
    <constructor-arg index="0" type="java.lang.Integer">
        <!-- value属性的值默认是String类型 -->
        <value>1001</value>
    </constructor-arg>
    <constructor-arg index="1" value="张三"/>
</bean>
```

### 2. 自动装配
Spring容器可以自动装配（autowire）相互协作Bean之间的关联关系，autowire可以针对单个Bean进行设置，方便之处在于减少XML注入配置。

在配置文件中，可以在\<bean>标签中使用autowire属性指定自动装配规则，一共有三种类型值。

- byName：根据属性名自动装配，此选项将检查容器，根据名字查找与属性名一致的Bean，然后将其与属性自动装配（setter注入）
- byType：如果容器中存在一个与指定属性类型相同的Bean，则将与此属性自动装配（setter注入）	
- constructor：与byType方式类似，不同之处在于它应用于构造器注入

### 3. 参数值注入

现有com.xms.Test类

```java
public class Test{
    
	private Integer id;
	private String name;
	
	private Emp emp;
	
	private List<String> languages;
	private Set<String> cities;
	private Map<String,Object> scores;
	private Properties properties;
}
```

#### 3.1 注入基本值
\<value>标签可以通过字符串指定属性或构造器参数的值，容器将字符串从java.lang.String类型转换为实际的属性或构造器参数类型，然后给Bean对象注入。

```xml
<bean id="test" class="com.xms.Test">
	<property name="id" value="1001"/>
    <property name="name" value="张三"/>
</bean>
```

#### 3.2 注入Bean对象

注入外部Bean（引用方式，方便重用）

#### 3.3 注入集合
通过\<list>，\<set>，\<map>，\<props>标签可以定义和设置与Java类型中对应的List，
Set，Map及Properties的属性值。

#### 3.4 注入Spring表达式

#### 3.5 注入NULL或空字符串	

示例

```xml
<!--配置Emp-->
<bean id="emp" class="com.xms.entity.Emp">
	<property name="id" value="1001"></property>
    <property name="name" value="张三"></property>
</bean>

<!--参数值注入示例-->
<bean id="test" class="com.xms.Test">
    <!-- 1. 注入基本值-->
	<property name="id" value="1001"/>
    <property name="name" value="张三"/>
    
    <!-- 2. 注入Bean对象-->
    <!--因为上面已经定义过一次Emp，所以容器中已经有了该Bean对象，这儿直接引用已经有的Bean对象就可以了-->
    <property name="emp" ref="emp"></property>
    
    <!-- 3. 注入集合-->
    <!-- List -->
    <property name="languages">
        <list>
            <value>C++</value>
            <value>Python</value>
            <value>JavaScript</value>
        </list>
    </property>
		
    <!-- Set -->
    <property name="cities">
        <set>
            <value>杭州</value>
            <value>苏州</value>
            <value>成都</value>
            <value>武汉</value>
        </set>
    </property>

    <!-- Map -->
    <property name="scores">
        <map>
            <entry key="JSD1908">
                <value>78</value>
            </entry>
            <entry key="JSD1910" value="81"/>
            <entry key="JSD1912" value="85"/>
        </map>
    </property>

    <!-- Properties -->
    <property name="properties">
        <props>
            <prop key="user">root</prop>
            <prop key="password">1234</prop>
        </props>
    </property>
</bean>

```




