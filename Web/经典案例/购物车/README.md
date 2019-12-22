## 购物车

### 1. 搭建简单的架子

```html
<!DOCTYPE html>
<html>
    <head>
        <title>购物车</title>
        <meta charset="utf-8"/>
        <script src="../jquery-1.9.1.min.js"></script>
    </head>
    <body>
        <h1>真划算</h1>
        <table>
            <tr>
                <th>商品</th>
                <th>单价(元)</th>
                <th>颜色</th>
                <th>库存</th>
                <th>好评率</th>
                <th>操作</th>
            </tr>
            <tr>
                <td>罗技M185鼠标</td>
                <td>80</td>
                <td>黑色</td>
                <td>893</td>
                <td>98%</td>
                <td align="center">
                    <input type="button" value="加入购物车" onclick="add_shoppingcart(this);"/>
                </td>
            </tr>
            <tr>
                <td>微软X470键盘</td>
                <td>150</td>
                <td>黑色</td>
                <td>9028</td>
                <td>96%</td>
                <td align="center">
                    <input type="button" value="加入购物车" onclick="add_shoppingcart(this);"/>
                </td>
            </tr>
            <tr>
                <td>洛克iphone11手机壳</td>
                <td>60</td>
                <td>透明</td>
                <td>672</td>
                <td>99%</td>
                <td align="center">
                    <input type="button" value="加入购物车" onclick="add_shoppingcart(this);"/>
                </td>
            </tr>
            <tr>
                <td>蓝牙耳机</td>
                <td>100</td>
                <td>蓝色</td>
                <td>8937</td>
                <td>95%</td>
                <td align="center">
                    <input type="button" value="加入购物车" onclick="add_shoppingcart(this);"/>
                </td>
            </tr>
            <tr>
                <td>金士顿U盘</td>
                <td>70</td>
                <td>红色</td>
                <td>482</td>
                <td>100%</td>
                <td align="center">
                    <input type="button" value="加入购物车" onclick="add_shoppingcart(this);"/>
                </td>
            </tr>
        </table>

        <h1>购物车</h1>
        <table>
            <thead>
            <tr>
                <th>商品</th>
                <th>单价(元)</th>
                <th>数量</th>
                <th>金额(元)</th>
                <th>删除</th>
            </tr>
            </thead>
            <tbody id="goods">
            </tbody>
            <tfoot>
            <tr>
                <td colspan="3" align="right">总计</td>
                <td id="total">0</td>
                <td></td>
            </tr>
            </tfoot>
        </table>
    </body>
</html>
```

### 2. 增加样式

```css
<style type="text/css">
    h1 {
        text-align: center;
}

table {
    margin: 0 auto;
    width: 60%;
    border: 2px solid #aaa;
    border-collapse: collapse;
}

table th, table td {
    border: 2px solid #aaa;
    padding: 5px;
}

th {
    background-color: #eee;
}
</style>
```

### 3. jQuery实现功能

注意：

1. 点击`加入购车`之后，会在下面的表里增加该商品的信息，该功能由add_shoppingcart(btn)函数实现，也就是给表格增加一个孩子(`父节点.append(子节点)`)，并且要在相应的显示金额的地方增加相应的金额
2. 可以给1步骤优化以下，如果该商品已经添加过购物车了，那么再添加的话，不应该是再增加一行，而应该是在该商品的数量上加1，所以在上面增加子节点的时候应该加一个判断
3. 每一行代表的是同一个商品，那么该行的金额显示那一块就应该显示的是：该商品数量x商品的单价

```js
<script src="../jquery-1.9.1.min.js"></script>
<script>
        //加入购物车
        function add_shoppingcart(btn) {
            // 判断要加入购物车的商品是否已经在购物车中存在
            var $tr = $(btn).parents("tr"); //  找到点击事件的那一行
            var name = $tr.children("td:eq(0)").html();
            var state = $("#goods td:contains("+name+")");
            var price = $tr.children("td:eq(1)").html();
            if (state.length == 0){
                // 说明该商品尚未加入购物车
                var node = "<tr><td>"+name+"</td>"+
                        "<td>"+price+"</td>"+
                        "<td><input type='button' onclick='decrease(this)' value='-'/>" +
                        "<input type='text' size='3' value='1'/>"+
                        "<input type='button' onclick='increase(this)' value='+'/>"+
                        "</td><td>"+price+"</td><td><input type='button' value='x' onclick='del(this)'/></td></tr>";
                // console.log((node));
                $("#goods").append(node);

                // 修改总金额
                // console.log("总金额增加："+price);
                setTotal(price);

            } else {
                // 该商品已经加入购物车
                // 找到该商品所在位置，在数量上加1
                increase(state.parent().children("td:eq(2)").children("input:eq(2)")[0]);
            }
        }

        function decrease(btn) {
            // 找到该行的总金额那一列
            var total = $(btn).parent().next("td");
            // 找到该商品在购物车里的数量对应的节点
            var num = $(btn).next("input");
            // 获取单价
            var price = $(btn).parent().prev("td").html();
            if (parseInt(num.val()) <= 0){
                num.val("0");
            } else {
                num.val(parseInt(num.val())-1);
                // 修改总金额
                total.html(parseInt(num.val())*parseInt(price));
                // 修改购物车的总金额
                setTotal(-parseInt(price));
            }
        }

        function increase(btn){
            // 找到该行的总金额那一列
            var total = $(btn).parent().next("td");
            // 获取单价
            var price = $(btn).parent().prev("td").html();
            // 找到该商品在购物车里的数量对应的节点
            var num = $(btn).prev("input");
            // console.log(num.val());
            num.val(parseInt(num.val())+1);
            // 修改总额
            total.html(parseInt(num.val())*parseInt(price));
            // 修改购物车的总金额
            setTotal(price);
        }

        function del(btn){
            // 删除按钮
            // 获取删除节点对应的节点
            var $td = $(btn).parent();
            // 获取该商品总共的金额（数量*单价）
            var total = $td.prev("td").html();
            // 删除该行
            $td.parent().remove();
            // 修改总额
            setTotal(-total);
        }

        function setTotal(price){
            // 修改购物车总金额
            console.log("要修改的总额："+price);
            var total = $("tfoot td:eq(1)");
            total.html(parseInt(total.html())+parseInt(price));
        }
</script>
```

