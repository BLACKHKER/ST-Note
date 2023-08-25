



# 1、注解 @interface

#### 元注解(官方注解)：@Target、@Retention

```java
@Target(ElementType.类型)	// 描述注解的使用范围	ElementType：元素类型 
@Target(ElementType.FIELD)  // 该注解只能放到属性头上	类型：Field(属性)、Method(方法)等其他类型
@Retention(RetentionPolicy.生命周期)	// RetentionPolicy：该注解的生命周期
@Retention(RetentionPolicy.RUNTIME) // runtime：运行时也存在生命周期
```



> 跟创建类、接口、枚举一致

#### 创建自定义注解：

```java
// @interface + 注解名
public @interface 注解名 {}
public @interface MyAnnotation {}	// 创建一个注解MyAnnotation
```

##### 1.创建自定义注解需要在注解头声明官方注解：

```java
@Target(ElementType.FIELD)  // 该注解只能放到属性头上
@Retention(RetentionPolicy.RUNTIME) // 该注解的生命周期，runtime代表在运行时也有
public @interface MyAnnotation {}
```



##### 2.注解的参数：

```java
public class Test{
    @MyAnnotation(id = 1, name = "刘备")	// 声明注解，没有Default的都要给值
    public void test1(){}
}

// 参数类型 + 参数名();
@Target(ElementType.METHOD)  // 该注解只能放到方法头上
@Retention(RetentionPolicy.RUNTIME) // 该注解的生命周期，runtime代表在运行时也有
public @interface MyAnnotation {
    int id();	// 注解没有默认值，则声明注解(在别的上面添加该注解)的时候必须给参数赋一个值。
    String name()
    int age() default 1;	// default：默认值 如果默认值为-1，则代表不存在
}
```

###### 如果注解只有一个参数，那么参数名建议用value,好处是：

```java
public class Test{
    @MyAnnotation2()	
    public void test2("123"){}		// 不用写value = "123"，可以直接写参数
}
@Target(ElementType.METHOD)  
@Retention(RetentionPolicy.RUNTIME) 
public @interface MyAnnotation2 {
    String value();
}
```









# 2、前端

## HTML

#### 转义字符：

```heml
&nbsp: 空格	&copy：版权符号	
```



#### 标签：

##### h1-h6：标题(由大到小)

```html
<h1>智慧园区信息化管理系统</h1>
```



##### p：段落

```html
<p>该代码标记了一个段落</p>
```



##### title：控制浏览器标签页显示的文字

```html
<title>智慧园区管理系统</title>
```



##### a：锚、超链接标签

```html
<a>点我跳转链接</a>
```

###### href：设定点击后跳转的链接，可以是本地页面，也可以提交一个请求

```html
<a href="http://www.baidu.com">点我跳转百度</a>
<!--让超链接标签无作用-->
<a href="javascript:void(0)">点我没有反应</a>
<a href="value='/user?method=selectById&id="+user.id+""/> <!--提交到名为user的servlet-->
```

###### target：通过对应属性值选择打开页面的方式

```html
<a href="http://www.baidu.com" target="_blank">点我跳转百度</a>	<!-- _blank -->
<!-- a标签target属性可以设置如下取值, 作用分别对应如下 --> 
<!-- _self 默认值, 在当前窗口或者框架中打开连接 -->
<!-- _blank 在新窗口或新的标签页中打开链接 -->
<!-- _parent 在父级的框架中打开, 如果自身是顶层, 与_self相同 -->
<!-- _top 在顶层的框架中打开; 当不在框架中使用则清除所有内容在当前窗口显示连接文档 -->
<!-- frameName 在指定的iframe内联框架中打开页面 -->
```

##### style：link、hover、active

```css
a:link{
	<!--未点击状态-->
}
a:hover{
	<!--指针在上方时状态-->
}
a:active{
	<!--点击但鼠标未松开-->
}
```



##### img：在网页中插入图片

```html
<img src="1.jpg">	<!--打开根目录下的1.jpg-->
```

###### alt：在地址有问题的时候，显示alt内的文字来替代图片

```html
<img src="1.jpg" alt="这张图片是一个范爷">
```



##### input：输入文本框

```html
<input>文本内容
```

###### type：文本类型

```html
<!--输入框-->
<input type="text">	<!--text：输入文本，正常显示文本-->
<input type="password">	<!--password：输入密码，默认显示*-->
<!--单选、复选框-->
<input type="radio">	
<input type="checkbox">
<!--提交表单，页面展示为一个Button按钮-->
<input type="submit">
<!--给多个单选、复选框设定为一组，就可以实现单选、实现多选数据打包提交-->
<input type="radio" name="sex">男
<input type="radio" name="sex">女
<input type="checkbox" name="hobby">吃饭
<input type="checkbox" name="hobby">打游戏
<!--单选、复选框可以设置默认值，默认勾选-->			<!--两种都可以-->
<input type="radio" name="sex" checked>男
<input type="radio" name="sex" checked="checked">女
<!--设置为按钮，按钮显示文本为点一下，点击后弹窗输出“你好”-->
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
req.getParameter("对应的name值")
```



##### 列表

###### ol：有序列表

```html
<ol type="a" start="2">	<!--以小写字母排序,从第二个开始(b)-->
    <li>🍎</li>	<!--type有1、a、A、I、i 数字、英文大小写、罗马大小写-->
    <li>⚽</li>
    <li>🤑</li>
</ol>
```

###### ul：无序列表

```html
<ul  style="list-style: none">	<!--不显示排序圆点-->
    <li>🍎</li>
    <li>⚽</li>
    <li>🤑</li>
</ul>
```



##### button：按钮

```html
<button>登录</button>	<!--显示一个登录按钮-->
```



##### select：下拉框

###### 配合option：

```html
<select>
	<option>请选择</option>
	<option>选项一</option>
	<option>选项二</option>
</select>
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



##### label：将文字和输入框进行绑定

```html
<!--绑定输入框，根据id来绑定-->
<label for="uname">用户名:</label> <!--将用户名三字绑定输入框，for属性的参数为要绑定输入框的id-->
<input id="uname" type="text" placeholder="请输入用户名">
```



##### table：一个表格

###### tr、th、td：表示行、表头、单元格

```html
<table>
	<tr>	<!--代表单元格的一行-->
    	<th>Month</th>	<!--定义表头，跟td唯一的区别是该标签定义的字会加粗-->
    	<th>Savings</th>
  	</tr>
	<tr>
		<td>January</td>
		<td>100</td>
	</tr>
</table>
```

###### colspan\rowspan：合并列/行

```html
<table>
	<tr>
		<td colspan="2" align="center">January</td> <!--代表合并一行的两个单元格-->
	</tr>
</table>
```

###### border-collapse：合并框线为一行

```html
<table border-collapse:collapse>
	<tr>
		<td colspan="2" align="center">January</td> <!--代表合并一行的两个单元格-->
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
    
  <thead>	<!-- thread内部必须拥有tr标签 -->
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



##### form：表单，搜集不同类型的用户输入。

```html
<form>
	<input type="text" name="firstname">
	<input type="radio" name="sex" value="male" checked>Male
    <input type="submit" value="Submit">
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

###### enctype：提交的数据以什么形式传输

```html
<!--将数据以二进制形式提交(就可以传输图片)-->
<form action="action_page.php" enctype="multipart/form-data">	
	<input type="text" name="firstname">
	<input type="submit">
</form> 
```



#### 定位：

##### margin：外边距	padding：内边距

###### 两个参数时分别表示上下、左右：

```html
margin：0 10px;	// 上下内边距为0px,左右内边距为10px
```

###### 四个参数时分别表示上、右、下、左(顺时针)：

```html
padding:0,0,0,10px;	// 上右下外边距为0，左外边距为10px
```





#### 选择器：

##### 优先级从高到底：行内样式>id选择器>类选择器>标签选择器

###### id选择器：

```html
#id名 {
	color: green;
}
```

###### 类选择器：

```html
.类名 {
	color: yellow;
}
```

###### 标签选择器：

```html
标签名 {
	color: red;
}
```

###### 选择器相加(类选择器+标签选择器)：

```html
<!--选择类为class的下面的第一个p标签-->
.show+p{	
	background:green;
}
<div class="show"></div>
<p>我是什么颜色？</p>
```

###### 选择器相引(类选择器~标签选择器)：

```html
<!--选择类为class的下面的所有p标签-->
.show~p{	
	background:green;
}
<div class="show"></div>
<p>我是什么颜色？</p>
<p>我是什么颜色？</p>
```



## JS(Java Script)

### 数据类型：

#### 基本数据类型：

number(数字)、boolean(布尔值)、string(字符串)、undefined(未定义)、null(空的)、Symbol(符号)

#### 引用数据类型：

也就是对象类型Object- - (对象)，function(函数)、date (时间)、array(数组)



#### 定义变量：var、let、const

##### 建议用let来定义变量(块级作用域)，因为var是全局变量(全局作用域)，会产生一些BUG。

###### 例如for循环：

```js
for (var i = 0; i < 3; i++) {
	console.log(i);	// 输出i
}								// 正常情况下是输出不了i的，i是for循环体定义的变量
console.log("i的值为：" + i);	// 但是这里可以输出，因为var定义的变量是全局变量，超范围用let则会报错
```

##### const类型的值必须初始化，而且初始值无法修改；类似于final

```js
const num = 10;
```



#### 创建数组：

##### 1、直接量定义数组：

```js
var nums = [1,2,3];	// js中是方括号，不是{}
```

##### 2、new关键字(1)：

```js
var nums = new Array(); // 用构造函数创建一个动态数组
```

##### new关键字(2)：

```js
var nums = new Array(3); // 用构造函数创建一个初始长度为三的数组
```

##### new关键字(3)：

```js
var c = new Array("8");	// 用构造函数创建一个带初始值的数组，而该数组的长度为1
```

> js里的数组是动态扩容的。创建数组会用空占位，所以push会在创建数组的长度后面继续添加：

```js
var a = new Array(3); // 创建一个长度为三的数组
names.push("张三");	// 添加一个张三
console.log(names.length);	// 长度为4
```

#### 数组添加

##### 数组名.push()：向数组“末尾”添加新元素

```js
var fruits = ["Apple","Orange","Banana","Strawberry"];
fruits.push("Mango");	
// 添加新元素，新数组不需要接收，直接修改原数组
var boxs = [...];	// 带对象的数组
var ids = [];	// 空数组
boxs.forEach(box => {	// 遍历boxs集合，拿到对象的id
    ids.push(box.id);	// 就会直接修改原数组ids的值
});
```

##### 数组名.unshift()：向数组“开头”添加新元素



#### 创建函数(方法)：

```js
function 函数名称(参数列表) {
	return 值;
}
```

##### 调用：

###### 无参无返回：

```
function test1() {

}
```



##### 构造方法：

```js
function Employee (id,name) {
	this.id = 1;	// this代表当前对象，构造方法上面没定义该属性，JS会动态创建一个属性
	this.name = "张三";
}
p1 = new Employee(2,"关羽");	// 创建一个对象
```





#### 常用方法

##### console.log：打印语句(println)

```js
console.log("要输出的语句");
```



##### 注意事项：

##### 1、判断字符串长度的.length是属性，不是.length()。

##### 2、new关键字调用构造函数。js中任何函数都可以看作构造函数

##### 3、subString(参数一，参数二)中的参数二不是指截取几位，而是从参数一截取到参数二的索引下标





#### JSON：统一前后端交互的数据类型

> JSON可以以字符串形式保存一个对象，后端返回数据就可以通过JSON来统一格式；

##### JSON保存一个对象：

```js
var 数据名 = '{"key":value}' or "{'key':value}"
var str = '{"name":"刘备","age":100}'	// 外面用'为了和内部""进行区分
```



##### 保存带对象属性的对象：

```js
var json1 = {"id": 1, "name": "刘备", "wujiang": {"id": 1, "name": "关羽"}};
console.log(json1.id);
console.log(json1.name);
console.log(json1.wujiang.id);
console.log(json1.wujiang.name);
```



##### 保存带List属性的对象：

```js
var json2 = {
    "id": 1, 
    "name": "刘备", 
    "dutyList": [{"did": 1, "dname": "君主"}, {"did": 2, "dname": "武将"}]};	// 集合
console.log(json2.id);
console.log(json2.name);
console.log(json2.dutyList[0].did);
console.log(json2.dutyList[0].dname);
console.log(json2.dutyList[1].did);
console.log(json2.dutyList[1].dname);
```



##### 假定上面的JSON字符串”str“是后端传到前端的，前端将JSON格式字符串对象转换为真正的JS对象：

###### parse()：将JSON格式字符串转换为js对象

```js
JSON.parse(JSON格式字符串)
var duiXiang = JSON.parse(str)
```

###### stringify()：将JSON对象转换为JSON格式字符串

```js
JSON.stringify(JSON对象)
var str = JSON.stringify(duixiang)
```







#### HTML DOM：文档对象模型，又称为文档树模型。

> 一套操作页面元素的API，DOM可以把HTML看作文档树，通过DOM提供的API可以对树上的节点进行操作。
>
> 基本概念：HTML DOM 文档对象是您的网页中所有其他对象的拥有者。
>

1. DOM 是 HTML 的标准对象模型和编程接口。它定义了：

2. 作为*对象*的 HTML元素

3. 所有 HTML 元素的属性

4. 访问所有 HTML 元素的方法

5. 所有 HTML 元素的事件

   换言之：HTML DOM 是关于如何获取、更改、添加或删除 HTML 元素的标准。

##### DOM常用操作：

1. 获取文档元素

2. 对文档元素进行增删改查操作

3. 事件操作

   

##### document：

document也是window对象地属性之一；

document对象是documentHTML的一个实例，也是window对象的一个属性，因此可以将document对象作为一个全局对象来访问。





##### getElementBy(类型)：通过类型查找标签(元素、对象)	element：元素

```js
document.getElementById("标签的id")
document.getElementById("rows")
```

###### 通过标签名：

```js
document.getElementsByTagName("name")
```

###### 通过类名：

```js
document.getElementsByClassName("name")
```

###### 通用类型：

```js
document.querySelector("id、类选择器")
```



##### 获取某个标签元素的值：标签.value(属性)

```js
<input type="text" id="rows"/>	// 假设输入5
let num = document.getElementById("rows").value	// num的值为5
```



##### innerHTML：改变指定标签元素的值

```html
<p id="p1">刘备</p>
<script>b
	document.getElementById("p1").innerHTML = "关羽";	// 将p标签内的值修改为关羽
</script>
```



#### 事件:

##### 不提交、不和Controller交互：

```js
document.querySelector("选择器").onclick = function(){
	// 要触发的事件
}
```

###### 以id、类选择器为例：点击按钮触发事件

```html
<button id="show">点我显示消息框</button>
<button class="cshow">点我显示class消息框</button>
<script>	// 点击按钮触发弹窗
    document.querySelector("#show").onclick = function () {
        alert("hello");
	}
    document.querySelector(".cshow").onclick = function () {
        alert("classhello");
	}
</script>
```

###### 如果只有一个button/提交标签，也可以直接写标签名：

```html
<button>点我显示消息框</button>
<script>	// 点击按钮触发弹窗
    document.querySelector("button").onclick = function () {
        alert("hello");
	}
