## Python Base

### 一、基础知识

#### 1.1 TODO





#### 1.2 标识符

##### 1.2.1 命名规则

1. 只允许数字、英文、下划线、中文[^1]；
2. 数字不可以开头；
3. 区分大小写
4. 不可以使用关键字[^2]





#### 1.3 注释

##### 1.3.1 单行注释

> `#`号

```python
# 注释内容
...
```



##### 1.3.2 多行注释

> 三个双引号`"""`

```python
""" 
多行注释
"""
```



##### 1.3.3 方法注释

> 快捷输入：在方法内部第一行打三个双引号回车

```python
def funcTest()
	"""回车"""
	TODO...
```





#### 1.4 运算符

加、减、乘、除、整除、取余、指数幂(开方)、赋值运算符、复合运算符

```python
+、-、*、/、//、%、**、=、+=、-=、*=、/=、%=、**=、//=
```

##### 1.4.1 除的类型转换

Python中除不尽，会自动转换类型，不想转换类型就需要用`//`(整除)

```python
a = 10
b = 3
c = a / b
print(c, type(c))
# 打印：3.3333333333333335 <class 'float'>
```

```python
a = 10
b = 3
c = a // b
print(c, type(c))
# 打印：3 <class 'int'>
```



##### 1.4.2 指数幂

```python
a = 10
b = 2
c = a ** b
print(c, type(c))
# 打印：100 <class 'int'>
```





#### 1.5 模块

类似于C的include导入的头文件，是用于组织和管理代码的一种方式。

一个模块是一个包含Python代码的文件，它可以包含变量、函数、类和其他可执行代码。

模块的主要目的是将相关的代码组织在一起，以便在需要时进行导入和重用。

##### 1.5.1 导入格式

```python
[from 模块名] import [模块 | 类 | 变量 | 函数 | *] [as 别名]
```



##### 1.5.2 常用组合形式

```python
import 模块名
from 模块名 import 类、变量、方法
from 模块名 import *
import 模块名 as 别名
from 模块名 import 功能名 as 别名
```



##### 1.5.3 基本使用

```python
# 导入time模块(模块)
import time
time.sleep(5)

# 使用*导入time模块的全部功能
from time import *
# 注意这里可以直接使用sleep方法
sleep(5)

# as加别名(模块)
import time as t
t.sleep(5)

# as加别名(方法\函数)
from time import sleep as t
t(5)
```



##### 1.5.4 自定义模块

> 可以直接访问方法，而无需通过类的实例

```python
from 类名 import 方法名
```

**注意**

1.导入外部包的时候，运行会把导入的外部模块中的方法也运行了，解决方案`__main__`[^5]

```python
# MyTestPackage
def test(a, b)
	print(a + b)
test(1, 2)

# MyRunPackage
# 导入外部包
from MyTestPackage import test
# 没有其他代码...运行MyRunPackage会输出(3)，也就是外部模块MyTestPackage的test方法被调用了
```

2.导入不同模块的同名方法，优先以最后导入的模块方法为准

```python
from package import test
from package2 import test
# 调用package2的test()方法
test()
```



##### 1.5.5 __ main __

> 解决导入包自动运行的问题，(类似)是Java的作用域private

```python
# 打main自动提示
if _ _name_ _ == "_ _main_ _":
	方法名
```

**实例**

```python
def test(a, b)
	print(a + b)
if _ _name_ _ == "_ _main_ _":
	test(1, 2)
```



##### 1.5.6 __ all __

> 限制外部模块使用`*`导入该模块后可以访问的方法，只限制`*`号，手动导入可以正常导入

```python
# 限制外部包只能使用testA方法
_ _ all _ _ = ["testA"]

def testA():
	print("testA")
	
def testB():
	print("testB")
```





#### 1.6 包

> 类似Java的maven package，打包成Jar文件，就可以从依赖中引入Jar

##### 1.6.1 概念

包由模块和__ init __.py组成，有就是包，没有就是文件夹



##### 1.6.2 导入包

```python
import 包名.模块名
```



##### 1.6.3 导入第三方包

> PIP：Python安装内置的程序，负责安装第三方包

###### CMD导入

```shell
pip install 包名称
```

![image-20230828134035628](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230828134035628.png)**网络优化**

> pip因为是连接的国外的网站，有的时候速度会很慢，可以通过如下命令配置镜像站(清华大学提供)

```shell
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple 包名
```

###### Pycharm导入

1. 右下角Interpreter Settings

![image-20230828134859892](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230828134859892.png)

2. 显示导入的第三方包

![image-20230828135258219](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230828135258219.png)

3. 安装

![image-20230828135648889](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230828135648889.png)

4. 搜索安装

![image-20230828140241042](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230828140241042.png)



##### 1.6.4 使用

```python
包名.模块名.目标
```



##### 1.6.5 创建包

右键 → New → Python Package

![image-20230828130853417](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230828130853417.png)



##### 1.6.6 __ init __.py

> 配置模块的访问权限：main/all

![image-20230828132701630](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230828132701630.png)







#### 1.N 控制台输入/输出

##### 1.N.1 输出

```python
# 打印单个，直接打印
print("123")

# 打印多个，用逗号分隔
num = 50
str = "String"
f = 1.23
print(num,str,f)
```



##### 1.N.2 输入

