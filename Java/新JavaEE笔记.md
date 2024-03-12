## JS(Java Script)：客户端动态脚本

### 引入：

```html
<script src="/路径"></script>	<!--必须有结尾，不能<script/>直接结束-->
```



### DOM：文档对象模型

> 文档对象模型，又称为文档树模型，一套操作页面元素的API。
>
> 可以把HTML看作文档树，通过DOM提供的API可以对树上的节点进行操作。

#### 基本概念：

当网页被加载时，浏览器自动创建页面的文档对象模型

DOM 就是一个HTML页面，代表整个网页，它将页面的每个标签都看作是一个对象。

DOM提供操作这些标签(对象)的方法，因为DOM文档对象是您的网页中所有其他对象的拥有者(可以理解为父类) 





#### DOM可以实现的功能：

1. 作为*对象*的 HTML元素
2. 所有 HTML 元素的属性
3. 访问所有 HTML 元素的方法
4. 所有 HTML 元素的事件



#### DOM常用操作：

1. 获取文档元素

2. 对文档元素进行增删改查操作

3. 事件操作

> 换言之：DOM 是关于如何获取、更改、添加或删除 HTML 元素的标准。
>





#### DOM包含的对象：

##### Document：文档对象

文档对象代表网页。访问 HTML 页面中的任何元素，从访问 document 对象开始。





#### DOM包含的属性：

##### 标签.value(属性)：获取某个标签元素的值

```js
<input type="text" id="rows"/>	// 假设输入5
let num = document.getElementById("rows").value	// num的值为5
```



##### innerHTML：改变指定标签元素的值

```html
<p id="p1">刘备</p>
<script>
	document.getElementById("p1").innerHTML = "关羽";	// 将p标签内的值修改为关羽
</script>
```



#### DOM包含的方法：

##### 查找 HTML 元素

| 方法                                  | 描述                     |
| :------------------------------------ | ------------------------ |
| document.getElementById(id)           | 通过元素 id 来查找元素   |
| document.getElementsByTagName(name)   | 通过标签名来查找元素     |
| document.getElementsByClassName(name) | 通过类名来查找元素       |
| getElementById(id)                    | 通过id查找元素，返回对象 |
| getElementsByTagName(name)            | 返回对象数组             |



##### 改变 HTML 元素

| 方法                                       | 描述                   |
| :----------------------------------------- | :--------------------- |
| element.innerHTML = new html content       | 改变元素的 inner HTML  |
| element.attribute = new value              | 改变 HTML 元素的属性值 |
| element.setAttribute(*attribute*, *value*) | 改变 HTML 元素的属性值 |
| element.style.property = new style         | 改变 HTML 元素的样式   |



##### 添加和删除元素

| 方法                                   | 描述                   |
| :------------------------------------- | :--------------------- |
| document.createElement(*element*)      | 创建 HTML 元素         |
| document.removeChild(thisNode、parent) | 删除父节点的一个子节点 |
| document.appendChild(*element*)        | 添加 HTML 元素         |
| document.replaceChild(*element*)       | 替换 HTML 元素         |
| document.write(*text*)                 | 写入 HTML 输出流       |







### BOM：浏览器对象模型

#### 基本概念：

跟DOM的区别是BOM将整个浏览器看作一个对象，比DOM(网页)范围要大，BOM包含DOM。





#### BOM对象(内置对象)

##### Window：浏览器对象，包含Document

```js
<script>window.document.xxx</script>
```



#### 属性

##### location：地址栏

```html
<p id="demo"></p>
<script>
    window.location.href // 属性返回当前页面的 URL
    document.getElementById("demo").innerHTML = 
    "本页面的完整 URL 是：<br>" + window.location.href;
</script>
```







### 变量

#### 定义：var、let、const

> JS中没有细分的变量类型，只有var，let、const，它们可以存储任意类型的数据

```js
var x = 1;	let x = 1;
```

> 建议用let来定义变量(块级作用域)，因为var是全局变量(全局作用域)，会产生一些BUG。

##### 例如for循环：

```js
for (var i = 0; i < 3; i++) {
	console.log(i);	// 输出i
}							
// 正常情况下是输出不了i的，i是for循环体定义的变量
console.log("i的值为：" + i);	// 但是这里可以输出，因为var定义的变量是全局变量，超范围用let则会报错
```



##### const：定义时必须初始化(赋值)，而且初始值无法修改；类似于final

```js
const num = 10;
```





#### 数据类型：

