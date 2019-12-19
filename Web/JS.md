### 1. js概述

js全称：javascript，一门客户端脚本语言

- js可以直接切入在HTML页面中，由浏览器解释执行，不进行预编译。
- 用于向页面添加动态交互行为和效果
- 具有与Java语言类似的语法，是一种网页的编程语言

#### 1.1 js操作的两大方向

1. DOM（HTML文档对象）
2. BOM（浏览器对象）

#### 1.2 特点

1. 解释执行

   不需要预编译，逐行执行

2. 基于对象

   内置了大量的现成对象

#### 1.3 作用

1. 实现客户端数据简单的计算
2. 客户端表单合法性验证
3. 可以添加浏览器事件的触发
4. 网页特殊显示效果的制作
5. 实现服务器的异步数据提交  （Ajax异步提交）

#### 1.4 遵循的es规范（es6）

1. 严格区分大小写
2. 变量取名由数字、字母、下划线、$组成，不能以数字开头，尽可能使用驼峰命名法

#### 1.5 js写法

1. 行内式（定义事件）

   在事件中定义操作，直接写js代码

   写法：

   ```html
   <标签 事件名=”js函数();“></标签>
   ```

   事件

   - onclick：鼠标单击
   - ondbclick：鼠标双击
   - onmouseover：鼠标移入
   - onmouseout：鼠标移出
   - onkeydom：键盘按下
   - onkeyup：键盘抬起
   - onblur：失去焦点
   - onfocus：获取焦点

2. 内部式（嵌入式）

   将js代码写在页面中的\<script>标签内

   写法

   ```js
   // 1.页面中添加<script>标签，在标签中写js脚本代码
   function 函数名([参数]){
       函数体;
   }
   // 2.使用行内式给事件添加函数，调用函数：函数名();
   ```

   不需要页面也可以直接在控制台（console）写js代码

   Enter回车会执行代码，可以用shift+enter换行。

3. 外部式（文件调用）

   将js代码位于单独的.js文件中（注意保存的编码）

   写法

   ```html
   // 1.在js文件中写js代码（定义函数）
   // 2.将js文件引入到当前页面中，
   <script src="js文件路径"></script>
   // 3.在行内式中添加事件，调用函数
   ```

### 2. js的组成

#### 2.1 变量和函数

##### 2.1.1 变量

js是弱类型语言，使用关键字var声明。

形如：

```js
var a = 1;  // number类型
var s = "张三";  // string类型

// 拆：
var a;  // 声明变量a,没有类型
var a = 1;  // 声明并初始化a,a为number类型
a = "张三";  // 此时a的类型变为了string

typeof 变量名;  // 验证变量的类型
```

*注意事项*

- js是弱类型语言，不同的变量类型会根据数值自动给定类型
- 变量本身是没有类型的，统一用关键字var声明，变量的值是有类型的
- 使用“=”进行复制，没有初始化的变量自动取值为undefined
- js存在变量声明提升（js会根据不同的值自动提升转换为对应的数据类型）

##### 2.1.2 全局函数

所有的js对象都可以使用

parseInt()   parseFloat  isNaN()

eval("js代码")  执行函数

- 只接收合法的表达式和语句
- 只接收原始的字符串

#### 2.2 变量的数据类型

作用域（定义变量可以用var / let / const / 无）：

- var声明的变量可以修改，不初始化输出undefined，有作用域

  定义在函数内部，属于私有变量，作用于整个函数体。

  定义在函数外部，属于全局变量，作用于整个js中，存在变量提升

- let是块级作用域，函数内部使用let定义后，对函数外部无影响

- const定义的变量初始化以后，不可以修改，属于常量

- 没有任何关键字声明的变量，属于全局变量。

1. 基本类型（number、string、boolean）

   - number：不区分整数和小数

   - string：一对单引号或者双引号包裹的字符串

     单双引号要交替使用，特殊字符需要转义

     常用函数

     ```js
     // 返回指定字符串a在str中第一次出现的位置，从fromIndex开始找
     str.indexOf("a",[fromIndex]);
     // 将指定字符串替换为指定字符串，替换第一个，属于不完全替换
     str.replace(oldStr, newStr); // 替换之后，原字符串依然没有改变，该方法只是返回了一个新的字符串
     ```

   - boolean：ture、false;

     boolean参与算数运算可以自动作为数值，true为1，false为0