> 就是从键盘接收，Java中的type x = new Scanner(System.in).next(); 
>
> 但是Python中从键盘接收的值，<font color="#f40">永远是String类型</font>

```python
变量名 = input()
```

**实例**

```python
# 从键盘接收数据
# 提前print打印提示语
print("你的名字是？")
name = input();
print(f"好的，{name}")

# 将提示语放到input方法中，作为参数，区别是没有换行
name = input("你的名字是？\n");
print(f"好的，{name}")
```

```python
user_name = input("请输入用户名: \n")
user_type = input("请输入账号身份: \n")
print(f"您好:{user_name},您是尊贵的{user_type}")

# 数据格式化处理
birth_year = input("Birth Year:")
age = 2024 - int(birth_year)
print(age)
```



---



### 二、数据类型

> 在Python中，变量的类型是根据赋给它的值来确定的，而不是在声明变量时进行定义。

#### 2.1 数字(Number)

##### 2.1.1 整数(int)

正、负整数，1、-1



##### 2.1.2 浮点数(float)

带小数点的数，3.14



##### 2.1.3 复数(complex)

1+2j，以j结尾表示负数



##### 2.1.4 数字精度控制

假如使用m.n控制数据的宽度和精度

m：控制宽度，要求是数字(很少使用)，设置的宽度小于数字自身则不生效，小数点和小数部分也参与宽度计算

n：控制小数点精度，要求是数字，会进行小数的四舍五入

**实例**

%5d：表示将宽度控制在五位，不足用空格补齐。

比如541，设置为5d：[空格] [空格] 541，用空格补齐宽度

%7.2f：表示将宽度控制为七位，将小数点精度控制为2，同样空格补齐宽度

比如54.156，设置%7.2f：[空格] [空格]  54.16，总长度7位，保留小数点后两位，第三位四舍五入，变成54.16

%.2f：表示不限制宽度，保留小数点后两位

```python
# 输出：修改精度后的值为：  54.16(包含两个空格)
num1 = 54.155
print("修改精度后的值为：%7.2f" %num1)
```





#### 2.2 字符串(String)

> 字符组成，单个字符也是字符串，没有char字符类型
>

##### 2.2.1 定义

> 三引号定义和多行注释的写法一样，使用变量接收它，它就是字符串，不接收就是注释

```python
# 单引号、双引号、三引号
str1 = 'String1'
str2 = "String2"
str3 = """String3"""
```



##### 2.2.2 字符串拼接

> 同Java，使用+号拼接，拼接的内容必须是String类型

```python
str1 = "Te"
str2 = "st"
print(str1 + str2 + "!")
```



##### 2.2.3 格式化

###### 占位符

> 跟C语言一样通过 %占位符占位，后面的字母代表不同的意思

```python
# 单占位符
name = "刘"
name2 = "君主刘备姓%s" %name
print(name2)

# 多占位符
name = "刘备"
name2 = "刘"
name2 = "君主 %s 姓 %s" % (name, name2)
print(name2)
```

| 占位符 | 含义                                     |
| ------ | ---------------------------------------- |
| %s     | 表示将变量变成字符串放入占位的地方       |
| %d     | 表示十进制整数类型的占位符               |
| %f     | 表示浮点数类型的占位符                   |
| %c     | 表示单个字符类型的占位符                 |
| %o     | 表示八进制整数类型的占位符               |
| %x     | 表示十六进制整数类型（小写字母）的占位符 |
| %X     | 表示十六进制整数类型（大写字母）的占位符 |
| %%     | 表示百分号字符 % 自身的占位符            |

###### format

> 没法配置精度

```python
name = "Alice"
age = 25
message = "My name is {} and I am {} years old.".format(name, age)
print(message)
```

###### f-strings

> 没法配置精度

```python
name = "Alice"
age = 25
# 在字符串前面添加一个标记f，参数通过{}花括号配合变量名处理
message = f"My name is {name} and I am {age} years old."
print(message)
```

###### 表达式

```python
str1 = "String"
print("1 * 1的结果是：%d" % (1 * 1))
print(f"1 * 1的结果是：{1 * 1}")
print(f"变量str的类型是：{type(str1)}")
```

**实例**

> 数字精度控制配合字符串格式化

```python
# 公司名
company = "蜀国"
# 当前股价
stock_price = 5.41
# 股票代码
stock_code = 521
# 股票每日增长系数
stock_price_daily_growth_factor = 1.3
# 增长天数
gorwth_days = 7
print(f"公司：{company},股票代码：{stock_code},当前股价：{stock_price}")
print("每日增长系数：%f，经过%d的增长后，股价达到了:%4.2f" % (
stock_price_daily_growth_factor, gorwth_days, 5.41 ** stock_price_daily_growth_factor))
```



##### 2.2.4 大小比较

字符串是根据ASCII码按位比较大小：ASCII值越大越大，小写大于大写

例如，azz : baa，baa大，先比较字符串的第一个字符，如果相等，比较第二个，以此类推

![ASCII Table](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/asciifull.gif)



##### 2.4.5 表达式

字符串可以和运算符组合成表达式：

```python
# 生成十个*号打印
print("*" * 10)
# 生成十个1打印
print("1" * 10)
```



#### 2.3 布尔(bool)

注意Python中的布尔是大写，true是不被识别的



```python
True
False
```





#### 2.4 空值(NoneType)

