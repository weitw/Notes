QQ:286389086  大崔

### 1. 该阶段计划：

网页基础（11天）

HTML/CSS/JS/JQuery

数据库（12天）

Mysql/Oracle/JDBC/XML

### 2. web概述

#### 2.1 web是什么

www(world wide web)，基于全球互联网的一个多媒体信息服务平台，提到网络，就应该想到web

#### 2.2 web的特性

web是BS架构， 还有一种CS架构（Client/Server）。

基于浏览器Browser/服务器Server的模式

#### 2.3 web的原理

当访问某个网站的网页时，访问的网页存放在服务器上，浏览器通过通讯协议发送请求，以获取服务器发送回来的响应，达到浏览网页的目的。

#### 2.4 web三要素

- 浏览器

  向服务器发送请求，下载服务器中的网页文件，解释执行文件，实现页面内容的展示

- 服务器

  接收浏览器的请求，发送响应的页面文件给浏览器

- 通信协议

  用于规范通信（https）

#### 2.5 web开发的三要素

- HTML

  构建网页结构

- CSS

  控制页面内容样式显示（美化页面的）

- JS

  添加动态交互效果和一些简单逻辑运算

#### 2.6 web浏览器

浏览器把源代码解释成图形化界面，也就是网页。

主流浏览器（内核浏览器）：IE(Edge)、Chrome、Firefox、Safari

360/搜狗这些是集成浏览器，有很多插件，不是主流浏览器



### 3. HTML

#### 3.1 html简介

HTML（Hyper Text Markup Landuage），超文本标记语言。

XML：可扩展标记语言（用来写配置文件）

HTML：固定标记语言（用来写网页文件）

XHTML：可扩展+固定标记语言

特点

- 一个纯文本类型的语言，用来设计网页的标记语言
- 用此语言编写的文件以.html或.htm为后缀。
- 该文件由浏览器解释执行
- HTML页面可以嵌套使用脚本语言（js）编写的程序段

#### 3.2标记（标签）

html标记通常也称为标签，标签由尖括号包围的关键字组成，通常成对出现（开始标签和结束标签）。

分类

- 双标签

  <标签名 属性="属性值"></标签名>

- 单标签

  <标签名 属性="属性值" />

#### 3.3 HTML版本

html有很多不同的版本，需要在写HTML文件时指定使用哪种版本的HTML，这样浏览器才能完全正确的显示HTML内容

H1~H3版本：政府机构和一些大型商业组织等

H4：分为过渡型、严格型、框架型

H5：<!DOCTYPE html>

#### 3.4 html结构

```html
<html>
    <head>网页配置信息</head>
    <body>网页显示内容</body>
</html>
```

```html
<head> <!--head标签包含以下标签-->
    <title>网页标题</title>
    <meta />元数据（消息头）
    <style>样式声明（内部）</style>
    <link />引入样式文件（外部）
    <script>js脚本代码</script>
</head>
```

#### 3.5 注释

<!--注释内容-->

#### 3.6 常用的固定标记

##### 3.6.1 文本标签

文本是网页重要组成部分，直接书写的文本会用浏览器默认的样式显示

- 标题标签`<h>`

  常用于标题的显示，以达到醒目的效果

  <h#>标题内容</h#>，#表示1到6的数字

  特点：独占一行，并且文本上下有间距

- 段落标签

  提供结构化文本显示方式，文本会用单独的段落显示，是块级标签

  `<p></p>`

- 分区标签

  - 行内分区元素（行内标签）：`<span></span>`

    特点：没有特点，纯文本

  - 块分区元素：`<div></div>`
  
    特点：独占一行，块级标签，元素前后会自动换行，块的上下无间距
  
- 单标签
  
  `</br>`，换行
  
  `<hr>`，水平线
  
- 其他常用
  
  `<i>斜体</i>`，`<b>粗体</b>`，`<del>删除线</del>`，`<u>下划线</u>`
  
  实体引用（有分号）
  
  ```html
  &nbsp;  空格
  &gt;    >
  &lt;    <
  &amp;   &
  ```

##### 3.6.2 图像和超链接标签

- 图像（行内块标签，只有块元素才可以设置宽高，行元素不能）

  `<img src="图片路径" width="图片宽" height="图高" border="边框" title="提示信息" alt="错误信息">`

  注意：src必须添加，需要引入图片路径。

  如果width和height只设置其中一个，那么默认按照图片的原始比例来显示，另一个值会默认按照比例设置

- 超链接（行内标签）

  `<a href="链接的url地址" target="页面的打开方式">文本或图像</a>`

  注意：完整的utl地址有https，比如要跳转百度网页，那么可以设置href="https://www.baidu.com"

  - target取值

    _self：在当前窗口打开新链接（默认）_

    blank：在新窗口打开链接

  - 锚点

    文档中某行的一个记号，用于链接到文档的某个位置

    定义锚点

    `<a name="锚点名"></a>`

    链接锚点

    `<a href="#锚点名"></a>`，#是用来告诉浏览器，链接不是一个页面，而是一个位置。

##### 3.6.3 列表标签

