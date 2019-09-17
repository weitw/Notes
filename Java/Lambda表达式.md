### Lambda表达式初试

1. 示例

   创建多线程并打印

   ```java
   // 方法一：可以创建一个Thread的子类来实现
   // 方法二：可以实习三Runnable的接口来使用
   // 方法三：匿名内部类
   new Thread(new Runnable {
       @Override
       public void run() {
           System.out.println(Thread.currentThread().getName() + "创建新线程");
       }
   }).start();
   
   // 现在可以使用lambda表达式
   new Thread(()->{
       System.out.println(Thread.currentThread().getName() + "创建新线程");
       }
    ).start()
   ```



###  Lambda表达式的标准格式

1. 格式：(参数列表) -> {一些重写的代码};

2. 解释：

   ()：接口中抽象方法的参数列表

   ->：传递的意思，把参数传递给方法体

   {}：重写接口的抽象方法的方法体



### 有参数的lambda表达式

1. 例子：在数组中定义几件商品，然后升序打印

2. 定义一个Goods类

   ```java
   // Goods类
   public class Goods {
       private String name;
       private int price;
   
       Goods() {
       }
   
       Goods(String name, int price) {
           this.name = name;
           this.price = price;
       }
       @Override
       public String toString() {
           return "Goods{" +
                   "name='" + name + '\'' +
                   ", price=" + price +
                   '}';
       }
   ｝
   ```

   在Main.java中创建类对象使用

   ```java
   Goods[] goods = {
       new Goods("a0", 8000),
       new Goods("a1", 9837),
       new Goods("a2", 5932)
   };
   // 匿名对象
   Arrays.sort(goods, new Comparator<Goods>() {
       @Override
       public int compare(Goods g1, Goods g2) {
           return g1.getPrice() - g2.getPrice();
       }
   });
   for (Goods good : goods) {
       System.out.println(good);
   }
   ```

   在Main.java中使用lambda表达式

   ```java
   // 用lambda表达式
   Arrays.sort(goods, (Goods g1, Goods g2) -> {
       return g1.getPrice() - g2.getPrice();
   });
   for (Goods good : goods) {
       System.out.println(good);
   }
   ```

   两种方法输出结果都是一样的

   ```java
   // 结果
   Goods{name='a2', price=5932}
   Goods{name='a0', price=8000}
   Goods{name='a1', price=9837}
   ```



### lambda表达式省略格式＆前提

   1. 省略格式。lambda表达式（可推导，可省略），凡是根据上下文推导出的内容，都可以省略书写。
   
      可以省略的内容：
   
      1. (参数列表)：括号中参数列表的数据类型可以不写（因为定义接口的方法，方法中的参数列表肯定是确定了数据类型的）
      
      2. (参数列表)：括号中的参数如果只有一个，那么类型和()都可以省略
      
      3. {代码}：如果{}中的代码只有一行，无论是否有返回值，都可以省略{}、return、分号
      
         ```java
         // 为简化前lambda表达式
         Arrays.sort(goods, (Goods g1, Goods g2) -> {
             return g1.getPrice() - g2.getPrice();
         });
         // 根据简化条件１，可以简化为下面的样子
         Arrays.sort(goods, (g1, g2) -> {
             return g1.getPrice() - g2.getPrice();
         });
         // 根据简化条件３，可以简化为下面的样子
         Arrays.sort(goods, (g1, ) -> g1.getPrice() - g2.getPrice()});
         ```
      
      2. 前提。lambda的语法非常简介，完全没有面向对象复杂的束缚，但是使用时候有几个问题
      
         1. 使用lambda必须具有接口，且要求接口中有且仅有一个抽象方法。
      
            无论是JDK内置的Runnable、Comparator接口还是自定义的接口，只有当接口中的抽象方法存在且唯一时，才可以使用lambda。
      
         2. 使用lambda笔试具有上下文推断
      
            也就是方法的参数或局部变量类型必须为lambda对一个的接口类型，才能使用lambda作为该接口的实例
      
         备注：有且仅有一个抽象方法的接口，成为**函数式接口**