## Spring事务处理

### 1. Spring事务处理
Spring框架能够全面的事务支持，它提供一致的事务管理
-提供简单易用的编程式事务管理的API	
-支持声明式事务管理

编程式事务
使用编程式事务时，Spring提供以下两种事务管理API
-TransactionTemplate
-PlatformTransactionManager

如果采用编程式事务管理，推荐使用	TransactionTemplate

TransactionTemplate与Spring中JdbcTemplate等模板风格相似，它也使用回调机制，将事
务代码与业务代码分离，便于开发者将精力集中在具体的业务编程上

public class EmpService{

private EmpDao empDao;
private TransactionTemplate transactionTemplate;

public void addEmps(){

transactionTemplate.execute(new TransactionCallback(){
public Object doInTransaction(TransactionStatus status){
//	业务代码
for(int i=0;i<5;i++){
empDao.add();
}
}
});

}

}	

声明式事务
Spring的声明式事务管理是通过Spring AOP实现的，使用时不需要修改原有的业务代码，只
需要	通过简单配置就可以追加事务控制功能，大多数Spring用户选择声明式事务管理，对程
序代码影响最小，也最符合非侵入理念

2.注解实现声明式事务
1）在配置文件中声明事务管理组件，开启事务注解扫描
<!-- 声明事务管理组件 -->
<bean id="" class="">
<property name="dataSource" ref=""/>
</bean>	

<!-- 开启事务注解支持 -->
<tx:annotation-driven transaction-manager=""/>

transaction-manager指定事务管理组件，需要根据数据库访问技术的不同选择不同的管理器
组件，例如：JDBC，MyBatis选择DataSourceTransactionManager，而Hibernate则选择
HibernateTransactionManager	

2）使用@Transactional注解
@Transactional可以用在类定义前和方法定义前，方法上的事务设置将优于类级别的事务设置

@Transactional注解有以下属性，在使用时可以根据需要指定
-propagation：事务传播，默认值是propagation_required
-isolation：事务隔离，默认值是isolation_default
-readOnly：只读/读写，默认值是可读写
-rollbackFor：遇到哪些异常回滚
-noRollbackFor：遇到哪些异常不回滚	

3.XML配置实现声明式事务			
-在配置文件中声明事务管理组件，配置事务作用的范围及类型

<!-- 声明事务管理组件 -->
<bean id="" class="">
<property name="dataSource" ref=""/>
</bean>	

<!-- XML配置声明式事务范围及类型 -->
<tx:advice id="" transaction-manager="">
<tx:attributes>
<tx:method name="" propagation=""/>
<tx:method name="" read-only=""/>
</tx:attributes>
</tx:advice>	

<aop:config>
<aop:advisor advice-ref="" pointcut=""/>
</aop:config>

4.事务回滚
默认情况下RuntimeException异常将触发事务回滚，任何CheckedException将不触发事务
回滚

常见RuntimeException和CheckedException如下：

RuntimeException：
NullPointerException
ClassCastException
NumberFormatException
IndexOutOfBoundsException

CheckedException：
ClassNotFoundException
IOException
NoSuchMethodException
NoSuchFieldException

对于CheckedException，需要手动指定异常类型，才能实现事务回滚

-使用注解实现声明式事务，按如下方式指定异常：
@Transactional(rollbackFor=ClassNotFoundException.class)	

-使用XML配置实现声明式事务时，按如下方式指定异常：
<tx:method name="" rollback-for="java.lang.ClassNotFoundException"/>	

5.事务传播
是指一个方法调用了另一个带有事务控制的方法，就需要指定事务传播的处理方案

6.事务隔离	
在数据库操作的过程中，如果两个事务并发执行，那么彼此之前的数据会发生影响，为了避免
这种并发冲突，需要将事务隔离开