##### 基本：number(数字)、boolean(布尔值)、string(字符串)、undefined(未定义)、null(空的)、Symbol(符号)

##### 引用：也就是对象类型Object(对象)，function(函数)、date (时间)、array(数组)







### 数组

#### 定义：

##### 1、直接定义数组：

```js
var nums = [1,2,3];	// js中是方括号，不是{}
```



##### 2、new关键字：

###### (1)用构造函数创建一个动态数组

```js
var nums = new Array();
```

###### (2)：用构造函数创建一个初始长度为三的数组

```js
var nums = new Array(3);
```

###### (3)：用构造函数创建一个带初始值的数组，而该数组的长度为1

```js
var c = new Array("8");
```

###### js里的数组是动态扩容的。创建数组会用空占位，所以push会在创建数组的长度后面继续添加：

```js
var a = new Array(3); // 创建一个长度为三的数组
names.push("张三");	// 添加一个张三
console.log(names.length);	// 数组长度为4
```





#### 数组方法：

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

```js

```





### 函数

#### 创建函数(方法)：

##### 基本函数：

```js
function 函数名称(参数列表) {
	return 值;
}
```



##### 构造函数(方法)：

```js
function Employee (id,name) {
	this.id = 1;	// this代表当前对象，构造方法上面没定义该属性，JS会动态创建一个属性
	this.name = "张三";
}
p1 = new Employee(2,"关羽");	// 创建一个对象
```



##### 匿名函数：

```js
window.onload = function(){
	init();
}
```



##### 调用：

###### 无参无返回：

```
function test1() {

}
```



#### 常用函数：

##### 输出

###### (将日志)输出到控制台(println)：

```js
console.log("要输出的语句");
```

###### alert：弹出框输出到页面

```js
alert("文本");
```

###### write：输出到页面

```js
document.write("文本");
// 支持标签输出
document.write("<a>文本</a>");
```



##### 赋值

```js
document.getElementById("id").属性名 = "属性值";
// 选中某id的复选框
document.getElementById("id").checked = "checked";
// 可以赋布尔值
document.getElementById("id").checked = "true/false";
```



##### 定时器

###### setTimeout(方法名,ms时间)：一次性定时器

```js
// 有小括号，有""
setTimeout("方法名()",ms时间)
// 没有小括号，也没有""
setTimeout(方法名,ms时间)
```

###### clearTimeout()：关闭计时功能

```js
// setTimeout("方法名()",ms时间)，有一个返回值可以接收
var timeStop;
timeStop = setTimeout("方法名()",ms时间);
// 将返回值给clearTimeout()方法，作为他的参数，就可以关闭计时
clearTimeout(timeStop);
```

###### setInterval()：每隔指定时间执行一次

```js
setInterval("方法名()",ms时间)
```

###### clearInterval()：关闭计时

```js

```





##### 初始化

###### 标签属性：

```html
<!--页面加载调用init方法，进行初始化-->
<body onload="init()"></body>	
<script>
    <!--init不需要()-->
    window.onload = init
   	<!--通过匿名函数实现-->
	window.onload = function(){
        init();
    }
</script>	

```



#### 注意事项：

##### 1、判断字符串长度的.length是属性，不是.length()方法

##### 2、new关键字调用构造函数。js中任何函数都可以看作构造函数

##### 3、subString(参数一，参数二)中的参数二不是指截取几位，而是从参数一截取到参数二的索引下标



---



## JQuery：创造EASY jS

### 在线引入JQuery：直接写在HTML里

```html
<script src="https://code.jquery.com/jquery-3.1.1.min.Js"></script>
```

> ##### 写JQuery要声明：写一个$符号

### 函数(方法)

#### $()：工厂函数

> ()就是工厂函数

```js
$("标签名/id、类选择器")
$("form")	// 将form标签转换为JQuery对象,JQuery对象其实就是JS对象，但是JS对象!=JQuery对象
```



#### 内置函数

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



##### serialize()：序列化表单值

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
// URL 编码格式的文本字符串
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





---





# 后端

## Tomcat

### idea配置TomCat的Maven插件：

#### 



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



## 三层架构：Controller、Service、Dao(Repository)

### Controller：前端控制层(Servlet)

> 主要是指与用户交互的界面,用于接收用户输入的数据和显示处理后用户需要的数据

#### 

### Service：业务逻辑层

> 前端控制层和数据库访问层之间的桥梁,实现业务逻辑,具体包含：验证、计算、业务规则等等



