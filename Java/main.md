[TOC]

### 集合

#### 1. Map

> Map的key必须是唯一的，如果重复了，那么后面put的值会覆盖之前的值

##### 1.1 创建一个HashMap对象

> HashMap<Object, Object> map = new HashMap<>();

##### 1.2 常用方法

| **方法摘要**     |                                                              |
| ---------------- | ------------------------------------------------------------ |
| ` void`          | `clear()`           从此映射中移除所有映射关系。             |
| ` Object`        | `clone()`           返回此 `HashMap` 实例的浅表副本：并不复制键和值本身。 |
| ` boolean`       | `containsKey(Object key)`           如果此映射包含对于指定键的映射关系，则返回 `true`。 |
| ` boolean`       | `containsValue(Object value)`           如果此映射将一个或多个键映射到指定值，则返回 `true`。 |
| ` V`             | `get(Object key)`           查找映射中key的value             |
| ` boolean`       | `isEmpty()`           如果此映射不包含键-值映射关系，则返回 `true`。 |
| ` Set<K>`        | `keySet()`           返回该map中所有的key                    |
| ` V`             | `put(K key, V value)`           在此映射中关联指定值与指定键。 |
| ` V`             | `remove(Object key)`           从此映射中移除指定键的映射关系（如果存在）。 |
| ` int`           | `size()`           返回该map的键值对数                       |
| ` Collection<V>` | `values()`           返回该map中所有的value                  |

##### 1.3 HashMap的遍历

```java
for (int key : map.keySet()) {
    System.out.println(key + ": " + map.get(key));
}
```

### 2. ArrayList

#### 2.1 常用方法

| **方法摘要** |                                                              |
| ------------ | ------------------------------------------------------------ |
| ` boolean`   | `add(E e)`           将指定的元素添加到此列表的尾部。        |
| ` void`      | `add(int index, E element)`           将指定的元素插入此列表中的指定位置。 |
| ` void`      | `clear()`           移除此列表中的所有元素。                 |
| ` Object`    | `clone()`           返回此 `ArrayList` 实例的浅表副本。      |
| ` boolean`   | `contains(Object o)`           如果此列表中包含指定的元素，则返回 `true`。 |
| ` E`         | `get(int index)`           返回此列表中指定位置上的元素。    |
| ` int`       | `indexOf(Object o)`           返回此列表中首次出现的指定元素的索引，或如果此列表不包含元素，则返回 -1。 |
| ` boolean`   | `isEmpty()`           如果此列表中没有元素，则返回 `true`    |
| ` E`         | `remove(int index)`           移除此列表中指定位置上的元素。 |
| ` boolean`   | `remove(Object o)`           移除此列表中首次出现的指定元素（如果存在）。 |
| ` E`         | `set(int index, E element)`           用指定的元素替代此列表中指定位置上的元素。 |
| ` int`       | `size()`           返回此列表中的元素数。                    |
| ` Object[]`  | `toArray()`           按适当顺序（从第一个到最后一个元素）返回包含此列表中所有元素的数组。 |

### 3. HashSet

#### 3.1 常用方法

| **方法摘要**   |                                                              |
| -------------- | ------------------------------------------------------------ |
| ` boolean`     | `add(E e)`           如果此 set 中尚未包含指定元素，则添加指定元素。 |
| ` void`        | `clear()`           从此 set 中移除所有元素。                |
| ` Object`      | `clone()`           返回此 `HashSet` 实例的浅表副本：并没有复制这些元素本身。 |
| ` boolean`     | `contains(Object o)`           如果此 set 包含指定元素，则返回 `true`。 |
| ` boolean`     | `isEmpty()`           如果此 set 不包含任何元素，则返回 `true`。 |
| ` Iterator<E>` | `iterator()`           返回对此 set 中元素进行迭代的迭代器。 |
| ` boolean`     | `remove(Object o)`           如果指定元素存在于此 set 中，则将其移除。 |
| ` int`         | `size()`           返回此 set 中的元素的数量（set 的容量）。 |

### 4. LinkedList

#### 4.1 常用方法