</script>
```



##### 提交、跳转：

> onclick会直接跳转，不显示alert，这时需要更改不在点击的时候触发，改为提交的时候：

```js
// onsubmit
document.querySelector("选择器").onsubmit = function(){
	// 要触发的事件
}
```



#### HTML BOM：

##### window对象：

> 所有的浏览器都支持window对象，它支持浏览器窗口。
>
> 所有的js全局对象，函数以及变量都能自动成为window对象地成员。
>
> 全局变量是window对象的属性，全局函数是window对象的方法。
>
> 甚至（HTML DOM 的）document 对象也是 window 对象属性

```js
window.document.getElementById("header");
```

###### 属性：





##### location.href：指定一个URL地址

```js
function urlTest() {
	location.href="URL"
}
```



---



## JQuery：创造EASY jS

#### 在线引入JQuery：直接写在HTML里

```html
<script src="https://code.jquery.com/jquery-3.1.1.min.Js"></script>
```

> ##### 写JQuery要声明：写一个$符号
>

#### $()：工厂函数

> ()就是工厂函数

```js
$("标签名/id、类选择器")
$("form")	// 将form标签转换为JQuery对象,JQuery对象其实就是JS对象，但是JS对象!=JQuery对象
```

#### API：

##### on()：触发事件

```js
on("事件名",触发该事件后执行的代码(匿名函数));
```



##### each()：遍历每个对象

###### 遍历所有复选框对象：

```js
$JQuery对象.each(function (i) {	// i会从0开始自增
	data[i] = $(this).val();	// 获取当前对象的值保存到数组data中
});
```



##### val()：当前对象的值

```js
if($(this).val() == '')	// 如果当前对象的值不为空	
```



##### serialize()：序列化表单值，创建 URL 编码文本字符串

###### 可以选择一个或多个表单元素（比如 input或textarea以及select），或者 form 元素本身：

```html
<form id="form1">
	<!--假设有多个input、-->
</form>
<!--JQuery-->
<!--返回name="123"&password="123"URL编码请求字符串-->
<!--可以用于ajax请求的data属性-->
$("#form1").serialize()
```

###### 序列化的值可在生成AJAX请求时用于URL/data中：

```json
name="123"&password="123"	// 用于前端请求的URL传参
```



##### JSON.parse(JSON字符串)：将JSON格式字符串转换成对象数组

```js
let houseData = JSON.parse(data);
```



##### JQuery实现点击触发事件(提交)

```js
$("标签名/id、类选择器").on("事件名",触发该事件后执行的代码(匿名函数));
$("form").on("submit",function() {
    alert("执行JQuery");
});
```



##### 验证元素是否非空：

```js
var 变量名 = $("选择器").val()	// 获取值保存
if (变量名.length == 0){...}	// 执行非空验证
```



##### JQuery实现点击登录按钮验证是否非空，提交表单：

```js
<script>
    //  鼠标点击登录按钮的时候进行登录验证(点击按钮时执行这个函数)
    document.querySelector("#signup_forms_submit").onclick = function () {

    //  把html标签转换为js对象
    let emailObj = document.querySelector("#signup_name")

    //  获取对象里面的值：
    let uname = emailObj.value;
    console.log("用户名是：" + uname)

    //  获取密码框的值
    var upwd = document.querySelector("#signup_password").value;

    //  用户名和密码都不能为空！
    if (uname != "" && upwd != "") {
        //  TODO 提交数据到后台
        //  数据打包发送到后台，直接提交form表单
        document.querySelector("#loginForm").submit();
        // alert("登陆成功@！")
    } else {
    	confirm("用户名或密码不能为空！")
    }
	}
</script>
```









### AJAX：异步请求

##### 语法：

```jquery
$.ajax({url,settings(参数列表)})
```



##### settings：

- ###### url：设置请求的映射地址

- ###### data：设置请求时携带参数

- ###### type：设置请求方式(get、post)，默认get

- ###### dataType：设置返回参数的类型(一般设置为JSON)

- ###### contentType：上传到服务器的内容(data)的编码类型

- ###### success：请求成功执行的操作，该属性的值一般是一个函数function(){}

- ###### error：请求失败执行的操作，一般也是一个函数

- ###### async：表示当前请求是一个异步请求，默认为true，false则为同步请求



#### 注意：异步请求无法获取Session中的值，后端传值需要将数据序列化成JSON格式的字符串，再通过响应对象(response).getWriter().write(JSON字符串)返回参数



##### 实例：

```json
$.ajax(
	url : "/select",
	data : "uname='刘备'&pwd='123'",// 后台如果是RequestBody可以是空的：JSON.stringify({})
    type: "post",
    // 预期服务器返回的数据类型
    dataType: "json",
    //  发送信息至服务器时内容编码类型
    contentType: "application/json"
	success : function(data){
    	/*
    		方法中的data为后台返回的数据，后台通过以下操作返回数据：
            List<Userinfo> userinfos = this.selectAll();	-- 调用方法获取到List
            String jsonStr = JSON.toJSONString(userinfos); -- 通过fastJSON转换JSON
            resp.getWriter().write(jsonStr); -- 响应对象.getWriter().write(json)
    	*/
	}
})
```

#### FastJSON参考框架文档；







## VUE：

### 引入Vue:

```html
<!--引入Vue.js文件-->
<script type="text/javascript" src="本地资源路径(js/vue.js"></script>	
```



### 参数列表：

#### el：将Vue挂载到某一标签上(div)

```html
<body>
    <div id="app"> Vue作用范围 </div>	<!--Vue的作用范围是该div内-->
<script>
	var v = new Vue({
        el: "#app" // 要挂载的标签的id
        // 其他参数列表
    })
</script>
</body>
```



#### data：保存当前Vue对象中定义的值

```html
<script>
	var v = new Vue({
        el: "#app" // 要挂载的标签的id
        data: {
        	age: 20,
        	sex: 1,
        	text: "value1",	// 定义普通值1
        	text2: "<h1>value2</h1>",	// 定义带标签的值2
        	attribute: "attributeTest"	// 定义一个值，用于给标签的属性赋值(标签属性绑定)
            user: {"uname": "嬛嬛", "age": 20, "address": "成都"},	// 定义对象
            stus: [	// 定义数组，数组里存储了多个对象
                {"sname": "小张", "age": 21, "address": "北京"},
        		{"sname": "小蒲", "age": 22, "address": "上海"},
            	{"sname": "小向", "age": 23, "address": "杭州"}
    		],
        }
    })
</script>
```



##### 插值表达式 / v-text:参数名：直接输出属性值

```html
<!--1.插值表达式-->
<!--{{参数名/属性名}}-->
<h2>{{text}}</h2>	<!--输出value1-->
<!--{{对象名.属性}}-->
<h2>{{user.uname}}</h2>	<!--输出嬛嬛-->
<!--可以写表达式-->
<h2>{{age+1}}</h2>	<!--输出age+1,21-->
<!--三目运算符-->
<h2>{{sex == 1 ? 男 : 女}}</h2>
<!--2.v-text文本的绑定-->
<!--v-text="参数名"-->
<h2 v-text="text"></h2>	<!--输出value1-->
```



##### v-html:参数名：属性值带标签，以标签格式输出

```html
<!--v-html带标签的文本绑定-->
<h2 v-html="text2"></h2>	<!--输出h1标签，内容为value2-->
```



##### v-bind:参数名：绑定标签属性

```html
<!-- v-bind:绑定标签属性案例 -->
<!-- 绑定name属性,该标签name属性的值为"attribute" -->
<div v-bind:name="attribute"></div>
```

###### 简写：只在属性名前写一个冒号(:)来绑定

```html
<div v-bind:name="attribute" :class="attribute" :title="attribute">绑定标签属性简写</div>
```



##### v-model:参数名：双向的属性绑定

```html
<!-- v-model:双向数据绑定案例 -->
<input type="text" v-model="txt"/>	<!-- 修改该输入框的值会将data中txt属性的值一并修改 -->
<div v-text="txt"></div>	<!--所以这个div展示的数据也会跟着改变-->
```





#### methods：保存当前Vue对象中的定义的函数(方法)

```html
<script>
    var vm = new Vue({
       	// 定义Vue函数
        methods: {
            // 定义函数 函数名:匿名函数
            func1: function () {
                alert("点击事件绑定成功！");
            }
        }
    });
</script>
```



##### v-on:事件名="函数名()"：给某个标签绑定事件

```html
<!-- 给按钮绑定点击事件  自动调用func1函数 -->
<button v-on:click="func1()">绑定事件按钮</button>
<!-- 绑定事件简写 -->
<button @click="func1">绑定事件简写按钮</button>
```





#### 生命周期函数(钩子函数)

##### created: 回调函数：在Vue对象创建时执行的函数

```html
<script>
    var vm = new Vue({
       	//加载页面时调用methods中的func1方法
        created: function () {
    		this.func1();
		}
    });
</script>
```



##### mounted:回调函数：当页面上所有内容加载完成后才调用

```html
<script>
    var vm = new Vue({
        //当页面上所有内容加载完成后调用methods中的func1方法
       	mounted: function () {
    		alert("mounted已调用！")
		}
    });
</script>
```





#### v-if / v-else / v-if-else：分支语句

> v-if="布尔表达式"：

```html
<div id="app">
    <span v-if="num >= 90 && num <= 100">A</span>
    <span v-else-if="num >= 80 && num < 90">B</span>
    <span v-else-if="num >= 60 && num < 80">C</span>
    <span v-else="num < 60">D</span>
    <br>
    <input type="text" v-model="num">	<!--双向绑定num-->
</div>
<script type="text/javascript">
    var vm = new Vue({
        el: '#app',
        data: {  
            num: 10
        }
    });
</script>
```





#### v-for：循环

##### 循环遍历数组中所有对象：

> v-for:"循环变量 in 被遍历集合(数组)"
>
> 循环变量.属性名

##### 示例：

```html
<div id="app">
    <table>
        <tr v-for="student in students">
            <td>{{student.sname}}</td>
            <td>{{student.age}}</td>
            <td>{{student.address}}</td>
        </tr>
    </table>
</div>
<script>
    var vm = new Vue({
        el: '#app',
        data: {
            students: [
                {"sname": "小张", "age": 21, "address": "北京"},
                {"sname": "小蒲", "age": 22, "address": "上海"},
                {"sname": "小向", "age": 23, "address": "杭州"}
            ]
        }
    });
</script>
```





#### Axios：Vue中的异步请求(ajax)

> 异步请求不能在后端跳转页面，要在前端实现：window.locatioin.href = "url"

```html
<!--引入axios的js库-->
<script type="text/javascript" src="本地资源路径(js/axios.js)"></script>
```



##### axios.请求方式("后端映射地址?参数1&参数2").then(后端响应JSON数据 => {回调函数})

###### get请求示例：

```html
<script>
/* get请求第一种传参方式：拼接字符串 */
axios.get("/html95/vue?name=" + this.user.uname).then(res => {
    console.log(res);	// res: 表示后端响应的信息，其中有参数：data
    console.log(res.data);	// res.data 表示后端响应信息中携带的数据
    this.user = res.data	// 把数据赋值给user变量
});

/* get请求第2种传参方式：使用params进行传参 */
axios.get("/day10/UserServlet", {params: this.user}).then(res => {
    this.user = res.data	// 把数据赋值给user变量
});
</script>
```

##### 实例：

```html
<script type="text/javascript">
    var vm = new Vue({
        el: '#app', 
        data: {  
            user: {
                "name": "刘备",
                "sex": "男",
                "age": 60,
                "phone": "1"
            }
        },
        // 加载页面之前调用methods中的selectUserById方法
        created: function () {
            this.selectUserById();
        },
        methods: {
            selectUserById: function () {
                //发送异步请求，访问控制器UserServlet
                axios.get("/day10/UserServlet").then(res => {
                    this.user = res.data	// 把后端返回的JSON数据赋值给user变量
                });
            }
        }

    });
</script>
```







## Element：基于Vue的前端模板

```html
<!-- 引入ElementUI的css样式 -->
<link rel="stylesheet" href="https://unpkg.com/element-ui/lib/theme-chalk/index.css">
<!-- 引入ElementUI的js库 -->
<script src="https://unpkg.com/element-ui/lib/index.js"></script>
```







---



### 快速构建Web项目：

#### 配置Tomcat：

##### 1、添加Tomcat：

![image-20221013190936825](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20221013190936825.png)

###### 取消打勾：

![image-20221013191019609](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20221013191019609.png)

##### 2、将项目变成WEB项目：

![image-20221013191044092](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20221013191044092.png)



![image-20221013191104957](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20221013191104957.png)

##### 3、在tomcat里添加Artifact，发布成一个目录：

![image-20221013191128468](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20221013191128468.png)

![image-20221013191157107](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20221013191157107.png)

##### 取逻辑名：

![image-20221013191354319](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20221013191354319.png)

##### 删除jsp：

![image-20221013192359076](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20221013192359076.png)

##### 将前端页面拖进web文件夹后即可在Tomcat服务器(浏览器)中访问：

![image-20221013192645389](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20221013192645389.png)



#### 设置为主页面：

##### 访问主页需要输入很长一段：

![image-20221013194630800](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20221013194630800.png)

##### 可以将一个页面设置为主页面，只输入根目录(逻辑名)就能直接访问(ip:8080/cloudStudy/)：

```xml
<welcome-file-list>
	<welcome-file>jumpPage.html</welcome-file>
    <!--绝对路径，此代码表示将根目录(web)下的jumpPage设置为访问根目录展示的页面-->
</welcome-file-list>
```

![image-20221015233457686](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20221015233457686.png)

##### 但是这样访问没有CSS、js等修饰：

![image-20221013194909013](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20221013194909013.png)

##### 解决这个问题使用js代码实现：

#### window.location.href：在当前页面打开指定路径的页面(设置一个伪跳转)

```js
window.location.href = "login/test.html";
```

![image-20221015234656254](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20221015234656254.png)

```html
<script>
    // 以下代码是在哪里执行的
    // 结论：js代码是在客户端那边执行的。客户端就是浏览器!!!!
    // DOM模型，操作网页的内容
    window.location.href = "login/test.html";;//表示在此页面打开指定路径的页面，参数必须是绝对路径
</script>						
```

XML设置默认主页面，就可以将“跳转页面”设置为主页面，由“跳转页面”来展示真正的主页面。



---



## maven

##### 提供一个固定格式的XML语句，自动下载JAR包；

#### 配置：

##### 1、右键项目根目录，Add Framework Support

![image-20221014002941733](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20221014002941733.png)

##### 2、勾选maven：

![image-20221014003047449](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20221014003047449.png) 

##### 3、自动生成pom.xml：

![image-20221014003310382](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20221014003310382.png)

##### 4、添加依赖：

![image-20221014003804671](S:\TypoaPicture\image-20221014003804671.png)

```xml
<dependencies>
	<dependency>
		<!--...直接在下载网站拷贝-->
	</dependency>