2. 特殊类型（undefined、none）

   - undefined：变量声明未初始化，该变量的值和类型均为undefined
   - null：代表无值或者无对象，可以通过一个变量赋值为null来清空变量的内容

3. 对象类型（object）

   - 内置对象
   - 外部对象
   - 自定义对象

### 3. 类型转换

1. 自动转换（直接转换属于默认规则）

   - number + string = string
   - string + boolean  = string
   - number + boolean = number   // true为1, false为0
   - boolean + boolean = number  // 比如两个true相加：2

2. 强制转换（利用类型转换函数）

   - toString()：可以将任何类型转换为string类型，使用该方法会返回一个字符串类型，但是原数据本身的类型是没有改变的。

   - parseInt()：强制转换为整数，全局函数（类似Java中的静态方法，不需要用变量去调用），带有**截取功能**（去掉小数点后面的内容）

     ```js
     注意：NaN（Not a Number）不是一个数字
     console.log(parseInt("a.j3"));  // 返回的结果是NaN
     parseInt("3.a3");  // 小数点后面的内容什么都可以
     ```

   - parseFloat()：强制转换为小数，全局函数，有截取功能

     ```js
     // 从第一位开始，直到最后一位数字
     console.log(parseFloat("ad.32"));  // NaN
     console.log(parseFloat("23a.33"));  // 23
     ```

     介绍另一个全局函数isNaN()，判断是否为非数字

     ```js
     isNaN(12);  // false
     isNaN("12");  // false
     isNaN("a12");  // true
     isNaN("12a");  // true
     ```


### 4. 运算符

#### 4.1 数学运算符

\+ - * / % ++ -- &&

7/2 = 3.5;

&&：是按位与（&&前面的内容是0000000或者11111111），false和0代表0000000，非0或者非fase表示111111

/+：表示加法运算、字符串拼接

/：整数相除的结果为小数

#### 4.2 关系运算符

\> >= < <= == != ===

==：只比较值(相当于java中的equals())

===：值和类型都要比较

#### 4.3 逻辑运算符

& || ！

短路逻辑结果为boolean（true或false）

非短路逻辑结果为number(1或0)

#### 4.4.条件运算符

判断表达式？表达式1：表达式2；

注意：**js中出现的判断表达式，条件表达式可以为任意表达式，可以为任何类型（Java中只能是true或者false，不能用1代表true）**

非0、非空、对象->true

0、null、""、undefined、NaN->false

### 5. 流程控制

#### 5.1 分支流程

if else、switch case

#### 5.2 循环流程

for、while、do...while

### 6. 对象

#### 6.1 内置对象

##### 6.1.1 简单内置对象

Number、String

###### 6.1.1.1 Number对象

var age = 10;   // 类型是number

var salary = new Number(200);   // 类型是object类型，这种方式不常用

常用函数：
- num.toFixed(n)：将数值转换为字符串，并通过四舍五入保留小数点后n位，如果位数不够则补0；
- num.toString()：转换为字符串
- num.valueOf()：得到该对象的值

###### 6.1.1.2 String对象

var str1 = "abc";

var str2 = new String("sjfei");   // 不常用

常用函数和属性
- length：返回字符串长度
- toUpperCase()：小写转大写
- toLowerCase()：大写转小写
- charAt()：返回指定索引的字符
- indexOf(findStr,[i])：从指定下标位置查找第一次出现的的findStr的位置
- lastIndexOf(findStr)：返回指定字符串最后一次出现的位置
- substring(start, [end])：截取指定下标位置的字符串，前包后不包[)
- split(byStr, [howmany])：将字符串进行拆分，得到字符串数组
- repalce(findStr, toStr)：字符串替换（每次只替换一个）
- slice(start, end)：字符串切片，返回一个新的字符串

