## Spring对JDBC整合支持
### 1. Spring对DAO提供哪些支持

1. Spring对DAO异常提供统一处理
2. Spring对DAO编写提供支持的抽象类
3. 减少DAO编码量，提高编程效率

### 2. Spring对DAO异常支持
Spring把特定某种技术的异常，如SQLException，统一转换为自己的异常，异常以
DataAccessException为父类，它封装原始的异常对象，不会丢失原始错误信息

DataAccessException继承于RuntimeException，是非检查异常，不会因为没有处理异常
而出现编译错误，如果异常必须要自定义处理，可以用拦截器统一处理

### 3. Spring对DAO编写支持
Spring为了便于以一种一致的方式使用各种数据库访问技术，如JDBC，SpringJDBC，
MyBatis，Hibernate，Spring提供一套抽象的DAO类，通过DAO类提供的方法可以获得数据
库访问技术相关的数据源和其他配置信息

- JdbcTemplate：封装常用JDBC操作方法

- JdbcDaoSupport：JDBC数据库访问对象的基类

- HibernateTemplate：封装常用Hibernate方法

- HibernateDaoSupport：Hibernate数据库访问对象的基类

JdbcDaoSupport
利用JDBC技术编写DAO的父类，通过此类提供的方法可便于获取Connection和JdbcTemplate

JdbcDaoSupport使用时需要注入一个DataSource

JdbcTemplate
封装了连接获取以及连接释放等工作，从而简化我们对JDBC的使用避免忘记关闭连接等错误

### 4. 如何编写DAO组件
基于SpringJdbc技术编写DAO组件可以采用以下两种方式：

- DAO**继承JdbcDaoSupport**，通过**getJdbcTemplate方法**获取**JdbcTemplate对象**，需要
  在DAO实现类中注入一个DataSource对象来完成JdbcTemplate的实例化

  ```java
  @Repository
  public class DeptDao extends JdbcDaoSupport {
  	@Resource
  	public void setJt(JdbcTemplate jt) {
  		super.setJdbcTemplate(jt);
  	}
  	
  	public List<Dept> findAdll(){
  		String sql = "select * from dept";
  		return this.getJdbcTemplate().query(sql, new DeptRowMapper());
  	}
  	
  	class DeptRowMapper implements RowMapper<Dept>{
  
  		@Override
  		public Dept mapRow(ResultSet rs, int index) throws SQLException{
  			Dept dept = new Dept();
  			dept.setDeptno(rs.getInt("deptno"));
  			dept.setDname(rs.getString("dname"));
  			return dept;
  		}
  		
  	}
  ```

  

- DAO不继承JdbcDaoSupport，在Spring的容器中配置一个JdbcTemplate的Bean，然后
  注入给DAO组件

  例子

  ```java
  @Repository  // 注解，表示将类交给容器处理
  public class EmpDao{
      @Resource  // 注入
  	private JdbcTemplate jdbcTemplate;
  	
  	// 查询所有员工
  	public List<Emp> findAll(){
  		String sql = "select * from emp";
  		return jdbcTemplate.query(sql, new EmpRowMapper());
  	}
      
      // 根据员工号查询员工
  	public Emp findByEmpno(int empno) {
  		String sql = "select * from emp where empno=?";
  		return jdbcTemplate.queryForObject(sql, new Object[] {empno}, new EmpRowMapper());
  	}
  	
  	// 添加员工
  	public void save(Emp emp) {
  		String sql = "insert into emp(ename,salary,bonus,hiredate,deptno) values(?,?,?,?,?)";
  		Object[] parameters = {emp.getEname(), emp.getSalary(),
  				emp.getBonus(), emp.getHiredate(), emp.getDeptno()};
  		jdbcTemplate.update(sql, parameters);
  	}
  	
  	// 更新员工信息
  	public void update(Emp emp) {
  		String sql = "update emp set ename=?,salary=?,"
  				+ "bonus=?,hiredate=?,deptno=? where empno=?";
  		Object [] parameters = {emp.getEname(),emp.getSalary(),
  				emp.getBonus(),emp.getHiredate(),emp.getDeptno(),emp.getEmpno()};
  		jdbcTemplate.update(sql, parameters);
  	}
  	
  	// 删除员工
  	public void delete(int empno) {
  		String sql = "delete from emp where empno=?";
  		jdbcTemplate.update(sql, empno);
  	}
  	
  	class EmpRowMapper implements RowMapper<Emp>{
  		@Override
  		public Emp mapRow(ResultSet rs, int index) throws SQLException {
  			Emp emp = new Emp();
  			emp.setEmpno(rs.getInt("empno"));
  			emp.setEname(rs.getString("ename"));
  			emp.setSalary(rs.getDouble("salary"));
  			emp.setBonus(rs.getDouble("bonus"));
  			emp.setHiredate(rs.getDate("hiredate"));
  			emp.setDeptno(rs.getInt("deptno"));
  			return emp;
  		}
  }
  ```

  为了实现jdbcTemplate值的注入，需要在Spring容器的配置文件中写配置

  ```java
  <util:properties id="db" location="classpath:db.properties"/>
  
  <bean id="ds" class="org.apache.commons.dbcp2.BasicDataSource">
          <property name="driverClassName" value="#{db.MySQL_Driver}"/>
          <property name="url" value="#{db.MySQL_Url}"/>
          <property name="username" value="#{db.MySQL_User}"/>
          <property name="password" value="#{db.MySQL_Pwd}"/>
  </bean>
  
   <!-- 定义JdbcTemplate -->
   <bean class="org.springframework.jdbc.core.JdbcTemplate">
              <property name="dataSource" ref="ds"/>
   </bean>
  
   <context:component-scan base-package="com.xms"/>
  ```

  











































