</dependencies>	<!--首次下载，标签里面的会显示红色，表示还未下载到本地-->
```

##### 5、下载到本地：

> 可以选择阿里云服务器的JARmaven路径，下载速度快；

写完XML右上角会有一个![image-20221014004129289](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20221014004129289.png)图标，点击即开始下载。



---

## Tomcat



### tomcat服务器端返回的状态码

##### 2XX 表示成功：

200 表示客户端的请求在服务器端被正常处理。
204 表示请求被处理成功但是没有资源返回。
206 表示客户端进行了范围请求，而服务器成功执行了get（）请求。

##### 3XX 表示重定向：

301 表示永久重定向。
302 临时重定向。
303 与302有相同的功能，都表示请求对应着另一个URI，但是303使用了get()方法。
304 表示服务器允许请求访问资源，但没有满足条件的情况。

##### 4XX 表示客户端错误：

400 请求的报文中存在语法错误。
401 发送的请求需要HTTP的认证。
403 请求访问资源被服务器拒绝。
404 服务器无法找到请求的资源。

##### 5XX 服务器错误：

500 服务器端在执行请求时发生错误或者是Web应用存在故障。
503 服务器超负载或者正在停机维护。



---



## HttpServlet：

#### Servlet生命周期：

##### 客户端向服务器端发出请求(点击按钮提交表单submit) --> 服务器解析请求 --> 服务器创建Servlet对象 --> Servlet对象调用init方法 --> 

###### init()方法：

什么时候被调用： init()方法只会被调用一次，是在第一次访问or创建Servlet 的时候被调用，在后续的每次请求时都不会再调用方法了。
作用： 用于 Servlet 的初始化，可以简单地创建或加载一些数据，这些数据将被用于 Servlet 的整个生命周期。

#####  --> 调用service方法(req.get获取数据进行处理) --> 输出响应信息(resp响应对象转发、重定向到另一个页面等)

#####  --> 响应给客户端 --> 调用destroy()方法(不再路由服务器接收到的请求)

###### destory()方法：

关闭服务器时自动调用，如果手动调用，servlet被销毁，但是并不立即被回收，再次请求时，并不重新初始化



##### 当点击网页上的登录按钮时，Tomcat会去调用Java里的HttpServlet类的service方法，

##### 不是我们自己的方法，那么可以手动继承HttpServlet类并重写该方法：

```java
import javax.servlet.http.HttpServlet;	//	先导包，手动引入并下载
public class LoginController extends HttpServlet{
	//	直接写service，代码提示自动继承
}
```

```java
public class LoginController extends HttpServlet{
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.service(req, resp);	// 删除这行
    }
}
```

##### 重写后依然不能运行，因为当有多个service的情况下，Tomcat不知道该运行哪个类里的service方法。

##### 此时给类添加一个注解，Tomcat就知道该执行哪个类的service方法了：

###### @WebServlet：

```java
@WebServlet	//	添加在类上面
public class LoginController extends HttpServlet{
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.service(req, resp);	// 删除这行
    }
}
```

##### 该注解有一个属性：String[] urlPatterns() default{};	用于映射；

浏览器地址就写：`http://ip地址:端口/项目名/类的映射地址：`

比如：`http://localhost:8080/could/login`

```java
@WebServlet(urlPatterns = "/login")	//映射地址前面必须加斜杠，类和类之间的不能重复，斜杠代表根目录
public class LoginController extends HttpServlet{
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("你成功了！");
    }
}
```

##### 总结：

> 从Tomcat上获取图片：

​	http://localhost:8080/could/a.jpg

> 获取html：

​	http://localhost:8080/could/index.html

以上都有一个对应的路径。

那么获取Java类，could后面写的就是该类的注解：urlPatterns所自定义的地址：

```java
@WebServlet(urlPatterns = "/login")	//	假定是这个
```

​	那么调用执行该类的service方法：http://localhost:8080/could/login即可。

> 注解参数可以简写：

```java
@WebServlet("/login")
```







### 提交表单&URL获取传参：

#### 客户端-->Tomcat服务器端：HttpServletRequest

##### http://localhost:8080/could/login现在可以通过该链接访问我们指定的login方法；

> 方法的参数则可以通过URL来进行传递，格式为(一个参数)：

```java
http://localhost:8080/could/login?参数名=值
http://localhost:8080/could/login?uname=zhangsan
```

> 两个参数用&连接：

```java
http://localhost:8080/could/login?uname=zhangsan&pwd=123456
```

> 当客户端通过URL向Tomcat发出请求的时候，该请求会被封装成一个请求对象，对象里有URL传递的值，发送给Tomcat，Tomcat不会处理该对象，会直接把对象传给对应的继承HttpServlet类的service方法；

##### 对象的类型是：HttpServletRequest 类型

```java
@Override
protected void service(HttpServletRequest req, HttpServletResponse resp) throws Exception {		//HttpServletRequest req，req是请求对象
	System.out.println("你成功了！");
}
```

##### getParameter()：获取HttpServletRequest 对象的值(URL里的参数)：

```java
http://localhost:8080/could/login?uname=zhangsan;
//  语法：请求对象.getParameter("参数名")	// 参数名就是输入框<input>的name参数写的值
String uname = req.getParameter("uname");	//默认是String，用String接收
System.out.println("用户名是：" + uname);	// 输出zhangsan
```

> 获取不到值需要给输入框写一个Value(默认输入框值)：

```html
 <tr>
     <td>爱好</td>
     <td>		<!--value就是要获取的值--> <!--name就是getParameter()里的参数名-->
         <input value="看电影" name="like" type="checkbox">看电影
         <input value="看书" name="like" type="checkbox">看书
         <input value="打篮球" name="like" type="checkbox">打篮球
	</td>	<!--name一致，表示他们是一组复选框，传值的时候会传递整组勾选的值-->
</tr>
```

###### HttpServletRequest对应的方法：

![资源分配图](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/20200305162823909.jpg)



###### 根据不同的参数调用同一Controller的不同方法：

在页面提交、指定Controller映射地址后写一个问号跟上参数名、参数值：

```jsp
<!--controller映射地址?参数名=参数值-->
<a lay-href="org?opt=list">机构管理</a>	<!--传递一个opt，值为list-->
<a lay-href="org?opt=del">删除机构</a>	<!--传递一个opt，值为del-->
```

后台Controller根据不同的值来做不同的数据处理：

```java
// 首先获取参数以及参数值
String opt = req.getParameter("opt");
if (opt.equals("list")) {
	// 展示相关操作
} else () {
	// 删除相关操作
}
```









#### Tomcat服务器端-->客户端：HttpServletResponse

> 传回客户端也有对应的对象：HttpServletResponse

##### 响应客户端方案 	

##### 方案一：

###### 创建一个打印流：

```java
PrintWriter writer = resp.getWriter();	// 获取打印流对象writer
```

###### 调用write()：

```java
writer.write("你好收到了");	// 向客户端(浏览器)输出“你好收到了”
```

> 注意：中文输出到网页会乱码；解决方式：

```java
// 防止接收中文乱码
接收客户端对象.setCharacterEncoding("UTF-8");	
req.setCharacterEncoding("UTF-8");	

// 防止返回中文乱码
响应客户端对象.setHeader("响应头属性名","值");// 设置响应头通用方法
resp.setHeader("Content-Type","text/html;charset=utf-8");
响应客户端对象.setContentType("text/html;charset=字符集");	// 设置响应头ContentType
resp.setContentType("text/html;charset=utf-8");
```

##### 如果输出HTML对应标签类型的内容：

```java
writer.write("<h1 style = 'color:red'>我是西门吹雪</h1>");	// 直接在字符串里写上标签
writer.write("<script>alert('请问吃饭了吗？')</script>");	// JS同理，弹出窗口alert
```

###### 最后关闭流：

```java
writer.close();
```



##### 方案二：转发器

> 判断用户登录成功/登陆失败，我们都要给用户返回一整个页面，就需要转发器：
>

###### getRequestDispatcher()：获取转发器

```java
接收客户端对象.获取转发器("返回页面的绝对路径").forward(接收对象,响应对象);
req.getRequestDispatcher("home.jsp").forward(req, resp);	// 转发根目录下的页面home.jsp
```



##### 方案三：重定向

```java
响应客户端对象.sendRedirect("返回页面的绝对路径");
resp.sendRedirect("/html99/home.jsp");	// 重定向让客户端再发起一个请求访问获取根目录的home.jsp
```

> 重定向需要全路径(加上TomCat配置的WEB应用路径)



##### 转发器和重定向的区别：

1、转发器一次请求，服务器会将客户端请求访问的页面在内部获取到，再转发给客户端；

重定向则是告诉客户端该访问哪里，让客户端重新发送一个请求，自己获取访问的页面。

2、地址栏不同

重定向地址栏会发生变化，转发地址栏不会发生变化；

3、是否共享数据

重定向两次请求不共享数据，转发一次请求共享数据（在request级别使用信息共享，使用重定向必然出错）；

4、跳转限制

重定向可以跳转到任意URL，转发只能跳转本站点资源；

5、发生行为不同

重定向是客户端行为，转发是服务器端行为；





#### 客户端接收服务器端返回的值：根据不同的登录用户返回不同的登录成功/失败页面

##### 实例：显示用户===登陆成功，===部分需要动态显示

##### 方案一：转发实现

```java
// 给接收客户端对象添加一条属性(setAttribute方法)：
接收客户端对象.setAttribute("key", 值);	// 跟Map类似，key好比变量名，值就是该变量的值
req.setAttribute("uname", uname);	// 第二个uname就是之前获取的输入框的账号(用户名)
```

> 配合转发器：

```java
req.setAttribute("uname", uname);
接收客户端对象.获取转发器("返回页面的绝对路径").forward(接收对象,响应对象);
req.getRequestDispatcher("home.jsp").forward(req, resp);	// 返回根目录下的页面home.jsp
// 这样，转发器就会将修改后的响应客户端对象req一起返回给home.jsp页面
```



##### 方案二：重定向实现

###### Servlet除了生命周期外，还有三个作用域：

1. Application(Web容器)(ServletContext)：存活范围最大的对象，只要服务器没有关闭，该对象中的数据就会一直存在。在整个服务器运行过程当中，application对象只有一个。
2. Session(会话)：浏览器未关闭或30分钟不使用该对象。session对象内数据的存活范围也就是session对象的存活范围（只要浏览器不关闭，session对象就会一直存在），因此在同一个浏览器窗口中，无论向服务器端发送多少个请求，session对象只有一个。
3. Request(请求)：仅在当前请求中有效。request表示一个请求，只要发出一个请求就会创建一个request，当客户端向服务器端发送一个请求，服务器向客户端返回一个响应后(请求结束后)，该请求对象就被销毁了；之后再向服务器端发送新的请求时，服务器会创建新的request对象，该request对象与之前的request对象没有任何关系，因此也无法获得在之前的request对象中所存放的任何数据。

> 因为重定向内部实际上产生了两次请求，而req默认是request，第一次请求结束后req就销毁了。 所以如果重定向要实现向客户端发送值的功能，则需要在给req接收客户端对象存值的时候，先获取Session或生命周期更长的对象，再进行存值。

```java
请求对象.getSession	// 获取Session对象，类型是HttpSession;
HttpSession session = req.getSession;	// 先获取生命周期更长的对象Session

作用域对象.setAttribute();	// 给作用域添加值
session.setAttribute("uname", uname);

/*以上两步可以写为一行*/
req.getSession.setAttribute("key、value");
resp.sendRedirect("home.jsp");	// 重定向
```

###### JSP里也可以重定向：

```jsp
<%response.sendRedirect("页面地址");	// 不是resp,是response	%>
```



> 客户端页面将服务器端返回的值：req里的uname获取出来，需要java语句，就要将前端页面改成JSP页面：

##### 客户端页面home.jsp：

###### 写法一，获取值后输出：

```jsp
<%	// 接收req里的的值在jsp里不能直接req.get，而是rquest.get，该方法返回Object
    // 从request作用域取uname值
    Object obj = request.getAttribute("uname");	// 获取接收客户端对象的属性名为uname的值
	<h1>欢迎<%=obj %>登录</h1>	// jsp中输出指定的值：=变量值，类似print 
%>
```

###### 写法二，EL表达式直接取值：

```jsp
<h1>欢迎${requestScope.属性名(别名)}登录</h1> <!--表示接收request作用域的，也有sessionScope-->
<h1>欢迎${requestScope.uname}登录</h1>
<!--
可以不写接收对象requestScope编译器会自动寻找对应的key进行匹配输出request-session- servletContext)
-->
<h1>欢迎${uname}登录</h1>	
```

> 区别就是输出的时候，写法一若没获取到值，会显示NULL，而第二种会显示空。所以建议使用第二种来取值



##### 获取并输出对象\数组\集合里的值：

###### 后台返回数组：

```java
String[] names = {"刘备","关羽"};	// 定义一个名称数组
req.getSession.setAttribute("names",names);	// 第一个names是key，别名,第二个是value，就是数组。
resp.sendRedirect("home.jsp");	// 重定向
```

###### 前台接收并输出：

```jsp
<!--EL表达式取值：-->
<h1>${names}</h1>h1> <!--输出该数组(地址)-->
<h1>${names[0]},${names[1]}</h1>h1>	<!--输出指定key的对应下标的值：刘备，关羽-->
```



###### 后台返回对象：

```java
// 假设有学生类Student，属性id、name
Student stu1 = new Student(1,"张飞");	// new一个张飞
req.getSession.setAttribute("stu",stu1);	// 传一个对象stu1
resp.sendRedirect("home.jsp");	// 重定向
```

###### 前台接收并输出：

```jsp
<h1>id是：${stu.id},name是：${stu.name}</h1>	<!--直接key打点调用属性-->
```

> JSP获取对象属性值底层是调用该类的get\set方法，所以对象对应的实体类必须有对应的get\set方法才能输出



###### 后台返回集合：

```java
ArrayList<Student> stus = new ArrayList<>();
stus.add(stu1);
req.getSession.setAttribute("stuList",stus);
```

###### 前台接收并输出：

```jsp
<h1>${stuList.get(0).id}</h1>	<!--获取key对应集合的第1个对象的id-->
```

##### 遍历则需要JSTL标签库框架，参考框架文档；



---



## JSP ：视图引擎技术

##### 想要拿到响应客户端对象返回的值，显示在HTML页面中，需要在HTML中写java代码，就需要JSP

> 执行流程：服务器端 -> 客户端

服务器先解析，解析后交给响应对象resp返回给客户端。

性能很慢。底层是利用输出流一行一行将页面white()出来的，类似于：

```java
PrintWriter writer = resp.getWriter();  //创建一个输出流
writer.write("<h1 style = 'color:red'>我是西门吹雪</h1>");
```



##### 格式：

```jsp
<标签><%java代码%></标签>
```

###### 多个<%%>标签可以拼接：

```jsp
<标签><% for (int i = 0; i < 3; i++){ %></标签>
<标签><% java代码 %></标签>	<标签><% // 拼接为一个Java语句%></标签>
<标签><% } %></标签>
```



##### 实际应用：

###### 引用资源比如CSS样式表，href需要添加项目的别名：

```jsp
<link rel="sytlesheet" href="根目录(Web别名映射地址)/css/login.css">	<!--连接外部样式表-->
<link rel="sytlesheet" href="could/css/login.css">	<!--could相当于Web蓝点文件夹-->
```

###### 如果Web项目的映射地址修改了，所有的外部样式表也要修改，那么可以用Java代码实现动态获取项目映射地址

```jsp
<link rel="sytlesheet" href="${pageContext.request.contextPath}/css/login.css">
```

在HTML中写JAVA代码不利于维护，JSTL替代JSP：



---



## JSTL：标签库框架，引入和JS搭配的新网页标签

##### 1.需要添加META-INF标签文件到WEB-INF下

##### 2.需要在页面头声明JSTL(1.2)

```js
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %> // 表示使用c标签</c:>
```

##### 3.导包，参考Maven



#### 500jstl报错解决：

##### tomcat版本有关系：

