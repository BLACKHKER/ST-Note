



# 1、注解 @interface

#### 元注解(官方注解)：@Target、@Retention

```java
d@Target(ElementType.类型)	// 描述注解的使用范围	ElementType：元素类型 
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



##### 提交、跳转：

> onclick会直接跳转，不显示alert，这时需要更改不在点击的时候触发，改为提交的时候：

```js
// onsubmit
document.querySelector("选择器").onsubmit = function(){
	// 要触发的事件
}
```



---



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
    dataType: "json",
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
<!--{{参数名}}-->
<!--{{对象名.属性}}-->
<h2>{{text}}</h2>	<!--输出value1-->
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
<!-- 绑定name属性,该标签name属性的值为attribute的值"attributeTest" -->
<div v-bind:name="attribute"></div>
```

###### 简写：只在属性名前写一个冒号(:)来绑定

```html
<div v-bind:name="attribute" :class="attribute" :title="attribute">绑定标签属性简写</div>
```



##### v-model:参数名：双向的属性绑定

```html
<!-- v-model:双向数据绑定案例 -->	<!---->
<input type="text" v-model="txt"/>	<!-- 修改该输入框的值会将data中text属性的值一并修改-->
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





#### created: 回调函数：在Vue对象创建时执行的函数

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





#### mounted:回调函数：当页面上所有内容加载完成后才调用

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

![image-20221013190936825](S:\woniu\TypoaPicture\image-20221013190936825.png)

###### 取消打勾：

![image-20221013191019609](S:\woniu\TypoaPicture\image-20221013191019609.png)

##### 2、将项目变成WEB项目：

![image-20221013191044092](S:\woniu\TypoaPicture\image-20221013191044092.png)



![image-20221013191104957](S:\woniu\TypoaPicture\image-20221013191104957.png)

##### 3、在tomcat里添加Artifact，发布成一个目录：

![image-20221013191128468](S:\woniu\TypoaPicture\image-20221013191128468.png)

![image-20221013191157107](S:\woniu\TypoaPicture\image-20221013191157107.png)

##### 取逻辑名：

![image-20221013191354319](S:\woniu\TypoaPicture\image-20221013191354319.png)

##### 删除jsp：

![image-20221013192359076](S:\woniu\TypoaPicture\image-20221013192359076.png)

##### 将前端页面拖进web文件夹后即可在Tomcat服务器(浏览器)中访问：

![image-20221013192645389](S:\woniu\TypoaPicture\image-20221013192645389.png)



#### 设置为主页面：

##### 访问主页需要输入很长一段：

![image-20221013194630800](S:\woniu\TypoaPicture\image-20221013194630800.png)

##### 可以将一个页面设置为主页面，只输入根目录(逻辑名)就能直接访问(ip:8080/cloudStudy/)：

```xml
<welcome-file-list>
	<welcome-file>jumpPage.html</welcome-file>
    <!--绝对路径，此代码表示将根目录(web)下的jumpPage设置为访问根目录展示的页面-->
</welcome-file-list>
```

![image-20221015233457686](S:\woniu\TypoaPicture\image-20221015233457686.png)

##### 但是这样访问没有CSS、js等修饰：

##### ![image-20221013194909013](S:\woniu\TypoaPicture\image-20221013194909013.png)

##### 解决这个问题使用js代码实现：

#### window.location.href：在当前页面打开指定路径的页面(设置一个伪跳转)

```js
window.location.href = "login/test.html";
```

![image-20221015234656254](S:\woniu\TypoaPicture\image-20221015234656254.png)

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

![image-20221014002941733](S:\woniu\TypoaPicture\image-20221014002941733.png)

##### 2、勾选maven：

######                                 ![image-20221014003047449](S:\woniu\TypoaPicture\image-20221014003047449.png) 

##### 3、自动生成pom.xml：

###### 								![image-20221014003310382](S:\woniu\TypoaPicture\image-20221014003310382.png)

##### 4、添加依赖：

![image-20221014003804671](S:\woniu\TypoaPicture\image-20221014003804671.png)

```xml
<dependencies>
	<dependency>
		<!--...直接在下载网站拷贝-->
	</dependency>
</dependencies>	<!--首次下载，标签里面的会显示红色，表示还未下载到本地-->
```

##### 5、下载到本地：

> 可以选择阿里云服务器的JARmaven路径，下载速度快；

写完XML右上角会有一个![image-20221014004129289](S:\woniu\TypoaPicture\image-20221014004129289.png)图标，点击即开始下载。



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















## SpringMVC：替代Servlet

> 配置springmvc-config.xml、web.xml文件参考框架文档

### 使用：

#### 注解：

##### @Component：是spring中的一个注解，它的作用就是实现bean的注入。

##### 在Java的web开发中，提供3个@Component注解衍生注解（功能与@component一样）分别是：

###### 1、@Controller 控制器（注入controller） 用于标注控制层，管理页面及数据转发。

###### 2、@Service 服务（注入service） 用于标注服务层，主要用来进行业务的逻辑处理

###### 3、@Repository（实现dao访问） 用于标注数据访问层，也可以说用于标注数据访问组件，即DAO组件

而@Component泛指各种组件，就是说当我们的类不属于各种归类的时候（不属于@Controller、@Services等的时候），我们就可以使用@Component来标注这个类。



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
    mv.setViewName("/home.html");   // 写视图的路径即可
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



###### axios请求可以直接写对象

```json
// 定义一个对象
var obj = {"name":"刘备","age":13}
axios.post("映射地址",对象(obj)).then(res => {
    console.log()
})
```







### @ResponseBody(resp)：将返回的数据转换为JSON对象

> 配合Jackson(annotations,core,databind三个jar包)，会将该方法各种返回值：对象、List集合、Map集合转换为JSON格式的字符串返回给前端

#### 配置springmvc-config.xml标签< mvc:annotation-driven >标签内的数据

```xml
<mvc:annotation-driven>
	<mvc:message-converters>
	<bean class="org.springframework.http.converter.StringHttpMessageConverter"></bean>
	<bean 	class="org.springframework.http.converter.json.MappingJackson2HttpMessageConverter">		</bean>
    </mvc:message-converters>
</mvc:annotation-driven>
```

这个注解设置在方法头部，被设置的方法返回值不会转发或重定向，会直接输出





#### @RestController = @Controller + @ResponseBody 

所以类上加了@RestController，该类所有方法进行跳转都会失败(ResponseBody把返回格式化成JSON字符串了)









### 全局异常处理：

##### @ControllerAdvice：声明当前类是一个异常处理类

##### @RestControllerAdvice = @ControllerAdvice + @ResponseBody 

##### @ExceptionHandler(Exception.class) ：处理具体异常类型



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







### SpringMVC拦截器

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
        <!--/** :表示拦截所有controller接口-->
        <mvc:mapping path="/**"/>
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



> 





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





### IOC容器获取Dao层对象：

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





### 事务：

##### 导包：

##### 使用Spring自带的事务管理，在SpringMVC-config中配置事务管理器对象，注入数据源：

```xml
<bean id="自定义id transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
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













