### 1. Spring与MyBatis整合

Spring与MyBatis整合需要引入一个mybatis-spring.jar整合包，此整合包由Mybatis提供。此整合包提供以下与整合相关的API。

1. SqlSessionFactoryBean

   为整合应用提供SqlSession对象。

2. MypperFactoryBean

   根据指定的Mapper接口生成对应的实例对象

SqlSessionFactoryBean在applicationContext.xml中配置：

```xml
<bean class="org.mybatis.sprng.SqlSessionFactoryBean">
	<!--指定连接资源-->
    
    <!--指定映射文件-->
</bean>
```

MapperFactoryBean的配置方式

```xml
<bean id="empMapper" class="org.mybatis.spring.mapper.MapperFactoryBean">
	<property name="mapperInterface" value="com.xms.dao.EmpMapper"></property>
    <property name="sqlSession" ref=""></property>
</bean>
```



























































