### Dao：数据库访问层(JDBC)

> 对数据库的增删改查



---



## HttpServlet

### Servlet生命周期

#### 客户端向服务器端发出请求(点击按钮提交表单submit) --> 服务器解析请求 --> 服务器创建Servlet对象 --> Servlet对象调用init方法 --> 

##### init()方法：

###### 什么时候被调用？

 init()方法只会被调用一次，在第一次访问or创建Servlet 的时候调用，在后续的每次请求时都不会再调用方法了。

###### 作用？

 用于 Servlet 的初始化，可以简单地创建或加载一些数据，这些数据将被用于 Servlet 的整个生命周期。

####  --> 调用service方法(req.get获取数据进行处理) --> 输出响应信息(resp响应对象转发、重定向到另一个页面等) --> 响应给客户端 --> 调用destroy()方法(不再路由服务器接收到的请求)

##### destory()方法：

关闭服务器时自动调用，如果手动调用，servlet被销毁，但是并不立即被回收，再次请求时，并不重新初始化



### 使用

> 引入TomCat根目录src/lib下servlet-api.jar，或先import，手动点击自动下载引入

#### 继承HttpServlet：

当前端发起请求时，Tomcat接收后，会去调用Java里的HttpServlet类的service方法，

Service不是我们自己的方法，那么可以手动继承HttpServlet类并重写该方法：

```java
import javax.servlet.http.HttpServlet;	//	先导包，手动引入并下载
public class LoginController extends HttpServlet {
	//	直接写service，代码提示自动继承父类service方法
}
```

##### 实例：

```java
public class LoginController extends HttpServlet{
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.service(req, resp);	// 删除这行
    }
}
```





#### 声明Servlet：

重写后依然不能运行，因为当有多个service的情况下，Tomcat不知道该运行哪个类里的service方法。

此时给类添加一个注解，Tomcat就知道该执行哪个类的service方法了：@WebServlet

##### 实例：

```java
@WebServlet	//	添加在类上面
public class LoginController extends HttpServlet{
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.service(req, resp);	// 删除这行
    }
}
```

###### 该注解有一个属性：String[] urlPatterns() default{};	用于映射；

浏览器地址就写：`http://ip地址:端口/项目名/类的映射地址：`

比如：`http://localhost:8080/could/login`

```java
@WebServlet(urlPatterns = "/login")	// 映射地址前面必须加斜杠，类和类之间的不能重复，斜杠代表根目录
public class LoginController extends HttpServlet{
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("你成功了！");
    }
}
```





### 总结：

从Tomcat上获取图片：http://localhost:8080/项目逻辑名(TomCat中配置)/以WebApp为根目录的文件路径

##### 例如：

###### 获取后端保存的图片a.jpg：

​	http://localhost:8080/could/a.jpg

###### 获取html页面：

​	http://localhost:8080/could/index.html

以上都有一个对应的路径。那么获取后端的Servlet类，项目逻辑名后面写的就是声明Servlet时使用的注解@WebServlet的参数urlPatterns的值：

```java
@WebServlet(urlPatterns = "/login")	//	假定是这个
```

​	那么调用执行该类的service方法：http://localhost:8080/could/login即可。

> 注解参数可以简写：省略urlPatterns属性名

```java
@WebServlet("/login")	// 必须由'/'开头
```







### 客户端-->Tomcat服务器端：HttpServletRequest

#### URL传参&提交表单：

现在可以通过该链接访问我们指定的login方法：http://localhost:8080/could/login

方法的参数则可以通过URL来进行传递，格式为(一个参数)：

```java
http://localhost:8080/could/login?参数名=值
http://localhost:8080/could/login?uname=zhangsan
```

两个参数用&连接：

```java
http://localhost:8080/could/login?uname=zhangsan&pwd=123456
```

当客户端通过URL向Tomcat发出请求的时候，该请求会被封装成一个请求对象，对象里有URL传递的值，发送给Tomcat，但是Tomcat不会处理该对象，而是会直接把对象传给对应的继承HttpServlet类的service方法，这个对象的类型就是：HttpServletRequest 类型

```java
@Override
protected void service(HttpServletRequest req) throws Exception {				
    // HttpServletRequest req，req是请求对象
	System.out.println("已访问Servlet！");
}
```





#### 方法：

##### getParameter()：获取HttpServletRequest 对象的值(URL里的参数)

语法：请求对象.getParameter("参数名")， 参数名就是表单中所有标签元素的name参数写的值