##### 6.1.2 组合内置对象

 Math、Date、Array

###### 6.1.2.1 Math

不用创建对象，直接就可以调用其中的方法

Math.PI，Math.sqrt();

###### 6.1.2.2 Date

var date = new Date()；  // 获取当前系统时间

var date2 = new Date("2009/07/02 20:03:03")； // 指定日期时间

常用函数

- date.getTime()：获取时间戳
- date.getDate()：获取日期（号数）
- date.getDay()：获取周几
- date.getFullYear()：获取年份
- date.toLocaleString()：将时间转换为本地时间字符串
- date.setDate()：修改日期本身的值(比如设置23，表示这个月的23号，0表示上一个月的最后一天)

###### 6.1.2.3 Array

**数组中元素的类型可以不一致**

var arr1 = [10，"张三"，true，{"name"："李四"}]；

var arr2 = new Array(10，"张三"，true，{"name"："李四"})；

var arr3 = new Array()；

var arr4 = new Array(5)； // 指定初始化数组的长度

注意：

数组长度可变，由内部元素撑开

```js
var arr = new Array();  // arr = [];
arr[0] = 12;  // arr = [12];
arr[3] = 32;  // arr = [12, empty, empty, 32];
```

二维数组

var a = [[11，2]，["减速"]，["jfeif"，true]]；

常用函数和属性：

- length：获取数组的长度

- reverse()：反转数组

- join("分隔符")：数组转换为字符串

- sort([函数])：数组排序，函数可选。

  默认规则：数据的首个字符排序

  自定义规则：根据传入的函数规则进行排序

  例如：

  ```js
  var arr = [1, 23, 58, 145, 351];
  // 自定义排序规则
  function sortSelf(a, b){
  	return a-b;
  }
  arr.sort(sortSelf);  // 注意，只需要传入函数名就可以了，不用传参，传参就是调用函数了
  console.log(arr);
  ```

##### 6.1.3 复杂内置对象

Function、RegeExp

###### 6.1.3.1 Function

js中函数就是Function对象，函数名就是指向Function对象的引用。可以直接使用函数名访问函数对象，函数名()调用对象

在js中没有方法的重载，调用时能找到方法名，则执行方法体内容。如果有重名的，那么调用时以最后一个为准

```js
function f(str){
    console.log("hello");
}
f();  // 这样也可以调用上面定义的函数
```

函数定义：

- 方式一

  使用function关键字声明一个函数

  function 函数名([参数列表]){

  ​		函数体；

  ​		return 返回值；

  }

  函数的返回值默认返回undefined，可以使用return返回具体的值

- 方式二

  var 函数名 = function([参数列表]){

  ​		函数体；

  ​		return 返回值；

  }

- 方式三

  创建一个Function对象

  var 函数名 = new Function("参数一","参数二",...."函数体")；

  注意，小括号里前面的是函数的参数，最后一个是函数体

- 方式四（es6以后）

  var 函数名 = ([参数列表]) => {

  ​		函数体；

  ​		return返回值；

  }

  如果只有一条一句，{}可以省略，并且如果这一条语句是一句return的话，那么return可以也可以省略

js如果要实现类似于Java重载效果可以使用arguments对象，实现重载效果。

arguments：代表当前方法被传入的所有参数形成的参数数组

arguments.length：函数的参数个数

arguments[下标]：取对应下标的参数

```js
// 创建一个函数，实现重载效果
function f3(a,b,c){
	if (arguments.length == 0){
		console.log("没有参数");
	} else if (arguments.length == 1){
		console.log("有一个参数" + arguments[0]);
	} else if (arguments.length == 2){
		console.log("有两个参数" + arguments[0] + arguments[1]);
	} else {
		console.log("有多个参数" + arguments[0] + arguments[1] + arguments[2]);
	}
}
```

###### 6.1.3.2 RegExp

var reg = /正则表达式/tag；

var reg = new RegExp("正则表达式"，"tag")；

tag是标识：

- g：global，设置当前匹配为全局匹配
- i：ignore，忽略匹配中的大小写检查

正则表达式常用的组成部分

