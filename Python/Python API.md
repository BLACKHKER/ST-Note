## Python API

### 一、基本数据类型

#### 1.1 字符串

##### 1.1.1 通过下标索引取值

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



##### 1.2 更新

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



##### 1.3 查找

```python
# 获取对应字符串的下标起始位置
字符串.index(要查询下标的字符串)

# 统计字符串中某字符串的出现次数
字符串.count(统计的字符串)

# 统计字符串的长度
字符串.len()
```





#### 1.2 列表

##### 1.2.1 插入元素

```python
# 在列表的末尾新增元素
列表名.append(插入的元素)

# 在指定下标的位置插入新元素
列表名.insert(下标, 元素值)

# 将其他容器的元素添加到该列表的末尾
列表名.extend(其他容器的容器名)
```



##### 1.2.2 删除元素

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



##### 1.2.3 修改元素

```python
# 修改特定位置的元素值
列表[正/反下标] = 修改后的值
```



##### 1.2.4 查找元素

```python
# 查找某元素在列表中的下标索引	-- 不存在会报错xxx is not in list
myList.index("元素名")
```



##### 1.2.5 统计元素

```python
# 统计列表内某元素的数量(数据类型同样做区分)
列表名.count(元素)

# 获取列表大小(Java size())
len(列表名)
```





#### 1.3 元组

> 元组不可修改，所以没有其他方法，但是如果元组的元素是List，那么可以修改list的值

##### 1.3.1 查找元素

```python
# 查找某元素在列表中的下标索引	-- 不存在会报错xxx is not in tuple
元组名.index("元素名")
```



##### 1.3.2 统计元素

```python
# 统计元组内某元素的数量(数据类型同样做区分)
元组名.count(元素)

# 获取元组大小(Java size())
len(元组名)
```



##### 1.3.3 修改元组中List的数据

```python
my_tuple = (1, 2, [4, 3])
# 修改list中第一位为3第二位为4
my_tuple[2][0] = 3
my_tuple[2][1] = 4
```





#### 1.4 集合

##### 1.4.1 添加元素

```python
# 添加新元素到集合
集合名.add(元素内容)
```



##### 1.4.2 移除元素

```python
# 根据元素名从集合中移除元素
集合名.remove(元素名)

# 随机弹出一个元素(类似于JavaStack栈)
集合名.pop()

# 清空集合
集合名.clear()
```



##### 1.4.3 修改元素

```python
# 取差集：根据集合1和集合2的差集(集合1有而集合2没有的)，返回一个新集合，原集合不变
集合1.difference(集合2)

# 取差集2：以集合1为主集合，在集合1内删除和集合2相同的元素，集合1被修改，集合2不变
集合1.difference_update(集合2)

# 合并集合，返回并集，原集合1和集合2不变
集合1.union(集合2)
```



##### 1.4.4 统计元素

```python
# 统计集合内元素数量
len(集合名)
```





#### 1.5 字典

##### 1.5.1 新增元素

```python
# 新增元素：如果这个key不存在，等同于新增一个键值对，存在即修改对应key的值
字典名[key] = value
```



##### 1.5.2 删除元素

```python
# 从字典中弹出一个元素(key)
字典名.pop(key)

# 清空字典
字典名.clear()
```



##### 1.5.3 更新元素

```python
# 更新元素：修改对应key的值
字典名[key] = value
```



##### 1.5.4 统计元素

```python
# 获取字典全部的key
字典名.keys()

# 统计字典内的元素数量
len(字典名)
```





#### 1.6 容器(通用)

##### 1.6.1 容器长度

> len(容器名)

```python
string = "123"
list = [1, 2, 3]
tuple = (1, 2, 3)
set = {1, 2, 3}
dic = {"1": 10, "2": 20, "3": 30}
len(string)
len(list)
len(tuple)
len(set)
len(dic)
```



##### 1.6.2 容器最大元素

> max(容器名)

```python
max(string)
max(list)
max(tuple)
max(set)
max(dic)
```



##### 1.6.3 容器最小元素

> min(容器名)

```python
min(string)
min(list)
min(tuple)
min(set)
min(dic)
```



##### 1.6.4 容器转换

> 字典进行容器转换的时候，只会保存key

