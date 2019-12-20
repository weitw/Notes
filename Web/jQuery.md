## jQuery

### 1. jQuery 简介

jQuery是一个js框架，轻量级的js库（函数）

#### 1.1 特点

- 封装了js原生里面的js、css、DOM等操作，提供了一致的、简洁的API

- 兼容各个版本的浏览器、css3、html5
- 封装了对Ajax、动画的支持
- 实现了html内容和表现的分离

#### 1.2 jQuery的使用

步骤：引入jQuery文件，使用其提供的函数

注意：jQuery本身是一个扩展了的js数组

#### 1.3 jQuery和JS原生转换

- JS原生-->jQuery

  $(原生对象)-->返回转换后的jQuery对象

- jQuery-->JS原生

  jQuery对象[下标]-->返回转换后的JS原生对象

### 2. jQuery选择器

#### 2.1 基本选择器

| 选择器                | 描述             |
| --------------------- | ---------------- |
| $("$id值")            | 根据id值找节点   |
| $("标签名")           | 根据标签名找节点 |
| $(".class值")         | 根据类名找节点   |
| $("选择器1选择2")     | 交集选择器       |
| $("选择器1，选择器2") | 并集选择器       |

#### 2.2 层次选择器

| 选择器               | 描述                                                       |
| -------------------- | ---------------------------------------------------------- |
| $("选择器1 选择器2") | 找后代                                                     |
| $("选择器1>选择器2") | 找儿子                                                     |
| $("选择器1+选择器2") | 找下一个相邻节点（**注意：看下面的找下一个相邻节点案例**） |
| $("选择器1~选择器2") | 找所有弟弟                                                 |

*示例：*

```js
<body>
    <div>
        <p id="i">p1节点</p>
        <p class="c">p2节点</p>
        <p>p3节点</p>
        <span>我是div里面的span</span>
    </div>
    <span>我是div的第一个弟弟span</span>
    <span>我是div的第二个弟弟span</span>
    <p>我是div的第三个弟弟p</p>
</body>
<script>
    // 找所有后代
    console.log($("div p"));
    // 找儿子
    console.log($("div>span"));
    // 找下一个相邻节点
    console.log($("div+span"));  
	// 注意，不能跳过最近的相邻节点去找其他的相邻节点,例如不能使用$("div+p")，来找第三个弟弟


    // 找所有相邻节点
    console.log($("div~span"));
</script>
```

#### 2.3 过滤选择器

常用于表格和列表

| 选择器            | 描述                                       |
| ----------------- | ------------------------------------------ |
| :first            | 第一个。例如：$("选择器:first")            |
| :last             | 最后一个。例如：$("选择器:last")           |
| :even             | 偶数行（下标从0开始）                      |
| :odd              | 奇数行（下标从1开始）                      |
| :not("选择器")    | 把符合该选择器的元素排出在外               |
| :eq(index)        | 下标等于index的元素                        |
| :gt(index)        | 下标大于index的元素                        |
| :lt(index)        | 下标小于index的元素（注意：下标从0开始）   |
| :hidden           | 找到所有隐藏元素                           |
| :visible          | 找到所有可见元素                           |
| :contains("text") | 找到包含指定text文本的元素                 |
| :empty            | 找到不包含任何内容的元素（属性和文本内容） |

*示例：*

$("选择器").css("样式", "样式值");

```js
<body>
    <table border="1px" cellspacing="0px"
    cellpadding="0px" width="300px"> 
        <tr>
        <td>姓名</td>
        <td>年龄</td>
        </tr>
        <tr>
            <td id="i">张三</td>
        <td>23</td>
        </tr>
        <tr>
                <td>李四</td>
        <td>32</td>
        </tr>
        <tr>
                <td>王二麻子</td>
        <td>64</td>
        </tr>
    </table>
    <input type="hidden" value="123" />
    <input type="text" value="456" />
    <span>程序员</span>
    <span>海贼王</span>
    <span></span>

</body>
<script>
            // 将第一行变成红色
            //		$("table tr:first").css("background-color","red");
            //		// 将最后一行变成蓝色
            //		$("table tr:last").css("color","blue");

            // 将表格奇数行变成黄色，偶数行变成灰色
            //		$("table tr:odd").css("background-color","white");
            //		$("table tr:even").css("background-color","ghostwhite");

            // 将表格中除了id=i的节点，其他节点变成蓝色
            //		$("table td:not('#i')").css("background-color","blue");

            // 找张三节点变成绿色
            //		$("table td:eq(2)").css("background-color","greenyellow");
            // 嵌套使用
            //		$("table tr:eq(1) td:eq(0)").css("background-color","gold");

            //		$("table tr:gt(2)").css("background-color","greenyellow");

            //		console.log($("input:hidden").val());
            //		console.log($("input:visible").val());

            console.log($("span:contains('海贼王')"))
console.log($("span:empty"));
</script>
```

