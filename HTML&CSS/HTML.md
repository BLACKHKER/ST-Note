## HTML

### 一、环境搭建

> 前端开发工具：Visual Studio Code

#### 打开HTML页面：

##### 1.Open With Life Server：通过端口方式打开(页面地址栏显示IP地址端口号)



##### 2.Open In Default Browser：通过浏览器方式打开(页面地址栏显示页面的绝对路径)

> 区别：通过端口方式打开的页面会跟随页面更改实时更新





#### 快捷生成HTML页面：

```
!：生成全部结构
!!!：生成 <!DOCTYPE html>
```







### 二、HTML基本结构

```html
<!--声明HTML文档-->
<html>

<head>
  <title>网页标题</title>
</head>

<body>
  网页正文内容
</body>

</html>
```

#### 转义字符：解决特定场景字符冲突的问题

```html
&nbsp; 空格	&gt; >大于	&lt; <小于	&copy; 版权符号	
```

```html
<!--这样是输入不了的，会被浏览器转换为标签，输出空白-->
这是段落标签：<p></p>
<!--使用转义字符，正常输出：这是段落标签：< p > < /p >-->
这是段落标签：&lt; p &gt; &lt; /p &gt;
```



#### 标签(灰字表示该标签的属性)：

> 元素(标签)类型分为块级元素、行级元素、行块级元素

##### 块级元素：独占一行，从上到下排序

```html
<p>  <div>  <dl>  <form>  <h1-h6>  <hr> ...
```

块级元素一般可嵌套块级元素或行内元素；

两个块级元素连续编辑时，会在页面自动换行显示。

每个块级元素默认占一行高度，一行内添加一个块级元素后无法一般无法添加其他元素（float浮动后除外）。

块级元素一般作为容器出现，用来组织结构，但并不全是如此，有些块级元素，只能包含块级元素；其他的块级元素则可以包含行级元素，也有一些则既可以包含块级，也可以包含行级元素。

###### 特点：

1. 总是在新行上开始
2. 高度，行高以及外边距和内边距都可控制
3. 它可以容纳内联元素和其他块元素 



##### 行级(行内)元素：从左到右依次排列

```html
<a>  <br/>  <img/>  <input> ...
```

也叫内联元素、内嵌元素；行内元素一般都是基于语义级(semantic)的基本元素，只能容纳文本或其他内联元素，例如文字这类元素，各个字母之间横向排列，到最右端自动折行

常见内联元素a、span、iframe等或元素样式为display : inline的都是行内元素

###### 特点：

1. 和其他元素都在一行上
2. 高，行高及外边距和内边距不可改变
3. 宽度就是它的文字或图片的宽度，不可改变
4. 内联元素只能容纳文本或者其他内联元素

###### 对行内元素，需要注意如下：

1. 设置宽度width 无效
2. 设置高度height 无效，可以通过line-height来设置
3. 设置margin 只有左右margin有效，上下无效。
4. 设置padding只有左右padding有效，上下则无效。注意元素范围是增大了，但对元素周围的内容没影响



##### 行块级元素：

```

```

1. 



##### 行级元素与块级元素的区别：

块级：独占一行，默认情况下宽度自动填满其父元素宽度
行内：不会独占一行，相邻的行内元素会排在同一行。其宽度随内容的变化而变化。

块级：块级元素可以设置宽高
行内：行内元素不可以设置宽高

块级：块级元素margin，padding都可以设置
行内：行内元素水平方向的margin-left; margin-right; padding-left; padding-right;可以生效								但是垂直方向的margin-bottom; margin-top; padding-top; padding-bottom;却不能生效。

块级：display:block;
行内：display:inline;
可以通过修改display属性来切换块级元素和行内元素



> 单双标签的区别在于是否用于修饰内容，单标签不含内容独立也可以使用

##### 单标签：

```html
<!--换行--> 
<br/>
<!--水平线--> 
<hr/>
```



##### title：控制浏览器标签页显示的文字

```html
<title>智慧园区管理系统</title>
```



##### h1-h6：标题(由大到小)

```html
<h1>标题</h1>
```



##### p：段落

```html
<p>该代码标记了一个段落</p>
```



##### a：锚、超链接标签

```html
<a>点我跳转链接</a>
```

###### href：设定点击后跳转的链接，可以是本地页面，也可以提交一个请求,也可以是图片等服务器资源

```html
<a href="http://www.baidu.com">点我跳转百度</a>
<!--让超链接标签无作用-->
<a href="javascript:void(0)">点我没有反应</a>
<!--提交到名为user的servlet,携带userid-->
<a href="value='/user?method=selectById&id="+user.id+""/>
```

###### target：通过对应属性值选择打开页面的方式

