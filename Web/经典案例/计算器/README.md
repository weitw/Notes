## 写一个简单的计算器

### 1. 搭建一个简单的架子

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>计算器</title>
    </head>
    <body>
		<table align="center">
			<tr>
				<td colspan="5"></td>
			</tr>
			<tr>
				<td>1</td>
				<td>2</td>
				<td>3</td>
				<td>+</td>
				<td>C</td>
			</tr>
			<tr>
				<td>4</td>
				<td>5</td>
				<td>6</td>
				<td>-</td>
				<td rowspan="3">=</td>
			</tr>
			<tr>
				<td>7</td>
				<td>8</td>
				<td>9</td>
				<td>*</td>
			</tr>
			<tr>
				<td>00</td>
				<td>0</td>
				<td>.</td>
				<td>/</td>
			</tr>
		</table>
	</body>
</html>
```

### 2. 增加一些样式

```css
<style>
            *{
                margin: 0;
                padding: 0;
            }
            table{
                /*表格的样式*/
                width:500px;
				height:500px;
				border: 1px solid black;
				background-color: #999999;
				cellspacing:0px;
            }
            td{
                /*td节点正常的样式*/
                cursor: pointer;
				width:40px;
				height: 30px;
				border: 1px solid #FFFFFF;
				background: #999999;
				color: #FFFFFF;
				text-align: center;
				font-weight: bold;
				font-family: "微软雅黑";
            }
            td:hover{
                /*鼠标悬停在td节点时的样式*/
                background: #008000;
            }
        </style>
```

### 3. js实现计算功能

注意，需要因为使用了jQuery，所以需要先导入该框架，就是下面代码的第一个script

```js
<script src="./jquery-1.9.1.min.js"></script>
<script>
    $(function () {
        var str = "";
        // 获取输入框的节点
        var $input = $("table tr:eq(0) td");
    	// 用户点击任何一个td节点都会触发下面的点击事件
        $("td").click(function () {
            // 获取用户点击的那个td节点的文本内容
            var text = $(this).html();
            console.log(text);
            if (text == "="){
                try{
                    /* 当用户点击的是=的时候，我们应该计算此时表达式的值，然后在输入框（第一个td节点）打印出来
                    * 下面代码中的eval(str)，就是计算表达式的值，如果表达式不是一个正规的数学表达式，那么会抛出异常
                    */
                    $input.html(eval(str));
                } catch (e) {
                    // 说明抛出了异常，那么我们应该在输入框提示用户输入非法
                    $input.html("<span style='color: red;'>非法输入!</span>");
                } finally {
                    // 最后让表达式变为最初的空字符串
                    str = "";
                }
            } else if (text == "C"){
                // 用户点击了C这个节点，那么表示要清空输入框中的内容
                str = "";
                $input.html(str);
            } else {
                // 表达式累加，然后在输入框显示。
                str += text;
                $input.html(str);
            }
        })
    })
</script>
```

















































