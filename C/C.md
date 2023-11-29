## C - 基础

> 二进制 → 汇编指令(助记符) → VB → C
>
> 编译器：Clang、**GCC**、WIN-TC、**MSVC**、Turbo C

### 一、基础项目构建

> 展示使用VS2022(Visual Studio)

#### 1.1 新建项目

1. 初始页创建新项目

![image-20231123161401763](A:\Typora\TyporaPicture\image-20231123161401763.png)

2. 选择空项目

![image-20231123161607812](A:\Typora\TyporaPicture\image-20231123161607812.png)

3. 配置路径信息，创建

![image-20231123161858875](A:\Typora\TyporaPicture\image-20231123161858875.png)





#### 1.2 创建不同源文件

> C文件分为.c(源码)、.h(头文件，可以理解为Java类+接口)

所有文件均可以在解决方案资源管理器中创建：

![image-20231123162349780](A:\Typora\TyporaPicture\image-20231123162349780.png)

##### .c文件的创建

1. 源文件 → 添加 → 新建项

![image-20231123162629570](A:\Typora\TyporaPicture\image-20231123162629570.png)

2. 选择C++文件，<font color="#f40">修改后缀名</font>

> 如果不是这个页面，那么点击显示所有模板即可，默认.cpp(c plus plus C++)注意修改为.c(C)

![image-20231123162804084](A:\Typora\TyporaPicture\image-20231123162804084.png)

3. 模板代码

   > stdio的解释：std：标准    i：input(输入)    o：output(输出)

   ```c
   #include <stdio.h>
   
   int main()
   {
       printf("BHKDOS\n");
       
       return 0;
   }
   ```

   



##### .h文件的创建





---



### 二、基础数据类型

#### 2.1 整型

##### 2.1.1 short

短整型，占用2个字节



##### 2.1.2 int

整型，占用2或4个字节，一般为四个字节，一些嵌入式系统中的编译器可能将int类型设置为占用2个字节



##### 2.1.3 long

长整型，占用4或8个字节，在32位平台上占用4个字节，而在64位平台上占用8个字节。



##### 2.1.4 long long int

> 简写为long long

长长整型，占用8个字节



##### 2.1.5 size_t

C 语言中的一种无符号整数类型，在标准库 `<stddef.h>` 中定义。它是用来表示对象大小、数组索引和内存分配的数据类型。它是无符号的，因此只能表示非负的整数值。

`size_t` 的主要用途之一是在和内存分配相关的函数中，例如 `malloc()` 和 `sizeof` 运算符。这些函数通常返回或接受 `size_t` 类型的值，用于表示分配的内存大小或对象的大小。



#### 2.2 浮点数

##### 2.2.1 float

单精度浮点数，占用4个字节



##### 2.2.2 double

双精度浮点数，占用8个字节



#### 2.3 字符型

##### 2.3.1 char

字符，在不同编码中占不同字节：ASCII占1字节，UTF-8占1-4字节(中文等非ASCII占3-4字节)

```c
/* 单引号 */
char en = 'a'
```



##### 2.3.2 char[]

字符串，在C语言中没有Java中的String类型，使用字符数组保存字符串，字符串末尾使用`\0`作为结束标志

![image-20231127153046112](A:\Typora\TyporaPicture\image-20231127153046112.png)

```c
/* 保存字符串时 双引号 长度为字符个数 + 1(7)多了一个\0 */
char str[] = "String";

/* 保存字符数组时 花括号 长度为字符个数(6) */
char arr[] = {'a', 'b', 'c', 'd', 'e', 'f'};
```

> <font color="#f40">注意：</font>两种类型打印时的效果不同，因为数组保存字符串时自动拼接一个结束符`\0`，而数组保存字符数组不会自动拼接结束符`\0`，系统判断字符串是否结束是以\0为基准，所以会把数组`arr`的内存后面的数据也打印出来，知道遇到`\0`为止
>
> ```c
> int main()
> {
>     char str[] = "String";
>     char arr[] = { 'a', 'b', 'c', 'd', 'e', 'f' };
> 
>     printf("str: %s\n", str);
>     printf("arr: %s\n", arr);
> 
>     return 0;
> }
> ```
>
> ![image-20231127153950627](A:\Typora\TyporaPicture\image-20231127153950627.png)



---



### 三、变量/常量

#### 3.1 变量

变量表示可变的量，类似于Java中非final、static修饰的参数





#### 3.2 变量的作用域

##### 3.2.1 局部变量

同Java，函数(方法)内部定义的变量，只能在函数内部(花括号{}为界)使用，函数外无法访问



