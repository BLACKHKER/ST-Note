## Python基础

### 变量

> 变量没有数据类型，定义的时候不需要分配数据类型

#### 标识符

只允许英文、中文、数字、下划线，数字不可以开头，区分大小写，不可以使用关键字

```python
Abc = 10
abc = 11
# 打印11
print(abc)
```





#### 作用域

##### 局部变量(成员变量)

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









### 数据类型

#### 数字(Number)

##### 整数(int)

正、负整数，1、-1



##### 浮点数(float)

带小数点的数，3.14



##### 复数(complex)

1+2j，以j结尾表示负数



##### 布尔(bool)

True、False





#### 字符串(String)

字符组成，单个字符也是字符串，没有char字符类型

##### 定义的三种方式

> 三引号定义和多行注释的写法一样，使用变量接受它，它就是字符串，不接收就是注释

```python
# 单引号、双引号、三引号
str1 = 'String1'
str2 = "String2"
str3 = """String3"""
```



##### 字符串拼接

> 跟Java一样使用+号拼接，拼接的内容必须是String类型

```python
str1 = "Te"
str2 = "st"
print(str1 + str2 + "!")
```



##### 字符串格式化

###### 占位符

> 跟C语言一样通过 %占位符占位，后面的字母代表不同的意思

- %s：表示将变量变成字符串放入占位的地方
- %d：表示十进制整数类型的占位符。
- %f：表示浮点数类型的占位符。
- %c：表示单个字符类型的占位符。
- %o：表示八进制整数类型的占位符。
- %x：表示十六进制整数类型（小写字母）的占位符。
- %X：表示十六进制整数类型（大写字母）的占位符。
- %%：表示百分号字符 % 自身的占位符。

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

###### format()

> 没法配置精度

```python
name = "Alice"
age = 25
message = "My name is {} and I am {} years old.".format(name, age)
print(message)
```

###### f-strings(格式化字符串字面值)

> 没法配置精度

```python
name = "Alice"
age = 25
# 在字符串前面添加一个标记f，参数通过{}花括号配合变量名处理
message = f"My name is {name} and I am {age} years old."
print(message)
```



##### 表达式格式化

```python
str1 = "String"
print("1 * 1的结果是：%d" % (1 * 1))
print(f"1 * 1的结果是：{1 * 1}")
print(f"变量str的类型是：{type(str1)}")
```



##### 数字精度控制

使用m.n控制数据的宽度和精度

m：控制宽度，要求是数字(很少使用)，设置的宽度小于数字自身则不生效，小数点和小数部分也参与宽度计算

n：控制小数点精度，要求是数字，会进行小数的四舍五入

###### 示例

%5d：表示将宽度控制在五位，比如数字541，设置为5d就会变成：[空格] [空格] 541，用空格补齐宽度

%7.2f：表示将宽度控制为7，将小数点精度控制为2，比如54.156，设置%7.2f后变成：[空格] [空格]  54.16，总长度7位，保留小数点后两位，第三位四舍五入，变成54.16

%.2f：表示不限制宽度，保留小数点后两位

```python
num1 = 54.155
print("修改精度后的值为：%7.2f" %num1)
# 输出：修改精度后的值为：  54.16(包含两个空格)
```

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



##### 字符串比大小

字符串大小是根据ASCII码按位比较：ASCII值越小越大，小写大于大写

azz : baa baa大，先比较字符串的第一个字符，如果相等，比较第二个，以此类推



##### 方法

###### 通过下标索引取值

> 字符串底层跟Java一样，也是final数组，所以可以用下标取值，但是**无法修改**

```python
string = "abcdefg"
# 从前向后，下标从0开始
s = string[0]
# 打印a
print(s)
# 从后向前，下标从-1开始
s2 = string[-1]
# 打印g
print(s2)
```

###### 更新

```python
# 字符串替换：将字符串内的全部字符串1替换成字符串2，返回新字符串，不修改原字符串
字符串.replace(字符串1, 字符串2)

# 字符串分割：按照指定字符串分割，返回列表，同样不修改原字符串
字符串.split(分割字符串标识)

# 字符串规整：去除前后空格
字符串.strip()
# 去除前后指定字符串	-- 注意这里的去除字符串是单个字符：abcba.strip(ab)，得到的就是c，ab看成单个字符
字符串.strip(字符串)
```

###### 查找

```python
# 获取对应字符串的下标起始位置
字符串.index(要查询下标的字符串)

# 统计字符串中某字符串的出现次数
字符串.count(统计的字符串)

# 统计字符串的长度
字符串.len()
```







#### 列表(List)(Java List)

**有序**、**可重复**、记录大量数据，可变的数据结构，用方括号`[]`表示。它可以包含**任意类型**的元素，并且允许元素重复。列表可以通过索引访问、添加、删除和修改元素。列表常用于存储和处理多个相关的元素。

##### 定义

###### 定义列表

```python
# 空列表
[]

# 空列表
myList = []

# 可以在创建列表时初始化元素：list(range(1,5)) --- [1,2,3,4]
myList = list()
myList = [1, 2, 3, 4, 5]
```