#### 2.4 属性定位选择器

| 选择器       | 描述                            |
| ------------ | ------------------------------- |
| [属性名]     | 找到所有具有该属性的元素        |
| [属性名=值]  | 找到属性=属性值的元素           |
| [属性名!=值] | 找到属性！=属性值的元素         |
| [属性名^=值] | 找到属性=以指定属性值开头的元素 |

```js
// 示例
<body>
    <span class="c1">一</span>
    <span class="c2">二</span>
    <span class="c3">三</span>
    <span class="c4">四</span>
    <span>五</span>
</body>
<script>
    //[属性名]
    //$("[class]").css("color","red");
    $("span[class!=c4]").css("color","red");
	$("span[class^=c]").css("color","aquamarine");
</script>
```

#### 2.5 状态过滤选择器

| 选择器     | 描述           |
| ---------- | -------------- |
| :enabled   | 找可用元素     |
| :disabled  | 找不可用元素   |
| :checked   | 找选中元素     |
| :selected  | 找选中的option |
|            |                |
| 表单选择器 |                |
| :text      | 文本框         |
| :password  | 密码框         |
| :radio     | 单选框         |
| :checkbox  | 复选框         |
| :submit    | 提交按钮       |

```js
// 示例
<body>
    <form action="" method="" enctype="">
        用户名：<input value="zs" /><br>
        密码：<input type="password" value="123" disabled /><br/>
        爱好：
        <input type="checkbox" checked/>篮球
        <input type="checkbox" />足球
        <input type="checkbox" checked/>排球
    </form>
</body>
<script>
		// 找表单中普通文本
		console.log($("input:text").val());
		// 找密码框
		console.log($("input:password"));
		// 找表单中的被禁用的节点
		console.log($("input:disabled"));
		// 找所有复选框节点
		console.log($("input:checkbox"));
		// 找所有被选中的节点
		console.log($("input:checked"));
</script>
```

### 3. jQuery的DOM操作

#### 3.1 增加节点

##### 3.1.1 使用html()函数增加节点

该方法类似innerHTML，在html("html代码")

##### 3.1.2 通过函数的方式

步骤

1. 创建节点：jQuery对象节点

2. 指定新节点位置

   - `父节点.append(子节点)`。作为父节点的最后一个子节点增加

   - `父节点.prepend(子节点)`。作为父节点的第一个子节点

   - `兄弟节点.after(子节点)`。作为兄弟节点的下一个弟弟

   - `兄弟.before(子节点)`。作为兄弟的上一个哥哥

     **注意：如果节点找到的是多个，那么以上方法增加会在所有找到的节点后都增加一个子节点**

     ```js
     <body>
         请输入姓名：<input type="text" name="user" />
         <br/><br/>
         <input type="button" value="增加" onclick="add()" />
         <ul>
             <li>张三</li>
         	<li>李四</li>
        	</ul>
     </body>
     <script>
             function add(){
                 // 创建新节点
                 var $inputTag = $("input[name=user]");
                 var $user = $inputTag.val();
                 var li = "<li>" + $user + "</li>"; // JS原生的
                 var $li = $(li);
                 // 父节点.append(子节点)
                 // $("ul").append($li);
                 // 添加到第一恶
                 // $("ul").prepend($li);
                 // 兄弟节点添加
                 // $("li").after($li);  // 为所有的li标签之后添加
                 $("li").before($li);
             }
     </script>
     ```

#### 3.3 删除节点

| 方法                 | 描述                           |
| -------------------- | ------------------------------ |
| obj.remove([选择器]) | 删除节点                       |
| obj.empty()          | 清空节点文本内容，节点没有消失 |

```js
// 删除第一个li节点
 $("li:first").remove();  // 谁调用就删谁
 // 删除id为i的节点
 $("li").remove("#i");
// 清空第二个li节点的内容
 $("li:eq(1)").empty();
```


#### 3.3 修改节点

修改节点的属性、文本内容、样式

