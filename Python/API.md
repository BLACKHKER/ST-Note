## API

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





#### 容器相关

##### len()：计算容器长度

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



##### max()：获取容器中的最大元素

```python
max(容器名)
```



##### min()：获取容器中的最小元素

```python
min(容器名)
```



##### 容器转换

> 字典进行容器转换的时候，只会保存key

```python
list(容器名)
set(容器名)
tuple(容器名)
set(容器名)
# 只有set可以转字典
dict(set集合)
```



##### 容器排序

```python
# 升序，reverse为False的时候为降序
sorted(容器名, [reverse=True](可选参数))
```







#### 线程

##### 线程休眠

```python
# 线程休眠指定的毫秒数
time.sleep(ms)
```