> Tomcat6 实现了 servlet 2.5 和JSP2.1的规范，可以支持JSTL1.2；
>
> Tomcat5实现了 servlet 2.4 和JSP2.0的规范，只能支持JSTL1.1；

##### 如果是使用tomcat7及以上版本出现问题：tomcat7+版本不再支持jstl标签库自动导入，需要自己手动添加。

###### 将jstl1.2.jar中的c.tld(或如果使用jstl1.1版本，将standard.jar中的c.tld)拷出一份来放到WEB-INF路径下

###### web.xml配置中需要如下配置：

```xml
<jsp-config>
      <taglib>
          <taglib-uri>http://java.sun.com/jsp/jstl/core</taglib-uri>
          <taglib-location>/WEB-INF/c.tld</taglib-location>
      </taglib>
</jsp-config>
```



#### out和set：

##### out

|         <c:out value=”aaa”/>          | 输出aaa字符串常量               |
| :-----------------------------------: | :------------------------------ |
|        <c:out value=”${aaa}”/>        | 与${aaa}相同                    |
| <c:out value=”${aaa}” default=”xxx”/> | 当${aaa}不存在时，输出xxx字符串 |


​	

url
　　url标签会在需要URL重写时添加sessionId。
<c:url value="/"/>	输出上下文路径：/day08_01/
<c:url value="/" var="a" scope="request"/>	把本该输出的结果赋给变量a。范围为request
<c:url value="/AServlet"/>	输出：/day08_01/AServlet
<c:url value="/AServlet">
<c:param name="username" value="abc"/>
<c:param name="password" value="123"/>
</c:url>	输出：/day08_01/AServlet?username=abc&password=123

4.4　if 
　　if标签的test属性必须是一个boolean类型的值，如果test的值为true，那么执行if标签的内容，否则不执行。
<c:set var="a" value="hello"/>
<c:if test="${not empty a }">
	<c:out value="${a }"/>
</c:if>



4.5　choose
choose标签对应Java中的if/else if/else结构。when标签的test为true时，会执行这个when的内容。当所有when标签的test都为false时，才会执行otherwise标签的内容。
<c:set var="score" value="${param.score }"/>
<c:choose>
	<c:when test="${score > 100 || score < 0}">错误的分数：${score }</c:when>
	<c:when test="${score >= 90 }">A级</c:when>
	<c:when test="${score >= 80 }">B级</c:when>
	<c:when test="${score >= 70 }">C级</c:when>
	<c:when test="${score >= 60 }">D级</c:when>
	<c:otherwise>E级</c:otherwise>
</c:choose>

4.6　forEach

forEach当前就是循环标签了，forEach标签有多种两种使用方式：
使用循环变量，指定开始和结束值，类似for(int i = 1; i <= 10; i++) {}；
循环遍历集合，类似for(Object o : 集合)；

循环变量方式：
<c:set var="sum" value="0" />
<c:forEach var="i" begin="1" end="10"> for(int i =1;i<10;i++) {
	<c:set var="sum" value="${sum + i}" /> // sum = sum + i // sum += i;
</c:forEach> }
<c:out value="sum = ${sum }"/>
<c:set var="sum" value="0" />
<c:forEach var="i" begin="1" end="10" step="2">
	<c:set var="sum" value="${sum + i}" />
</c:forEach>
<c:out value="sum = ${sum }"/>


遍历集合或数组方式：
<%
String[] names = {"zhangSan", "liSi", "wangWu", "zhaoLiu"};
pageContext.setAttribute("ns", names);
%>
<c:forEach var="item" items="${ns }"> for(String item : names)
	<c:out value="name: ${item }"/><br/>
</c:forEach>

遍历List
<%
	List<String> names = new ArrayList<String>();
	names.add("zhangSan");
	names.add("liSi");
	names.add("wangWu");
	names.add("zhaoLiu");
	pageContext.setAttribute("ns", names);
%>
<c:forEach var="item" items="${ns }">
	<c:out value="name: ${item }"/><br/>
</c:forEach>

遍历Map
<%
	Map<String,String> stu = new LinkedHashMap<String,String>();
	stu.put("number", "N_1001");
	stu.put("name", "zhangSan");
	stu.put("age", "23");
	stu.put("sex", "male");
	pageContext.setAttribute("stu", stu);
%>
<c:forEach var="item" items="${stu }">
	<c:out value="${item.key }: ${item.value }"/><br/>
</c:forEach>



##### 遍历从后台返回的响应对象resp的值：

```jsp
ArrayList<Student> students = new ArrayList<Student>();	<!--创建一个学生集合，假设有学生-->
req.setAttribute("list",students)	<!--将集合添加到请求对象中，list是key-->
<!--每遍历一次就将key对应的value(student集合)的一条保存到var临时变量里，可以理解为for循环的i-->
<c:forEach items="${req的key}" var="临时变量"> 
	${临时变量.属性名}
</c:forEach>
<c:forEach items="${list}" var="student"> 
    option
	${student.id}
    ${student.name}	...
</c:forEach>
```







---



### ServletContextListener：监听器

#### 解决只有在调用JDBC内的方法才创建数据库连接池的性能问题

> 目前Java包下有两层，controller控制层(获取前端页面的各项参数)，dao数据操作层(JDBC)，
>
> 监听器属于平级的listener文件夹

##### 写监听器的类要实现一个接口：ServletContextListener，该接口有两个抽象方法，在Tomcat启动和关闭调用

```java
public class ComboPooledDataSourcelint implements ServletContextListener {
    // 服务器启动自动调用
    @Override
    public void contextInitialized(ServletContextEvent servletContextEvent) {}

    // 服务器关闭自动调用
    @Override
    public void contextDestroyed(ServletContextEvent servletContextEvent) {}
}
```

##### 最后通过注解声明给Web服务器，这是一个监听器：

```java
@WebListener
public class ComboPooledDataSourcelint implements ServletContextListener {
    @Override
    public void contextInitialized(ServletContextEvent servletContextEvent) {}
    @Override
    public void contextDestroyed(ServletContextEvent servletContextEvent) {}
}
```

##### 就可以在服务器启动时创建连接池：

```java
public void contextInitialized(ServletContextEvent servletContextEvent) {
        // 创建连接池对象
        ComboPooledDataSource dataSource = new ComboPooledDataSource();
        // 将创建的连接池对象给JDBC工具类，静态属性通过类名调用
        JDBCUtil.dataSource = dataSource;
        // 启动服务器这句话必须打印
        System.out.println("创建连接池对象成功.......");
}
```

##### JDBC就不再用静态代码块：

```java
public final class JDBCUtil {
    // 创建数据库连接池静态对象变量
    public static ComboPooledDataSource dataSource;
    
    // 原静态代码块，首次调用该类方法，或者访问类成员的时候，会且只执行1次！！
    static {
        dataSource = new ComboPooledDataSource();
        System.out.println("创建连接池对象成功.......");
    }
    
	// 返回一个数据库连接
    public static Connection getConnection() throws SQLException {
        Connection conn = dataSource.getConnection();
        return conn;
    }
```



---



## MVC框架思想：

> M：Model，实体类  V：View，视图，前端页面  C：Controller，控制器

##### 客户端 -> 控制器 -> 视图

不直接访问视图，先通过Controller

用户客户端和控制器进行交互，控制器负责判断调用哪些视图页面、实体类数据，向客户端展示；

实体类将数据给到视图。 

使用控制器，可以让页面和数据更加安全。



---



## WebFilter：过滤器

> 在WebServlet的service方法之前执行，可以添加多个，多个过滤器称为过滤器链；

#### 1.要实现一个接口：Filter(javax.servlet)

##### 该接口有三个抽象方法(生命周期)：init()、doFilter()、destory()

1. init方法:（生）容器中过滤器生成的时候调用;
2. destroy方法:（死）容器中过滤器销毁的时候调用
3. doFilter方法：过滤器的主要代码

#### 2.要用注解声明该类是一个过滤器：@WebFilter

@WebFilter(value = "要过滤的资源的路径")

##### 过滤器实例：

```java
@WebFilter(value = "/home.jsp")	// 拦截所有访问该页面的请求(必须加斜杠)
public class TestFilter implements Filter {
    
    @Override
    public void init(FilterConfig config) throws ServletException {
		System.out.println("过滤器init方法被调用了，过滤器已创建！");
    }
    
    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws Exception {
        System.out.println("请求被拦截了！");
        // HttpServletRequest继承ServletRequest，想要实现controller的操作就要向下转型
        // 把servletRequest转换为子类对象req,servletResponse转换为resp
        HttpServletRequest req = (HttpServletRequest) servletRequest;
        HttpServletResponse resp = (HttpServlet)servletResponse;
        // 获取Session里key为uname的value值
        Object uname = req.getSession().getAttribute("uname");
    	// TODO 进行逻辑判断，比如用户是否登录。uname不为空就是登录
        if(uname != null) {
            // 已登录，放行，让程序继续执行下一个Filter或者Servlet,不放行就无法访问资源,必须写
            // filterChain.doFilter()是指这个过滤器使用完后还可以调用其他过滤器
        	filterChain.doFilter(servletRequest,servletResponse);
        } else {
            // 未登录，重定向到登录页面
            resp.sendRedirect("login.jsp");
        }
    }
    
    @Override
    public void destroy() {
    	System.out.println("过滤器destroy方法被调用了，过滤器已销毁！");
    }
}
```



---



## AOP，面向切面编程-代理设计模式：Proxy

#### 工厂方法代理：

获取该类注解的参数

##### 定义一个注解“代理”：

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
public @interface Proxies {
    Class c();	// 注解有一个属性c，Class类型
}
```

##### 获取注解参数(属性值）：

```java
该类的Class.getAnnotation(注解名.class); 返回注解类型的对象(Annotation)
// 假设该注解为Proxies
Proxies annotation = (Proxies) target.getAnnotation(Proxies.class);	// 获取注解对象并强转

注解对象.注解属性(); 返回该属性的数据类型
Class c = annotation.c();	// 获取该注解的属性c的值，c数据类型是Class，用Class类型接收
```

 

#### 动态代理：一个代理解决所有需求(卖车、卖手机、卖装备)

##### JDK动态代理：JDKDynamic

> 代理类和被代理类要共同实现一个接口

###### Proxy.newInstance，返回一个代理对象：

> 创建一个被代理对象：宝马汽车制造商

```
BaoMaCompapny baoMaCompapny = new BaoMaCompapny();
```

> 创建一个代理对象(Proxy是Java.long.refect反射包下面的)

```
Object obj = Proxy.newProxyInstance(?,?,?);	// 返回Object
```

>  三个参数，1.被代理对象的类的类加载器 2.被代理对象实现的接口 3.InvocationHandler接口

1. baoMaCompapny.getClass().getClassLoader()获取被代理对象的Class再通过Class获取类加载器
2. baoMaCompapny.getClass().getInterfaces() 同理，获取Class后获取该类实现的接口
3. 接口不能创建出实例，只能通过实现接口的方法来创建对象：匿名实现类

```java
public static void main(String[] args) {
    // 创建一个被代理对象：宝马汽车制造商
    BaoMaCompapny baoMaCompapny = new BaoMaCompapny();
   	/* 
   		创建一个代理对象三个参数：
    	1.被代理对象的类的类加载器 
   		2.被代理对象实现的接口 
    	3.InvocationHandler接口(拦截器)
    */
    Object obj = Proxy.newProxyInstance
	(baoMaCompapny.getClass().getClassLoader(), baoMaCompapny.getClass().getInterfaces(), 		new InvocationHandler() {
        @Override                       // method其实就是被代理对象的create方法
      	public Object invoke(Object proxy, Method method, Object[] args) throws Throwable 		  {
        	System.out.println("before");
            // 根据方法对象，调用方法，invoke里传一个被代理类的对象，会自动调用它的方法
            // 调用被代理对象的方法，传被代理对象，如果该方法有参数，需要传一个args(invoke方法的参数)
            method.invoke(baoMaCompapny);
            System.out.println("after");
            return null;
        }
    });	// 实现类类体和方法参数右括号
    // 将Object类型的代理对象转换为被代理对象继承的接口类型
    CarFactory proxy = (CarFactory) obj;
    // 代理对象调用被代理的方法，但是实际上是调用的invoke
    proxy.create();
    
    // 查看JDK生产的代理对象所属的Class,可以添加一句代码，生成一个com文件夹
    System.getProperties().put("sun.misc.ProxyGenerator.saveGeneratedFiles", "true");
}
```



###### AA类需要一个代理：

```java
class AA {
    public void show() {
        for (int i = 0; i < 10000; i++) {
            System.out.println(i);
        }
    }
}
```





##### CGLIB动态代理：

> 代理类继承被代理类

###### CGLIB：

```java
/*Enhancer：CGLIB里的增强类，创建一个增强对象*/
Enhancer 对象名 = new Enhancer(); 
Enhancer enhancer = new Enhancer();

/*给代理添加一个父类(被代理的类)*/
enhancer.setSuperclass(父类.class);	
enhancer.setSuperclass(AA.class)	// 代理AA，将AA视为该代理的父类

/*拦截被代理方法，传一个方法拦截器*/
enhancer.setCallback(方法拦截器);
enhancer.setCallback(new MethodInterceptor() {
	@Override				// 跟JDK动态代理一样，method其实就是被代理对象的create方法
    public Object intercept(Object o, Method method, Object[] objects, MethodProxy methodProxy) throws Throwable {
        System.out.println("---");
        methodProxy.invokeSuper(new AA(),null);
     	return null;
     }
});

/*创建代理对象*/
增强类对象.create();	// create()方法返回Object
AA a = (AA)enhancer.create() //	Object类型的对象强转成AA类型的a

/*代理对象调用被代理对象的方法*/
a.show();	// 因为a已经代理AA类了，所以实际调用的是：MethodInterceptor()方法

/*执行被代理类的方法*/
// 将被代理的方法写在MethodInterceptor()方法中
method.invoke(被代理类的对象,方法参数);
```





##### Aspect动态代理：

> 不需要继承

##### 需要下载插件：AspectJ

> 添加类注解：@Aspect

```java
@Aspect	// 注解在类头上，这个被注解的类就是代理类了
public class AspjDemo {}
```

> 添加方法注解：@Before、@After、@AfterReturning、@Around

注解有参数：execution()，括号里第一个是返回值，后面写需要被代理的类的某个方法(绝对路径)

例如：

```java
@Before("execution(* com.woniu.proxy.AA.show(..))")
```

*号代表寻找该路径下任何返回值的方法(void、int、boolean...)

方法参数的".."代表任何参数，有参无参都匹配

还可以这样：

```java
@Before("execution(* com.woniu.proxy.*.*(..))")
```

代表扫描proxy包下的所有类的所有方法无论什么参数什么返回值都拦截(代理)



###### 不同的注解区别在于执行时间不同：

```java
@Aspect
public class AspjDemo {

    // 前置通知，在目标方法执行之前执行
    @Before("execution(* com.woniu.proxy.AA.show(..))")
    public void before() {
        System.out.println("show方法之前执行");
    }

    // 后置通知，在目标方法执行完之后执行
    @After("execution(* com.woniu.proxy.AA.*(..))")
    public void after() {
        System.out.println("show方法执行完之后执行");
    }

    // 返回通知，目标方法结束立即执行(比after)
    @AfterReturning("execution(* com.woniu.proxy.AA.show(..))")
    public void afterReturning() {
        System.out.println("show方法返回立即执行");
    }
    