| 描述         | 函数          | 对应JS中的代码  |
| ------------ | ------------- | :-------------- |
| 1. 节点的value值 |               |               |
| 获取文本的值 | `obj.val()`   | `ele.value;`    |
| 修改文本的值 | `obj.val("值")` | `ele.value="值"` |
| 2. 节点的HTML内容 |  |  |
| 获取 | `obj.html()`<br />`obj.text()` | `ele.innerHTML` |
| 修改 | `obj.html("值")` | `ele.innerHTML="值"` |
| 3. 节点的属性 |  |  |
| 获取 | `obj.attr("属性")` | ``ele.属性`<br />ele.getAttribute("属性")` |
| 修改 | `obj.attr("属性"，"属性值")` | `ele.属性=属性值`<br />`ele.setAttrribute("属性","属性值")` |
| 4. 节点的样式 |  |  |
| 获取 | `obj.css()` | `ele.style` |
| 修改 | `obj.css("样式"，"样式值")`<br />`obj.css({"样式1":"样式值1","样式2":"样式值2"})` | `ele.style="值"` |
| 5. 动态修改样式（推荐） |  |  |
| 给对象添加指定的class | `obj.addClass("类名")` |  |
| 删除对象指定的class | `obj.removeClass("类名")` |  |

```js
     function changeNode(){
    // 属性修改
         //			$("input[name=user]").val("猴子");

         // 修改节点的HTML内容，或者text内容
    //			$("#i").html("<span>白起</span>");
         //			$("#i").text("<span>白起</span>");

         // 属性修改
    //			$("#i").attr("id", "j");
     
    // 样式修改
         //			$("#i").attr("style","color:red");
    $("#i").css({"color":"red", "background-color":"blue","font-size":"23px"});
     }
```



#### 3.2 查找节点

| 函数                     | 描述                     |
| ------------------------ | ------------------------ |
| `obj.children()`         | 找所有子节点             |
| `obj.children("选择器")` | 根据选择器找子节点       |
| `obj.next([选择器])`     | 找下一个弟弟             |
| `obj.prev([选择器])`     | 找上一个哥哥             |
| `obj.siblings()`         | 所有的兄弟               |
| `obj.parent()`           | 父节点                   |
| `obj.parents("选择器")`  | 根据选择器找祖先节点     |
| `obj.find("选择器")`     | 找符合该选择器的后代元素 |

```js
// 注意，这个this代表的是JS对象，不是jQuery对象
<p onclick="showP(this)">我是p标签</p>
// 使用
function showP(p){
    $(p).css("color","red");
}
```



### 4. jQuery操作DOM事件

#### 4.1 方式一

若找到多个节点，jQuery会给每个节点都绑定事件

`jQuery对象.事件名(function() {})`;

例如：$p.click(function() {});

示例：$("ul li").click(function(){console.log($(this).text())});

#### 4.2 方式二

jQuery对象.on("事件名", function() { })；

```js
<body>
    <ul>
        <li>列表项1</li>
        <li style="background-color: yellow;">列表项2</li>
        <li>列表项3</li>
        <li>列表项4</li>
    </ul>
</body>
```

示例：$("ul li").on("click", function(){console.log($(this).text())});



### 5 DOM加载问题

1. 原生的实现方式：window.onload = function(){}

   可以让窗口先加载DOM树，完成加载之后，再执行后面的匿名函数

   当页面加载完成之后，产生一个load事件，对应的事件函数被执行；当页面加载完成（DOM树生成），此时查找任何DOM节点都可以被找到。

   ```js
   <script>
       window.onload = function(){
           var divEle = document.getElementById("i");
           console.log(divEle);
   	}
   </script>
   ```

2. jQuery方式：$(function(){})，可以让窗口先加载DOM树，完成加载之后，再执行后面的匿名函数

   ```js
   <script>    
   	// jQuery写法
       $(function(){
           var divEle = document.getElementById("i");
           console.log(divEle);
       })
   </script>
   ```



### 6. jQuery处理事件冒泡

jQuery事件触发之后，也会产生event事件对象（jQuery对象）

处理事件冒泡：`e.stopPropagation();`

### 7. 合成事件

`obj.hover(mouseover,mouseout)`；

### 8. jQuery动画效果

| 函数              | 描述 |
| ----------------- | ---- |
| `obj.hide()`      | 隐藏 |
| `obj.show()`      | 显示 |
| `obj.fadeIn()`    | 淡入 |
| `obj.fadeOut()`   | 淡出 |
| `obj.slideUp()`   | 收起 |
| `obj.slideDown()` | 展开 |

动画效果

obj.动画函数(时间[，回调函数]);

时间：整个动画完成需要的时间，ms值

回调函数：可选，动画完成之后需要执行的操作

### 9. 自定义动画

obj.animate({动画效果}，时间，[回调函数])

{}描述的是动画执行之后元素的效果

### 10. Java对象转成JSON字符串

