列表将具有像素特征或者具有先后顺序的几行文字进行对齐排列

列表由列表类型和列表项组成

```html
列表类型:
无序列表
<ul type="none"> <!--type属性可以将无序列表前的点去掉-->
    <li></li> 
    <li></li> 
</ul>
有序列表
<ol>
    <li></li>
    <li></li>
</ol>
```

type的值

无序列表默认是实心圆，可以自定义，

type="disc实心圆 | circle空心圆 | square实心矩形 | none无修饰"

有序列表默认是数字，

type="1数字 | a小写字母开始 | A大写字母 | i小写罗马数字 | I大写罗马数字"

##### 3.6.4 表格标签

表格标签常用与组织结构化信息，常用与页面的布局

1. 组成

```html
表格
<table>
	<tr>
    	<td></td> 列
    </tr>  行
</table>

```

2. 常用属性

   - \<table>里面的属性

     border="边框"

     bordercolor="边框颜色"

     width="宽度" 

     height="表格的高度" 

     cellspaceing="单元格之间的间距"

     cellpadding="单元格与内容的间距" 

     align="水平对齐方式">

   - \<tr>里的属性

     bgcolor=""：背景色

   - \<td>里的属性

     valign=""：垂直对齐方式

3. 不规则表格

   属性

   colspan="列的合并"

   rowspan="行的合并"

4. 表格划分

   三部分：

   - 表头：\<thead>\</thead>
   - 表体：\<tbody>\</tbody>
   - 表尾： \<tfoot>\</tfoot>

5. 表格嵌套

##### 3.6.5 表单标签

表单用于显示、收集、提交信息到服务器

1. 组成

   form标签和表单控件

2. 定义表单

   \<form>\</form>
   
   表示要将次标签中涵盖的控件中的数据传输到服务器
   
3. 主要属性
   
   action：表单提交的url地址
   
   method：表达数据提交给服务器的方式（get和post）
   
   enctype：表单数据的编码方式
   
4. 表单控件
   
   表单里面包含很多不同类型的表单控件，表单控件是一种HTML元素信息输入项
   
   包含两种类型
   
   - input元素（input，是一个行内块标签）
   
     文本框、密码框、单选框、复选框、按钮、隐藏域、文件选择框
   
   - 非input元素
   
     标签、文本域、下拉框
   
5. 文本框
  
     \<input type="text" name=""/>
   
   常用属性
   
   - type
   
     用来规定input元素的类型，默认是文本框类型
   
   - name
   
     规定input元素的名字（后台会根据name取数据），
   
   - value
   
     规定input元素的值
   
   - readonly
   
     true，表示输入框为只读。只需要些readonly就表示true了，不用写成readonly="true"
   
   - placeholder
   
     输入框提示信息
   
   - maxlength
   
     对顶输入框的字符长度
   
6. 密码框

     \<input type="password" />

     常用属性

     type、name

7. 单选框

     \<input type="radia" name="" value="" />

     常用属性

     name：用于实现分组，同一组的名称必须相同

     value：提交的数据值

     checked：true表示选中

8. 标签控件

     \<label for="控件的id">\</label>

     for：设置文本所关联的控件id，关联后点击标签等同于点击该控件

9. 复选框

     \<input type="checkbox" name="分组" value="值" checked>

10. 文件选择框

     \<input type="file" name=""/>，没有value值

11. 隐藏域

      \<input type="hidden" name="" value="" />

      隐藏域在表单中包含不希望用户看见的信息，很多时候借助该控件向后台提交重要数据。

12. 文本域(非input)

      相当于多行的文本框

      \<textarea name="" cols="" rows="">\</textarea>

      cols：列数

      rows：行数

13. 下拉框（非input）

      ```html
      <select name="">
          <option value="">选项一</option>
          <option value="">选项二</option>
      </select>
      ```

14. 按钮

      - 提交按钮：`<input type="submit" value="">`

        传送表单数据给服务器或其他程序

      - 重置按钮：`<input type="reset" value="">`

        清空表单内容，将全部表单控件设置为最初的默认值

      - 普通按钮：`input type="button" value=""`

        用于执行客户端脚本代码
    
15. 补充

      - 可以引入外部HTML文件的控件

      ​       `<iframe src="外部html文件地址"></iframe>`

      - 分组标签

        ```html
        <fieldset>
            <legend>请选择</legend>
            <input type="checkbox" name="a" />
            <input type="checkbox" name="b" />
        </fieldset>
        ```

16. H5新增的表单控件

    ```html
    <!-- 日期 -->
    <input type="date" /><br>
    <!-- 时间 -->
    <input type="time" /><br>
    <!-- 日期加时间 -->
    <input type="datetime-local" /><br>
    <!-- 邮箱 required表示必填-->
    <input type="email" required /><br>
    <!-- 网址 -->
    <input type="url" /><br>
    <!-- 颜色 -->
    <input type="color" /><br>
    <!-- 数字 -->
    <input type="number" min="1" max="10"/><br>
    <!-- 进度条 value="默认值" max="最大值" step="步长"-->
    <input type="range" value="0" max="50" step="10"/><br>
    ```

    

​      















































