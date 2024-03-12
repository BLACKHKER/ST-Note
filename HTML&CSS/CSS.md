## CSS：层叠样式表

> 优先级：就近原则，行内 > 内联 > 外联

### 引用方式：

##### 行内样式：

```html
<!--属性之间分号间隔-->
<标签名 style="属性1：属性值1；属性2：属性值2;">内容</标签名>
```



##### 内联样式：直接在HTML文件头编写CSS

```html
<!--HTMLhead标签中加入style标签，在style标签中编写CSS样式-->
<!--属性之间逗号间隔-->
<style>
    选择器 {
      属性1: 属性值1,
      属性2: 属性值2
    }
</style>
```



##### 外联样式：单独将CSS写成独立文件，内部直接引用.css文件

```html
<head>
    <!--引入地址、文件类型、和网页的关系(样式表)-->
    <!--除了地址其余都是固定格式-->
	<link href="/day01/css/style.css" type="text/css" rel="stylesheet"/>
</head>
```



### 选择器：优先级从高到底：id选择器>类选择器>标签选择器

> 选择器分为两种：基本选择器和复合选择器

#### 基本选择器

##### id选择器：

```css
#id名 {
	color: green;
}
```



##### 类选择器：

```css
.类名 {
	color: yellow;
}
```



##### 标签选择器：

```css
标签名 {
	color: red;
}
```



#### 复合选择器

##### 后代选择器(选择器1 选择器2 3 ...)：

```html
<!--选中所有被div包含的p元素(不止一层,支持多级嵌套)-->
<!--也可以是id选择器、类选择器等-->
<style>
    div p {
        color: red;
    }
</style>
<!--P1，div下有span，span下有p，也包含在内-->
<body>
  <div>
    <span>
      <p>P1</p>
    </span>
  </div>
  <p>P2</p>
</body>
```



##### 交集选择器(选择器之间无空格)：

```html
<!--只有两种形式(并且的关系，同时满足才选中)-->
<!--标签名.类名-->
<!--标签名#id名-->
<!--选中类名为red的所有div标签-->
<head>
  <style>
    div.red {
      color: red;
    }
  </style>
</head>

<body>
  <div class="red">divTest</div>
  <p class="red">pTest</p>
</body>
```



##### 并集选择器(选择器1,选择器2,3,...)：

> 给不同的标签元素使用相同的样式，解决代码冗余

```html
<!--给所有p标签、div标签里的span标签设置红色-->
<head>
  <style>
    p,div span{
      color: red;
    }
  </style>
</head>
<!--spanTest、pTest显示红色divTest不显示红色-->
<body>
  <div>
    <span>spanTest</span>
    divTest
  </div>
  <p>pTest</p>
</body>
```



##### 选择器相加 (选择器1+选择器2)：

```html
<!--选择类为class的下面的第一个p标签-->
<style>
    .show+p {	
        background:green;
    }
</style>
<div class="show"></div>
<p>我是什么颜色？</p>
```



##### 选择器相引(选择器1~选择器1)：

```html
<!--选择类为class的下面的所有p标签-->
.show~p{	
	background:green;
}
<div class="show"></div>
<p>我是什么颜色？</p>
<p>我是什么颜色？</p>
```







### 样式属性： 

#### font：字体

##### font-size：字体大小

```

```



##### font-family：字体家族(类型)

```

```



##### 复合属性(无属性名)：

```html
<!--属性值之间用空格分隔-->
<style>
	font:italic bold 30px 宋体;
</style>
```





#### color：颜色

##### rgb(数值1,数值2,数值3)

```html
<!--黄色-->
<style>
	div {
      color: rgb(255, 255, 0);
    }
</style>
```

> 数值为三原色(红,绿,蓝)的值，数值最小为0，最大为255



##### 十六进制数

```html
<!--红色-->
<style>
    div {
      color: #FF0000;
    }
</style>
<!--在相邻的两位都相同时可以简写-->
<style>
    div {
      color: #F00;
    }
</style>
```





#### text-align：文本方向

> 只在块级元素中生效(div)，行级元素(a)若没有父级块元素则不生效

##### center：居中

```html
<head>
  <style>
    div {
      text-align: center;
    }
  </style>
</head>

<body>
  <div>123</div>
</body>
```



##### left：左对齐

```css
text-align: left;
```



##### right：右对齐

```css
text-align: right;
```



#### text-decoration：下划线

```html
<!--取消/添加a标签下划线-->
<style>
    text-decoration: none;
    text-decoration: underline;
</style>;
```





#### background：背景样式

##### background-color：背景颜色

> 如果有图片，会覆盖背景颜色

```html
<style>
    div {
        background-color: blue;
    }
</style>
```