```python
n = None
print(n)
print(type(n))
```





#### 2.5 格式化

> 格式化后的数据类型(被格式化的数据)

**实例**

```python
now_year = "2024"
born_year = 1999
age = int(now_year) - born_year
print(age)
```



---



### 三、数据容器

> 所有容器对应API(增删改查)参阅`Python API.md`

#### 3.1 列表(List)

> <font color="#f40">有序</font>、<font color="#f40">可重复</font>、<font color="#f40">可变</font>的数据结构，用方括号`[]`表示。它可以包含<font color="#f40">任意类型</font>的元素，并且允许元素重复。列表可以通过索引访问、添加、删除和修改元素。列表常用于存储和处理多个相关的元素。
>
> 最接近数组的类型，区别是列表可以存储不同类型的元素，并且可以动态调整大小，不需要事先指定长度。

##### 3.1.1 定义

###### 普通列表

```python
# 空列表
[]

# 空列表
myList = []

# 可以在创建列表时初始化元素：list(range(1,5)) --- [1,2,3,4]
myList = list()
myList = [1, 2, 3, 4, 5]
```

###### 嵌套列表

> 类似于二维数组(矩阵)

```python
myList = [[1, 2, 3], [4, 5, 6]]
```



##### 3.1.2 索引

> 索引从0开始，注意下标越界异常(index outbound Exception)

```python
myList = [1, 2, 3, 4, 5]
# 打印1
print(myList[0])
```

###### 反向索引

> 从-1开始，就是-1为0号元素，依次类推-2、-3...，可以理解为倒排索引(从后往前取值)

```python
myList = [1, 2, 3, 4, 5]
# 打印5
print(myList[-1])
```

###### 矩阵索引

> 两个索引值

```python
myList2 = [[1, 2, 3], [4, 5, 6]]
print(myList2[0][1])
```



##### 3.1.3 遍历

###### while

```python
index = 0
myList = [1, 2, 3, 4, 5]
while index < len(myList):
    print(myList[index])
    index += 1
```

###### for

```python
index = 0
myList = [1, 2, 3, 4, 5]
for i in myList:
    print(i)
```





#### 3.2 元组(Tuple)

> <font color="#f40">有序</font>、<font color="#f40">可重复</font>、<font color="#f40">不可变</font>的数据结构，用圆括号`()`表示。类似于列表，可以包含<font color="#f40">任意类型</font>的元素，但一旦创建，就不能修改。元组常用于存储不可变的数据，如坐标、日期等。
>
> 只读的List列表，一旦创建不支持增删改。

##### 3.2.1 定义

###### 普通元组

> 注意：只有一个数据的时候，这个数据的后面要添逗号

```python
# 空元组
(元素1, 元素2, 元素3)
my_tuple = (元素1, 元素2, 元素3)

# 创建元组(初始化)的两种方式
my_tuple = ()
my_tuple = tuple()
```

###### 嵌套元组

```python
my_tuple = ( (1, 2, 3), (4, 5, 6) )
# 打印1
print(my_tuple[0] [0])
```



##### 3.2.2 索引

> 索引从0开始，注意下标越界异常(index outbound Exception)

```python
my_tuple = (1, 2, 3, 4, 5)
# 打印1
print(my_tuple[0])
```

###### 反向索引

> 从-1开始，就是-1为0号元素，依次类推-2、-3...，可以理解为倒排索引(从后往前取值)

```python
my_tuple = (1, 2, 3, 4, 5)
# 打印5
print(my_tuple[-1])
```

###### 矩阵索引

> 两个索引值

```python
my_tuple = ( (1, 2, 3), (4, 5, 6))
print(my_tuple[0][1])
```



##### 3.2.3 遍历

###### while

```python
index = 0
myArray = (1, 2, 3, 4, 5)
while index < len(myArray):
    print(myArray[index])
    index += 1
```

###### for

```python
index = 0
myArray = (1, 2, 3, 4, 5)
for i in myArray:
    print(i)
```





#### 3.3 集合(Set)

> <font color="#f40">无序</font>、<font color="#f40">不可重复</font>、<font color="#f40">可变</font>的数据结构，用花括号 `{}` 表示。集合中的元素是<font color="#f40">唯一</font>的，不允许重复。集合提供了快速的成员检查和数学集合操作，如交集、并集、差集等。
>
> 通过哈希表实现的，其元素没有固定的顺序，不支持索引。
>
> 集合中的元素不可以是list列表，因为集合是存储不重复的元素容器；可以存储元组(tuple)。

##### 3.3.1 定义

```python
my_set = {1, 2, 3, 4, 5}
# 使用set()函数时，参数为可迭代对象，这里给的是数组
my_set = set([1,2,3,4,5])
```



##### 3.3.2 遍历

> 集合不支持下标索引，不能用while循环

```python
for i in 集合名
print(i)
```





#### 3.4 字典(Dictionary)

> <font color="#f40">无序</font>、<font color="#f40">Key唯一</font>、<font color="#f40">可变的键值对</font>数据结构，用花括号 `{}` 表示。字典中的元素由键（key）和对应的值（value）组成，键必须是唯一的。字典常用于存储和检索具有关联关系的数据。
>
> 重复key，保存最后一个key的值。

```python
my_dict = {'name': 'Alice', 'age': 25, 'city': 'New York'}
```