```python
list(容器名)
set(容器名)
tuple(容器名)
set(容器名)
# 只有set可以转字典
dict(set集合)
```



##### 1.6.5 容器排序

> reverse为可选参数，true为升序，false为降序

```python
sorted(容器名, [reverse=boolean])
```



---



### 二、IO

#### print()

> 打印

##### print(参数、变量)

```python
print("Success!")
```



##### print(语句, end='')

> 不换行

```python
print("Success!" end='')
```





#### type()

> 判断数据的类型

##### 直接输出变量的类型信息

```python
num = 50
str = "String"
f = 1.23

print(type(num))
print(type(str))
print(type(f))

""" 
输出：
<class 'int'>
<class 'str'>
<class 'float'>
"""
```



##### 变量存储type的返回值

> type方法返回的结果是type类型

```python
num = 50
str = "String"
f = 1.23

a = type(num)
b = type(str)
c = type(f)

# 打印type的返回值和返回值类型
print(a,type(a))
print(b,type(b))
print(c,type(c))

"""
输出：
<class 'int'> <class 'type'>
<class 'str'> <class 'type'>
<class 'float'> <class 'type'>
"""
```





#### 类型转换

##### int()：转换成整数

```python
str = "1"
num = int(str)
```



##### float()：转换成浮点数

```python
str = "1.23"
f = float(str)
```



##### str()：转换成字符串

```python
num = 1
str = str(num)
```



##### 注意

Python不支持自动类型转换，比如int和String相加会报错，需要先将int转换成String类型，才能拼接成字符串

```python
num = 1
stri = "2"
print(str(num) + stri)
# 打印12
```







---



### 三、Math

#### random()

> 生成随机数

##### randint(最小值，最大值)

> 生成一个int类型的数字，区间在参数一和参数二之间(包含参数一和参数二)

###### 实例

```python
import random
num = random.randint(1,10)
```



##### random()

> 生成一个位于0和1之间的随机浮点数

###### 实例

```python
import random
f = random.random()
# 打印0.6858389579174713 <class 'float'>
print(f,type(f))
```



##### random.uniform(最小值,最大值)

> 生成一个位于指定范围的[最大值，最小值]中的随机浮点数

###### 实例

```python
import random
random_float = random.uniform(1.0,5.0)
print(random_float)
```





##### random.choice(序列名)

> 从序列中随机选择一个数字并返回，只能是List：[]

###### 实例

```python
import random

my_list = [1, 2, 3, 4, 5]
random_choice = random.choice(my_list)
print(random_choice)
```



##### random.shuffle(seq)

> 随机打乱序列 seq 中的元素顺序（就地修改）

###### 实例

```python
import random

my_list = [1, 2, 3, 4, 5]
random.shuffle(my_list)
print(my_list)
```



##### random.sample(population, k)

> 从总体 population 中随机选择 k 个不重复的元素作为样本，返回一个新的列表

###### 实例

```python
import random

my_list = [1, 2, 3, 4, 5]
random_sample = random.sample(my_list, 3)
print(random_sample)
```



​	

#### range()

> 获取一个等差序列(List、可变数组)

##### range(num)

> 从0开始，到num结束

###### 实例

```python
numsArray = range(10)
for i in numsArray:
    print(i)
# 打印0-9(十个数字)
```



##### range(num1, num2)

> 从num1开始，从num2结束，不含num2本身

###### 实例

```python
numsArray = range(10,18)
for i in numsArray:
	print(i)
# 打印10 - 17
```



##### range(num1, num2, num3)

> 从num1开始，到num2结束，步长为num3，不含num3

###### 实例

```python
numArray = range(4,10,2)
for i in numArray:
    print(i)
# 打印4,6,8
```



##### 统计x-y有几个偶数

```python
x = 1
y = 100
count = 0
numsArray = range(x, y)
for i in numsArray:
    if (i % 2 == 0):
        count += 1
print(f"{x}到{y}有{count}个偶数")
```



##### 注意

range()可以写在for循环中：

```python
for i in range(10)
	print(i)
# 打印0 - 9
```











#### 四、线程

##### 线程休眠

```python
# 线程休眠指定的毫秒数
time.sleep(ms)
```