##### background-image：背景图片

> 如果有图片，会覆盖背景颜色

```html
<!--当图片小于容器时(例如div)默认平铺从左到右，从上到下，可以不平铺(background-repeat)-->
<head>
    <style>
        div {
            background-image: url(地址);
            background-image: url(/day01/images/img1.jpg);
        }
    </style>
</head>

<body>
  <div></div>
</body>
```

###### 两种方式引入背景图片：img标签、div引入样式，使用background属性

```html
<head>
    <style>
        div {
            background-image: url(/day01/images/地址);
        }
    </style>
</head>

<body>
    <img src="/day01/images/地址"/>
    <div></div>
</body>
```



##### background-repeat：图片是否平铺

```html
<!--no-repeat不平铺-->
<!--repeat-x只在x轴平铺-->
<!--repeat-y只在y轴平铺-->
<style>
    div {
        background-image: url(/day01/images/img1.jpg);
        background-repeat:no-repeat;
        background-repeat:repeat-x;
    }
</style>
```



##### background-position：图片定位

> 在数学中是以左下角为轴心延申xy轴，在程序中是以左上角为轴心延申x轴y轴

```html
<!--向x轴(右)移动100像素，y轴(下)不变-->
<!--向x轴(右)移动百分之xxx(相对于父容器)，y轴(下)不变-->
<style>
    div {
        background-position:x轴位置(像素/百分比) y轴位置(像素/百分比);
        background-position:100px 0px;
    }
</style>
```

###### 可以是负数：

```css
<!--左移100px，图片会显示不全-->
background-position:-100px 0px;
```

###### 可以是方向：left、right、center、top、bottom

> 只规定一个关键词，第二个默认center

```css
<!--右上角-->
background-position:right top;
```



##### background：简写

```html
<style>
    div {
        background: color image repeat position ;
    }
</style>
```





#### 伪类：鼠标活动(标签名:活动状态)

> 一个特定的动作行为和一个标签配合使用，最常见的是和超链接标签<a>
>
> 伪类必须按序编写:link — :visited — :hover — :active

##### :link：未点击状态

```css
/*给a标签绑定状态，未点击时颜色为黑色*/
a:link {
	color: black;
}
```



##### :visited：点击后状态

```css
/*给a标签绑定状态，点击后颜色为紫色*/
a:link {
	color: slateblue;
}
```



##### :hover：指针悬停在上方时状态

```css
/*给a标签绑定状态，鼠标指针悬停在上方时颜色为红色*/
a:link {
	color: red;
}
```



##### :active：点击但鼠标未松开

```css
/*给a标签绑定状态，点击时颜色为天蓝色*/
a:link {
	color: aqua;
}
```





#### 盒子模型：

> 每个内容标签都是一个盒子，只要是盒子就有边框：border属性
>
> 边框border和标签里面的内容之间的距离就是内边距，两个盒子标签的border之间的距离就是外边距
>
> padding：内边距	margin：外边距，内容外有一个隐藏的border(边框)。

##### border：边框

```html
<!--设置内容标签(div)边框宽度、颜色、实心/虚线,以及简写(宽度、实心/虚线、颜色)-->
<style>
    div {
        border-width:1px;
        border-color:red;
        border-style:solid;
        border:1px,solid,black;
    }
</style>
```

###### div外面有body，body外面有html，它们也是盒子，那么跟div一样也可以设置border属性：

```html
<html>
<head>
  <style>
    div {
      border: 1px solid blue;
    }

    body {
      border: 1px solid black;
    }

    html {
      border: 1px solid red;
    }
  </style>
</head>

<body>
  <div>div</div>
</body>

</html>
```



##### margin：外边距——两个盒子之间的距离

```html
<head>
  <style>
    div {
      border: 1px solid blue;
    }

    p {
      border: 1px solid red;
    }
  </style>
</head>

<body>
  <!--div是没有外边距的，所以两个盒子会贴合-->
  <div>div1</div>
  <div>div2</div>
  <!--p是有外边距的，所以两个盒子中间会有空隙(边距)-->
  <p>p1</p>
  <p>p2</p>
</body>
```

###### 让p标签实现div的无外边距效果:

```html
<style>
    p {
        border: 1px solid red;
        margin: 0px;
    }
</style>
```

###### 同理，给div加上外边距实现p标签效果：

```html
<!--一个参数：上下左右外边距都为10px-->
<style>
    div {
        border: 1px solid red;
        margin: 10px;
    }
</style>
```

###### margin塌陷：设置垂直方向的margin：margin-top、margin-bottom时，不会叠加计算，水平方向的则可以