###### URL：

```url
http://localhost:8080/could/login?uname=zhangsan;
```

###### Servlet：

```java
String uname = req.getParameter("uname");	// 默认是String，用String接收
System.out.println("用户名是：" + uname);	// 输出zhangsan
```

获取不到值可以给输入框写一个Value(默认输入框值)：

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



##### HttpServletRequest对应的方法：

![资源分配图](https://s2.loli.net/2023/02/18/jYgCfsnT2MzZSGL.jpg)





#### 调用同一Controller的不同方法：设计一个不同的参数

在页面提交、指定Controller映射地址后写一个问号跟上参数名、参数值：

```jsp
<!--controller映射地址?参数名=参数值-->
<a lay-href="org?opt=list">机构管理</a>	<!--传递一个method，值为selectAll-->
<a lay-href="org?opt=del">删除机构</a>	<!--传递一个method，值为deleteById-->
```

后台Controller根据不同的method的值调用不同的方法：

```java
// 首先获取参数以及参数值
String method = req.getParameter("method");
if (method.equals("selectAll")) {
	// 调用查询方法，执行查询相关操作
} else () {
	// 调用删除方法，执行删除相关操作
}
```

> 可以封装一个BaseServlet，继承Servlet，通过反射自动根据不同的method的值调用方法
>







### Tomcat服务器端-->客户端：HttpServletResponse

#### 响应客户端方案 	

##### 方案一：

###### 创建一个打印流：

```java
PrintWriter writer = resp.getWriter();	// 获取打印流对象writer
```

###### 调用write()：

```java
writer.write("你好收到了");	// 向客户端(浏览器)输出“你好收到了”
```

###### 输出HTML对应标签类型的内容：

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





#### 转发器和重定向的区别：

1、请求次数不同

转发器一次请求，服务器会将客户端请求访问的页面在内部获取到，再转发给客户端；

重定向则是告诉客户端该访问哪里，让客户端重新发送一个请求，自己获取访问的页面。

2、地址栏不同

重定向地址栏会发生变化，转发地址栏不会发生变化；

3、是否共享数据

重定向两次请求不共享数据，转发一次请求共享数据（在request级别使用信息共享，使用重定向必然出错）；

4、跳转限制

重定向可以跳转到任意URL，转发只能跳转本站点资源；

5、发生行为不同

重定向是客户端行为，转发是服务器端行为；







### 前后端传值包含中文乱码

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

###### 





### 客户端接收服务器端返回的值：根据不同的登录用户返回不同的登录名

#### 实例：显示用户xxx登陆成功，xxx部分需要动态显示

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







## MyBatis：Dao层框架

### 配置：

##### 1、配置Maven(MySQL-Connector-java、MyBatis、Lombok)



##### 2、配置数据源(给连接池)：URL、用户名、密码, 写在resource目录 -> Mybatis引擎文件(mybatis-config.xml)

> URL涉及到MySQL驱动，需要引入驱动(MySQL的Maven)

##### mybatis-config.xml模板：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">	<!--约束头，这个文件能写哪些标签-->

<!--在Java中他是一个对象-->
<configuration>
    <!--引入单独配置文件(properties)，使用占位符配置数据源-->
    <properties resource="mysql.properties"></properties>
    
    <!--配置resultType的别名，两种方式-->
    <!--
        <typeAliases>
			配置单一类的别名(mapper中resultType写alias的值)
            <typeAlias type="com.woniu.entity.Student" alias="Student"/>
			配置一个包中的所有类(mapper中resultType直接写类名)
            <package name="com.woniu.entity"/>
        </typeAliases>
    -->

    <!-- log4j日志 (框架文件中有详细配置)-->
    <!-- 
        <settings>
             <setting name="logImpl" value="LOG4J"/>
         </settings>
     -->
    
    <!-- 配置mybatis运行环境,复数标签，表示可以配置多个environment(运行环境) -->
    <!-- default的值对应不同运行环境(environment)的id值 -->
    <environments default="development">
        <!-- 一组环境中的第一个 -->
        <environment id="development">
            <!-- 使用JDBC的事务管理 -->
            <transactionManager type="JDBC"/>
            <!--数据源，类型="连接池" 使用默认内置连接池-->
            <dataSource type="POOLED">
                <!-- MySQL数据库驱动配置(JDBC四大参数)-->
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
    
    <!-- 将mapper(xxxDao、xxxMapper.xml)文件加入到配置文件中 -->
    <mappers>
        <mapper resource="XxxMapper.xml"/>
    </mappers>
</configuration>
```



##### 单独配置数据源(外置JDBC四大参数值)：mysql.properties

> 不再将数据源的参数写在mybatis引擎文件,引入配置文件,引擎文件中写占位符,占位符的值在配置文件中获取

```properties
自定义属性名=属性值
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/数据库名?useUnicode=true&amp;characterEncoding=utf8&amp;serverTimezone=GMT%2B8
jdbc.username=数据库账户
jdbc.password=数据库密码
```



##### 引擎文件中使用${占位符(自定义属性名)}获取配置文件mysql.properties中的属性值：

```xml
<!-- 配置mybatis运行环境,environments，复数表示可以配置多个environment(运行环境) -->
<environments default="development">
    <!-- 一组环境中的第一个 -->
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







### 使用：

> 有实现类，在实现类中配置三个核心对象

#### XxxDaoImpl：Mybatis三大核心对象

##### 1. SqlSessionFactoryBuilder

配置文件mybatis-config.xml的configuration标签在Java中是一个对象：SqlSessionFactory

要把该标签转换为工厂对象，需要先将配置文件通过解析器进行解析

创建一个解析器对象，用于解析mybatis-config.xml这个文件，解析器类型是SqlSessionFactoryBuilder

```java
// 创建解析器对象builder
SqlSessionFactoryBuilder builder = new SqlSessionFactoryBuilder();	
```



##### 2. SqlSessionFactory(工厂)

> 解析器对象解析要求传一个Reader字符流对象

###### 定义mybatis_config配置文件地址：

```java
String resources = "mybatis_config.xml";
```

###### 获取Reader字符IO流：

```java
Reader reader = Resources.getResourceAsReader(mabatis配置文件);
Reader reader = Resources.getResourceAsReader(resoutces);
```

###### 将流交给解析器进行解析：

```java
// 解析器返回一个造代理对象的工厂
SqlSessionFactory sqlSessionFactory = 解析器对象.build(Reader reader);	
SqlSessionFactory sqlSessionFactory = builder.build(reader); 
```



##### 3. SqlSession(执行SQL命令)

> 该方法有一个参数为boolean的重载方法，true代表自动提交事务，false代表不自动提交。默认false

```java
SqlSession sqlSession = sqlSessionFactory.openSession(/*默认false，不提交*/);	
```



##### 4. getMapper()：操作mapper生成代理对象

```java
// 这里传递的是接口.class，Mybatis竟然可以创建对象
sqlSession.getMapper(被代理接口.class);	
// 返回对应接口的代理对象 跟代理的getProxy(被代理类的class)一致 用的动态代理：CGLIB
//生成代理对象dao
IOrgCorporationDao dao = sqlSession.getMapper(IOrgCorporationDao.class); 
```

###### 代理对象dao已经代理了IOrgCorpoprationDao接口，可以调用该接口的抽象方法：

```java
// 被代理接口，有方法save()
public interface IOrgCorporationDao {	
    // 向数据库添加一条数据
    public void save();	
}
// 被代理接口的实现类
public XxxdaoImpl {
    // 代理对象.接口方法
}
// IOrgCorporationDaoImpl：dao.save();	
// (一般是Controller层实现类)的方法调用抽象方法，失败：代理类没有方法，dao没有自己的方法体来代理执行
```





#### SQL语句(代理对象调用被代理接口方法后执行的方法体)有两种：xml实现、注解实现

##### mapper.xml模板

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--namespace属性指定被代理对象的所属类(接口)的全路径-->
<mapper namespace="以蓝色Java文件夹为根目录被代理接口路径">
	<!--SQL语句，或者说实现namespace接口的实现类(代理类)的方法体-->
</mapper>
```



##### xml实现：增删改

###### 被代理接口：

```java
public interface IOrgCorporationDao {
    // 调用的方法一，无参
    public void save();
    // 调用的方法二，有参
    public void save2(	
        // @Param("别名")该注解的参数值对应占位符中的参数名，方便维护
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

###### 直接写SQL语句(SQL写死)：

```xml
<mapper namespace="以蓝色Java文件夹为根目录被代理接口路径">
    <!--四个标签insert、delete、update、select-->
    <insert id="被代理接口内某个方法的方法名" parameterType="参数类型的全限定名">	
        <!--普通SQL语句-->
    </insert>
</mapper>
```

实例：

```xml
<!--mapper.xml模板-->
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="com.woniu.IOrgCorporationDao">
    <!--id:被代理接口的方法名 dao.save()调用该"方法体",执行SQL-->
	<insert id="save" parameterType="com.woniu.entity.Corporation">	
        INSERT INTO org_corporation(cname,pname,phone,state)
        VALUES ('阿里巴巴', '董本洪', '123123', '1')
    </insert>
</mapper>
```

###### Param占位符形式写SQL语句(动态传参)：

```xml
<mapper namespace="以蓝色Java文件夹为根目录被代理接口路径">
	<insert id="被代理接口内某个方法的方法名">
        <!--Param占位符SQL动态传参(#{参数名}或者${参数名}，一般用#)-->
    </insert>
</mapper>
```

实例：

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



##### xml实现：查

> 如果方法的参数有多个，必须使用@Param注解，如果多个参数中包含对象，则映射应写为注解别名.属性名

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

> 查询出的字段与实体类对象的属性不一致，实体对象的属性映射不上，给查询出的数据起别名或使用resultMap手动对应字段跟属性



##### resultType的基本类型和包装类型值：

```java
_int = int // 基本数据类型用下划线和类型表示
int = Integer // 包装类型直接用对应的拆箱类型表示
```





##### 映射文件中#和$的区别：

#相当于给参数加引号，参数值不固定，预编译，$相当于占位符，参数名是什么就是什么，直接打印

```sql
-- 传一个csdn
select * from user where name = #{name}
-- 结果为
select * from user where name = 'csdn'

select * from user where name = ${name}
-- 结果为
select * from user where name = csdn
```

> \#的优势就在于它能很大程度的防止sql注入，而$则不行。
>
> 比如：用户进行一个登录操作，后台sql验证式样的：
>
> ​	select * from user where username=#{name} and password = #{pwd}，
>
> 如果前台传来的用户名是“wang”，密码是 “1 or 1=1”，用#的方式就不会出现sql注入
>
> 而如果换成$方式，sql语句就变成了 
>
> ​	select * from user where username=wang and password = 1 or 1=1。这样的话就形成了sql注入。



##### 注解实现：纯注解方法体，不编写mapper.xml

> 只需要在被代理接口上添加注解@Mapper，SQL通过注解写在方法头上，不再写在mapper.xml配置文件了

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





#### 多表联查：

> 首先要有实体类，数据库每张表对应一个实体类，表的每列对应该实体类的属性，那么每行就是一个对象，查询返回对象，所以接口的抽象方法用List<实体类>来接收。

##### 接口：

```java
public interface IOrgCorporationDao {
    // 查询要有返回值，返回对象，List接收
    public List<OrgCorporationBean> findAll();	
}
```



##### 一步查询(普通查询)：id、result

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

###### 实体类：

```java

```

###### 实例：

```

```



##### 多对多：转换成一对多和多对一

> 一个学生选择多个课程，一个课程被多个学生选择，需要中间表(成绩表、选课表)

###### 实体类：

```java
// Student、Course(课程)省略、Score(成绩表)
public class Student {
    // 主键id
    private Integer sId;
    private String sName;
    // 选择的课程
    private List<Course> courses;
}

public class Course {
    // 主键id
    private Integer sId;
    private String sName;
    // 选择的学生
    private List<Student> student;
}

public class Score {
    // 主键id
    private Integer scoreId;
    // 两个对一
    private Student student;
    private Course course;
}
```

###### 实例：

```xml
<!--两个association-->
```



##### 分步查询

###### 原一步查询：根据id查询员工(对一association)

```xml
<select id="selectEmployeeById" resultMap="empMapper">
    <!--此处联表，联结部门表-->
    select * form employee e,department d where eId = #{eId} AND e.did = d.did
</select>

<resultMap id="empMapper" type="xxx.entity.Employee">
	<id column="eId" property="eId"/>
    <result column="eName" property="eName"/>
    <association property="department" javaType="xxx.entity.Department">
        <id column="dId" property="dId">
    	<!--员工表中有员工信息以及部门id，没有部门名称-->
        <result column="dName" property="dName">
    </association>
</resultMap>
```

###### 分步：select语句加上id

```xml
<select id="selectEmployeeById" resultMap="empMapper">
    <!--此处不联表-->
    select * form employee where eId = #{eId}
</select>

<resultMap id="empMapper" type="xxx.entity.Employee">
	<id column="eId" property="eId"/>
    <result column="eName" property="eName"/>
    <!--加上select、column属性-->
    <!--select的值为外置select标签语句的id，column的值为将上一次查询哪一字段值传到后面作为查询条件-->
    <association property="department" javaType="xxx.entity.Department" 
     select="selectDepartmentById" column="dIdxxx">
        <id column="dId" property="dId">
        <result column="dName" property="dName">
    </association>
</resultMap>

<!--将查询员工表的did传给这条查询SQL作为查询条件-->
<select id="selectDepartmentById" resultType="xxx.entity.Department">
    <!-- #{dIdxxx}association标签的属性：column的值-->
	SELECT * FROM department WHERE dId = #{dIdxxx}
</select>
```

> 总结：一对一，一个人只能有一个身份证号， 一个身份证号只能属于一个人，人实体类引入身份证对象。
>
> ​			一对多，一个班级拥有多个学生，班级实体类引入学生集合。
>
> ​			多对一，多个学生同属一个班级，查询所有学生并且将所属班级也查询出来。
>
> ​			多对多，





#### 特殊SQL

##### %模糊查询：

###### 直接拼接：

```SQL
SELECT * FROM student WHERE name LIKE '%' #{占位符} '%';
```

###### CONCAT：

```sql
SELECT * FROM student WHERE name LIKE CONCAT('%',#{占位符},'%');
```





#### 动态SQL

##### select：按条件拼接对应的SQL语句

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
        <if test="userName != null">
            and userName = "刘备"
        </if>
	</where>
</select>
```



##### choose...when...otherwise()

```xml
<choose>
	<when test="布尔表达式">
    	<!-- 满足...执行when,并跳出 -->
	</when>
    <otherwise>
    	<!-- 所有条件都不满足 -->
    </otherwise>
</choose>
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



##### include：sql片段复用

```xml
<sql id="自定义id">SQL语句</sql>
<select id="" resultType="">
	SQL语句 + <include refid="sql片段的id" />
</select>
```

###### 实例：

```xml
<sql id="select">FROM student</sql>
<select id="***" resultType="***">
	SELECT * <include refid="select" />
</select>
```





#### 在引擎文件(Myabtis_config)中引入mapper注解/mapper.xml

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





#### 驼峰转换：数据库列与实体类属性不一致

> 数据库列：stu_sname	实体类属性：stuName，下划线可以自动转换

##### 配置mybatis-config

```xml
<settings>
    <!-- 打开驼峰转换，默认false -->
    <setting name="mapUnderscoreToCamelCase" value="true"></setting>
</settings>
```







### 完整流程

#### 带接口实现类的方式：

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

###### 被代理接口的实现类

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



##### resources：

###### mapper.xml

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





#### 接口直接对应xxxmapper.xml的方式(动态代理)：

##### Dao层接口直接与同名的"xxxMapper.xml"对应，没有实现类

> 接口与XxxMapper.xml文件在一个包下(非Web项目)

###### 无Controller、Service层，Dao层(mapper)直接由测试类控制示例：

```java
public class OwnerTest {

    // private OwnerDaoImpl ownerMapper = new OwnerDaoImpl();

    private SqlSession sqlSession;
    private OwnerMapper ownerMapper;

    /**
     * Junit测试方法之前实例化代理对象
     */
    @Before
    public void before() {
        // 调用自封装的MybatisUtil获取Session对象
        sqlSession = MybatisUtil.getSession();
        // 获取接口的代理对象(Dao层对象没有Dao实现类也可以生成)
        // dao层接口必须跟mapper映射文件的文件名一致
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



---



## Spring：IOC/AOP

> 将控制层：Controller、业务层Service、数据操作层Dao创建的对象统一管理，解耦各个层之间的关系
>
> ###### 这种将创建对象操作交由外部框架管理的操作，就是IOC：控制反转

### IOC：容器/控制反转

##### 对象的创建是由程序控制的，现在将创建对象和管理对象的控制权交给Spring的IOC，就是控制反转。

> 引入SpringIOC相关的依赖，参考Maven文档引入spring-context即可，自动引入Spring(bean等)子包







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
String path = "spring文件名"
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

> Autowired不能指定id进行注入，要指定id进行注入还要使用@Qualifier进行配合

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





---











---





## 事务

> 事务实际上就是对数据库的一个或者多个更改
>
> 在增删改操作后，默认的自动提交事务，会直接操作数据库，关闭自动提交后，会先存放到缓存中，只能由COMMIT、ROLLBACK来结束事务。

### 事务的四大特性：ACID

#### 原子性：atomicity

一个事务要么全部提交成功，要么全部失败回滚，不能只执行其中的一部分操作，这就是事务的原子性





#### 一致性：consistency

事务的执行不能破坏数据库数据的完整性和一致性，如果数据库系统在运行过程中发生故障，一组SQL尚未完成就被迫中断，之前完成的SQL对数据库所作的修改已写入物理数据库，而这组事务中后面的SQL没有执行到，这时数据库就处于一种不正确的状态，也就是不一致的状态





#### 隔离性：isolation

事务的隔离性是指在并发环境中，并发的事务时相互隔离的，一个事务的执行不能不被其他事务干扰。不同的事务并发操作相同的数据时，每个事务都有各自完成的数据空间，即一个事务内部的操作及使用的数据对其他并发事务时隔离的，并发执行的各个事务之间不能相互干扰

##### 事务隔离级别：

|       name        |          | 脏读 | 不可重复读 | 幻读 |
| :---------------: | :------: | :--: | :--------: | :--: |
| READ-UNCOMMITTED  | 读未提交 |  Y   |     Y      |  Y   |
|  READ-COMMITTED   | 读已提交 |  N   |     Y      |  Y   |
| REPEATABLE(MySQL) | 可重复读 |  N   |     N      |  Y   |
|   SERIALIZABLE    |  串行化  |  N   |     N      |  N   |

###### 读未提交(脏读)：读到了没有提交的临时数据，该隔离级别允许脏读取，其隔离级别最低；比如A和B同时操作数据库，A在整个执行阶段，会将某数据的值从1开始一直加到10，然后进行事务提交，同时，事务B能够看到这个数据项在事务A操作过程中的所有中间值（如1变成2，2变成3等），而对这一系列的中间值的读取就是脏读

###### 读已提交：授权读取只允许获取已经提交的数据。比如事务A和事务B同时进行，事务A进行+1操作，此时，事务B无法看到这个数据项在事务A操作过程中的所有中间值，只能看到最终的10。另外，如果说有一个事务C，和事务A进行非常类似的操作，只是事务C是将数据项从10加到20，此时事务B也同样可以读取到20

###### 可重复读：用户执行查询过程中，只要没有执行增删改的操作，都是获取数据后缓存展示。查询后的数据可能会被另外的连接修改，看到的数据已经不具有时效性，如果执行修改，要使用数据库真实的数据修改，就是幻读。保证在事务处理过程中，多次读取同一个数据时，其值都和事务开始时是一致的，因此该事务级别禁止不可重复读取和脏读取，但是有可能出现幻影数据。所谓幻影数据，就是指同样的事务操作，在前后两个时间段内执行对同一个数据项的读取，可能出现不一致的结果。在上面的例子中，可重复读取隔离级别能够保证事务B在第一次事务操作过程中，始终对数据项读取到1，但是在下一次事务操作中，即使事务B（注意，事务名字虽然相同，但是指的是另一个事务操作）采用同样的查询方式，就可能读取到10或20；用户登录数据库，多次查询同一张表，看到的数据一致

###### 串行化：最严格的事务隔离级别，它要求所有事务串行执行，即事务只能一个接一个的进行处理，不能并发执行。





#### 持久性：durability

一旦事务提交，那么它对数据库中的对应数据的状态的变更就会永久保存到数据库中。--即使发生系统崩溃或机器宕机等故障，只要数据库能够重新启动，那么一定能够将其恢复到事务成功结束的状态



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



##### @Transactional注解的参数：异常的不同处理

> 受查异常：编译就不通过。非受查异常：运行时异常。只能回滚非受查异常，受查异常会提交

##### 受查异常的处理方式：

```java
@Transactional(rolllbackFor = Exception.class)	// 告诉框架某种受查异常回滚
@Transactional(noRolllbackFor = Exception.class)// 告诉框架某种非受查异常不回滚
```









##### 事务的传播机制：

###### REQUIRED：默认的spring事务传播级别

使用该级别的特点是，如果上下文中已经存在事务，那么就加入到事务中执行，如果当前上下文中不存在事务，则新建事务执行。所以这个级别通常能满足处理大多数的业务场景。

###### REQUIRES_NEW：解决发生异常时，finaly中的代码也被回滚的问题

每次都要一个新事务，该传播级别的特点是，每次都会新建一个事务，并且同时将上下文中的事务挂起，执行当前新建事务完成以后，上下文事务恢复再执行。