##### 3.4.1 定义

###### 普通字典

```python
# 定义空字典
dic = {}
dic = dict()
dic = {"key1": value2, "key2": value2}
```

###### 嵌套字典

```python
# 定义字典中，字典的value是一个新的字典
dic = {
	"key1": {
		"key1a": key1avalue,
		"key1b": key1bvalue,
		"key1c": key1cvalue,
	},
	"key2": {
		"key2a": key2avalue,
		"key2b": key2bvalue,
		"key2c": key2cvalue,
	}
}
# 取值就是：dic[key1] [key1a]
```



##### 3.4.2 遍历

```python
myDic = {"1": 10, "2": 20, "3": 30}
# 根据key遍历
keys = myDic.keys()
for key in keys:
	print(myDic[key])


# 根据字典遍历
for key in myDic
	print(myDic[key])
```



#### 3.5 序列(Sequence)

> 序列是指：<font color="#f40">内容连续</font>、<font color="#f40">有序</font>且可以<font color="#f40">用下标访问</font>的数据容器，列表(List)、元组(Tuple)、字符串(String)

##### 3.5.1 切片

> 从一个序列中取出一个子序列

**实例**

```python
"""
	从序列中，从指定位置开始，依次取出元素，到指定位置结束，得到一个新序列
	起始下标表示从何处开始，可以留空，留空视作从头开始
	结束下标表示何处结束，可以留空，留空视作截取到结尾，不包含当前
"""
# 步长表示依次取元素的间隔：
# 1表示一个个取元素(默认是1)，2表示每次跳过一个取，N表示每次跳过N-1个取，
# 步长为负数，表示反向取(注意起始下标和结束也要反向)
序列[起始下标:结束下标:步长]
```





#### 3.6 JSON(非内置容器)

##### 3.6.1 概念

json是键值对结构，常用于前后端数据的传输



##### 3.6.2 处理 

###### 列表嵌套字典转JSON

```python
import json

data = [{"name": "张大山", "age": 11}, {"name": "王大锤", "age": 13}, {"name": "赵小虎", "age": 16}]
# 将数据转换为JSON字符串，配置ensure_ascii不使用ASCII码转换中文
jsonStr = json.dumps(data, ensure_ascii=False)
# String类型
print(type(jsonStr))
print(jsonStr)
```

###### 字典转JSON

```python
import json

dic = {"name": "周杰伦", "addr": "台北"}
jsonStr = json.dumps(dic, ensure_ascii=False)
print(type(jsonStr))
print(jsonStr)
```

###### JSON字符串转List

```python
import json

jsonStr = [{"name": "张大山", "age": 11}, {"name": "王大锤", "age": 13}, {"name": "赵小虎", "age": 16}]
listA = list([{"name": "张大山", "age": 11}, {"name": "王大锤", "age": 13}, {"name": "赵小虎", "age": 16}])
print(type(listA))
print(listA)
```

###### JSON字符串转字典

```python
import json

jsonStr = {"name": "周杰伦", "addr": "台北"}
dictA = dict([{"name": "张大山", "age": 11}, {"name": "王大锤", "age": 13}, {"name": "赵小虎", "age": 16}])
print(type(dictA))
print(dictA)
```



---



### 四、流程控制

#### 4.1 分支

##### 4.1.1 if...

```python
if 条件:
    # 四个空格/tab
	条件成立TODO
```

**实例**

```python
age = 24
if age < 25:
    print("Success!")
```



##### 4.1.2 if...in...

> 判断元素x是否在y里，是返回True，否返回False

```
if x in y:
	条件成立 TODO
```



##### 4.1.3 if...else...

```python
if 条件:
    # 四个空格/tab
	条件成立 TODO
else:
    条件不成立 TODO
```

**实例**

```python
# if-else
age = 24
if age < 25:
    print("Success!")
else:
    print("Error!")
```



##### 4.1.4 if...elif...

```python
if 条件:
    # 四个空格/tab
	条件成立 TODO
elif 条件2:
    条件2不成立 TODO
else:
	TODO
```

**实例**

```python
age = 25
if age < 25:
    print("lt!")
elif age > 25:
    print("gt!")
else:
    print("True!")
```



##### 4.1.5 if嵌套

```python
if 条件:
    print("xxx")
	if 条件:
		条件成立 TODO
	elif 条件2:
    	条件2不成立 TODO
	else:
		TODO
elif 条件2:
    条件2不成立 TODO
else:
	TODO
```





#### 4.2 循环

##### 4.2.1 for

```python
for 临时变量 in 数据集:
	循环体...
```

**实例**

```python
# 判断字符串中有几个a
num = 0
str = "panda is big animal"
for i in str:
    if (i == "a"):
        num += 1
print(f"该字符串中有{num}个a字符")

# 九九乘法表
for i in range(1, 10):
    for j in range(1, i + 1):
        # if j <= i:
            print(f"{j}*{i}={i * j}\t", end='')
    print()
```

**注意**

for循环的临时变量是可以被外部访问到的，是全局变量

```python
for i in range(10)
	print(i)
print(i)
# 打印0 - 9和9，9打印了两遍
```

符合规范：先定义一个同名的全局变量

```python
i = 0
for i in range(10)
	print(i)
print(i)
# 打印
```



##### 4.2.2 while