- ()：限定范围

- []：枚举、范围  [12345]  [1-5]，标识其中之一

- {}：次数、个数  {3}，前面的内容出现3次，{3,8}，出现3到8次

  /a/：不安全匹配，只要部分满足就可以了

  /^a/：以a开头

  /a$/：以a结尾

  /^a$/：完全匹配

常用函数

- 正则对象.test(字符串)

  判断一个字符串是否匹配该正则表达式，返回true表示符合

  ```js
  var reg = /^a/;
  var state = reg.test("abc");  // state为true
  ```

String对象支持正则的函数

- str.replace(reg, toStr)：替换
- str.match(reg)；返回匹配字符串符合正则的内容，形成数组
- str.search(reg)；返回字符串第一次匹配正则的下标

#### 6.2 外部对象

##### 6.2.1 BOM(Broswer Object Model)

浏览器对象模型。用来访问和操作浏览器窗口，使js有能力和浏览器对话。执行操作不与页面内容发生直接关系，没有相关标准，但被广泛使用

window是前台最大的对象，表示浏览器窗口，全部的js都是全局属性、全局对象、全局函数。

比如alert()；等价于window.alert()；

###### 6.2.1.1 全局属性

- document

  窗口中显示的HTML文档

- history

  浏览器窗口的历史记录

- location

  窗口的文件地址

- screen

  浏览器当前屏幕

- navigator

  浏览器相关信息

###### 6.2.1.2 全局对象

window的5个属性可以分别获取其对应的5个对象

- Document

  DOM

- History

  | 属性和方法 | 描述                                                        |
  | ---------- | ----------------------------------------------------------- |
  | length     | 返回访问的地址个数                                          |
  | back()     | 返回上一个地址                                              |
  | forward()  | 进入下一个地址                                              |
  | go(index)  | index<0，表示回退<br />index>0，表示前进<br />index=0，刷新 |

- Location

  | 属性和方法 | 描述                         |
  | ---------- | ---------------------------- |
  | href       | 当前窗口正在浏览器的网页地址 |
  | reload()   | 重新载入当前页面（属性）     |

- Screen

  | 属性和方法  | 描述           |
  | ----------- | -------------- |
  | width       | 实际的屏幕宽度 |
  | height      | 实际的屏幕高度 |
  | availWidth  | 可用的屏幕宽度 |
  | availHeight | 可用的屏幕高度 |

- Navigator

  | 属性和方法 | 描述   |
  | ---------- | ------ |
  | userAgent  | 浏览器 |

###### 6.2.1.3 全局函数

| 对话框              | 描述                                                        |
| ------------------- | ----------------------------------------------------------- |
| window.alert(msg)   | 提示对话框                                                  |
| window.confirm(msg) | 确认对话框（返回一个boolean值，用于接收用户是确认还是取消） |
| window.prompt()     | 弹出输入框                                                  |
| window.open(url)    | 打开新窗口                                                  |

###### 6.2.1.3 定时器

1. 一次性定时器

   在指定的时间后开始执行，不是函数被调用之后立即执行

   ```js
   // t表示返回已经启动的定时器对象，time表示时间间隔，单位是ms
   var t = window.setTimeout("执行语"|函数名, time);
   
   // 传入的是执行语句
   setTimeout("alert('时间到了')", 2000);
   
   // 传入的是函数
   function f(){
       alert("时间到");
   }
   setTimeout(f, 2000);
   ```

   停止定时器：clearTimeout(t);

2. 周期性定时器

   以一定的时间间隔执行代码，循环执行

   ```js
   var t = setInterval("执行语句"|函数名, time);
   ```

   

##### 6.2.2 DOM(Document Object Model)

文档对象模型。用来操作文档，定义了访问和操作HTML文档的标准方法，应用程序通过DOM操作来实现对HTML文档数据的操作。当页面被加载时，浏览器会创建页面的文档对象模型（DOM树），通过可编程的对象模型，js能够创建动态的HTML，包括HTML元素、属性、样式、事件

在页面加载的时候，由浏览器生成的整个HTML文档，操作文档中任何内容，都需要通过document

