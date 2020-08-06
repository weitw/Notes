## JDK8.0(1.8)的新特性

### 1. Lambda表达式

lambda就是一个匿名函数，可以吧lambda表达式理解为是一段可以传递的代码（像数据一样传递）。利用lambda表达式可以写出更简洁，更灵活的代码。作为一种更紧凑的代码风格，使Java语言的表达能力得到了提升。

#### 1.1 概念

Lambda表达式在Java语言中引入了一个新的语法元素和操作符。这个操作符就是**->**，该操作符被称为Lambda操作符或者箭头符号。它将Lambda表达式分为两个部分：

- 左侧：指定了Lambda表达式需要的所有参数（即方法中需要的参数）
- 右侧：指定了Lambda体，即Lambda表达式要执行的功能

#### 1.2 语法格式

Lambda表达式的参数列表里面的数据类型可以省略不写，因为JVM编译器可以通过上下文推断出数据类型（类型推断）。

- 语法格式一

  ```java
  // 无参数无返回值
  Runnable r2 = ()-> System.out.println("HelloLambda");
  ```

- 语法格式二

  ```java
  // 有一个参数，无返回值
  Consumer<String> consumer2 = (s)-> System.out.println(s);
  ```

- 语法格式三

  ```java
  // 若只有一个参数，并且没有返回值，()可以省略
  Consumer<String> consumer2 = s-> System.out.println(s);
  ```

- 语法格式四

  ```java
  // 有两个以上的参数，有返回值，并且Lambda体中有多条语句，Lambda体必须要写{}
  Comparator<Integer> com1 = (x, y)-> {
      System.out.println("函数式接口");
      return x-y;
  };
  ```

- 语法格式五

  ```java
  // 若Lambda体中只有一条语句，return和{}都可以省略不写
  Comparator<Integer> com2 = (x, y) -> x-y;
  ```

#### 1.3 函数式接口

Lambda表达式需要函数式接口的支持。

函数式接口：接口中只有一个抽象方法的接口称为函数式接口。

可以使用注解@Functional Interface修饰，这个注解可以检查该接口是否为函数式接口

#### 1.4 Java8内置的四大核心函数式接口

- Consumer<T>：消费型接口

  `void accept(T t);`

- Supplier<T>：供给型接口

  `T get();`

- Function<T, R>：函数型接口

  `R apply(T);`

- Predicate<T>：断言型接口（判断用的）

  `boolean test(T t);`

### 2. 方法引用和构造器引用

#### 2.1 方法引用

若Lambda体中的内容已经有方法实现了，我们可以使用方法引用（可以理解为Lambda表达式另一种体现形式）

- 语法格式

  有三种格式，这三种格式都有限制条件，即引用的方法的参数列表和返回值都要和Lambda表达式中的参数列表和返回值一致。

  - 对象：：实例方法名

    ```java
    Consumer<String> con = (x)-> System.out.println(x);
    // 上面的代码其实可以改写为
    PrintStream ps = System.out;
    Consumer<String> con = (x)-> ps.println(x);
    con.accept("hello world");
    // Lambda体 System.out.println(x); 已经有方法可以实现该功能了，所以可以利用方法引用
    Consumer<String> con1 = ps::println;
    con1.accept("hello");
    ```

  - 类：：静态方法名

    ```java
    Comparator<Integer> com1 = (x, y) -> Integer.compare(x, y);
    System.out.println(com1.compare(2, 1));
    // 因为Comparator中的int compare(T o1, T o2)方法和Integer中的compare方法的返回值和参数列表相同，所以可以使用方法引用
    Comparator<Integer> com2 = Integer::compare;
    System.out.println(com2.compare(2, 5));
    ```

  - 类：：实例方法名

    ```java
    BiPredicate<String, String> bp1 = (str1, str2)-> str1.equals(str2);
    BiPredicate<String, String> bp2 = String::equals;
    // 使用这种格式需要有前提条件，上面的str1必须是equals()方法的调用者，str2必须作为参数传入这个方法中
    ```

#### 2.2 构造器引用

  ```java
  // 无参构造器引用
  Supplier<Employee> sup = ()-> new Employee();
  Supplier<Employee> sup2 = Employee::new;
  // 有参构造器引用
  Function<Integer, Employee> fun = (age)->new Employee(age);
  // 利用构造器引用
  Function<Integer, Employee> fun = Employee::new;
  System.out.println(fun.apply(23));
  ```

### 3. 接口中的默认方法和静态方法

例如