    public static void main(String[] args) {
        AA a = new AA();	// chu
        a.show();
    }
}
```

###### 还有一个特殊通知，需要参数：

```java
// 环绕通知，参数类型ProceedingJoinPoint
@Around("execution(* com.woniu.proxy.AA.show(..))")
public void huanRao(ProceedingJoinPoint point) throws Throwable {
	System.out.println("环绕前置通知");	// 在前置通知之前执行
	point.proceed();	// 放行，放行后才能执行后面的语句
	System.out.println("环绕后置通知");	// 放行后，在后置通知、返回通知之前执行
}
```







## Mybatis：替代JDBCUtil

### 配置Mybatis：

##### 1、配置Maven

##### 2、配置数据源(给连接池)：URL、用户名、密码, 写在Mybatis引擎文件 -> resource(mybatis-config.xml)

> 这个原生连接池没有c3p0好用，但是可以集成到Mybatis
>
> URL涉及到MySQL驱动，需要引入驱动(MySQL的Maven)

##### mybatis-config.xml：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">	<!--规定了这个文件能写哪些标签-->

<configuration> <!--在Java中他是一个对象-->
    <!--引入单独配置文件，使用占位符配置数据源-->
    <properties resource="mysql.properties"></properties>
	
    <!--配置resultType的别名，两种方式-->
    <!--
        <typeAliases>
			配置单一类的别名(写alias的值)
            <typeAlias type="com.woniu.entity.Student" alias="Student"/>
			配置一个包中的所有类(直接写类名)
            <package name="com.woniu.entity"/>
        </typeAliases>
    -->

    <!--log4j日志-->
    <!-- 
        <settings>
             <setting name="logImpl" value="LOG4J"/>
         </settings>
     -->
    
    <!-- 配置mybatis运行环境 -->
    <environments default="development">
        <environment id="development">
            <!-- 使用JDBC的事务管理 -->
            <transactionManager type="JDBC"/>
            <!--数据源-->
            <dataSource type="POOLED">
                <!-- MySQL数据库驱动配置-->
                <!-- 数据源四个value可以用properties单独配置 -->
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <!-- 连接数据库的URL -->
                <property name="url" 
                          value="jdbc:mysql://localhost:3306/数据库名?useUnicode=true&amp;characterEncoding=utf8&amp;serverTimezone=GMT%2B8"/>
                <property name="username" value="数据库账户"/>
                <property name="password" value="数据库密码"/>
            </dataSource>
        </environment>
    </environments>
    
    <!-- 将mapper文件加入到配置文件中 -->
    <mappers>
        <mapper resource="ParkingMapper.xml"/>
    </mappers>
</configuration>
```



##### 单独配置数据源：mysql.properties

> 不再将数据源的参数写在mybatis引擎文件,引入配置文件,引擎文件中写占位符,占位符的值在配置文件中获取

```properties
自定义属性名=属性值
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/数据库名?useUnicode=true&amp;characterEncoding=utf8&amp;serverTimezone=GMT%2B8
jdbc.username=数据库账户
jdbc.password=数据库密码
```



##### 引擎文件中使用${占位符}获取配置文件mysql.properties中的属性值：

```xml
<!-- 配置mybatis运行环境 -->
<environments default="development">
    <environment id="development">
        <!-- 使用JDBC的事务管理 -->
        <transactionManager type="JDBC"/>
        <!--数据源-->
        <dataSource type="POOLED">
            <!-- MySQL数据库驱动配置-->
            <!-- 四个value可以用properties单独配置 -->
            <property name="driver" value="${jdbc.driver}"/>
            <!-- 连接数据库的URL -->
            <property name="url" value="${jdbc.url}"/>
            <property name="username" value="${jdbc.username}"/>
            <property name="password" value="${jdbc.password}"/>
        </dataSource>
    </environment>
</environments>
```







### Mybatis三大核心对象

#### 1. SqlSessionFactoryBuilder

##### 配置文件mybatis-config.xml的configuration标签在Java中是一个对象：SqlSessionFactory

> 要把该标签转换为工厂对象，需要先将配置文件通过解析器进行解析



##### 创建一个解析器对象，用于解析mybatis-config.xml这个文件，解析器类型是SqlSessionFactoryBuilder

```java
// 创建解析器对象builder
SqlSessionFactoryBuilder builder = new SqlSessionFactoryBuilder();	
```





#### 2. SqlSessionFactory(工厂)

> 解析器对象解析要求传一个Reader字符流对象

##### 定义mybatis_config配置文件地址：

```java
String resources = "mybatis_config.xml";
```



##### 获取Reader字符IO流：

```java
Reader reader = Resources.getResourceAsReader(mabatis配置文件);
Reader reader = Resources.getResourceAsReader(resoutces);
```



##### 将流交给解析器进行解析：

```java
// 解析器返回一个造代理对象的工厂
SqlSessionFactory sqlSessionFactory = 解析器对象.build(Reader reader);	
SqlSessionFactory sqlSessionFactory = builder.build(reader); 
```





#### 3. SqlSession(执行SQL命令)

> 该方法有一个参数为boolean的重载方法，true代表自动提交事务，false代表不自动提交。默认false

```java
SqlSession sqlSession = sqlSessionFactory.openSession(/*默认false，不提交*/);	
```





#### 4. getMapper()：操作mapper生成代理对象

```java
// 这里传递的是接口.class，Mybatis竟然可以创建对象
sqlSession.getMapper(被代理接口.class);	
// 返回对应接口的代理对象 跟代理的getProxy(被代理类的class)一致 用的动态代理：CGLIB
//生成代理对象dao
IOrgCorporationDao dao = sqlSession.getMapper(IOrgCorporationDao.class); 
```

##### 代理对象dao已经代理了IOrgCorpoprationDao接口，可以调用该接口的抽象方法：

```java
// 被代理接口，有方法save()
public interface IOrgCorporationDao {	
    // 向数据库添加一条数据
    public void save();	
}
// IOrgCorporationDaoImpl：dao.save();	
// (一般是Controller层实现类)的方法调用抽象方法，失败：代理类没有方法，dao没有自己的方法体来代理执行
```







### mapper.xml：代理对象调用被代理接口执行的方法体

> 在Mybatis里，被代理接口的方法体的形式是一个xml文件：代理对象dao调用被代理接口的抽象方法，执行的是代理类自己的方法，那么这个代理类自己的方法的方法体，就是mapper.xml。

```xml
<!--mapper.xml模板-->
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--namespace属性指定被代理对象的所属类(接口)的全路径-->
<mapper namespace="以蓝色Java文件夹为根目录被代理接口路径">
	<!--SQL语句，或者说实现namespace接口的实现类(代理类)的方法体-->
</mapper>
```





#### SQL语句(代理对象调用被代理接口方法后执行的方法体)有两种：xml实现、注解实现

#### xml实现：增删改

##### 被代理接口：

```java
public interface IOrgCorporationDao {
    // 调用的方法一，无参
    public void save();
    // 调用的方法二，有参
    public void save2(	
        // 该注解的参数值对应占位符中的参数名，方便维护
        // 真正的属性名可以随意更改(int id => int c_id)
        @Param("id")
        	int id,	
        @Param("cname")
        	String cname,
        @Param("personName")
        	String pname,
        @Param("phone")
        	String phone,
        @Param("state")
        	int state
    );
}
```



##### 直接写SQL语句(SQL写死)：

```xml
<mapper namespace="以蓝色Java文件夹为根目录被代理接口路径">
    <!--四个标签insert、delete、update、select-->
    <insert id="被代理接口内某个方法的方法名">	
        <!--普通SQL语句-->
    </insert>
</mapper>
```

###### 实例：

```xml
<!--mapper.xml模板-->
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="com.woniu.IOrgCorporationDao">
    <!--id:被代理接口的方法名 dao.save()调用该"方法体",执行SQL-->
	<insert id="save">	
        INSERT INTO org_corporation(cname,pname,phone,state)
        VALUES ('阿里巴巴', '董本洪', '123123', '1')
    </insert>
</mapper>
```



##### Param占位符形式写SQL语句(动态传参)：

```xml
<mapper namespace="以蓝色Java文件夹为根目录被代理接口路径">
	<insert id="被代理接口内某个方法的方法名">
        <!--Param占位符SQL动态传参(#{参数名})-->
    </insert>
</mapper>
```

###### 实例：

```xml
<mapper namespace="com.woniu.IOrgCorporationDao">
    <!--id:被代理接口的方法名 dao.save2()调用该"方法体",执行SQL-->
	<insert id="save2">	
    	INSERT INTO org_corporation(cname,pname,phone,state)
    	VALUES(#{cname},#{personName},#{phone},#{state})
    </insert>
</mapper>
<!--调用：dao.save2("阿里妈妈","刘备","123123",1)-->
```



##### 如果方法的参数有多个，必须使用@Param注解，如果多个参数中包含对象，则映射应写为注解别名.属性名

###### 接口：

```java
public Student selectBySerch(@Param("student") Student student,@Param("name")String name)
```

###### xml：

```xml
<select id="selectBySerch" resuleType="">
    SELECT *
    FROM owner
    WHERE username = #{student.name}
    AND teachername= #{name}
</select>
```

###### xml中动态sql也一样要打点调用：

```xml
<if test="student.tel != null">
	AND tel LIKE concat('%',#{student.tel},'%')
</if>
```



##### 注解实现：纯注解方法体：不编写mapper.xml

##### 只需要在被代理接口上添加注解：@Mapper，SQL通过注解写在方法头上，不再写在mapper.xml配置文件了

###### 接口：

```java
@Mapper	// 固定格式@Mapper
public interface 接口名{
	/*四个注解，跟mapper一样：@Insert,@delete,@Update,@Select*/
	public void 方法名(@Param("参数名") 数据类型 属性名..);
}
```

###### 实例：

```java
@Mapper	
public interface IOrgManagerDao {
    @Insert("INSERT INTO org_manager VALUES(#{id},#{email},#{pwd},#{time})")
    public void add(
            @Param("id") int id,
            @Param("email") String email,
            @Param("pwd") String pwd,
            @Param("time") String time
    );
}
/*调用：dao.add("阿里妈妈","刘备","123123",1)*/
```

> 虽然不用写mapper.xml，但是要在核心配置文件Mybatis_config.xml里引入接口上方的注解@Mapper



#### 查询：

> 首先要有实体类，数据库每张表对应一个实体类，表的每列对应该实体类的属性，那么每行就是一个对象，查询返回对象，所以接口的抽象方法用List<实体类>来接收。

##### 接口：

```java
public interface IOrgCorporationDao {
    // 查询要有返回值，返回对象，List接收
    public List<OrgCorporationBean> findAll();	
}
```



##### 普通查询：id、result

###### 实体类：

```java
public class Student {
	private int id;
	private String name;
}
```

###### mapper.xml：

```xml
<!--namespace属性指定被代理对象的所属类的全路径-->
<mapper namespace="com.woniu.IOrgCorporationDao">
    <!--
		select:查询语句，还有insert、update、delete标签
		id:方法名
		resultMap对应映射方案resultMap标签的id，就是通过id选择映射方案(方案可以复用)
	-->
    <select id="方法名" resultMap="映射方案">
        <!--查询SQL语句-->
    </select>
    
    <!--配置映射方案是解决数据库字段名(列名)和实体类的属性对应不上的问题，所以如果对应的上可以省略-->
    <resultMap id="自定义映射方案名" type="实体类绝对路径"><!--type如果不写，默认就是List<Map>-->
        <!--主键用id标签,其余跟result一样-->
        <id column="数据库字段名(列名)" property="实体类属性名"></id>
        <result column="数据库字段名(列名)" property="实体类属性名"></result>
    </resultMap>
</mapper>
```

###### 实例：

```xml
<select id="findAll" resultMap="r1">
    SELECT * FROM org_corporation
</select>

<resultMap id="r1" type="com.woniu.entity.OrgCorporationBean">
    <id column="id" property="id"></id>
    <result column="cname" property="cname"></result>
    <result column="pname" property="pname"></result>
    <result column="phone" property="phone"></result>
    <result column="state" property="state"></result>
    <result column="cphoto" property="cphoto"></result>
</resultMap>
```

> 数据库字段名和实体类的属性对应不上的问题，也可以在查询的时候不用*，给每个字段取别名去对应实体类
>
> Mybatis底层默认有一级缓存，查询两次，第二次的list就是第一次查询的list。
>
> 一级缓存在进行增删改语句后失效。



##### 一对一(A类中的某一属性为B类对象)：association

###### 实体类：

```java
public class Student {
	private int id;
	private String name;
    // 班级
	private Clazz clazz;
}
```

###### 实例：查询学生同时查询班级信息(一个学生对应一个班级，也属于多对一，多个学生对应一个班级)

```xml
<select id="all" resultMap="student_map">
    SELECT s.id, s.name, s.gender, s.cid, c.name cname
    FROM student s,
    clazz c
    WHERE s.cid = c.id
    AND s.status = 0
</select>

<resultMap id="student_map" type="Student">
    <!--指定字段与属性的对应关系
    	column:字段名   property：属性      将哪个字段的值赋值给类中的哪个属性
    -->
    <id column="id" property="id"></id>
    <result column="name" property="name"></result>
    <result column="gender" property="gender"></result>
    <result column="cid" property="cid"></result>

    <!--
    	property：给哪个属性赋值
    	javaType：属性的类型
    -->
    <association property="clazz" javaType="Clazz">
        <!--将结果集中cid字段的值赋值给Clazz类中id-->
        <id column="cid" property="id"></id>
        <result column="cname" property="name"></result>
    </association>
</resultMap>
```



##### 一对多(关联另一个类型对象的集合)：collection

###### 实体类：

```java
public class House {
    // 主键id
    private Integer id;
    // 楼层
    private Integer storey;
    // 住户房间号
    private String numbers;
    // 是否入住
    private Integer status;
    // 入住时间
    private Date into_date;
    // 建筑物编号
    private Integer building_id;
    // 备注
    private String remarks;
    // 面积
    private Double area;
    // 一对多 一个房屋对应多个业主
    private List<Owner> owner;
}
```

###### mapper.xml：

```xml
<mapper namespace="com.woniu.IOrgCorporationDao">
    <!--
		id:方法名
		resultMap对应映射方案resultMap标签的id，就是通过id选择映射方案(方案可以复用)
	-->
    <select id="方法名" resultMap="映射方案">
        <!--查询SQL语句-->
    </select>
    
    <resultMap id="自定义映射方案名" type="实体类绝对路径"><!--type如果不写，默认就是List<Map>-->
        <!--主键用id标签,其余跟result一样-->
        <id column="数据库字段名(列名)" property="实体类属性名"></id>
        <result column="数据库字段名(列名)" property="实体类属性名"></result>
        <collection property="集合类型的属性名" oftype="该属性返回的类型">
        	<id column="数据库字段名(列名)" property="实体类属性名"></id>
        	<result column="数据库字段名(列名)" property="实体类属性名"></result>
        </collection>
    </resultMap>
</mapper>
```

###### 实例：