```html
<a href="http://www.baidu.com" target="xxx">点我跳转百度</a>
<!-- a标签target属性可以设置如下值, 作用分别对应如下 --> 
<!-- _self 默认值, 在当前窗口或者框架中打开连接 -->
<!-- _blank 在新窗口或新的标签页中打开链接 -->
<!-- _parent 在父级的框架中打开, 如果自身是顶层, 与_self相同 -->
<!-- _top 在顶层的框架中打开; 当不在框架中使用则清除所有内容在当前窗口显示连接文档 -->
<!-- frameName 在指定的iframe内联框架中打开页面 -->
```



##### img：在网页中插入图片

```html
<!--相对路径-->
<!--不以/开头-->
<img src="../1.jpg">	<!--在当前页面所在文件夹的上一级搜索1.jpg-->
<!--以/开头-->
<img src="/day01/img/1.jpg">	<!--以当前IP地址1.jpg-->

<!--绝对路径-->
<img src="D:/picture/1.jpg">	<!--打开D盘下的picture文件夹下的1.jpg-->
<!--协议://IP地址:端口/资源路径-->
<img src="https:/www.xxx.com/xxx.png">	<!--打开https://www.xxx.com下的xxx.png-->
```

###### alt：在地址资源无法访问的时候，显示alt内的文字来替代图片

```html
<img src="1.jpg" alt="这张图片是一个范爷">
```



##### 列表

###### ol：有序列表

```html
<!--type的属性值有1、a、A、I、i(数字、英文大小写、罗马大小写)-->
<!--start的值为正整数，代表起始排序数字-->
<!--以小写字母排序,从第二个开始(b)-->
<ol type="a" start="2">
    <li>🍎</li>	
    <li>⚽</li>
    <li>🤑</li>
</ol>
```

###### ul：无序列表

```html
<!--不显示排序圆点-->
<ul  style="list-style: none">
    <li>🍎</li>
    <li>⚽</li>
    <li>🤑</li>
</ul>
```

###### dl：定义列表

```html
<!--自带缩进、所有的dd都在dt后，实现图文混排-->
<!--学院、专业-->
<dl>
    <!--定义标题(dt的t是tittle)-->
    <dt>计算机学院</dt>
    <!--内容一-->
    <dd>软件开发</dd>
    <!--内容二-->
    <dd>电子商务</dd>
    <!--内容三-->
    <dd>游戏开发</dd>
    <dt>电子学院</dt>
    <dd>数字电路</dd>
    <dd>模拟电路</dd>
</dl>

<!--图文混排-->
<dl>
    <dt><img src="/day01/images/屏幕截图 2023-01-23 173204.jpg" alt="地址失效" /></dt>
    <dd>商品名称</dd>
    <dd>商品价格</dd>
</dl>
```



##### table：表格

###### tr、th、td：表示行、表头、单元格

```html
<table>
	<tr>	<!--代表单元格的一行-->
    	<th>Month</th>	<!--定义表头，跟td唯一的区别是该标签定义的字会加粗-->
    	<th>Savings</th>
  	</tr>
	<tr>
		<td>January</td> <!--定义单元格-->
		<td>100</td>
	</tr>
</table>
```

###### border：设置表格宽高,修改单元格大小

```html
<table border="1px" width="200px" height="100px">
	<tr>
		<td>1-1</td>
        <td>1-2</td>
        <td>1-3</td>
	</tr>
    <tr>
		<td>2-1</td>
        <td>2-2</td> 
        <td>2-3</td> 
	</tr>
    <tr>
		<td>3-1</td>
        <td>3-2</td> 
        <td>3-3</td> 
	</tr>
</table>
```

###### border-collapse：合并框线

```html
<!--将表格的所有内框线删除-->
<head>
  <title>网页标题</title>
  <style>
    table {
      border-collapse: collapse;
    }
  </style>
</head>
<table>
	tr...td
</table>
```

###### 合并单元格：跨列/跨行

```html
<table border="1px" width="200px" height="100px">
    <tr>
      <!-- 合并列，删除下一个td -->
      <td colspan="2">1-1</td>
      <td>1-3</td>
    </tr>
    <tr>
      <!-- 合并行，删除下一行对应列的td -->
      <td rowspan="2">2-1</td>
      <td>2-2</td>
      <td>2-3</td>
    </tr>
    <tr>
      <td>3-2</td>
      <td>3-3</td>
    </tr>
  </table>
```

###### thead、tbody、tfoot：定义表格分区

> thead：该标签内表示表格头，类似th
>
> tbody：标签内定义表格体，配合td
>
> tfoot：标签内定义表格脚。	table内乱序排列该三个标签，会自动纠正，按正确顺序排列展示

```html
<table>	
    <!-- thread内部必须拥有tr标签 -->
  <thead>
    <tr>
      <td>THEAD 中的文本</td>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>TBODY 中的文本</td> 
    </tr>
  </tbody>
    
  <tfoot>
    <tr>
      <td>TFOOT 中的文本</td>
    </tr>
  </tfoot>

</table>	
```