```python
while 条件:
	条件为True，执行...
...
```

**实例**

```python
age = 10
while age < 100:
    age += 1
print(age)
```



##### 4.2.3 循环中断

###### continue

> 跳出此次循环

```python
# continue
for i in range(1, 4):
    print(i)
    continue
    print("Success!")
# 打印123，没有Success！
```

###### break

> 跳出当前循环

```python
for i in range(1, 10):
    print(i)
    break
# 打印1,后面都不执行了
```



---



### 五、函数

> 函数可以直接用，如果在类中，跟Java一样，先创建实例，用实例调用方法

#### 5.1 定义

##### 5.1.1 函数结构

```python
def 函数名(参数):
	函数体
	return 返回值
```

**实例**

```python
# 函数Demo
def hello(text):
    print(text)
hello("Success！")
```





#### 5.2 传参方式

##### 5.2.1 位置参数

> 调用函数时根据函数定义的参数位置传递参数，传递的参数和方法的参数个数、参数顺序必须一致

```python
def testFunction(id, name, age)
	print(id + "-" name + "-" + age)
testFunction(1, "刘备", 18)
```



##### 5.2.2 关键字参数

> 传递参数的时候通过”键 = 值“的方式传递参数，不需要按顺序传递了

```python
def testFunction(id, name, age)
	print(id + "-" name + "-" + age)
testFunction(name = "刘备", age = 18, id = 1)
```

**注意**

函数调用时，如果有位置参数，位置参数必须在关键字参数的前面，且匹配参数顺序



##### 5.2.3 缺省参数(默认参数)

> 就是给方法的参数设定一个默认值，调用方法时可以不传该参数，如果传了，则覆盖默认参数

```
def testFunction(id, name = "刘备", age)
	print(id + "-" name + "-" + age)
testFunction(age = 18, id = 1)
```

**注意**

所有位置参数必须出现在默认参数前，包括函数定义和调用



##### 5.2.4 不定长参数

也叫可变参数，表示参数的个数不固定，适用于不确定要传多少个参数的场景

###### 位置传递

> 一个*号，所有的参数都会被args收集，args是一个元组(tuple)

```python
def testFunction(*args)
	print(args)
testFunction("刘备", 18, 1)
```

###### 关键字传递

> 两个*号，参数是"键=值"的形式，所有的键值对都会被kwargs收集，kwargs(keyword)是一个字典(dir)

```python
def testFunction(**kwargs)
	print(kwargs)
testFunction(name = "刘备", age = 18, id = 1)
```





#### 5.3 高阶函数

> 本质上是将一个函数作为参数传递给另一个函数
>
> 作用是传入计算逻辑，而非传入数据，逻辑固定参数不固定 → 逻辑不固定参数不固定

**实例**

```python
# 定义一个计算器函数
def compute(x, y):
	return x + y

# 新的函数调用需要一个计算器函数作为参数，函数内部使用了这个计算器函数
def function(compute):
	result = compute(1, 2)
	print(result)
```





#### 5.4 匿名函数(lambda)

> 函数定义中，def可以定义一个带有名称的函数，可以基于名称重复使用
>
> lambda关键字，可以定义匿名函数(无名称)，只可以使用一次
>
> <font color="#f40">写多行代码的情况，不可以使用lambda</font>，比如for、if、while这种

```python
# lambda是关键字，表示定义的是匿名函数
# 传入参数表示匿名函数的形式参数：x, y 表示接收两个形式参数
# 函数体，就是执行逻辑，注意只能写一行，无法写多行代码
lambda 传入参数: 函数体(一行代码)
```

**实例**

> 在使用函数作为参数传递的时候，避免了需要定义一个函数的复杂过程，类似于Java

```python
# 新的函数调用需要一个计算器函数作为参数，函数内部使用了这个计算器函数
def function(compute):
	result = compute(1, 2)
	print(result)
function(lambda x, y: x + y)
```





#### 5.5 返回值

##### 5.5.1 不返回(return)

返回None，方法依然可以使用变量来接受这个None类型的返回值



##### 5.5.2 返回单/多个参数

```python
# 单个参数，直接返回
return x

# 多个参数，用逗号分隔，接收按照返回值的顺序，写对应顺序的变量接收
return x, y

x, y = funcReturn()
```



---



### 六、面向对象

#### 6.1 类

##### 6.1.1 概念

同样包含属性，以及方法，通过创建类对象访问属性和方法

```python
class 类名:
    # 类属性(成员变量)
	属性1 = None
	属性2 = None
	属性3 = None
    
    # 类方法(成员方法)
    def 方法名(self,参数列表):
        执行体...
```





#### 6.2 对象

##### 6.2.1 概念



##### 6.2.2 创建

```python
# 括号可以理解为构造方法
对象(实例)名 = 类名()
```



##### 6.2.3 属性赋值

```python
对象名.属性名 = 属性值
```



##### 6.2.4 获取属性值

```python
对象名.属性名
```



##### 6.2.5 生命周期(作用域)

局部变量的作用域一般是以空格/Tab为界，也就是伪大括号(Python中没有大括号)

###### 局部变量(成员变量)

> 方法内部的变量

```python
def funcTest():
    num = 1
funcTest()
# 报错，局部变量
print(num)
```

###### 在方法中声明全局变量