```xml
<mapper namespace="com.woniu.mapper.HouseMapper">
	<!-- 一个房屋对应多个业主 -->
    <select id="selectHouseByid" resultMap="houseMapper">
        SELECT h.id,
               h.storey,
               h.numbers,
               h.status,
               h.into_date,
               h.building_id,
               h.remarks,
               h.area,
               o.id      oid,
               o.username,
               o.tel,
               o.sex,
               o.identity,
               o.house_id,
               o.remarks omark,
               o.password
        FROM house h,
             owner o
        WHERE h.id = o.house_id
          AND h.id = #{id}
    </select>

    <resultMap id="houseMapper" type="com.woniu.entity.House">
        <id column="id" property="id"/>
        <result column="storey" property="storey"/>
        <result column="numbers" property="numbers"/>
        <result column="status" property="status"/>
        <result column="into_date" property="into_date"/>
        <result column="building_id" property="building_id"/>
        <result column="remarks" property="remarks"/>
        <result column="area" property="area"/>
        <collection property="owner" ofType="com.woniu.entity.Owner">
            <id column="oid" property="id"></id>
            <result column="username" property="username"></result>
            <result column="tel" property="tel"></result>
            <result column="sex" property="sex"></result>
            <result column="identity" property="identity"></result>
            <result column="house_id" property="house_id"></result>
            <result column="omark" property="remarks"></result>
            <result column="password" property="password"></result>
        </collection>
    </resultMap>
</mapper>
```



##### 多对一：



##### 多对多：







> 总结：一对一，一个人只能有一个身份证号， 一个身份证号只能属于一个人，人实体类引入身份证对象。
>
> ​			一对多，一个班级拥有多个学生，班级实体类引入学生集合。
>
> ​			多对一，多个学生同属一个班级，



#### 动态SQL：

##### select:按条件拼接对应的SQL语句

##### where、if

```xml
<where>
    <if test="布尔表达式">
    	<!--为真执行-->...
    </if>
</where>
```

###### 实例：

```xml
<select id="selectUnameByPwd" resultMap="user_map">
    SELECT *
    FROM sys_user
    <where>
        <!--多条件用and和or-->
        <!--判断不为空且不为空字符串-->
        <if test="userName != null and userName != ''">
            and userName = "刘备"
        </if>
	</where>
</select>
```



##### foreach

```xml
<select id="方法名" resultMap="映射结果集">
    SQL语句
    <foreach collection="传入的数据类型(数组array/集合list)" separator="分隔符" open="起始字符" 		close="结束字符" item="循环变量(for循环中的i)">
    	#{循环变量}
    </foreach>
</select>
```

> 产生的SQL语句就是：起始字符 循环变量 分隔符 循环变量 结束字符

###### 实例：

```xml
<select id="***" resultMap="***">
    SELECT *
	FROM student
	WHERE id IN 
    <foreach collection="array" separator="，" open="(" close=")" item="id">
    	#{id}
    </foreach>
</select>
```



##### bind：内部数据处理

###### 分页查询：数据当前页、每页展示条数等不能直接在LIMIT中处理：

```xml
LIMIT (#{indexSize} - 1) * pageSize,#{pageSize}
```

###### 使用bind标签：

```xml
<select id="selectBySerch" resultType="com.woniu.entity.Owner">
    <bind name="自定义名" value="要进行的数据处理，外部参数不需要#{}，可以直接写参数获取"/>
    SQL语句
    LIMIT #{indexSize},#{pageSize}
</select>
```

###### 实例：

```xml
<select id="selectBySerch" resultType="com.woniu.entity.Owner">
    <bind name="indexSize" value="(index - 1) * pageSize"/>
    SELECT *
    FROM owner
    <where>
        <if test="owner.username != null">
            AND username LIKE concat('%',#{owner.username},'%')
        </if>
        <if test="owner.tel != null">
            AND tel LIKE concat('%',#{owner.tel},'%')
        </if>
    </where>
    LIMIT #{indexSize},#{pageSize}
</select>
```



##### update:如果对应参数有值

```xml
<set>
    <if test="布尔表达式">
		<!--为真执行-->...
    </if>	
</set>
```

###### 实例：

```xml
<update id="updateUser" >
    update t_user
    <set>
        <if test="userName != null">
			userName = #{userName},
        </if>	
    </set>
</update>
```



##### sql片段复用：

```xml
<select id="" resultType="">
	SQL语句 + <include refid="sql片段的id" />
</select>
<sql id="自定义id">SQL语句</sql>
```

###### 实例：

```xml
<select id="***" resultType="***">
	SELECT * <include refid="select" />
</select>
<sql id="select">FROM student</sql>
```







### 在引擎文件(Myabtis_config)中引入mapper注解/mapper.xml

##### 所有的实现类：mapper.xml,都要加到Mybatis引擎文件中：Mybatis-congfig.xml，一起交给解析器解析

```xml
<environments>
	<!--Mybatis运行环境配置-->
</environments>
<mappers>
    <!--接口文件与映射文件(Mapper.xml)不在同一路径下,仅能用resource加载映射文件-->
    <mapper resource="以resources为根目录mapper.xml的路径"/>
    <!--接口文件与映射文件在同一路径下,且接口名与映射文件名相同,并且映射文件命名为接口全类名的情况-->
    <!-- @Mapper注解的SQL引入：class-->
    <mapper class="被代理接口全路径"/>
    <!-- 指定扫描mapper接口对应的包 -->
    <package name="xxxMapper接口文件所在目录(全路径)"/>	
</mappers>
```

###### 实例：

```xml
<mappers>
    <mapper resource="mapper/org-mapper.xml"/>
    <mapper class="com.woniu.IOrgManagerDao"/>
    <package name="com.woniu.mapper"/>
</mappers>
```



##### 解析器解析完mappers标签的内容后，就会转换成代理对象，再给dao，dao变成正式的非空的代理对象





### 完整流程：

#### 一、带接口实现类的方式：

##### controller：

###### 创建被代理接口的实现类的对象，调用类里的方法

```java
@RequestMapping("/login")
    public ModelAndView login(String email , String pwd) {
        ModelAndView mv = new ModelAndView();	// 视图模型
        // 处理逻辑验证，访问数据库，委托给dao层帮我们完成，也就我的下一层
        IAccountDao dao = new IAccountDaoImpl();	// 创建DAO层实现类的对象
        boolean success = dao.实现类方法(email,pwd);	// 传参数给实现类
}
```



##### Dao：

###### 被代理接口的实现类：

```java
public class IOrgCorporationDaoImpl implements IOrgCorporationDao{
	public boolean login(String email,String pwd){  
        // 创建解析器，用于解析mybatis_config.xml
        SqlSessionFactoryBuilder builder = new SqlSessionFactoryBuilder();
        
		// 解析器解析配置文件，生成sqlSession工厂
        String resources = "mybatis_config.xml";
        Reader reader = Resources.getResourceAsReader(resources);
        SqlSessionFactory factory = builder.build(reader);		
        // 以上三句可以简写成一句话
        sqlsession工厂 = builder.build(Resources.getResourceAsReader("mybatis.xml"));	

        // openSession有参数，true/false，表示是否自动提交事务
        SqlSession sqlSession = factory.openSession();
        
        // 这个dao是接口IOrgCorporationDao的代理对象，调用的login是接口的方法体->mapper.xml
        IOrgCorporationDao dao = sqlSession.getMapper(IOrgCorporationDao.class);
        
		// 调用被代理接口login()方法，执行代理类mapper.xml中mapper标签的SQL语句
        boolean success = dao.login(email,pwd);	
        sqlSession.close();	// 关闭sqlSession，工厂会将该Session回收
        return success;	// 返回mapper的查询结果
    }
}
```

###### 被代理接口，有方法login()

```java
public interface IOrgCorporationDao {
    // 登录方法			
    public boolean login(@Param("email") String email, @Param("pwd") String password);	
}
/*
	Param：自定义别名，xxxmapper.xml的SQL语句参数使用,修改实体类属性xml中的SQL语句不用更改,扩展性更好
	使用@Param注解好处：方法参数名可以不与xxMapper.xml引用的#{参数名}一致
	但是注意@Param("")里面的值(自定义别名)要与xxMapper.xml中#{}里的值一致
*/
```



##### resources：

###### mapper.xml：

```xml
<mapper>	<!--id：定义该方法体属于哪个方法 resultType：定义方法的返回值-->
	<select id="login" resultType="boolean">	
        select count(1) > 0 from account where email = #{email} and pwd = #{pwd}
    </select>
</mapper>
```

##### mapper.xml返回布尔，实现类接收后return给controller，controller根据结果来返回相应的页面，流程结束



> 大多数XML标签可以简写：

```xml
<result ... >...</result> --> <result ... />
```





#### 二、接口直接对应xxxmapper.xml的方式：

##### Dao层接口直接与同名的"xxxMapper.xml"对应，没有实现类

> 接口与XxxMapper.xml文件在一个包下(非Web项目)

###### 无Controller、Service层，Dao层(mapper)直接由测试类控制示例：

```java
public class OwnerTest {

    //    private OwnerDaoImpl ownerMapper = new OwnerDaoImpl();

    private SqlSession sqlSession;
    private OwnerMapper ownerMapper;

    /**
     * Junit测试方法之前实例化代理对象
     */
    @Before
    public void before() {
        // 调用自封装的MybatisUtil获取Session对象
        sqlSession = MybatisUtil.getSession();
        // 获取接口的代理对象
        ownerMapper = sqlSession.getMapper(OwnerMapper.class);
    }

    /**
     * Junit测试方法之后关闭session
     */
    @After
    public void after() {
        if (sqlSession != null) {
            sqlSession.close();
        }
    }

    /**
     * 根据业主对象模糊查询(分页)
     */
    @Test
    public void selectBySerch() {
        // 页码
        Integer index = 0;
        // 每页查询条数
        Integer pageSize = 2;
        Owner owner = new Owner();
        owner.setUsername("x");
        owner.setTel("7");
        List<Owner> owners = ownerMapper.selectBySerch(owner, index, pageSize);

        System.out.println("=========打印查询对象属性=========");
        System.out.println(owner);

        System.out.println("=========打印查询结果集=========");
        owners.forEach(System.out::println);
    }

    /**
     * 查询所有业主
     */
    @Test
    public void selectALl() {
        List<Owner> owners = ownerMapper.selectALl();
        owners.forEach(System.out::println);
    }
}
```









#### 底层实现详解：

##### 一、读取Mybatis配置文件信息

##### 二、获取SqlSessionFactory

1. 使用XMLMappperBuilder解析Mybatis配置文件，封装成Environment对象，再把Environment对象设置给Configuration对象；
2. 调用ConfigurationElement函数，最终执行addMappedStatement方法，将mapper配置文件中的每一条SQL语句封装成mappedStatement对象，作为value保存在HashMap集合中；
3. 进入addLoaderResource方法，使用HashSet集合存放mybatis的mapper.xml 映射文件路径地址;
4. 进入bindMapperForNamespace()方法，通过namespace使用Java反射机制找到mapper接口，再调用addMapper（）方法，判断是否是接口类型，是否注册过（注册过则抛出异常）其中mapperRegistry通过HashMap保存mapper接口，【key：接口；value：MapperProxyFactory】

##### 三、获取session

1. 进入openSession（）方法，执行newExecutor（）方法创建执行器； 
2. 先创建 SimpleExecutor简单执行器，再判断是否开启了二级缓存，默认是开启的，就会去创建CacheExecutor缓存执行器，
3. 执行interceptorChain.pluginAll()方法，责任链设计模式，底层使用动态代理技术，使开发者可以自定义插件开发，只需要实现Interceptor接口，并指定想要拦截的方法签名即可，最后返回执行器；

##### 四、操作mapper接口 

1. 调用getMapper()方法，最终执行mapperProxyFactory.newInstance(sqlSession)方法创建代理类MapperProxy；
2. 当我们调用mapper,getUser()方法的时候，就会去执行MapperProxy代理类的invoke（）方法；
3. 判断mapper接口是否有实现类，显然我们没有实现类，则调用cacheMapperMethod()方法去缓存中获取要代理的方法method； 
4. 进入cacheMapperMethod()方法先去查找缓存中有没有，没有的话将mapper配置文件中配置的SQL语句和对应的mapper接口方法进行关联并放入map缓存中，后期直接走缓存了，最后执行execute()方法；
5. 执行execute（）方法，最终调用selectOne（）方法； 
6. 进入selectOne()方法，底层还是查询所有的，但是取第一个，查询多个的话会抛出异常； 
7. 进入selectList()方法，调用getMapperStatement()方法获取对应的SQL语句；
8. 执行query（）方法进行查询，判断如果开启了二级缓存并且配置了二级缓存存储介质（Redis,EhCache..）则先走二级缓存中查询数据，第一次查询是没有缓存数据的，则刷新缓存配置，清除缓存。
9. 二级缓存(sessionFactory)中没有查询到数据，就回去执行BaseExecutor去查询 HashMap一级缓存中（sqlSession）是否有缓存数据，一级缓存（PerpetualCache）存放在内存中的，同理也是没有的，最后查询数据库DB 
10. 将从数据库查询出来的数据缓存到一级缓存中，再把一级缓存中的数据同步到二级缓存，添加到二级缓存之前先添加到getTransactionalCache的entritiesToAddOnCommit的map集合中临时缓存起来； 
11. 调用executor.close()方法循环迭代TransactionCache,最后将临时map缓存数据提交到二级缓存中,如果事务回滚，则会将缓存数据清除掉
12. 再次查询的话，就有缓存了，会直接查询到缓存数据返回，不会去查询数据库DB 







## SpringMVC：替代Servlet

> 配置springmvc-config.xml、web.xml文件参考框架文档

##### @Controller：声明该类是一个控制器类

```java
@Controller
public class **Controller {
	// 方法
}
```



##### @RequestMapping(参数列表)：声明该方法的映射地址、接收那种类型的请求等

```java
@Controller
public class **Controller {
	@RequestMapping(参数列表)
    public void login() {
        System.out.println("登录成功！");
    }
}
```



##### 参数列表：

###### path/value：映射地址

###### method：该方法支持的请求类型

```java
// 该方法映射地址为/login，只支持get类型的请求
@RequestMapping(path = "/login", method = RequestMethod.GET)
public void login() {
	System.out.println("登录成功！");	
}
```



##### 实例：

```java
@Controller
public class OrgController {
    // 1.这个路径在根目录下：http://localhost:8080/项目映射地址/login
    // 2.该方法只支持get类型的请求
    @RequestMapping(path = "/login", method = RequestMethod.GET)
    public void login() {
        System.out.println("登录成功！");
    }
}
```





### 获取参数：

##### 1. HttpServletRequest/HttpServletResponse：原生态写法

> 直接在方法加Http参数

```java
@RequestMapping("/login2")
public void login2(HttpServletRequest req) {
    String uname = req.getParameter("uname");
    System.out.println("姓名是：" + uname);
}
```



##### 2. @RequestParam：注解

> 调方法的时候，把用户名和密码直接传进来 后面用一个参数接收

```java
// 这种在参数前添加注解@RequestParam的写法，客户端必须传参数，否则报错，可以不写，就不用必须传参
@RequestMapping("/login3")
public void login3(@RequestParam("uname") String uname, 
                   @RequestParam("upwd") String upwd) {
	System.out.println("姓名是：" + uname + " " + "密码是：" + upwd);
}
```



##### 3. restful：URL风格

###### 格式：/映射地址/{占位符}

使用restful风格的url传递参数，改变了原写法：?"参数名"=值 ，

一般与@RequestMapping(method = RequestMethod.GET)一起使用，搭配@PathVariable注解

```java
// 前端：http://localhost:8080/mvc/login4/值1/值2
@RequestMapping("/login4/{uname}")    
public void login4(@PathVariable("uname") String n) {  // 把注解对应的uname值传给被注解的n
    System.out.println("姓名是：" + n);
}
```