###### 定义嵌套列表

```python
myList = [[1, 2, 3], [4, 5, 6]]
```



##### 索引(同Java)

> 索引从0开始，跟Java一样，注意index outbound Exception下标越界异常

```python
myList = [1, 2, 3, 4, 5]
# 打印1
print(myList[0])
```

###### 反向索引

> 从-1开始，就是-1为0号元素，依次类推-2、-3...

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



##### 方法

###### 插入元素

```python
# 在列表的末尾新增元素
列表名.append(插入的元素)

# 在指定下标的位置插入新元素
列表名.insert(下标, 元素值)

# 将其他容器的元素添加到该列表的末尾
列表名.extend(其他容器的容器名)
```

###### 删除元素

```python
# 删除指定下标的元素
del 列表名[下标]

# 弹出指定下标的元素(弹出类似于Java的Stack栈，返回弹出的数据)
列表名.pop(下标)

# 删除列表中第一个匹配指定值的元素
列表名.remove(参数)

# 清空列表
列表名.clear()
```

###### 修改元素

```python
# 修改特定位置的元素值
列表[正/反下标] = 修改后的值
```

###### 查找元素

```python
# 查找某元素在列表中的下标索引	-- 不存在会报错xxx is not in list
myList.index("元素名")
```

###### 统计元素

```python
# 统计列表内某元素的数量(数据类型同样做区分)
列表名.count(元素)

# 获取列表大小(Java size())
len(列表名)
```



##### 遍历

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





#### 元组(Tuple)(Java Array)

> 只读的List列表

**有序**、**可重复**、记录大量数据，不可变的数据结构，用圆括号`()`表示。类似于列表，元组可以包含**任意类型**的元素，但一旦创建，就不能修改。元组常用于存储不可变的数据，如坐标、日期等。

##### 定义

###### 定义元组

> 注意只有一个数据的时候，这个数据的后面要添逗号

```python
# 空元组
(元素1, 元素2, 元素3)
array = (元素1, 元素2, 元素3)

# 可以在创建元组时初始化
array = ()
array = tuple()
```

###### 定义嵌套元组

```python
array = ( (1, 2, 3), (4, 5, 6) )
print(array[0] [0])
# 打印1
```



##### 索引(同Java)

> 索引从0开始，跟Java一样，注意index outbound Exception下标越界异常

```python
myArray = (1, 2, 3, 4, 5)
# 打印1
print(myList[0])
```

###### 反向索引

> 从-1开始，就是-1为0号元素，依次类推-2、-3...

```python
myArray = (1, 2, 3, 4, 5)
# 打印5
print(myArray[-1])
```

###### 矩阵索引

> 两个索引值

```python
myArray = ( (1, 2, 3), (4, 5, 6))
print(myArray[0][1])
```



##### 方法

> 元组不可修改，所以没有其他方法，但是元组的元素如果是list，那么可以修改list的值

###### 查找元素

```python
# 查找某元素在列表中的下标索引	-- 不存在会报错xxx is not in list
元组名.index("元素名")
```

###### 统计元素

```python
# 统计元组内某元素的数量(数据类型同样做区分)
元组名.count(元素)

# 获取元组大小(Java size())
len(元组名)
```

###### 修改元组中的list数据

```python
myArray = (1, 2, [4, 3])
# 修改list中第一位为3第二位为4
myArray[2][0] = 3
myArray[2][1] = 4
```



##### 遍历

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





#### 序列

##### 概念

序列是指：内容连续、有序且可以用下标访问的数据容器，列表(list)、元组(tuple)、字符串(str)



##### 常用操作

###### 切片

> 从一个序列中取出一个子序列

###### 示例

```python
# 从序列中，从指定位置开始，依次取出元素，到指定位置结束，得到一个新序列
# 起始下标表示从何处开始，可以留空，留空视作从头开始
# 结束下标表示何处结束，可以留空，留空视作截取到结尾，不包含当前
# 步长表示依次取元素的间隔：
# 1表示一个个取元素(默认是1)，2表示每次跳过一个取，N表示每次跳过N-1个取，
# 步长为负数，表示反向取(注意起始下标和结束也要反向)
序列[起始下标:结束下标:步长]
```





#### 集合(Set)(Java Set)

**无序**、**不可重复**、记录大量数据，可变的数据结构，用花括号 `{}` 表示。集合中的元素是唯一的，不允许重复。集合提供了快速的成员检查和数学集合操作，如交集、并集、差集等。

##### 定义

```python
# 空集合
集合名 = {1, 2, 3, 4, 5}
集合名 = set()
```



##### 方法

###### 添加元素

```python
# 添加新元素到集合
集合名.add(元素内容)
```

###### 移除元素

```python
# 根据元素名从集合中移除元素
集合名.remove(元素名)

# 随机弹出一个元素(类似于JavaStack栈)
集合名.pop()

# 清空集合
集合名.clear()
```

###### 修改