##### 3.2.2 全局变量

函数(方法)外部定义的变量，可以被其他函数访问，作用域是整个工程(extern 引入)



##### 3.2.3 extern关键字

引入外部变量，实现的是类似于`#include`的功能，在C语言中表示该变量是在外部定义的

**实例**

> 两个.c文件，一个定义x，一个引入并使用x

num.c

```c
int x = 8;
```

calculator.c

```c
#include <stdio.h>

/* 声明变量x是来自外部定义的参数 */
extern int x;

int main()
{
    /* 打印x = 8 */
    printf("x的值为：%d", x);
}
```



##### 3.2.4 注意事项

1. 在C语言中，同类型相同命名的变量，不能在**一个作用域**重复出现：

```c
/* 重复定义错误 */
int a = 8;
int a = 8;
```

2. 局部变量和全局变量是可以重名的，调用遵循就近原则

```c
/* 打印值为局部变量的值:88 */
int a = 8;
void print_num()
{
    int a = 88;
    printf("a = %d", a);
}
```





#### 3.3 变量的生命周期

##### 3.3.1 局部变量

生命周期取决于作用域大小，进入作用域生命周期开始，退出作用域生命周期结束



##### 3.3.2 全局变量

在整个程序的生命周期中，程序不结束，变量不释放





#### 3.4 常量

##### 3.4.1 字面常量

一个确定的值，没有对应的标识符(变量名)去接收：

```c
int main()
{
    8;
    8.88;
    'x';
    "blackhker";   
}
```



##### 3.4.2 const关键字(常变量)

const修饰的变量不可修改，本质上就是一个常量，我们对这种变量成为常变量，可以理解为Java中的final

> 底层原理：
>
> `const` 的底层原理涉及编译器和内存管理的机制。下面是一些关于 `const` 的底层原理的解释：
>
> 1. 符号表：在编译过程中，编译器会创建符号表，用于管理程序中的标识符（如变量名、函数名等）。对于声明为 `const` 的变量，在符号表中将其标记为只读（read-only）。
> 2. 常量折叠（Constant Folding）：如果 `const` 常量在编译时已经确定了其值，编译器可以将对该常量的引用替换为其实际的值。这个过程称为常量折叠，它可以在编译时进行优化。
> 3. 存储位置：`const` 常量可以存储在不同的位置，具体取决于其作用域和声明方式。如果 `const` 声明在函数内部，则通常将其存储在栈上。如果 `const` 声明在文件范围内或使用了 `static` 修饰符，则通常将其存储在静态数据区。
> 4. 访问权限：通过将变量声明为 `const`，可以提供访问权限的限制。对于 `const` 变量，编译器会在编译时进行静态检查，防止对其进行修改。

**实例**：

```c
/* 报错，const左值不可赋值 */
#include <stdio.h>

int main()
{
    const int a = 8;
    a = 10;
    printf("a = %d", a);
    
    return 0;
}
```



##### 3.4.3 define 标识符常量

直接定义死的一个常量，可以理解为Java 中的static final，跟全局常变量的区别是不进入编译，所以不占用内存，并且define标识符定义的参数是无类型的，且后期不可修改

> define标识符常量命名，必须全部大写

```c
#define MAX = 8;

int main()
{
    printf("MAX = %d", MAX);
    int a = MAX;
    printf("a = %d\n", a);
    
    return 0;
}
```



##### 3.4.4 枚举常量

枚举常量的值是定义好的，只能是枚举内列出的值，不可更改，枚举常量的默认值是从0开始逐步递增

```c
#include <stdio.h>

enum FRUIT
{
    /* 枚举常量 */
    APPLE,
    ORANGE,
    BANANA,
};

int main()
{
    enum FRUIT fruit0 = APPLE;
    enum FRUIT fruit1 = ORANGE;
    enum FRUIT fruit2 = BANANA;

    /* 输出0,1,2 */ 
    printf("%d\n",APPLE);
    printf("%d\n", ORANGE);
    printf("%d\n", BANANA);

    return 0;
}
```





#### 3.5 转义字符

##### 3.5.1 三字母词

一些旧的编译器会将例如下面的内容进行转换：

```c
??( → [    ??) → ]
```

例如下面的代码会打印：`(are you ok]`，`而不是(are you ok??)`

```c
int main()
{
    printf("%s","(are you ok??)");
}
```

为了防止这种情况，就需要使用转义字符表示：

```c
int main()
{
    printf("%s","(are you ok\?\?)");
}
```



##### 3.5.2 C内置的转义字符