##### @PathVariable注解：映射 restful风格URL的占位符

> 通过 @PathVariable 可以将URL中占位符参数和控制器方法的参数进行映射:URL 中的 {xxx} 占位符可以通过
>
> @PathVariable(“xxx”) 绑定到操作方法的入参中。

###### 若方法参数名称和需要绑定的url中变量名称一致时,可以简写(注解后没有括号):

```java
@RequestMapping("/getUser/{name}")
public User getUser(@PathVariable String name){
	return userService.selectUser(name);
}
```

###### 若方法参数名称和需要绑定的url中变量名称不一致时，写成(注解后有括号):

```java
@RequestMapping("/getUserById/{name}")
// 表示将URL中name的值映射(传递)给方法中的参数"userName"
public User getUser(@PathVariable("name") String userName){
	return userService.selectUser(userName);
}
```





### 响应：

##### 1.打印流直接输出输出标签或内容(JSP底层实现原理)

> 缺点：Java里面写html代码

```java
@RequestMapping("/reg")
public void register(HttpServletRequest req, HttpServletResponse resp) throws Exception {
    String msg = "注册成功！";
    // 防止乱码
    resp.setContentType("text/html;charset=utf-8");	
    // 获取打印流对象
    PrintWriter writer = resp.getWriter();
    // 通过打印流对象输出字符串"msg"
    writer.write(msg);
    // 关闭流
    writer.close();
}
```



##### 2.转发/重定向

###### 转发：

```java
@RequestMapping("/reg2")
public String register2() {
    // 以前：req.getRequestDispacher("/home.html").forward(req.resp);
    // 现在：直接return 视图的路径	语法："/转发页面的全路径"
    return "/home.html";    // 默认就是转发,省略前缀，但是也可以写
}
```

###### 重定向：

```java
@RequestMapping("/reg3")
public String register3() {
    // 以前：req.getRequestDispacher("/home.html").forward(req.resp);
    // 现在：在视图的路径前加一个 redirect:/	语法："redirect:/转发页面的全路径"
    return "redirect:/home.html";
}
```



##### 3.返回Model and View(视图和数据)

```java
@RequestMapping("/reg4")
public ModelAndView register4() {
    //既可以保存一个视图，也可以保存相关数据
    ModelAndView mv = new ModelAndView();
    mv.setViewName("/home.html");   // 写视图的路径即可，注意有正斜线
    // 存了一个值
    mv.addObject("uname", "admin");
    // 存一个数组
    mv.addObject("names", Arrays.asList("💧", "💧", "💧"));
    // 存一个map集合
    Map<String, Integer> m = new HashMap<>();
    mv.addObject("m", m);
    // SpringMVC默认用转发
    return mv;
}
```








### @RequestBody(req)：将json格式的数据转为java对象

##### 表示接收前端JSON格式的数据,多用在方法参数前,接收前台json数据,把json数据封装成对象,请求必须是post请求

###### ajax请求参数为字符串

type的值是post

contenttype的值必须是application/json

data的值必须是JSON格式字符串，不能是json对象

> 将对象转换为JSON格式字符串 ->  data:JSON.stringify("json对象")
>



###### axios请求可以直接写对象，post默认会将对象转换成JSON格式的数据

```json
// 定义一个对象
var obj = {"name":"刘备","age":13}
axios.post("映射地址",对象(obj)).then(res => {
    console.log()
})
```







### @ResponseBody(resp)：将返回的数据转换为JSON对象

> 配合Jackson(annotations,core,databind三个jar包)，会将该方法各种返回值：对象、List集合、Map集合转换为JSON格式的字符串返回给前端



会直接转换成对象，前端不需要再JSON.parse(data)将JSON字符串转对象！！！



#### @RestController = @Controller + @ResponseBody 

所以类上加了@RestController，该类所有方法进行跳转都会失败(ResponseBody把返回格式化成JSON字符串了)



##### 配置springmvc-config.xml标签< mvc:annotation-driven >标签内的数据

```xml
<mvc:annotation-driven>
	<mvc:message-converters>
	<bean class="org.springframework.http.converter.StringHttpMessageConverter"></bean>
	<bean class="org.springframework.http.converter.json.MappingJackson2HttpMessageConverter"></bean>
    </mvc:message-converters>
</mvc:annotation-driven>
```

这个注解设置在方法头部，被设置的方法返回值不会转发或重定向，会直接输出







### 全局异常处理：

###### @Component：创建当前类对象，跟controller一样，所以要修改SpringMVC-config的扫描器扫描包的位置从项目根目录或能扫描到该注解的目录

###### @ControllerAdvice：声明当前类是一个异常处理类

###### @RestControllerAdvice = @ControllerAdvice + @ResponseBody 

###### @ExceptionHandler(Exception.class) ：处理具体异常类型



##### 全局异常处理类示例：

```java
// 相当于@ControllerAdvice + @ResponseBody，所有方法上不用再单独写ResponseBody了
// @RestControllerAdvice
@Component
@ControllerAdvice
public class GlobalExceptionHandler {
	// 处理所有异常的方法，但返回不是ResultObject对象，是JSON格式的数据(@ResponseBody)
    @ResponseBody 
	@ExceptionHandler(Exception.class) // 处理具体异常类型
	public ResultObject nullException(Exception e) {
		e.printStackTrace();
		return ResultObject.error(); // error的属性：message = 请求失败
	}
}
```

> 后端有错误会出现异常500页面，设置了全局异常处理，会将后端的异常传递给被@ControllerAdvice注解声明的异常处理类，由该类中不同的异常处理方法处理。
>
> 以上述示例为例，该会返回一个JSON格式的ResultObject类型的对象，例如{"code":500,"success":false,"message":""请求失败,"data":null}
>
> 上述示例是所有异常一个方法，可以让不同异常类型走不同的方法，不返回字符串，而是根据不同的异常在方法中进行不同的处理，这就是全局异常处理解决的问题：将所有类型的异常处理从各处理过程解耦出来。







### 日期转换：让前端字符串类型数据与后端Date类型数据映射

#### 注解转换：只能处理一种日期格式的字符串

> 在实体类的某个属性上使用注解@DateTimeFormat(pattern="yyyy-MM-dd")，该属性必须要有get/set

##### 实体类：在对应Date类型的属性上加注解

```java
public class Userinfo {
	//插入数据日期和时间	注意：只能处理一种日期格式
	@DateTimeFormat(pattern="yyyy-MM-dd HH:mm:ss") 
	private Date insertDate;
}
```

##### 前端往后端传值：

```json
/testDataFormat?insertDate=2022-10-10 (空格) 11:10:10
```

##### 测试类：测试前端传递的字符串日期数据

```java
@RequestMapping("/testDataFormat")
@ResponseBody
public Userinfo testDataFormat(Userinfo userinfo) {
    System.out.println(userinfo);
    return userinfo;
}
```

##### 输出：

```json
insertDate = Thu Dec 01 11:46:00 GMT+08:00 2022
```

> 只有加了注解，前端字符串日期才能被映射到后端的日期类型的属性上,不会报400,解决了类型不匹配的问题





#### 自定义日期转换类，写一个类，实现Converter接口(org.springframework.convert...)

> 可以处理多种日期格式的字符串

##### 自定义日期转换类：

```java
public class MyConverters implements Converter<String, Date>{
	@Override	// source: 前端字符串日期对象
	public Date convert(String source) {	// 在convert方法中实现日期的转换
        // yyyy-横杠类型日期
		SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
		try {
			return format.parse(source);
		} catch (ParseException e) {
            // yyyy/正斜杠类型日期
			format = new SimpleDateFormat("yyyy/MM/dd HH:mm:ss");
			try {
				return format.parse(source);
			} catch (ParseException e1) {
				e1.printStackTrace();
			}
		}
		return null;
	}
}
```



##### 配置SpringMVC-config.xml

###### mvc:annotation-driven标签加属性：conversion-service = "日期转换器id"

> conversion-service：转换服务

```xml
<!--代表开启SpringMVC的注解驱动,允许通过注解方式开发-->
<mvc:annotation-driven conversion-service="converterService"></mvc:annotation-driven>
```

###### 配置日期转换器：

> 属性：
>
> id="自定义" 	class="org.springframework.format.support.FormattingConversionServiceFactoryBean"

```xml
<!-- 配置日期转换器 -->
<bean id="converterService" 		class="org.springframework.format.support.FormattingConversionServiceFactoryBean">
	<property name="converters">
		<set>
            <!--class值是自定义日期转换器的全路径，可以配置多个bean标签——多个日期转换器-->
			<bean class="com.wn.bean.MyConverters"></bean>
		</set>
	</property>
</bean>
```







### SpringMVC拦截器：

> 拦截器(interceptor)和过滤器(filter)类似，过滤器可以拦截访问的所有请求。
>
> 拦截器拦截所有Controller接口(方法)，如果是静态资源则不会被拦截

##### 通常使用拦截器实现用户登录验证或者权限控制、日志记录等



##### 自定义拦截器类,实现Handlerinterceptor接口/继承HandlerAdapater类，在springmvc-config中配置拦截器



##### 自定义拦截器类：实现该接口的三个方法

```java
public class LoginInterceptor implements HandlerInterceptor{

    // 执行被拦截Controller接口(方法)之前执行该方法
    // 返回布尔，true表示放行，执行下一个拦截器或者执行要访问的Controller方法 false：不放行
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        return true;
    }
    
    // 执行Controller接口完成之后，渲染视图之前执行
    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        System.out.println("执行postHandle方法！");
    }

    // 执行Controller接口完成之后，渲染视图之后执行
    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        System.out.println("执行afterCompletion方法！");
    }
}
```



##### 配置springmvc-config：

```xml
<!-- 配置用户登录拦截器 -->
<mvc:interceptors>
    <mvc:interceptor>
        <!--/** :表示拦截所有(通配符)controller接口-->
        <mvc:mapping path="/**"/>
        <!--配置特殊放行路径-->
        <mvc:exclude-mapping path="/user/login"/>
        <mvc:exclude-mapping path="/js/**"/> 
        <!-- 拦截后执行的自定义拦截器类 -->
        <bean class="com.woniu.community.interceptor.LoginInterceptor"></bean>
        <!--可以配置多个拦截器-->
        <!--拦截器2、3.....-->
    </mvc:interceptor>
</mvc:interceptors>
```



##### 实例：

```java
@Override
public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object arg2) throws Exception {
	// 拦截所有访问controller接口的请求
    String uri = request.getRequestURI();
    // 如果访问地址是toLogin或者login，直接放行
    if (uri.endsWith("/toLogin") || uri.endsWith("/login")) {
        return true;
    } else {
        // 获取session域中用户信息
        User user = (User) request.getSession().getAttribute("user");
        if (user != null) {
            //表示用户已登录 则可以访问main.jsp中链接
            return true;
        } else {
            return false;
        }
    }
}
```







### SpringMVC文件上传：

##### 导入jar包，配置springmvc-config，编写接口，提供上传文件的页面(必须使用表单实现提交文件，entype="multipart/form-data"，且是post请求)，最后通过input type="file"实现提交文件



---



## Spring：IOC/AOP

> 将控制层：Controller、业务层Service、数据操作层Dao创建的对象统一管理，解耦各个层之间的关系
>
> ###### 这种将创建对象操作交由外部框架管理的操作，就是IOC：控制反转

### IOC：容器/控制反转

##### 对象的创建是由程序控制的，现在将创建对象和管理对象的控制权交给Spring的IOC，就是控制反转。

> 引入SpringIOC相关的依赖，参考Maven文档SpringMVC引入即可，自动引入Spring子包







### 创建对象：

#### 1.通过配置文件创建Student对象

> 1.创建实体类
>
> 2.创建配置spring-config.xml

##### spring-config.xml：将类的全路径配置在bean标签中

```xml
<!--
	id：表示当前对象唯一标识符(获取对象通过id值来获取)
	class：参数是一个类的全路径，表示创建该类对象
-->
<bean id="student" class="com.wn.bean.Student"></bean>
```





#### 2.使用静态工厂类创建对象

> 1.创建实体类
>
> 2.创建工厂类，提供一个静态方法，返回值是该类类型对象
>
> 3.创建/配置spring-config.xml

##### 工厂类：

```java
public class StudentFactory {
	// 静态方法：类名.class 创建Student对象并返回
    public static Student getStudent() {
        return new Student();
    }
}
```



##### spring-config.xml：

```xml
<!-- 
	id：表示当前对象唯一标识符(获取对象通过id值来获取)
	class：参数是一个工厂类的全路径
	factory-method： 指定该工厂类中的静态方法(方法名)
-->
<bean id="student" class="com.wn.bean.StudentFactory" factory-method="getStudent"/>
```





#### 3.非静态工厂类创建对象

> 1.创建实体类
>
> 2.创建工厂类，提供一个非静态(对象)方法，返回值是该类类型对象
>
> 3.创建/配置spring-config.xml

##### 工厂类：

```java
public class StudentFactory {
	// 非静态方法,对象名.class
    public Student getStudent() {
        return new Student();
    }
}
```



##### spring-config.xml：

```xml
<!-- 
	id:表示工厂标识符
	class:参数是一个工厂类的全路径
-->
<bean id="studentFactory" class="com.wn.bean.StudentFactory"></bean> 
<!-- 
	id：表示当前对象唯一标识符(获取对象通过id值来获取)
	factory-bean:工厂标识符(使用该工厂类创建对象)
	factory-method:指定该工厂类中的方法(方法名)
-->
<bean id="student" factory-bean="studentFactory" factory-method="getStudent"></bean> 
```





#### 公共测试类：

```java
// 在方法中加载配置文件：spring-config.xml
// 配置文件加载后，会根据配置的bean标签创建对象，方法到IOC容器中
ApplicationContext context = new ClassPathXmlApplicationContext("spring配置文件全名");
ApplicationContext context = new ClassPathXmlApplicationContext("spring-config.xml");
// 从IOC容器中获取Student对象(强转)
实体类 实例名 = (实体类强转) context.getBean("bean标签的id属性值");
Student student = (Student) context.getBean("student");
```





#### 4.通过配置类创建对象(Spring3.x版本及以上才支持)

> 1.创建实体类
>
> 2.创建配置类，放在配置包(package)
>
> 3.创建/配置spring-config.xml中使用扫描器(context:component-scan)扫描该配置类

##### 配置类：

```java
//声明当前类是一个配置类
@Configuration 
public class BeanConfiguration {
	// 在方法上使用@Bean注解，表示把方法返回对象交由IOC管理
	@Bean
    // 创建对象方法，方法名称任意(方法名称作用相当于 <bean id="xxx">)
	public Student getstudent() {
		return new Student();
	}
}
```



##### spring-config.xml：

```xml
<!--
	扫描指定包路径(实体类包entity路径)下的类注解@Configuration，
	并将该类下的所有@Bean方法返回对象放到IOC容器中
-->
<context:component-scan base-package="com.woniu.bean"/>
```





#### 5.通过IOC注解创建对象

##### @Component：使用在类上，表示创建该类对象，并交由IOC容器管理( 相当于：bean id="xxx")

> 获取对象的需要的id为被注解的类首字母小写，类User被注解，id就是user，注意配置扫描器扫描被注解类

```java
User user = (User) context.getBean("user");
```

##### @Component衍生出三个注解：@Controller、@Service、@Repository

实体类entity、工具类util：@Component

Controller：@Controller

Service层：@Service

Dao层：@Repository，可以混用，都可以创建对象。