```python
# 取差集：根据集合1和集合2的差集(集合1有而集合2没有的)，返回一个新集合，原集合不变
集合1.difference(集合2)

# 取差集2：以集合1为主集合，在集合1内删除和集合2相同的元素，集合1被修改，集合2不变
集合1.difference_update(集合2)

# 合并集合，返回并集，原集合1和集合2不变
集合1.union(集合2)
```

###### 查询

```python
# 统计集合内元素数量
len(集合名)
```



##### 遍历

> 集合不支持下标索引，不能用while循环

```python
for i in 集合名
print(i)
```



##### 注意

集合中的元素不可以是list列表，因为集合是存储不重复的元素容器，可以存储元组(tuple)





#### 字典(Dictionary)(Java Map)

**无序**、**Key唯一**，记录大量数据，可变的**键值对数据结构**，用花括号 `{}` 表示。字典中的元素由键（key）和对应的值（value）组成，键必须是唯一的。字典常用于存储和检索具有关联关系的数据。

```python
my_dict = {'name': 'Alice', 'age': 25, 'city': 'New York'}
```

##### 定义

###### 定义字典

> 重复key，保存最后一个key的值

```python
# 定义空字典
dic = {}
dic = dict()
dic = {"key1": value2, "key2": value2}
```

###### 定义嵌套字典

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



##### 方法

###### 新增

```python
# 新增元素：如果这个key不存在，等同于新增一个键值对，存在即修改对应key的值
字典名[key] = value
```

###### 删除

```python
# 从字典中弹出一个元素(key)
字典名.pop(key)

# 清空字典
字典名.clear()
```

###### 更新元素

```python
# 更新元素：修改对应key的值
字典名[key] = value
```

###### 查询

```python
# 获取字典全部的key
字典名.keys()

# 统计字典内的元素数量
len(字典名)
```



##### 遍历

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















### 输出打印

```python
# 打印单个，直接打印
print("123")

# 打印多个，用逗号分隔
num = 50
str = "String"
f = 1.23
print(num,str,f)
```







### 注释

#### 单行注释

##### #号

```python
# 注释内容
...
```





#### 多行注释

##### 三个双引号"”“

```python
""" 
多行注释
"""
```







### 运算符

#### 基本

##### 加、减、乘、除、整除、取余、指数幂(开方)、赋值运算符、复合运算符、

```python
+、-、*、/、//、%、**、=、+=、-=、*=、/=、%=、**=、//=
```



##### 注意

###### Python中除不尽，会自动转换类型，不想转换类型就需要用//整除

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

###### 指数幂是直接用的

```python
a = 10
b = 2
c = a ** b
print(c, type(c))
# 打印：100 <class 'int'>
```







### 数据输入(接收键盘输入)

> 就是Java中的type x = new Scanner(System.in).next(); 

```python
变量名 = input()
```

##### 示例

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
```



##### 注意

从键盘接收的值，永远是String类型







### 流程控制

#### 判断

##### if

```python
if 条件:
    # 四个空格/tab
	条件成立TODO
```

###### 示例

```python
age = 24
if age < 25:
    print("Success!")
```



##### if-else

```python
if 条件:
    # 四个空格/tab
	条件成立 TODO
else:
    条件不成立 TODO
```

###### 示例

```python
# if-else
age = 24
if age < 25:
    print("Success!")
else:
    print("Error!")
```



##### elif

```python
if 条件:
    # 四个空格/tab
	条件成立 TODO
elif 条件2:
    条件2不成立 TODO
else:
	TODO
```

###### 示例

```python
age = 25
if age < 25:
    print("lt!")
elif age > 25:
    print("gt!")
else:
    print("True!")
```



##### if嵌套

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





#### 循环

##### while

```python
while 条件:
	条件为True，执行...
...
```

###### 实例

```python
age = 10
while age < 100:
    age += 1
print(age)
```



##### for

```python
for 临时变量 in 数据集:
	循环体...
```

###### 实例

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

###### 注意

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



##### 循环中断

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







### 函数(方法)

> 函数可以直接用，如果在类中，跟Java一样，先创建实例，用实例调用方法

#### 定义

##### 函数结构

```python
def 函数名(参数):
	函数体
	return 返回值
```



##### 实例

###### 普通函数

```python
# 函数Demo
def hello(text):
    print(text)
hello("Success！")
```

###### 方法

```python
class Student
	def hello(text)
	print(text)
# 先创建实例，再通过实例调用方法
student = Student()
hello("Success!")
```







#### 返回值

##### 声明变量

对一个不想赋初值的变量，可以用None声明

```python
num = None
```



##### 声明判断

在if判断中，None等同于false

```python
result = None
# None表示false，not None就是true
if not result
```



##### 声明方法

如果为空，或不返回，默认返回None

###### 注意

函数有返回值，返回值类型就是方法指定的类型，没有返回值，返回值是None，类型是NoneType

等同于Java中的Null



##### 方法注释

在方法内部第一行打三个双引号回车

```python
def funcTest()
	"""回车"""
	TODO...
```