```python
def funcTest():
    # 必须先定义，后使用，且不能定义同时赋值
    global num
    num = 1
funcTest()
print(num)
# 打印1
```





#### 6.3 方法

##### 6.3.1 方法调用

```python
对象名.方法名
```

**实例**

```python
class Student
	def hello(text)
	print(text)
# 先创建实例，再通过实例调用方法
student = Student()
hello("Success!")
```



##### 6.3.2 构造方法

> _ _ init _ _，创建对象时传入参数，使用构造方法可以不写属性，会自动创建并赋值，写则只赋值

```python
class Person:
    
    # 属性(成员变量)
	id = None
	name = None
	
	# 构造方法
	def __init__(self, id, name):
		self.id = id
		self.name = name
		

person = Person(1, "刘备")
```



##### 6.3.3 魔术方法

> Python中类内置了一些方法，有不同的特殊功能，_ _ init _ _就是其中之一，这些方法统称为魔术方法
>
> 前面两个下划线后面两个下划线包裹起来的方法都是内置的魔术方法

###### _ _ str _ _

> 类似于Java中的重写toString()

```python
class Person:
    
    # 属性(成员变量)
	id = None
	name = None
	
	# 构造方法
	def __init__(self, id, name):
		self.id = id
		self.name = name
	
	# 重写toString方法
	def __str__(self):
		return f"student类对象,id={self.id}, name={self.name}"

person = Person(1, "刘备")
```

###### _ _ eq _ _

> 比较方法(equals)
>
> 不重写equals方法，对象之间比较的是内存地址，那么不同的对象比较一定是False，即便属性值相同。
>
> 重写eq方法，可以自定义比较的逻辑，例如比较属性值。

```python
class Person:
    
    # 属性(成员变量)
	id = None
	name = None
	
	# 构造方法
	def __init__(self, id, name):
		self.id = id
		self.name = name
	
	# 小于符号比较方法,other是另一个对象
	def __eq__(self, other):
		return self.id == other.id

person = Person(1, "刘备")
person2 = Person(2, "关羽")

# False
print(person == person2)
```

###### _ _ lt _ _

> 小于符号比较方法(less than)

```python
class Person:
    
    # 属性(成员变量)
	id = None
	name = None
	
	# 构造方法
	def __init__(self, id, name):
		self.id = id
		self.name = name
	
	# 小于符号比较方法,other是另一个对象
	def __lt__(self, other):
		return self.id < other.id

person = Person(1, "刘备")
person2 = Person(2, "关羽")

# True
print(person < person2)

# False
print(person < person2)
```

###### _ _ le _ _

> 小于等于符号比较方法(less than or equal)

```python
class Person:
    
    # 属性(成员变量)
	id = None
	name = None
	
	# 构造方法
	def __init__(self, id, name):
		self.id = id
		self.name = name
	
	# 小于符号比较方法,other是另一个对象
	def __le__(self, other):
		return self.id <= other.id

person = Person(1, "刘备")
person2 = Person(2, "关羽")

# True
print(person < person2)

# False
print(person < person2)
```

###### 其他魔术方法

![魔术方法](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/%E9%AD%94%E6%9C%AF%E6%96%B9%E6%B3%95.png)



##### 6.3.4 self

> 代表实例本身(调用该方法的对象，类似于Java中的this)
>
> 成员方法的参数必须携带self，但是传参时可以忽略。
>
> 方法内部访问类的成员变量，必须使用self。

```python
class Person:
	id = None
	name = None

	def sayHi(self):
		print("你好，我是{self.name}，很高兴认识你！")

    def sayMessage(self, message):
        print(f"你好，我是：{self.name}，这个问题:{message}需要解决一下")


# xxx.py
person = Person()
person.id = 1
person.name = "刘备"
person.sayHello()
# self可以不传参，只传message即可
person.sayMessage("index of outBounds")

# 输出：
# 你好，我是刘备，很高兴认识你！
# 你好，我是：刘备，这个问题index of outBounds需要解决一下
```







#### 6.4 封装、继承、多态

##### 6.4.1 封装

封装是一种隐藏对象内部细节的方式，只向外界暴露需要使用的方法和属性。这样做的好处是可以保护数据的完整性，并使代码更易于维护和理解。比如将类的属性私有化只暴漏接口给外部调用，例如构造方法



##### 6.4.2 继承

> 代码复用，公共代码写成父类

继承是一种可以让某个类型获得另一个类型的字段和方法的功能。这使得父类的设计和实现可以被重用，并可以在子类中添加新的功能。

###### 单一继承

```python
class 类名(父类):
	...
```

```python
class Animal:
	name = None
	color = None
	species = None
	
	eat方法...

# Dog类继承Animal类
class Dog(Animal):
	# 品种
	breed = None
	
	run方法...
```

###### 多重继承

> 一个类继承多个父类，父类里的参数重名，继承第一个(从左到右)

```python
class 类名(父类1, 父类2, 父类3...):
    # pass是语法补全，类定义什么都没写会报错，用pass占位就不报错了
	.../pass
```



##### 6.4.3 多态

> 父类对象的子类引用调用方法，使同一种行为，使用不同类型的对象调用的方法不同，得到不同的运行结果

多态是指一个引用变量到底会调用哪个类(父/子)的方法，不由引用变量的类型决定，而是由其实际的类型决定。在运行时可以改变引用变量的实际类型，也就是可以改变程序的行为，这就是多态性。