DOM查找节点，先要保证页面上的DOM树已经生成

*常用操作*

读取节点信息、修改节点信息、创建新节点、删除节点

js创建动态的HTML->元素、属性、样式、事件

js对DOM的操作有：查找、读取、修改、新增、删除

###### 6.2.2.1 查找

- 通过id查找

  `document.getElementById("id名")`，如果id值错误，返回null

- 通过标签名查找

  `document.getElementsByTagName("标签名")`，**注意这儿是复数。**根据指定的标签名，返回全部的元素，得到一个数组，如果找不到，则返回空数组，根据下标可以定位具体的节点。

  属性innerHTML表示该标签下的文本（包括内部的标签），innerText表示该标签下的文本内容，不包含标签

  例如

  ```js
  <li><span>文本内容</span></li>
  document.getElementsByTagName("li")
  innertHTML得到的是<span>文本内容</span>
  innertText得到的是文本内容
  ```

- 通过添加name属性查找

  `document.getElementsByName("name属性值")`，根据指定的name返回全部的元素组成数组。

- 通过层次关系查找

  `ele.parentNode`，遵循文档的上下层次结构，查找单个父节点

  `ele.childNodes`，注意是复数，查找多个子节点，得到一个数组

- 根据选择器查找

  `document.querySelector("选择器")`，返回符合选择器的第一个节点

  `document.querySelectorAll("选择器")`，返回符合选择器的所有节点
  
- 根据class属性查找

  `document.getElementsByClassName("类名")`，根据指定的class返回全部的元素组成数组

###### 6.2.2.2 读取和修改

文本内容

- innerHTML属性

  设置或者获取位于节点对象起始和结束内的文本，不解析HTML文本，将文本内容当成字符串打印

  读取：ele.innerHTML

  修改：ele.innerHTML="值"

- innerText属性

  设置合作恶化获取节点对象起始和结束内的文本，只能获取解析之后的文本内容

  读取：ele.innerHTML

  修改：ele.innerHTML="值"

属性

- 读取

  ele.属性

  ele.getAttribute(属性名)

- 修改

  ele.属性=值

  ele.setAttribute(属性名，值)

样式

- 读取

  ele.style

  ele.getAttribute("style");

- 修改

  ele.style="样式：样式值；..."

  ele.setAttribute("style", "样式：样式值；...");

  ele.style.样式属性="样式值"；

  **第三种方式要将font-size改为驼峰写法：fontSize**

样式推荐：获取、修改节点的class

获取：ele.className

设置：ele.className="值"；

图片的显示和影藏

###### 6.2.2.3 增加节点

- 通过innerHTML属性给页面添加节点

  ele.innerHTML="html代码"

- 通过函数给页面添加节点

  - 创建节点

    document.createElement("节点名称");

  - 指定新节点的位置

    追加新节点作为父节点的最后一个子节点，

    父节点.appendChild(新节点);

  - 以旧节点为参考点，新节点位于此节点之前添加

    父节点.insertBefore(新节点，旧节点);

###### 6.2.2.4 删除节点

父节点.removeChild(删除的指定节点);

###### 6.2.2.5 事件

指元素状态改变，用户在操作鼠标或者键盘时触发的动作。

1. 鼠标事件

   | 操作        | 描述     |
   | ----------- | -------- |
   | onclick     | 鼠标单击 |
   | ondblclick  | 鼠标双击 |
   | onmouseover | 移入     |
   | onmousedown | 按下     |
   | onmouseup   | 抬起     |

2. 键盘事件

   | 操作      | 描述     |
   | --------- | -------- |
   | e.keyCode | 键码值   |
   | onkeydown | 按钮按下 |
   | onkeyup   | 按钮松开 |

3. 状态改变事件

   | 操作     | 描述                           |
   | -------- | ------------------------------ |
   | onfocus  | 获取焦点                       |
   | onblur   | 失去焦点                       |
   | onchange | 选择（下拉框、单选框、复选框） |
   | onsubmit | 表单提交                       |
   | onload   | 加载                           |

   
















