```html
<!-- 两个div之间上下的距离不是20px，而是10px -->
<head>
  <style>
    div {
      border: 1px solid blue;
      margin-top: 10px;
      margin-bottom: 10px;
    }
  </style>
</head>

<body>
  <div>div1</div>
  <div>div2</div>
</body>
```



##### padding：内边距——盒子(标签)中的被包裹的内容，距离边框(border)的距离

```html
<head>
  <style>
    div {
      border: 1px solid blue;
      padding: 10px;
    }

    span {
      border: 1px solid red;
    }
  </style>
</head>

<body>
  <div>
    <span>div1</span>
  </div>
</body>
```



##### 两个参数时分别表示上下、左右：

###### 上下内边距为0px,左右内边距为10px

```css
margin:0 10px;
```



##### 四个参数时分别表示上、右、下、左(顺时针)：

###### 上右下外边距为0，左外边距为10px

```css
padding:0,0,0,10px;
```



##### 取消所有标签的内外边距：

```html
<style>
    * {
        margin: 0px;
        padding: 0px;
    }
</style>
```



##### float：浮动——修改标签的默认排版

###### 实例：修改ul列表中里的垂直排列为水平排列

```html
<head>
  <style>
    ul {
      list-style-type: none;
    }

    ul li {
      border: 1px solid black;
      float: left;
      margin-left: 10px;
    }
  </style>
</head>

<body>
  <ul>
    <li>aaa</li>
    <li>bbb</li>
    <li>ccc</li>
  </ul>
</body>
```

> a标签默认排序从左到右(行级)，div默认排序从上到下(块级元素独占一行)，这种默认布局，称为标准流布局

###### 浮动后的元素，不再拥有独立的空间，后一个元素会自动覆盖浮动元素的空间：

```html
<!-- 示例：div1浮动后，div2会到左上角 -->
<head>
  <style>
    #div1 {
      width: 100px;
      height: 100px;
      border: 1px solid red;
      float: left;
    }

    #div2 {
      width: 200px;
      height: 200px;
      border: 1px solid blue;
      
    }

    #div3 {
      width: 300px;
      height: 300px;
      border: 1px solid green;
      
    }
  </style>
</head>

<body>
  <div id="div1">div1</div>
  <div id="div2">div2</div>
  <div id="div3">div3</div>
</body>
```

###### 效果：

![float](https://s2.loli.net/2023/02/11/cnAPtIXV75h4ylG.jpg)

##### clear：清除其上方元素left/right浮动时，对该元素的影响(设置该元素不覆盖上一个浮动元素的空间)

###### 三个属性：left、right、both，代表不占用使用left/right浮动元素的空间，和都不占用

```html
<style>
    #div1 {
        width: 100px;
        height: 100px;
        border: 1px solid red;
        float: left;
    }

    #div2 {
        width: 200px;
        height: 200px;
        border: 1px solid blue;
        float: right;
    }

    #div3 {
        width: 300px;
        height: 300px;
        border: 1px solid green;
		clear: both;
    }
</style>
```

###### 效果：

![屏幕截图 2023-01-26 170402](https://s2.loli.net/2023/02/11/BmD7cQnMUg3oa1p.jpg)



#### position：定位

> float和positon的区别在于float后的元素没有自己的占位(二维)，而position则是保留占位移动盒子(三维层)

> 四个方向上下左右分别为：top，bottom，left，right

##### static(默认)：静态定位，标准流的位置

```html
<!-- 无法加四个属性,强行加不修改盒子位置 -->
```



##### relative：相对定位——相对标准流的位置发生偏移

###### 将div2盒子向下(Y轴)走50px，向右(X轴)走100px

```html
<style>
    #div1 {
        width: 100px;
        height: 100px;
        background: red;
    }

    #div2 {
        width: 200px;
        height: 200px;
        background: blue;
        position: relative;
        top: 50px;
        left: 100px;
    }

    #div3 {
        width: 300px;
        height: 300px;
        background: green;
    }
</style>
```

![屏幕截图 2023-01-26 181922](https://s2.loli.net/2023/02/11/6KPmHDcEwQ51yk7.jpg)



##### absolute：绝对定位——相对父级元素发生偏移

> 如果父级元素没有定位属性(position)，就会根据父级的父级进行定位，没有父级则相对浏览器(HTML盒子)

```html
<!-- 做绝对定位让父级先有一个相对定位，父级元素的position:relative -->
```



##### fixed：固定定位——相对浏览器(HTML)页面进行定位

```html
<!-- 位置不变，永远在一个位置(相对游览器) -->
<style>
    #div1 {
        width: 100px;
        height: 100px;
        background: red;
        position: fixed;
        top: 50px;
        left: 50px;
    }
</style>
```