> 进制的打印，打印为该进制数(八、十六)转换为十进制数后的ASCII码

| 转义字符 |                       释义                        |
| :------: | :-----------------------------------------------: |
|   `\\`   |                    反斜杠字符                     |
|   `\'`   |                    单引号字符                     |
|   `\"`   |                    双引号字符                     |
|   `\?`   |                     问号字符                      |
|   `\a`   |                  警报(响铃)字符                   |
|   `\b`   |                     退格字符                      |
|   `\f`   |                     换页字符                      |
|   `\n`   |                     换行字符                      |
|   `\r`   |                     回车字符                      |
|   `\t`   |                    水平制表符                     |
|   `\v`   |                    垂直制表符                     |
|   `\0`   |                空字符(NULL字符串)                 |
|  `\nnn`  |   八进制字符，其中nnn是一个八进制数(例如：\123)   |
|  `\xhh`  | 十六进制字符，其中xhh是一个十六进制数(例如：\x0A) |



---



### 四、注释

#### 4.1 注释风格

**原则**

统一采用`/**/`方式注释，且注释内容左右各留一个空格，如`/* message */`；注释必须使用英文。

**示例**

```C
/* TODO */
```





#### 4.2 函数注释

**原则**

对外接口按doxgen要求的格式书写，且注释和函数定义间不留空行； 

对内接口在需要时添加注释，注释位于定义前。

**示例**

```c
/**
 * 函数功能
 *
 * @param  参数名  参数解释
 * @param  work  the work to be initialized
 * @param  fn    the call back function to run
 * @param  arg   the paraments of the function
 * @param  dly   ms to delay before run
 * 
 * @return  the operation status, 0 is OK, others is error
 */
int aos_work_init(aos_work_t *work, void (*fn)(void *), void *arg, int dly);
```





#### 4.3 变量注释

**原则**

注释在变量定义后，在仅有一个需要注释的变量时与分号之间只留一个空格； 

若多行变量定义均需注释，则最长变量定义留一个空格，其他注释与其对齐。

**示例**

```c
int func1(void)
{
    int ret; /* return value */
    ...
    return 0;
}

int func2(void)
{
    int ret;   /* return value */
    int value; /* value */
    ...
    return 0;
}
```



---



### 五、流程控制

> 流程控制包含：顺序结构、选择(分支)结构、循环结构

#### 5.1 选择语句

> 同Java，流程控制语句跟Java的区别是C中没有布尔类型，True/False取决于参数是否为0

##### 5.1.1 if...else

**实例**

```c
int main()
{
    int num = 0;

    scanf("%d", &num);

    if (1 == num)
    {
        printf("Success! %d", num);
    }
    else 
    {
        printf("Error! %d", num);
    }

    return 0;
}
```



##### 5.1.2 switch

##### 实例

```

```





#### 5.2 循环语句

> 同Java循环，Java的for循环：
>
> ```java
> public class Demo {
>     public static void main(String[] args){
>         // 循环变量i是定义在循环中的
>         for(int i = 0; i < 8; i++)
>         {
>             // TODO循环体
>         }
>     }
> }
> ```

##### 5.2.1 for

```c
for(循环变量初始化; 条件判断; 结束后执行的语句)
{
    /* TODO循环体 */
}
```

**实例**

```c
#include <stdio.h>

int main()
{
    int round = 0;
    for (round = 0; round < 8; round++)
    {
        printf("第%d次打印\n", round);
    }

    return 0;
}
```



##### 5.2.2 while

```c
while(条件判断)
{
    /* TODO循环体 */
}
```

**实例**

```c
#include <stdio.h>

int main()
{
    int round = 0;
    while (round < 8)
    {
        printf("第%d次打印\n", round);
        round++;
    }

    return 0;
}
```



##### 5.2.3 do...while



```c
do
{
    /* 循环体 */
} while(条件判断);
```

**实例**

```c
#include <stdio.h>

int main()
{
    int round = 0;

    do
    {
        printf("第%d次打印\n", round);
        round++;
    } while (round < 8);
    

    return 0;
}
```



---



### 六、函数

#### 6.1 函数定义

**实例**

functions.h

> .h头文件类似Java的接口，定义函数的返回值、函数名、参数类型、参数个数
>
> ```c
> #ifndef FUNCTIONS_H
> #define FUNCTIONS_H
> ...
> #endif 
> ```
>
> 这种结构是头文件的保护机制，作用是确保同一个头文件不会被多次包含，以防止重复定义和编译错误。
>
> 当一个头文件被多次包含时，编译器会对其中的内容进行重复处理，导致重复定义的错误。