##### form：表单，搜集不同类型的用户输入

> 表单元素：文本框、密码框、单选框、复选框、下拉框、按钮，一个表里包含多个表单元素

```html
<!--点击按钮跳转到home页面-->
<form action="/day01/home.html" method="get">
	<input type="text"><br/>
    <input type="password"><br/>
    <!--两种注册方式-->
    <input type="submit" value="注册">
    <button type="submit">登录</button>
</form>
```

###### action：定义提交表单数据的位置

```html
<!--提交表单数据到action_page.php页面,也可以是Controller映射地址-->
<form action="action_page.php">
	<input type="text" name="firstname">
	<input type="submit">
</form> 
```

###### method：定义提交请求的方式get/post

get请求：get把参数包含在URL中，get请求直接将请求头和数据data发送，只发一个包

post请求：post通过request body传递参数，post先发送请求头，服务器响应才发送数据data，发两个包

> 区别：
>
> 1. GET在浏览器回退时是无害的，而POST会再次提交请求。
> 2. GET产生的URL地址可以被赋值，而POST不可以。
> 3. GET请求会被浏览器主动cache，而POST不会，除非手动设置。
> 4. GET请求只能进行url编码，而POST支持多种编码方式。
> 5. GET请求参数会被完整保留在浏览器历史记录里，而POST中的参数不会被保留。
> 6. GET请求在URL中传送的参数是有长度限制的，而POST没有，取决于不同浏览器的地址栏长度限制
> 7. 对参数的数据类型，GET只接受ASCII字符，而POST没有限制。
> 8. GET比POST更不安全，因为参数直接暴露在URL上，所以不能用来传递敏感信息。
> 9. GET参数通过URL传递，POST放在Request body中。

###### enctype：提交的数据以什么形式传输

```html
<!--将数据以二进制形式提交(就可以传输图片)-->
<form action="action_page.php" enctype="multipart/form-data">	
	<input type="text" name="firstname">
	<input type="submit">
</form> 
```



##### input：输入文本框

```html
<input>文本内容</input>
```

###### type：文本类型

```html
<!--输入框-->
<input type="text">	<!--text：输入文本，正常显示文本-->
<input type="password">	<!--password：输入密码，默认显示*-->

<!--单选、复选框-->
<input type="radio">	
<input type="checkbox">
<!--给多个单选、复选框使用name属性设定为一组，就可以实现单选、实现多选数据打包提交-->
<input type="radio" name="sex">男
<input type="radio" name="sex">女
<input type="checkbox" name="hobby">吃饭
<input type="checkbox" name="hobby">打游戏
<!--单选、复选框可以设置默认值，默认勾选-->
<!--两种都可以-->
<input type="radio" name="sex" checked>男
<input type="radio" name="sex" checked="checked">女

<!--提交按钮，页面展示为一个Button按钮-->
<input type="submit">
<!--重置按钮，页面展示为一个Button按钮,点击重置所有表单内容(清空/复位)-->
<input type="reset">
<!--设置为按钮，按钮显示文本为点一下，点击触发onclick中的事件“你好”-->
<input type="button" value="点一下" onclick="alert('你好')">
```

###### placeholder：输入框内置背景文字

```html
<input type="text" placeholder="请输入管理员登录账号">
```

###### maxlength：设定输入文本框的最大输入长度

```html
<input type="text" placeholder="请输入管理员登录账号" maxlength="20">
```

###### title：鼠标悬停在文本框显示的文字

```html
<input type="text" placeholder="请输入管理员登录账号" maxlength="20" title="账号">
```

###### name：提交到后台的属性名

```html
<input type="text" placeholder="请输入用户名"name="loginName">
```

后台：

```java
// 通过对应name的值获取对应表单输入框参数
String xxx = req.getParameter("对应的name值")
```



##### label：将内容和输入框进行绑定

```html
<!--绑定输入框，根据id来绑定-->
<!--将用户名三字绑定输入框，for属性的参数为要绑定输入框的id-->
<!--具体效果：点击文字也可以选中绑定的输入框，增加用户体验-->
<label for="uname">用户名:</label>
<input id="uname" type="text" placeholder="请输入用户名">
```



##### select：下拉框

###### 配合option：框内选项

```html
<select>
	<option>请选择</option>
	<option>选项一</option>
	<option>选项二</option>
</select>
```



##### button：按钮

```html
<!--显示一个登录按钮-->
<button>登录</button>
```



##### iframe：内置窗体(在一个页面中展示另一个页面)

###### src：指定窗体内要展示的页面路径，可以是互联网资源

```html
<iframe src="http://www.baidu.com" width="100% height="100%"></iframe>
```

###### frameborder：窗体框线

```html
<iframe frameborder="0"></iframe>	<!--将框线隐藏-->
```