| **方法摘要** |                                                              |
| ------------ | ------------------------------------------------------------ |
| ` boolean`   | `add(E e)`           将指定元素添加到此列表的结尾。          |
| ` void`      | `clear()`           从此列表中移除所有元素。                 |
| ` Object`    | `clone()`           返回此 `LinkedList` 的浅表副本。         |
| ` boolean`   | `contains(Object o)`           如果此列表包含指定元素，则返回 `true`。 |
| ` int`       | `indexOf(Object o)`           返回此列表中首次出现的指定元素的索引，如果此列表中不包含该元素，则返回 -1。 |
| ` boolean`   | `offer(E e)`           将指定元素添加到此列表的末尾（最后一个元素）。 |
| ` E`         | `peek()`           获取但不移除此列表的头（第一个元素）。    |
| ` E`         | `pop()`           从此列表所表示的堆栈处弹出一个元素。       |
| ` void`      | `push(E e)`           将元素推入此列表所表示的堆栈。         |
| ` E`         | `remove()`           获取并移除此列表的头（第一个元素）。    |
| ` int`       | `size()`           返回此列表的元素数。                      |
| ` Object[]`  | `toArray()`           返回以适当顺序（从第一个元素到最后一个元素）包含此列表中所有元素的数组。 |


### 异常及处理

#### 1. throw关键字

> 抛出指定的异常。
>
> - 格式：`throw new XxxException("产生异常的原因");`
>
>   > **注意**:
>   >
>   > - throw关键字必须写在方法的内部
>   >
>   > - XxxException必须是Exception或者它的子类
>   >
>   > - throw抛出了异常，那么就必须要处理异常
>   >
>   >   > - 如果异常是RuntimeException类或者它的子类，那就不用处理，默认交给JVM处理
>   >   >
>   >   > - 否则必须用throws或者try...catch...处理

#### 2. Objects非空判断

> 在检验参数是否为空时，可以使用下面的方法
>
> `Objects.requireNonNull(obj)`，该方法的源码。
>
> ![Objects.requireNonNull](./img/Objects.png)
>
> 例如
>
> ```java
> int getIndex(int[] arr, index) {
>     Objects.requireNonNull(arr, "传递的数组是null");
>     Objects.requireNonNull(index);
> }
> ```

#### 3. throws关键字

> 这是处理异常的第一种方法：交给别人处理
>
> - 作用：使用throws声明异常，然后交给该方法的调用者，最后交给JVM--中断处理
>
> - 使用格式：
>
> ```java
> 修饰符　返回值类型　方法名(参数列表)　throws XxxException, ....{
> throw new XxxException(".....");
> .....
> }
> ```
> - 注意：
>   1. throws关键字必须写在方法声明处
>   
>   2. throw关键字后边声明的异常必须是Exception或者其子类
>   
> 3. 方法内部如果抛出了多个异常异常对象，那么就要在throws后加几个异常对象。如果多个异常对象之间存在父子关系，则只需要声明父类异常
>   
>   4. 声明的异常要么是交给JVM处理，要么是自己写try...catch...处理
>   
> - 例子
>
> ![ThrowsDemo](./img/ThrowsDemo.png)
>

#### 4. try...catch...

> - 格式：
>
> ```java
> try {
> ....
> } catch (定义一个异常的变量，用来接受try中抛出的异常对象){
> ...
> }
> ```
>   - 注意：try 中可能会抛出多个异常对象，那么就要用多个catch来处理
>
>   - Throwable类中国定义了３个异常处理的方法
>
>    > 1. String getMessage()  返回此throwable的简短描述
>    > 2. String toString() 返回此throwable的详细消息字符串
>    > 3. void printStackTrace() JVM打印就是使用了该方法，信息是最多的。
>   
>   - 例如
> ![TryCatchDemo](./img/TryCatchDemo.png) 
>
>   结果是　
>
> ![TryDemoResult](./img/TryDemoResult.png)

#### 5. finally

> 无论是否发生异常都会执行的代码块，不能单独使用，只能和try...catch搭配使用