```java
public interface MyFun {
	// 默认方法
	default String getName() {
		return "呵呵";
	}
	// 静态方法
	public static void show() {
		System.out.println("接口中的静态方法");
	}
}
```

如果一个类的父类和它实现的接口类中有同样的方法，那么该类会选择父类中的方法执行。

### 4. 日期

#### 4.1 SimpleDateFormat线程不安全

Date()对象显示的日期样式不是我们需要的，一般会使用SimpleDateFormat来进行格式化，但是SimpleDateFormat是线程不安全的，因为这个这个类是继承与DateFormat的，DateFormat中有一个Calender属性，可以说SimpleDateFormat的格式化就是依赖于这个属性的。

SimpleDateFormat的format方法中将传入的Date对象会交给calendar属性（calendar.setTime(date);）；当A线程传入时间a调用format方法进行格式化，format方法还没执行完，此时B线程传入时间b调用format方法进行格式化，则A线程中的calendar的time就变成了B线程传入的时间b了，当执行format方法中的subFormat方法时，获取到的格式化的时间是不正确的。

Java8中可以使用LocalDate(日期)、LocalTime(时间)、LocalDateTime(日期时间)对象来处理日期时间。

#### 4.1 LocalDate的基本使用

```java
public class Test2 {
    public static void main(String[] args){
        // 获取当前日期
        LocalDate date = LocalDate.now();
        System.out.println(date);
        // 获取年月日
        int year = date.getYear();
        int month = date.getMonthValue();  // date.getMonth()获取到的是Month对象
        int day = date.getDayOfMonth();
        System.out.println(year+"-"+month+"-"+day);
        // 修改日期
        LocalDate newDate = date.withYear(2019).withMonth(12).withDayOfMonth(12);
        System.out.println("修改后的时间："+newDate);
        // 解析日期
        LocalDate parseDate = LocalDate.parse("2008-08-08");
        System.out.println("解析日期："+parseDate);
    }
}
```

结果：

![image-20200806095047810](/home/exile/.config/Typora/typora-user-images/image-20200806095047810.png)

注意：

- date.getMonth()获取到的是月份的英文单词，date.getMonthValue()才是获取数字的月份
- 解析日期要注意，日期格式必须为yyyy-MM-dd这种，比如"2008-8-8"这种是会抛出异常的，必须要是两位的月份和日。而且间隔必须是"-"不能是":"这个要注意，下面将的LocalTime的解析就是":"间隔了，要注意区分。

#### 4.2 LocalTime的基本使用

```java
public class Test2 {
    public static void main(String[] args){
        // 获取时间
        LocalTime time = LocalTime.now();
        System.out.println(time);
        // 获取时分秒
        int hour = time.getHour();
        int minute = time.getMinute();
        int second = time.getSecond();
        System.out.println(hour+":"+minute+":"+second);
        // 修改时间
        LocalTime newTime = time.withHour(12).withMinute(9).withSecond(34);
        System.out.println("修改后的时间"+newTime);
        // 解析时间
        LocalTime parseTime = LocalTime.parse("20:12:08");
        System.out.println(parseTime);
    }
}
```

结果：

![image-20200806095322318](/home/exile/.config/Typora/typora-user-images/image-20200806095322318.png)

注意：

- 解析日期要注意，日期格式必须为HH:mm:ss这种，比如"20:2:12"这种是会抛出异常的，必须要是两位的时分秒。而且间隔必须是":"不能是"-"，和LocalDate是不同的。

#### 4.3 LocalDateTime的基本使用

```java
public class Test2 {
    public static void main(String[] args){
        // LocalDateTime的使用
        LocalDateTime date = LocalDateTime.now();
        System.out.println(date);
        // 获取年月日，时分秒
        // 和上面的LocalDate和LocalTime一样。
        System.out.println(date.getYear()+"-"+date.getMonthValue()+"-"+date.getDayOfMonth()+" "+
                date.getHour()+":"+date.getMinute()+":"+date.getSecond());
        // 修改日期时间
        System.out.println(date.withYear(2009).withHour(22).withSecond(12));
        // 解析日期时间
        System.out.println(LocalDateTime.parse("2008-12-02T12:12:12"));
    }
}
```

结果：

![image-20200806100249930](/home/exile/.config/Typora/typora-user-images/image-20200806100249930.png)



注意：

- 获取和修改日期时间与LocalDate和LocalTime一样的用法。注意事项也一样
- 解析日期时间要注意，按照我们的习惯可能日期和时间之间是用空格隔开，比如："2008-12-02 12:12:12"，但是这样会抛出异常，必须用T来替代空格。

