###### 复写

> 可以理解为重写，即方法名、方法参数名、参数个数一致，子类方法重写内部的具体实现，称为复写。

```python
class Phone:
	# 序列号
	IMEI = None
	# 手机厂商
	producer = "HUAWEI"
	
	def call():
		print("4G通话")

class MyPhone(Phone):
	# 重写手机厂商
	producer = "IPHONE"
	
	# 重写父类方法
	def call():
		print("5G通话")
```





#### 6.5 接口

> Python接口的写法更像是Java抽象类

##### 6.5.1 定义



**实例**

1. 父类保存抽象方法

```python
# 空调类
class AC:
	def coolWind(self):
		"""制冷"""
		pass
	def hotWind(self):
		"""制热"""
		pass
	def swingLeftAndRight(self):
		"""摆动"""
		pass
    def makeCool(ac: AC):
        # 运行
        ac.coolWind()
```

2. 子类实现

```python
class MediaAC(AC):
	def coolWind(self):
		"""制冷"""
		print("美的空调制冷")
	def hotWind(self):
		"""制热"""
		print("美的空调制热")
	def swingLeftAndRight(self):
		"""摆动"""
		print("美的空调摆动")
        
class GreeAC(AC):
	def coolWind(self):
		"""制冷"""
		print("格力空调制冷")
	def hotWind(self):
		"""制热"""
		print("格力空调制热")
	def swingLeftAndRight(self):
		"""摆动"""
		print("格力空调摆动")
```

3. 调用

```python
def makeCool(ac: AC):
    # 运行
    ac.coolWind()


media: MediaAC = MediaAC()
gree: GreeAC = GreeAC()

makeCool(media)
makeCool(gree)
```





---





### 七、关键字

#### 7.1 None

函数有返回值，返回值类型就是方法指定的类型，没有返回值，返回值是None，类型是NoneType。

##### 7.1.1 声明变量

对一个不想赋初值的变量，可以用None声明

```python
num = None
```



##### 7.1.2 判断

在if判断中，None等同于false

```python
result = None
# None表示false，not None就是true
if not result
```



##### 7.1.4 方法返回

如果为空，或不返回，默认返回None





#### 7.2 super

##### 7.2.1 概念

在重写了父类的属性、方法后，调用会优先使用子类重写的，如果想调用父类的成员变量或者方法，使用super



##### 7.1.2 调用父类方式

###### 父类名调用

```python
父类名.成员变量
父类名.成员方法(self)
```

###### super()调用

```
super().成员变量
super().成员方法()
```





---



### 八、可见性(作用域)

#### 8.1 概念

可见性提高了代码的可读性，主要跟性能无关，好的设计是和可见性有很大关系的；

一个类内部的、仅自己使用的属性/方法都设计成private，仅public对外供外部调用的接口，其他人就只需要看这些public的属性/方法的实现就可以。

类似于单例模式，仅public一个创建单例实例对象的方法——<font color="#f40">封装</font>

##### 8.1.1 private

对象无法给`__`(private)修饰的私有成员变量赋值、无法访问私有方法。

```python
# 不报错，但赋值失效
对象名.__变量名 == xxx
# 报错，提示没有这个成员方法
对象名.__方法名
```

在类内部可以访问，下例age是私有的，通过公开方法(在类内部)访问age以及私有方法：

```python
class Person:
    
    # 属性(成员变量)
    id = None
    name = None
    __age = 10
    
    # 构造方法
    def __init__(self, id, name):
        self.id = id
        self.name = name
    
    # 私有方法
    def __returnFalse(self):
        return "未成年，无法查询！"
    
    # 公开方法
    def getAge(self):
        if self.__age > 18:
            # 调用私有属性
            return self.__age
        else:
            # 调用私有方法
            return self.__returnFalse()
        
person = Person(1, "刘备")
person.getAge()
```



---



### 九、文件操作(IO 流)

#### 9.1 打开/创建文件

> 注意encoding的参数顺序不是第三位，传参方式不能用位置参数[^3]，要用关键字参数[^4]直接指定
>
> 最后要关闭文件，否则一直占用该文件，或者使用with open
>
> ```python
> # 关闭文件(关闭流)
> 文件对象.close()
> ```
>

##### 9.1.1 open

```python
# name:文件名(可以有路径) 
# model:打开文件的模式(只读r、写入w、追加a...)
# encoding:编码格式(一般使用UTF-8)
open(name, mode, encoding)
```



##### 9.1.2 with open

通过在with open的语句块中对文件进行操作，可以自动关闭文件，不需要close()

```python
with open("D:\logs\exportData.txt", "r", encoding="UTF-8") as f:
    for line in f:
	    print(line)
```



##### 9.1.3 访问模式的区别

r：以只读的方式打开文件。文件的指针会放在文件的开头。默认模式

w：打开一个文件只用于写入。如果文件已存在则打开该文件从头编辑，原有内容删除，文件不存在创建新文件

a：打开文件用于追加，文件存在写入到已有内容之后，文件不存在，创建新文件写入





#### 9.2 读取文件

> 文件的关闭是自动的(垃圾回收)，但是在处理大量文件的时候，显式关闭文件可以更好地管理资源

##### 9.2.1 read