##### 设置对象属性值：

###### @Value：只能给普通类型的属性设置值

```java
@Component
public class User{
    @Value("刘备")
	private String name;
    // get/set/toString...    
}
```

###### @Resource：引用类型属性设置值，Java提供

```java
@Component
public class User{
    // 根据类型注入,xml文件中要先配置才能赋值
	@Resource	
    private Cat cat;
    // get/set/toString...    
}
```

###### @Autowired：引用类型属性设置值，Spring框架提供

```java
@Component
public class User{
    // 根据类型注入,xml文件中要先配置才能赋值,赋值的对象是默认的对象，想根据id赋值不同的:@Qualifier()
	@Autowired	
    // @Qualifier("IOC容器中创建的对象的id:<bean id="xxx">")
    // 使用xml创建的cat2对象的属性
    @Qualifier("cat2")
    private Cat cat;
    // get/set/toString...    
}
```



> 不支持数组、集合等赋值





### DI：依赖注入(给IOC容器对象赋值)

> 依赖注入不能单独存在，必须和IOC容器一起使用

#### set注入：通过对象的属性的set方法给属性赋值

##### 基础类型：

###### 实体类：

```java
public class User{
	private String name;
    // get/set/toString 必须有该属性的set方法...
    public void setName(String name){
        this.name = name;
    }
}
```

###### spring-config.xml：

```xml
<!--IOC通过配置文件创建对象:bean标签创建完，在该对象中配置property标签实现注入-->
<bean id="user" class="com.woniu.community.entity.User">
    <!--
        name:该对象的某一属性的属性名
        value:要给该属性赋的值
    -->
	<!--给当前的User类型对象name属性注入值：刘备-->
	<property name="name" value="刘备"></property>
</bean>
```

###### 测试类：

```java
User user = (User) context.getBean("user");
System.out.println(user);	// name = 刘备
```



##### 引用类型：

###### 实体类：

```java
public class User{
    private String name;
	private Cat cat;
	// get/set/toString...
}

public class Cat{
	private String cName;
    private Integer age;
    private String type;
	// get/set/toString...
}
```

###### spring-config.xml：

```xml
<!--创建Cat对象-->
<bean id="cat" class="com.woniu.community.entity.Cat">
	<property name="cName" value="关羽"></property>
    <property name="age" value="5"></property>
    <property name="type" value="蓝猫"></property>
</bean>
<!--创建User对象-->
<bean id="user" class="com.woniu.community.entity.User">
    <!--
        name:该对象的某一属性的属性名
        value:要给该属性赋的值
		ref:表示引用对象的id值(Cat对象Bean标签的id值:cat)
    -->
	<!--给当前的User类型对象name属性注入值：刘备-->
	<property name="name" value="刘备"></property>
    <property name="cat" ref="cat"></property>
</bean>
```

###### 测试类：

```java
User user = (User) context.getBean("user");
System.out.println(user);	// name = 刘备 cat = Cat[cName=关羽,age=5,type=蓝猫]
```



##### 复杂类型：

###### 实体类：

```java
public class CollectionBean{
    private String[] arr;
	private List<String> list;
    private Set<String> set;
    private Map<String,Object> map;
	// 配置文件类型
    private Properties pros;
    private Cat[] cats;
	// get/set/toString...
}
```

###### spring-config.xml：

```xml
<bean id="coll" class="com.woniu.community.entity.CollectionBean">
    
	<!--数组(字符串类型)属性注入值-->
    <property name="arr">
        <array>
            <value>刘备</value>
            <value>关羽</value>
            <value>张飞</value>
        </array>
    </property>
    
    <!--List集合(字符串类型)属性注入值-->
    <property name="list">
        <list>
            <value>刘备</value>
            <value>关羽</value>
            <value>张飞</value>
        </list>
    </property>
    
    <!--Set集合(字符串类型)属性注入值-->
    <property name="list">
        <set>
            <value>刘备</value>
            <value>关羽</value>
            <value>张飞</value>
        </set>
    </property>
    
    <!--Map集合(String，任意类型)属性注入值-->
    <property name="list">
        <map>
            <entry key="uname" value="刘备"></entry>
            <entry key="age" value="123"></entry>
            <entry key="sex" value="男"></entry>
        </map>
    </property>
    
    <!--Property属性注入值-->
    <property name="list">
        <props>
            <prop key="driverclass">com.mysql.jdbc.Driver</prop>
            <prop key="username">root</prop>
            <prop key="password">root</prop>
        </props>
    </property>
    
    <!--Cat数组注入值-->
    <property name="cats">
        <array>
            <bean id="cat1" class="com.woniu.community.entity.Cat">
                <property name="cName" value="关羽"></property>
    			<property name="age" value="55"></property>
            	<property name="type" value="蓝猫"></property>
            </bean>
            <bean id="cat2" class="com.woniu.community.entity.Cat">
                <property name="cName" value="张飞"></property>
    			<property name="age" value="36"></property>
            	<property name="type" value="黑猫"></property>
            </bean>
        </array>
    </property>
    
</bean>
```

###### 测试类：

```java
CollectionBean bean = (CollectionBean) context.getBean("coll");
System.out.println(bean);	
// CollectionBean [arr=[刘备,关羽,张飞],list=[刘备,关羽,张飞],set=[刘备,关羽,张飞]]
// CollectionBean [map={uname=刘备,age=123,sex=男}]
// CollectionBean [pros={driverclass=com.mysql.jdbc.Driver,username=root,password=root}]
// CollectionBean [cats=[Cat [cName=关羽,age=55,type=蓝猫], Cat [...] ]]
```





#### 构造方法注入：通过构造函数(构造方法)给属性设置值

##### 实体类：

```java
public class User{
	private String name;
    private Integer age;
	// 构造方法
    public User(String bname,Integer bage){
        this.name = bname;
        this.age = bage;
    }
}
```

##### spring-config.xml：

```xml
<!--根据构造方法参数名称注入值-->
<bean id="user1" class="com.woniu.community.entity.User">
    <!--
		name:构造方法中的参数名
		value:该参数的参数值
	-->
    <constructor-arg name="bname" value="刘备"></constructor-arg>
    <constructor-arg name="bage" value="12"></constructor-arg>
</bean>

<!--根据构造方法参数顺序(下标)注入值-->
<bean id="user2" class="com.woniu.community.entity.User">
    <!--
		index:下标位，从0开始
		value:该参数的参数值
	-->
    <constructor-arg index="0" value="刘备"></constructor-arg>
    <constructor-arg index="1" value="12"></constructor-arg>
</bean>

<!--根据构造方法参数类型注入值-->
<bean id="user2" class="com.woniu.community.entity.User">
    <!--
		type:该参数的类型全路径
		value:该参数的参数值
	-->
    <constructor-arg type="java.lang.String" value="刘备"></constructor-arg>
    <constructor-arg index="java.lang.Integer" value="12"></constructor-arg>
</bean>
```

##### 测试类：

```java
User user = (User) context.getBean("user1...2...");
System.out.println(user);	
// User [name=刘备,age=12]
```





### IOC容器获取Dao层对象

##### 配置文件方式创建获取：

###### Service：

```java
// @不同层的注解
public class UserServiceImpl implements UserService {
    // private UserDao userDao = new UserDaoImpl();
	// 定义dao层对象，不直接new，从IOC容器中获取，通过set注入
    // @Resource：从IOC容器中获取被注解类型的对象，注入到属性中
    @Resource
    private UserDao userDao;
    
    // 定义set方法
    public void setUserDao(UserDao userDao){
        this.userDao = userDao;
    }
}
```

###### spring-config.xml：也可以配置在mvc-config.xml

```xml
<!--通过实体类创建dao层对象-->
<bean id="userDao" class="com.woniu.dao.impl.UserDaoImpl"></bean>
<!--通过实体类创建service层对象，将dao层对象注入到service层-->
<bean id="userService" class="com.woniu.service.impl.UserServiceImpl">
    <!-- 
		name:Service层set方法的参数
		ref: UserDaoImpl类型dao层对象的id
	-->
    <property name="userDao" ref="userDao"></property>
</bean>
```



##### 简化配置开发：SpringIOC容器注解开发





### 事务

> 事务实际上就是对数据库的一个或者多个更改
>
> 在增删改操作后，默认的自动提交事务会直接操作数据库，关闭自动提交后，会先存放到缓存中，只能由COMMIT、ROLLBACK来结束事务。

#### MySQL事务处理

> "@@变量名"表示系统变量。SHOW VARIABLES -- 显示所有系统变量

##### 手动事务：关闭自动提交

###### 开启/关闭自动提交事务：修改系统变量autocommit

```sql
SET @@autocommit = 1;	-- 关闭自动提交事务(0关闭，1开启)
-- 支持范围操作
-- session：会话级别，只影响当前用户，一个连接，别的连接不受影响
SET @@session.autocommit = 1;
-- global：全局级别，影响全部用户，多个连接，后续的连接受影响
```

> global设置的域，后续用户的session和global都一致，但是设置global域的用户的session当前不受影响
>
> 对设置global的用户当前无用，对之后的用户有用，设置的用户再次登录生效

###### 手动提交/回滚事务：

```sql
COMMIT | ROLLBACK	-- 必须先关闭自动提交事务
```



##### 自定义事务：不关闭自动提交

```sql
BEGIN | START TRANSACTION -- 开启自定义事务 
-- SQL增删改语句...
COMMIT | ROLLBACK 		  -- 然后手动提交/回滚
```

> 自定义事务开启后，后面的所有SQL都会按照一个事务处理，直到COMMIT/ROLLBACK结束





#### JDBC事务处理

##### 在service层编写事务：







#### Spring事务处理

##### 导包：



##### 添加tx约束：



##### 使用Spring自带的事务管理，在SpringMVC-config中配置事务管理器对象，注入数据源：

```xml
<bean id="自定义事务管理器的id transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
    <property name="这个属性名必须是 dataSource" ref="数据源的id dataSource"></property>
</bean>
```



##### 开启事务注解开发：

```xml
<tx:annotation-driven transaction-manager="事务管理器的id transactionManager">
```



##### 配置好后在对应方法头上加注解：

```java
@Transactional	// 代表此方法出现问题，会自动回滚，不会提交事务
public void transactional(...){数据库操作}
```

###### 可以用在类上(不建议)：

```java
@Transactional	// 代表此类中所有方法，出现问题，会自动回滚，不会提交事务
public class transactional(...){数据库操作}
```



##### 异常的不同处理：

> 受查异常：编译就不通过。非受查异常：运行时异常。

###### 只能回滚非受查异常，受查异常会提交



##### 受查异常的处理方式：

```java
@Transactional(rolllbackFor = Exception.class)	// 告诉框架某种受查异常回滚
@Transactional(noRolllbackFor = Exception.class)// 告诉框架某种非受查异常不回滚
```



##### 事务隔离级别：

|       name        |          | 脏读 | 不可重复读 | 幻读 |
| :---------------: | :------: | :--: | :--------: | :--: |
| READ-UNCOMMITTED  | 读未提交 |  Y   |     Y      |  Y   |
|  READ-COMMITTED   | 读已提交 |  N   |     Y      |  Y   |
| REPEATABLE(MySQL) | 可重复读 |  N   |     N      |  Y   |
|   SERIALIZABLE    |  串行化  |  N   |     N      |  N   |

脏读：读到了没有提交的临时数据

幻读：用户执行查询过程中，只要没有执行增删改的操作，都是获取数据后缓存展示。查询后的数据可能会被另外的连接修改，看到的数据已经不具有时效性，如果执行修改，要使用数据库真实的数据修改，就是幻读。

不可重复读：用户登录数据库，多次查询同一张表，看到的数据不一致

可重复读：用户登录数据库，多次查询同一张表，看到的数据一致。





##### 事务的传播机制：

###### REQUIRED：默认的spring事务传播级别

使用该级别的特点是，如果上下文中已经存在事务，那么就加入到事务中执行，如果当前上下文中不存在事务，则新建事务执行。所以这个级别通常能满足处理大多数的业务场景。

###### REQUIRES_NEW：解决发生异常时，finaly中的代码也被回滚的问题

每次都要一个新事务，该传播级别的特点是，每次都会新建一个事务，并且同时将上下文中的事务挂起，执行当前新建事务完成以后，上下文事务恢复再执行。







### SSM整合：Spring+SpringMVC+MyBatis

Mybatis中所有对象：SqlSessionFactoryBuilder、SqlSessionFactory、SqlSession都有IOC处理

事务交由Spring







### 分页：

##### 1.前端添加分页插件(elementUI)

```html
<!--el-table标签下面-->
<!--total：总记录数(数据条数)-->
<el-pagination
  background
  layout="prev, pager, next"
  :total="1000">
</el-pagination>
<!--el-table标签下面-->
```

2.mybatis-config配置插件

```xml
<!-- 分页插件 -->
<plugins>
    <plugin interceptor="com.github.pagehelper.PageInterceptor">
    	<property name="helperDialect" value="mysql"/>
    </plugin>
</plugins>
```





##### pageInfo对象中各个get方法获取的值列表

```java
private int pageNum; //当前页
 
private int pageSize; //每页的数量
    
private int size; //当前页的数量
    
//由于startRow和endRow不常用，这里说个具体的用法
//可以在页面中"显示startRow到endRow 共size条数据"
//当前页面第一个元素在数据库中的行号
private int startRow;
 
private int endRow; //当前页面最后一个元素在数据库中的行号
 
private long total; //总记录数
    
private int pages; //总页数
    
private List<T> list; //结果集(每页显示的数据)
    
private int firstPage; //第一页
    
private int prePage; //前一页
    
private boolean isFirstPage = false;  //是否为第一页
    
private boolean isLastPage = false; //是否为最后一页
   
private boolean hasPreviousPage = false; //是否有前一页
   
private boolean hasNextPage = false; //是否有下一页
 
private int navigatePages; //导航页码数
 
private int[] navigatepageNums; //所有导航页号
```







### 登录验证码：

##### 引入huTool(Maven)

##### 设计请求方法：

```java
@RequestMapping("/getCode")
public void getCode(HttpServletResponse resp, HttpSession session) throws IOException {
    // 生成验证码，返回LineCaptcha类型的对象
    // createLine表示干扰横线的验证码，参数中定义宽、高、验证码长度、干扰线条数
    LineCaptcha lineCaptcha = CaptchaUtil.createLineCaptcha(宽, 高, 验证码长度, 干扰线条数);
    // 保存验证码的随机数(验证码图片的内容)到Session域中
    session.setAttribute("key", lineCaptcha.getCode());
    // 获取响应流
    ServletOutputStream 流名称 = resp.getOutputStream();
    // 通过流响应验证码图片给前端，三个参数(验证码图片、图片格式、通过什么方式(流)响应)
    ImageIO.write(lineCaptcha.getImage(), "JPEG", sos);
}
```

##### 示例：

```java
@RequestMapping("/getCode")
public void getCode(HttpServletResponse resp, HttpSession session) throws IOException {
    LineCaptcha lineCaptcha = CaptchaUtil.createLineCaptcha(116, 36, 4, 10);
    session.setAttribute("code", lineCaptcha.getCode());
    ServletOutputStream sos = resp.getOutputStream();
    ImageIO.write(lineCaptcha.getImage(), "JPEG", sos);
}
```





##### 数据库查询MD5对应字符串：

```sql
-- 查询12345对应MD5
SELECT MD5("12345") FROM dual
```