```c
#ifndef FUNCTIONS_H
#define FUNCTIONS_H

int add(int a, int b);
void printMessage();

#endif
```

functions.c

> .c类似于Java的接口实现类，定义函数的具体执行逻辑

```c
#include <stdio.h>
#include functions.h

int add(int a, int b)
{
    return a + b;   
}

void print_message()
{
    printf("Message");
}
```

main.c

> 其他文件就可以通过引入头文件(.h文件)，来调用其他文件中定义的函数

```c
#include <stdio.h>
#include functions.h

int main()
{
    int sum = add(1, 2);
    print_message();
}
```





#### 6.2 和Java方法的区别

C中的函数和Java中的方法区别不是很大，主要有以下几点：

1. **语法和声明方式**：

   C：函数的声明通常在头文件声明(类似于Java的接口)，通过`#include`引入，函数的定义可以放在文件的任意位置。

   Java：方法是类的成员，需要在类中声明和定义，方法的定义必须在类的大括号内部。

2. **对象和类的概念**：

   C：过程式编程语言，函数通常是独立的，不依赖于特定的对象或类。

   Java：面向对象的语言，方法通常是与类关联的。方法是类的成员，可以访问对象的属性和其他方法。

3. **参数传递方式**：

   C：函数的参数传递通常是按值传递，即将参数的值复制给函数的形式参数。

   Java：方法参数传递方式有两种——按值传递和按引用传递。基本类型的参数按值传递，而对象引用作为参数时，实际上传递的是引用的副本，但仍可以通过引用修改对象的状态。

4. **返回值类型**：

   C：函数可以有各种不同的返回值类型，例如整数、浮点数、指针等。

   Java：方法也可以有各种不同的返回类型，但必须明确指定返回类型，并且只能返回一个值或者返回空（void）。

5. **异常处理**：

   C：异常处理通常通过返回值或者特定的错误码来实现。

   Java：方法具有内置的异常处理机制。方法可以声明并抛出异常，并通过try-catch语句来处理异常。



---



### 七、数组

> 同Java，下标从零开始

#### 7.1 数组定义

##### 7.1.1 一维数组(普通数组)

```c
#include <stdio.h>

#define MAX 8

int main()
{
    /* 不包含长度的定义 */
    int num[] = {0, 1, 2, 3, 4, 5, 6, 7};
    
    /* 包含长度的定义 */
    int arr[MAX] = {0, 1, 2, 3, 4, 5, 6, 7};
    for(int i = 0; i < MAX; i++)
    {
        printf("%d ", arr[i]);
    }
}
```

##### 7.1.2 二维数组(矩阵)

```c
#include <stdio.h>

#define ROWS 3
#define COLS 3

int main()
{
    int matrix[ROWS][COLS] = 
    {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };
    
    /* 访问矩阵元素 */
    printf("遍历矩阵:\n");
    for(int i = 0; i < ROWS; i++)
    {
        for(int j = 0; j < COLS; j++)
        {
            printf("%d ", matrix[i][j]);
        }
        printf("\n");
    }
    
    return 0;
}
```





#### 7.2 和Java数组的区别

1. **长度的确定**：

   C：数组的长度在声明时必须明确指定，并且是固定的，不能动态改变。

   Java：数组的长度可以在运行时动态创建和改变。

2. **内存管理**：

   C：数组是通过指针来访问和管理的，需要手动分配和释放内存。程序员需要负责确保足够的内存空间用于存储数组元素，并手动释放内存以避免内存泄漏。

   Java：数组是通过引用来访问和管理的，内存管理由Java虚拟机（JVM）自动处理，包括内存的分配和垃圾回收。

3. **异常处理**：

   C：数组越界访问可能导致未定义的行为，例如访问不存在的数组元素或者访问超出数组边界的位置。

   Java：数组越界访问会抛出 `ArrayIndexOutOfBoundsException` 异常，可以通过异常处理机制进行捕获和处理。

4. **多维数组支持**：

   C：多维数组是通过数组的数组来实现的，例如二维数组是数组的数组。

   Java：提供了直接支持多维数组的语法，可以使用类似于 `int[][]` 的语法直接声明和操作多维数组。

5. **功能和方法**：

   C：数组是一组连续的内存单元，没有对象的特性，只能通过下标访问元素，没有内置的方法或属性。

   Java：数组是对象，继承自 `java.lang.Object` 类，因此可以使用数组相关的方法和操作，例如 `length` 属性获取数组长度，`clone()` 方法复制数组等。