```python
# num表示要从文件中读取的数据的长度(单位字节)，如果没有传入num，就表示读取文件中的所有数据
context = 文件对象.read([num])
```



##### 9.2.2 readlines

```python
# 按照行的方式把整个文件的内容一次性读取，并且返回的是一个列表(List)，每一行的数据为一个元素
context = 文件对象.readlines()
```

###### for循环读取文件

```python
# for循环读取文件行S，每一个line就是文件的一行数据
for line in open("D:\logs\exportData.txt", "r", encoding="UTF-8"):
    print(line)
f.close()
```





#### 9.3 写入文件

> close()方法内置了flush()操作

1. open()

> 文件不存在，会自动创建文件

```python
# 打开/创建文件用w模式打开
file = open("D:\logs\writeData.txt", "w", encoding="UTF-8")

# 追加文件用a模式打开，追加不换行
file = open("D:\logs\writeData.txt", "a", encoding="UTF-8")
```

2. write()

```python
文件对象.write("写入内容")
```

3. flush()

> 文件在操作时(write())是没有直接写入的，是保存在内存中(缓冲区，同C++)，这样避免频繁的操作硬盘。

```python
# 内容刷新
文件对象.flush()
```



---



### 十、异常

未指定正确异常，将无法捕获，异常具有传递性(同Java)，多个方法调用中间有异常会向上层传递。

#### 10.1 基本语法

> 同try-catch

##### 10.1.1 捕获所有异常

```python
try:
	可能发生错误的代码
except:
	发生错误后执行的内容
```

##### 10.1.2 捕获指定异常

```python
try:
	可能发生错误的代码
except 异常类型 as 自定义异常名:
	发生错误后执行的内容
```



##### 10.1.3 捕获多个异常

> 将要捕获的异常写在except后，使用元组的方式进行书写

```python
try:
	可能发生错误的代码
except (异常类型1,异常类型2) as 自定义异常名:
	发生错误后执行的内容
```

**实例**

```python
try:
	1 / 0
except (NameError,ZeroDivisionError) as e:
	print("出现了变量未定义或除以0的异常！")
```





#### 10.2 else

> 没有出现异常执行，非必须

```python
try:
	可能发生错误的代码
except 异常类型 as 自定义异常名:
	发生错误后执行的内容
else:
	没有出现异常执行的内容
```





#### 10.3 finally

> 无论是否出现异常都执行，非必须，但是finally<font color="#f40">不是一定执行</font>的，注意某些操作不能放到finally块。

```python
try:
	可能发生错误的代码
except 异常类型 as 自定义异常名:
	发生错误后执行的内容
else:
	没有出现异常执行的内容
finally:
    最终执行(关闭文件流等【※不建议】)
```



---



### 十一、注解

> 在Python3.5+引入，类似于Java的泛型

#### 11.1 类型注解

Python没有Java的参数类型限制，可以使用注解实现标记数据类型，本质上方便了Pycharm做类型推断

##### 11.1.1 基础类型注解

```python
变量名: 类型注解 = 参数值
name: str = "刘备"
```



##### 11.1.2 类对象注解

```python
对象名: 类型 = 类名()
class Student:
# 正常定义
stu = Student()
# 注解声明对象stu的类型是Student
stu: Student = Student()
```



##### 11.1.3 容器注解

```python
"""========================简易注解========================"""
# 列表
myList: list = [1, 2, 3]
# 元组
myTuple: tuple = (1, 2, 3)
# 集合
mySet: set = {1, 2, 3}
# 字典
myDict: dict = {1: "刘备", 2: "关羽"}
# 字符串
myString: str = "刘备"

"""========================详细注解(声明容器保存的元素类型)========================"""
# 列表
myList: list[int] = [1, 2, 3]
# 元组
myTuple: tuple[int, str, bool] = (1, "2", True)
# 集合
mySet: set[int] = {1, 2, 3}
# 字典
myDict: dict[int, str] = {1: "刘备", 2: "关羽"}
```



##### 11.1.4 注释实现类型注解

```python
class Student():
	pass
var1 = random.randint(1, 10)	# type: int
var2 = json.loads(data)			# type: dict[str, int]
var3 = func()					# type: Student
```





#### 11.2 形参列表/返回值注解

> 建议性注解

##### 11.2.1 形参注解

```python
def 方法名(形参名: 类型, 形参名: 类型):
	return x + y
```



##### 11.2.2 返回值注解

```python
def 方法名(data: list) -> 返回类型
	return data
```





#### 11.3 union(联合)注解

##### 11.3.1 基本使用

1. 导包

```python
from typing import Union
```

2. 实例

```python
"""=============================容器注解============================="""
实例名: 注解类型[Union(联合类型1，联合类型2)] = [数据1, 数据2, "数据3", "数据4"]
myList: list = [1, 2, "3", "4"]
# 新增了数据字符串"3"、"4",list类型已经限制不了了，转换为：
myList: list[Union(int, str)] = [1, 2, "3", "4"]

"""=============================方法注解============================="""
def 方法名(data: Union[参数类型1, 参数类型2...]):
def func(data: Union[int, str]):
```



---



### 解释文档

[^1]:Python3以后支持汉字，但不建议使用
[^2]:关键字获取 import keyword	print(keyword.kwlist)
[^3]: 5.2.1 位置参数
[^4]:5.2.2 关键字参数
[^5]:1.5.5 __main__
