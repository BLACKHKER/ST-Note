## C++ Based

### 一、基础项目构建

#### 1.1 文件类型

##### 1.1.1 .h(头文件)

头文件**一般**定义函数的返回值、函数名、0参数类型以及参数个数，它可以定义函数体，但是会使链接过程变得复杂

**实例**

*Log.h*(定义函数体)

```c++
void log(const char* message)
{
    std::cout << message << std::endl;
}
```

*Log.h*(仅定义函数结构)

```c++
void log(const char* message);
```

如果定义了函数体却没有做特殊处理，那么在多个文件引入该头文件时，会造成函数重定义；

原因是`#include`的实现原理：编译阶段预处理器打开这个文件，然后阅读文件并将文件内容**粘贴**到你的文件中。

例如：

*Log.cpp*

```c++
#include <iostream>

#include "Log.h"

void initLog()
{
    log("initialized Log");
}
```

*Main.cpp*

```c++
#include <iostream>

#include "Log.h"

int main()
{
    log("Start");
    std::cin.get();
}
```

实际效果：

*Log.cpp*

```c++
#include <iostream>

/* Log.h的内容直接复制粘站 */
void log(const char* message)
{
    std::cout << message << std::endl;
}

void initLog()
{
    log("initialized Log");
}
```

*Main.cpp*

```c++
#include <iostream>

/* Log.h的内容直接复制粘站 */
void log(const char* message)
{
    std::cout << message << std::endl;
}

int main()
{
    log("Start");
    std::cin.get();
}
```

重复定义了Log函数，报错。解决方案有几种：

*Log.h*

```c++
#pragma once

/* 
    将函数修改成static，修改后log函数只能是内部函数；
    static关键字在头文件中的作用与在源文件中的作用是不同的
    头文件中，将函数定义为static只是将其链接属性设置为内部链接，以避免在不同的源文件中出现重复定义的错误。
    函数一样会被粘贴过来，但是函数是static修饰的，静态的只在当前源文件可见，就不会跟其他源文件的函数冲突。
*/
static void log(const char* message)
{
    std::cout << message << std::endl;
}

/* inline，获取实际的函数体，并将函数调用替换为函数体 */
inline void log(const char* message)
{
    std::cout << message << std::endl;
}

/* main函数会变成这样 */
int main()
{
    /*
        log("Start");
        std::cin.get();
    */
    
    std::cout << "Start" << std::endl;
    std::cin.get();
}
```

###### #pragma once

首先，所有`#`开头的，都是预处理指令；

它本质上是一个被发送到编译器或预处理器的指令，作用是只包括这个文件一次：

监督这个头文件，防止被重复包含，放到一个翻译单元(.cpp)中。

###### <>和""的区别

告诉编译器不同的搜寻路径，<>表示头文件在项目里的某个位置，""则表示在当前文件的位置目录中寻找指定的头文件。 所以自己定义的一般使用""表示，系统函数使用<>表示。

例如当前文件A.cpp在A:/Study/std/A.cpp下，头文件如果也在std目录，直接引入：

#include "A.h"，如果在上一级：#include "../A.h"，以此类推。

**总结**

头文件中建议定义函数的结构，而不定义函数的内容，防止函数的重定义。

C++的系统函数没有后缀名，为了区分C的系统函数：

```c++
/* C标准库 */
#include <stdio.h>
/* C++标准库 */
#include <iostream>
```



##### 1.1.2 .c(源代码文件)

源代码编写的文件，包括函数、变量等





#### 1.2 编译与链接

##### 1.2.1 编译(Compile)

> 参考编译原理(书) TODO
>
> 编译是针对一个源文件(.cpp)的，有多少个源文件就需要编译多少次，生成对应个数的目标文件**(.obj)**

###### 为什么会有编译

以下是二进制表示输出到控制台"VIP会员"的命令

```v
指令(输出)    V        I        P            会                员
10110000 10101011 00110001 00011100 00110011 00111110 01010011 11110000
```

二进制效率过于低下，所以有了编程语言来简化这个步骤，不需要编写二进制指令了；

但是CPU只执行二进制指令，那么就有了一个工具，**编译器(Compiler)**，由编译器将代码转换成二进制的格式。

编译器能够识别代码中的关键字和特定的语法，按照代码的思路转换成二进制代码，这个过程就是**编译(Compile)**

C语言的编译器由很多种，取决于平台：

| 平台      | 编译器     | 编译生成格式 |
| --------- | ---------- | ------------ |
| Windows   | Visual C++ | .obj         |
| Linux     | GCC        | .o           |
| Unix(Mac) | LLVM/Clang |              |

C++编译后生成一个**目标文件(.obj)**文件，这个文件是二进制格式，跟可执行文件.exe是一样的；

###### 为什么编译不直接生成可执行文件

1. 模块化编译：将程序分为多个编译单元（源文件）可以提高代码的可维护性和编译的效率。每个编译单元可以独立地进行编译，生成对应的目标文件。这种模块化的编译方式使得只有在需要时才需要重新编译修改的部分，而不必重新编译整个程序。这对于大型项目来说特别重要。
2. 链接过程：生成目标文件是为了后续的链接过程。链接器将多个目标文件（以及必要的库文件）合并在一起，解决符号引用、进行地址重定位等操作，生成最终的可执行文件。链接过程需要将目标文件与系统组件（如标准库和动态链接库）结合起来，以创建一个完整的可执行文件。
3. 可移植性：生成目标文件可以使得代码在不同的平台上进行链接和执行。目标文件是与特定平台无关的中间格式，可以在不同的操作系统和硬件上进行链接，以生成适用于该平台的可执行文件。

编译只是将代码变成CPU可直接执行的二进制形式，它还需要和系统组件(标准库、动态链接库)结合起来，这些组件是必须的。组件可以理解为系统API或自己写的函数，函数在不同的.cpp文件中相互引用，就需要**链接(Link)**

###### 运行原理

1. 预处理

编译器执行时，首先会对代码进行**预处理**，也就是说所有的预处理语句优先执行。列如`#include`；

它指定了想要包含的文件，然后预处理器打开这个文件，然后阅读文件并将文件内容粘贴到你的文件中。

**实例**

*BHK.h*

```c++
}
```

*Main.cpp*

```c++
int main()
{
    int a = 10;
    int b = 88;
    int result = a * b;

    return result;
/* 主函数少了一个括号，一样可以正常运行，引入的BHK.h代替了括号 */
#include "BHK.h"
```

2. 生成目标文件

预处理之后剩余的代码会进行记号化和解析，把代码整理成编译器能够理解和推理的格式；或者说将代码转换成常量数据和各种指令。最后变成一个**抽象语法树**，它是代码整个执行流程的一种表示。最后根据这个抽象语法树生成二进制代码，机器码。

.cpp文件我们称为**翻译单元**，每个翻译单元生成一个目标文件(.obj)。



##### 1.2.2 链接(Link)

链接在运行或build时才发生，编译不会链接。

链接其实是一个"打包"的过程，将所有目标文件整个成一个可执行文件，这个工作交给**链接器(Linker)**

链接器的工作是找到符号和函数的位置，连接函数，将多个源文件中的函数调用整合起来。

在build整个项目时，所有文件都会被编译。链接器会找到正确的函数的定义位置，并将函数定义(函数体)导入到声明该函数的文件中，供其他文件使用。如果找不到函数定义，就报链接错误，“无法解析的外部符号”



---



### 二、数据类型

#### 2.1 整型

##### 2.1.1 short

短整型，占用2个字节



##### 2.1.2 int

整型，占用二或四个字节，一般为四个字节，占用大小取决于编译器。一些嵌入式系统中的编译器可能将int为二个字节。

对于有符号的 `int` 类型，其取值范围为 `-2147483648` 到 `2147483647`。

对于无符号的 `int` 类型（也称为 `unsigned int`），它的取值范围从 `0` 到 `4294967295`。

取值范围分别是2^31 - 1



##### 2.1.3 long

长整型，占用4或8个字节，在32位平台上占用4个字节，而在64位平台上占用8个字节，也就是说大小取决于编译器。



##### 2.1.4 long long int

长长整型，占用8个字节，简写为long long





#### 2.2 浮点数

##### 2.2.1 float

单精度浮点数，占用4个字节



##### 2.2.2 double

双精度浮点数，占用8个字节





#### 2.3 字符型

##### 2.3.1 char

字符，在不同编码中占不同字节：ASCII占1字节，UTF-8占1-4字节(中文等非ASCII占3-4字节)

C++对待字符通过ASCII字符进行文本编码，一个字符就是一个字节

```c
/* 单引号 */
char en = 'a'
```



##### 2.3.2 char*/char[]

字符串，在C++中，底层使用字符数组保存字符串，字符串末尾使用`\0`作为结束标志。

![image-20231127153046112](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231127153046112.png)

```c++
/* 
    char*在C++11中被弃用，但是还是可以使用，编译器底层进行了优化
    其实可以不使用const，不想去改变这些的值，所以使用const，VS中可能会报错必须使用const
    项目-属性-C/C++-语言-符合模式调到否即不报错
*/
const char* str2 = "Blackhker";

/* 保存字符串时 双引号 长度为字符个数 + 1(7)多了一个\0 */
char str[] = "String";

/* 保存字符数组时 花括号 长度为字符个数(6) */
char arr[] = {'a', 'b', 'c', 'd', 'e', 'f'};
```

> <font color="#f40">注意：</font>两种类型打印时的效果不同，因为数组保存字符串时自动拼接一个结束符`\0`，而数组保存字符数组不会自动拼接结束符(空终止字符)`\0`，系统判断字符串是否结束是以\0为基准，所以会把数组`arr`的内存后面的数据也打印出来，直到遇到`\0`为止
>
> ```c++
> #include <iostream>
> 
> int main()
> {
>     char str[] = "String";
>     char arr[6] = { 'a', 'b', 'c', 'd', 'e', 'f' };
>     
>     /* 空终止字符的两种表示 */
>     char arr2[7] = { 'a', 'b', 'c', 'd', 'e', 'f' , '\0' };
>     char arr3[7] = { 'a', 'b', 'c', 'd', 'e', 'f' , 0 };
>     
>     /* 输出很多其他乱码，因为到空终止字符才结束 */
>     std::cout << arr << std::endl;
>     str[2] = 'X';
> 
>     return 0;
> }
> ```
>
> ![image-20231229165332509](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231229165332509.png)



##### 2.3.3 BasicString

> C++中使用字符串。建议使用std::string

C++标准库中有一个String类，底层是一个模板类BasicString，String则是该模板类的模板版本

它提供了很多操作字符串的API，以及新的字符串创建方式，还有一个WString(weight String)宽字符串

还有很多数据结构，也建议使用自己编写的String实现

```c++
#include <iostream>
#include <string>

int main()
{
    std::string str = "123";

    std::cout << str << std::endl;

    std::cin.get();

    return 0;
}
```





#### 2.4 布尔

> 在内存中，布尔依然是需要分配一个字节的，虽然一个比特1/0即可以表示true/false，但是我们寻址的时候，是按字节寻址(8bit)，所以底层的处理是一个字节存储八个bool类型的值，这样充分使用空间。

##### 2.4.1 bool

boolean，占用一个字节(实际为一个比特)，有两个值：true/false。

在C++中，非零即为真，一个布尔类型的变量，值为true的时候，打印输出1；反之，输出0。





#### 2.5 数组

> 处理相同类型的多个元素，因为是连续的内存，数组被定义并初始化后，大小是固定的，不可修改。

##### 2.5.1 定义

###### 在栈上创建数组

```c++
数据类型 数组名[数组大小];
数据类型 数组名[] = {元素A, 元素B, 元素C...};
数据类型 数组名[数组大小] = {元素A, 元素B, 元素C...};
```

###### 在堆上创建数组

> 因为栈数组的生命周期只有一个当前函数，出了当前函数就释放，所以需要堆数组
>
> 使用场景就是跨方法使用数组的时候，比如将一个数组作为返回值返回，这个数组是这个函数创建的，就需要使用new在堆上创建数组。

```c++
/* 创建一个在堆上的数组 */
数据类型* 数组指针名 = new 数据类型[数组大小];
/* 从堆上删除(释放)该数组 */
delete[] 数组指针名;
```

###### 使用官方的array创建数组

> 建议使用，比原始数组更安全

```c++
std::array<数据类型, 数组大小> 数组名;
```

**实例**

```c++
#include <iostream>
#include <array>

int main()
{
    /* 在栈上创建数组 */
	int example[5];
	int example2[] = { 1, 2, 3 };
	int example3[5] = { 1, 2, 3 };

    /* 在堆上创建数组 */
    int* example4 = new int[5];
    delete[] example4
        
    /* C++11创建数组，注意引入array包 */
    std::array<int, 5> example5;
    /* array包数组初始化 */
    for(int i = 0; i < example5.size(); i++)
    {
        example5[i] = 2;
    }
     
	std::cin.get();
}
```



##### 2.5.2 访问

数组下标(索引)是从0开始，可以理解为偏移，一个数组是连续的一块内存，分割成好几份，第一份对于当前内存的偏移量是0，所以数组第一个元素的下标(索引)就是0，最后一个元素的下标就是数组大小 - 1。

如果访问数组不存在的下标，C++称为**内存访问违规**，也就是Java的下标越界异常

```c++
#include <iostream>

int main()
{
	int example[5];
	/* 给数组的第一个元素赋值 */
	example[0] = 2;
	example[4] = 4;

	/* 数组元素给变量初始化 */
	int a = example[0];

	/* 输出元素的值 */
	std::cout << example[0] << std::endl;
	/* 输出数组所在的地址 */
	std::cout << example << std::endl;

	std::cin.get();
}
```

###### 指针访问/操作

> 一个指针+int x的位置，取决于该指针的指针类型，类型大小 * x就是实际该指针要移动的字节数

```c++
#include <iostream>

int main()
{
    int example[5];
    int* ptr = example;

    /* 给数组的第一个元素赋值 */
    example[0] = 2222222;
    example[4] = 4;

    /* 初始化整个数组 */
    for (int i = 0; i < 5; i++)
    {
        example[i] = 2;
    }

    /*
        移动指针的位置，向后移两位，本质上是移动8个字节
        因为是int类型的指针，2(位) * 4(字节) = 8
    */
    *(ptr + 2) = 6;

    /* 输出元素的值(6) */
    std::cout << example[2] << std::endl;
    /* 输出数组所在的地址 */
    std::cout << example << std::endl;

    std::cin.get();
}
```



##### 2.5.3 标准数组

C++11里面定义了一个标准的数组：`std::array`，它是一个内置的数据结构



##### 2.5.4 其他问题

C++<font color="#f40">没有和数组大小相关的概念</font>，例如array.size()；是没有的，可以使用sizeof(数组名)获取数组内部的元素使用了多少空间。

```c++
/* 栈数组 */
数组元素类型 count = sizeof(数组名) / sizeof(数组元素类型);
/* 堆数组得到的是指针的大小 */
数组元素类型 size = sizeof(数组指针) / sizeof(数组元素类型);
```

所以需要手动维护一个数组大小的变量：

```c++
/* constexpr关键字声明常量表达式，在类中的常量表达式必须是静态的。 */
static constexpr int exampleSize = 5;
int example[exampleSize]
```



---



### 三、函数

#### 3.1 函数定义

**实例**

functions.h

.h头文件定义函数的返回值、函数名、参数类型、参数个数，类似Java的接口。

> ```c++
> #ifndef _FUNCTIONS_H
> #define _FUNCTIONS_H
> ...
> #endif 
> ```
>
> 这种结构是头文件的保护机制，作用是确保同一个头文件不会被多次包含，以防止重复定义和编译错误。
>
> 一个头文件被多次包含时，编译器会对其中的内容进行重复处理，导致重复定义的错误。在C++中，可以使用`#pragma once`代替，但是它是非标准的预处理指令，可能不兼容。

```c++
#ifndef FUNCTIONS_H
#define FUNCTIONS_H

int multiply(int a, int b);
void printMessage();

#endif
```

functions.c

.c源文件定义函数的具体执行逻辑，类似于Java的接口实现类，

```c++
#include <stdio.h>
#include functions.h

int multiply(int a, int b)
{
    return a * b;   
}

void print_message()
{
    std::cout << "Message" << std::endl;
    std::cin.get();
}
```

main.cpp

> 其他文件就可以通过引入头文件(.h文件)，来调用其他文件中定义的函数

```c++
#include functions.h

int main()
{
    int sum = multiply(1, 2);
    print_message();
}
```





#### 3.2 函数声明

> 函数声明可以使用#include头文件的形式替代

##### 3.2.1 概念

一个函数引用外部函数时，需要进行一个预声明，来表示这个函数是由外部引用的，不在本文件中

**实例**

Main.cpp

```c++
#include <iostream>

/* 预声明Log是一个函数，定义在其他文件中 */
void Log(const char*);
/* 形参参数名可以省略，但建议加上，便于提高维护性 */
void Log(const char* message);

int main()
{
    /* 日志打印 */
    Log("Hello World!");
    std::cin.get();
}
```

Log.cpp

```c++
#include <iostream>

void Log(const char* message)
{
    std::cout << message << std::endl;
}
```



##### 3.2.2 总结

函数声明会告诉编译器，哪些东西虽然没有在当前文件定义，但是是在其他文件中定义的；

编译器其实并不确定在其他文件中是否真的定义了，但声明了编译器便不再报错。

那么编译器是如何运行到正确的代码的？解决这个问题的，就是**链接(Linking)**



---



### 四、流程控制

> 流程控制包含：顺序结构、选择(分支)结构、循环结构
>
> 条件语句、if语句、分支语句，基于条件语句评估后执行不同的分支语句(true/false)
>
> 底层对应不同的内存块，跳到不同的内存块开始执行指令，所以if语句和分支语句有很大的内存开销。

#### 4.1 分支

> C++中不同于C，它有布尔类型，if的参数也是布尔

##### 4.1.1 if...else

> if底层只是对参数进行检查，判断它是否为0，为0即为false

```c++
if(false) -- false
if(true) -- true
```

**实例1**

基本数据类型的判断

```c++
#include <iostream>

#include "Log.h"

int main()
{
    int x = 5;
    /* 
        比较x是否等于5，“==”是equals比较的是两个地址保存的二进制数，逐位比较(bit) 
        比较两个数是否相等，本质上是获取他们四个字节的内存，然后比较内存中每个比特位是否相等
    */
    bool flag = x == 5;
    if (flag)
    {
        log("true");
    }
    else
    {
        log("false");
    }

    std::cin.get();
}
```

**实例2**

指针类型判断

```c++
#include <iostream>

#define LOG(message) std::cout << message << std::endl;

int main()
{
    /* 
        nullptr是一个关键字，表示一个不指向任何有效对象或函数的指针
        类型为 nullptr_t，并且可以隐式地转换为任意指针类型
    */
    const char* ptr = nullptr;
    if (ptr)
    {
        LOG(ptr);
    }
    else
    {
        LOG("ptr is NULL!");
    }

    std::cin.get();
}
```



##### 4.1.2 if...else if

> else if不是c+的关键字，本质上是else嵌套了if，上面的if执行了，那么elseif就不会执行

```c++
if(...)
{
    ...
}
else if(...)
{
    ...
}
```

else...if本质上是：

```c++
if(...)
{
    ...
}
else
{
    if(...)
    {
        ...
    }
}
```

**实例**

```c++
#include <iostream>

#define LOG(message) std::cout << message << std::endl;

int main()
{
    const char* ptr = "Hello";
    if (ptr)
    {
        LOG(ptr);
    }
    /*
        只要执行了一个if，后面的都不执行，所以else if不会执行，只打印一个Hello;
        如果是这样，那么都执行，本质上是两个if：
        if(ptr == "Hello")
        {
            LOG("Ptr is Hello!");
        }
    */
    else if(ptr == "Hello")
    {
        LOG("Ptr is Hello!");
    }
    else
    {
        LOG("Ptr is NULL!");
    }

    std::cin.get();
}
```





#### 4.2 循环

##### 4.2.1 for

> 循环的条件判断不建议写<=、>=，影响性能，因为做的是小于以及等于的比较，多了一步运算

```c++
for(循环变量初始化; 条件判断condition; 结束后执行的语句)
{
    /* TODO循环体 */
}
```

**实例**

```c++
#include <iostream>

#define LOG(message) std::cout << message << std::endl;

int main()
{
	for (int i = 0; i < 5; i++)
	{
		LOG("Hello World!");
	}

    std::cin.get();
}
```

除了条件判断，其他的都可以省略，写在其他位置：

```c++
#include <iostream>

#define LOG(message) std::cout << message << std::endl;

int main()
{
	int i = 0;
	for ( ; i < 5; )
	{
		LOG("Hello World!");
		i++;
	}

    std::cin.get();
}
```

因为条件判断本质上是布尔，也可以这么写：

```c++
#include <iostream>

#define LOG(message) std::cout << message << std::endl;

int main()
{
    int i = 0;
    bool condition = true;
    for ( ; condition; )
    {
        LOG("Hello World!");
        i++;

        if (!(i < 5))
        {
            condition = false;
        }
    }

    std::cin.get();
}
```



##### 4.2.2 while

```c
while(条件判断condition)
{
    /* TODO循环体 */
}
```

**实例**

```c++
#include <iostream>

#define LOG(message) std::cout << message << std::endl;

int main()
{
    int i = 0;
    
    while (i < 5)
    {
        LOG("Hello World!");
        i++;
    }

    std::cin.get();
}
```



##### 4.2.3 do...while

```c
do
{
    /* 循环体 */
} while(条件判断condition);
```

**实例**

```c++
#include <iostream>

#define LOG(message) std::cout << message << std::endl;

int main()
{
    int j = 0;
    
    do
    {
        LOG("Hello World!");
        j++;
    } while (j < 5);

    std::cin.get();
}
```



##### 4.2.4 continue/break

> 同Java

```c
/* 跳出此次循环 */
continue;

/* 跳出循环 */
break;
```



---



### 五、指针/引用

#### 5.1 指针

##### 5.1.1 概念

指针 == 内存地址，它是一个在内存中保存地址的整数；

变量在内存中对应的地址，在C++语言中可以用一种特殊的变量储存，这个变量就是指针；

内存单元(参考计算机组成原理)每个字节都有编号，这个编号就是内存地址，内存地址也称为指针；那么储存这个地址的变量就是指针变量

```c++
data_type data_name = data;
data_type *p_name = &data_name;
```

**实例**

```c++
#include <iostream>

#define LOG(message) std::cout << message << std::endl;

int main()
{

    /* 定义空指针 */
    void* ptr = NULL;

    /* C++11新类型定义空指针 */
    void* ptr2 = nullptr;

    /* 使用new关键字申请了堆中8字节的内存(char数组)，返回一个指向该数组的指针 */
    char* buffer = new char[8];

    /* memset()使用指定的数据填充内存块 */
    memset(buffer, 0, 8);

    /* 使用delete释放内存 */
    delete[] buffer;

    std::cin.get();
}
```





#### 5.2 引用

##### 5.2.1 概念

引用是指针的包装与简化，它是一个语法糖，让指针更易于理解。它类似于给一个变量起别名。

**实例**

```c++
#include <iostream>

#define LOG(message) std::cout << message << std::endl;

int main()
{
    int a = 5;

    /* 定义一个引用，&是类型的一部分，int&是一个整体 */
    int& ref = a;

    /* 更改引用的值 */
    ref = 2;

    /* 输出2，因为引用ref本质上是指向a的指针 */
    LOG(a);

    std::cin.get();
}
```



##### 5.2.2 使用场景

调用一个函数，使用值传递的方式，函数不会对实参做改变：

```c++
#include <iostream>

#define LOG(message) std::cout << message << std::endl;

void increment(int num)
{
    /* 这里的num本质上是复制后的值 */
    num++;
}

int main()
{
    int a = 5;

    /* 定义一个引用，&是类型的一部分，int&是一个整体 */
    int& ref = a;

    /* 值传递，拷贝变量的值，复制到函数中 */
    increment(a);

    /* 打印5，因为给函数的是复制的值，而不是a本身 */
    LOG(a);

    std::cin.get();
}
```

那么通过指针传递变量本身(地址)给函数，就可以修改a的值：

```c++
#include <iostream>

#define LOG(message) std::cout << message << std::endl;

void increment(int* num)
{
    /* 
        这里的num是变量a的引用(地址)
        要加上*号，表示操作指针(地址)的内容，而不是地址本身
        不加的话就变成了更改num的地址，+1(对地址递增)
        给指针加括号的原因是想要先引用，再自增
    */
    (*num)++;
}

int main()
{
    int a = 5;

    /* 指针(地址)传递 */
    increment(&a);

    /* 打印6 */
    LOG(a);

    std::cin.get();
}
```

指针还是很麻烦，使用引用来简化：

```c++
#include <iostream>

#define LOG(message) std::cout << message << std::endl;

void increment(int& num)
{
    /* 引用简化 */
    num++;
}

int main()
{
    int a = 5;

    /* 引用传递，拷贝变量的值，复制到函数中 */
    increment(a);

    /* 打印5，因为给函数的是复制的值，而不是a本身 */
    LOG(a);

    std::cin.get();
}
```



##### 5.2.3 注意事项

引用一旦创建，就不能改变引用的东西。它不像指针，可以让一个指向x的值去指向y(本质上是更改保存的地址)

可以理解为引用是指针常量，一旦确定了指向的地址不可更改。类似于final修饰的指针；

如果一定要更改，那么使用指针。



---



### 六、面向对象

#### 6.1 类

##### 6.1.1 概念

同Java一致，对于C++来说，面向对象不是强制的，它只是提供了一种编写代码的方式。

```c++
class 类名
{
可见性范围:
    属性类型 属性名;
};
```

**实例**

> 日志类，注意这里的public是重复的，也就是说可以写多个，取决于自己喜好

```c++
#include <iostream>

class Log
{
public:
    /* 日志等级为错误(0) */
    const int logLevelError = 0;
    /* 日志等级为警告(1) */
    const int logLevelWarning = 1;
    /* 日志等级为信息 */
    const int logLevelinfo = 2;
private:
    /* 日志等级，私有的类成员变量用m当作前缀 */
    int m_LogLevel;
public:
    function...
}
```



##### 6.1.2 类&结构体

它们没有什么区别，只有一个可见度的区别，类的所有成员(属性)是默认private的，而结构体不是。

使用哪个取决于编码风格，以及具体的使用场景：

1. 通常结构体用于表示一整组数据，例如一个向量用两个浮点数表示(大小、方向)；这时就使用结构体，因为它是抽象的概念，不具备其他功能(方法)。而类则是有具体的真实生活中的实例，才去使用。因为它有某种行为需要使用方法进行修饰描述。

2. 有继承需求的情况，使用类，像Java一样，需要一个完整的类层次结构，或者继承结构等。



##### 6.1.3 Log类(v1)

```c++
#include <iostream>

class Log
{
public:
    /* 日志等级为错误(0) */
    const int logLevelError = 0;
    /* 日志等级为警告(1) */
    const int logLevelWarning = 1;
    /* 日志等级为信息(2) */
    const int logLevelInfo = 2;

private:
    /* 日志等级，私有的类成员变量用m当作前缀 */
    int m_LogLevel;
public:

    /**
     * 设置日志等级
     * @param level 代表等级的数字
     */
    void setLevel(int level)
    {
        m_LogLevel = level;
    }

    /**
     * 错误日志
     * 
     * @param message 日志信息
     */
    void error(const char* message)
    {
        /* 如果设置的日志级别大于等于当前日志的级别，才打印该日志 */
        if (m_LogLevel >= logLevelError)
        {
            std::cout << "[ERROR]:" << message << std::endl;
        }
    }

    /**
     * 警告日志
     *
     * @param message 日志信息
     */
    void warn(const char* message)
    {
        if(m_LogLevel >= logLevelWarning)
        {
            std::cout << "[WARNING]:" << message << std::endl;
        }
        
    }

    /**
     * 信息日志
     *
     * @param message 日志信息
     */
    void info(const char* message)
    {
        if (m_LogLevel >= logLevelInfo)
        {
            std::cout << "[INFO]:" << message << std::endl;
        }
    }
};

int main()
{
    Log log;
    log.setLevel(log.logLevelWarning);
    log.warn("Hello World!");
    std::cin.get();
}
```













#### 6.2 对象

##### 6.2.1 概念

对象是类的具体概念，或者说是类的实例，跟Java一样；

对象中的属性跟Java不同，它默认所有属性是私有的，需要手动给属性分配不同的可见性范围；

这意味着只有类中的方法才能访问对象中的变量(属性)。

C++创建对象，有两种：使用/不使用new，区别是对象的存储位置(堆/栈)



##### 6.2.2 创建

不使用new是在栈上创建，这种方式会在当前作用域中自动分配对象的内存，并在作用域结束时自动销毁对象：

```c++
类名 对象名(实例名);
```

**实例**

```c++
/* 创建对象 */
ClassName objectName;

/* 对象调用对象方法 */ 
objectName.methodName();

/* 访问对象属性 */
objectName.properties = x;

/* 不需要手动关闭对象 */
```

使用new是在堆上创建，这种返回一个指向对象的指针。

这种方式需要手动释放内存，并且需要在不再需要对象时使用delete运算符释放相关内存。

```
类名* 指针名 = new 类名();
```

**实例**

```c++
/* 使用 new 创建对象 */
ClassName* objectPtr = new ClassName();

/* 使用对象指针调用对象方法 */
objectPtr->methodName();

/* 使用对象指针访问对象成员 */
objectPtr->memberVariable;

/* 释放对象所占用的内存 */ 
delete objectPtr;
```





#### 6.3 方法

##### 6.3.1 概念

方法是类的行为，所以方法需要通过类对象(类的实例)去调用



##### 6.3.2 方法调用

###### 方法在类外部

```c++
#include <iostream>

#define LOG(message) std::cout << message << std::endl;

/**
 * 玩家类
 */
class Player
{
public:
    /* 坐标 */
    int x, y;

    /* 移动速度 */
    int speed;
};

/**
 * 移动方法
 * @param player 玩家对象
 * @param xa 玩家在x轴移动的距离
 * @param ya 玩家在y轴移动的距离
 */
void move(Player& player, int xa, int ya)
{
    /* 距离 * 移速确定最后的坐标 */
    player.x = xa * player.speed;
    player.y = ya * player.speed;
}

int main()
{
    Player player;
    move(player, 1, -1);

    std::cin.get();
}
```

###### 方法在类内部

```c++
#include <iostream>

#define LOG(message) std::cout << message << std::endl;

/**
 * 玩家类
 */
class Player
{
public:
    /* 坐标 */
    int x, y;

    /* 移动速度 */
    int speed;

    /**
     * 移动方法
     * @param player 玩家对象
     * @param xa 玩家在x轴移动的距离
     * @param ya 玩家在y轴移动的距离
     */
    void move(int xa, int ya)
    {
        /* 距离 * 移速确定最后的坐标 */
        x = xa * speed;
        y = ya * speed;
    }
};

int main()
{
    /* 在栈上创建对象 */
    Player player;

    /* 对象调用方法 */
    player.move(1, -1);

    std::cin.get();
}
```



##### 6.3.3 构造方法

类对象(实例)的初始化，如果不显式的赋值，这个对象的各个属性的值，是随机的。

属性值取决于给对象的该属性分配的内存块的值，所以类的内部需要一个方法，用于在创建对象的时候赋初值。相当于给保存该属性的内存块进行初始化。

###### 不使用构造

> 打印的值是内存空间的值，因为分配内存是随机的，所以值也是随机的

```c++
#include <iostream>

class Entity
{
public:
    float x;
    float y;

    void print()
    {
        std::cout << x << "," << y << std::endl;
    }
};

int main()
{
    Entity entity;
    entity.print();
    std::cin.get();
}
```

###### 模拟构造

> 手动调用模拟的构造方法，在创建类对象的时候进行属性的初始化

```c++
#include <iostream>

class Entity
{
public:
    float x;
    float y;

    void init()
    {
        x = 0.0f;
        y = 0.0f;
    }

    void print()
    {
        std::cout << x << "," << y << std::endl;
    }
};

int main()
{
    Entity entity;
    entity.init();
    entity.print();
    std::cin.get();
}
```

###### 构造实例

> 构造方法跟类名同名，没有返回值。分为无参构造、有参构造，默认生成一个无参构造；
>
> 构造方法会在创建对象时自动调用(包括new)，这也是构造方法跟普通方法的区别。
>
> 如果**没有创建对象**，仅通过类名**调用静态方法**，那么构造方法是**不会执行**的。

```c++
#include <iostream>

class Entity
{
public:
    float x;
    float y;

    /**
     * 无参构造
     */
    Entity()
    {
        x = 0.0f;
        y = 0.0f;
    }

    /**
     * 有参构造
     */
    Entity(float x1, float y2)
    {
        x = x1;
        y = y2;
    }

    void print()
    {
        std::cout << x << "," << y << std::endl;
    }
};

int main()
{
    /* 无参构造对象 */
    Entity entity;
    entity.print();

    /* 有参构造对象 */
    Entity entity2(1.2f, 3.4f);
    entity2.print();

    std::cin.get();
}
```

###### 删除默认构造

> 构造方法 = delete;

```c++
#include <iostream>

class Log
{
public:

    Log() = delete;

    static void write()
    {
        std::cout << "Success!" << std::endl;
    }
};

int main()
{
    /* 无法创建实例，默认的构造方法被删除 */
    Log log;

    std::cin.get();
}
```

###### 复制构造

TODO

###### 移动构造

TODO

###### 初始化列表

```c++
class Player
{
private:
    int m_age;
	std::string m_name;
public:

	/**
	 * 构造函数
	 * 构造函数的初始化列表(: 后面的部分)用于初始化 Player 类的成员变量 m_name，
	 * 通过将传入的 name 参数赋值给 m_name 来初始化成员变量。
	 * 多个属性用逗号分隔
	 */
	Player(int age, const std::string& name)
		: m_age(age), m_name(name), {}
};
```



##### 6.3.4 析构方法(函数)

> 构造方法在创建类对象时调用，相反的，析构方法在销毁对象是调用；
>
> 它实现的卸载变量，并清理你使用过的内存。
>
> 如果不清理释放内存，在对象过多的时候，会造成内存泄漏。

```c++
~类名()
{
   ...
}
```

**实例**

```c++
#include <iostream>

class Entity
{
public:
    float x;
    float y;

    /**
     * 无参构造
     */
    Entity()
    {
        x = 0.0f;
        y = 0.0f;
        std::cout << "Created Entity" << std::endl;
    }

    /**
     * 有参构造
     */
    Entity(float x1, float y2)
    {
        x = x1;
        y = y2;
    }

    /**
     * 析构方法
     */
    ~Entity()
    {
        std::cout << "Destroyed Entity" << std::endl;
    }

    void print()
    {
        std::cout << x << "," << y << std::endl;
    }
};

void function()
{
    /* 在栈上创建一个对象，函数执行结束则该对象自动调用析构函数 */
    Entity e;
    e.print();

    std::cout << "==================" << std::endl;

    /* 在堆上创建对象，不会自动调用析构函数，需要手动释放内存 */
    Entity* e2 = new Entity();
    /* 指针调用使用箭头操作符 */
    e2->print();
    /* 手动释放内存 */
    delete e2;
}

int main()
{
    function();

    std::cin.get();
}
```

###### 手动调用

> 手动调用析构函数不会删除对象，只是单纯的执行代码

```c++
#include <iostream>

class Entity
{
public:
    float x;
    float y;

    /**
     * 析构方法
     */
    ~Entity()
    {
        std::cout << "Destroyed Entity" << std::endl;
    }
};

void function()
{
    /* 手动调用析构函数，它会执行两次 */
    e.~Entity();
}

int main()
{
    function();

    std::cin.get();
}
```





#### 6.4 继承

继承跟Java一样，子类继承父类的所有**非私有**属性/方法，解决了代码重复度高的问题

可以理解为子类是父类的超集，包含一切父类的东西(前提是公开的public)并且有所**扩展**。

**实例**

```c++
#include <iostream>

/**
 * 实体类，表示所有角色都具备的功能，例如移动
 */
class Entity 
{
public:

    /* 角色坐标 */
    float x = 0;
    float y = 0;

    /**
     * 角色移动方法
     * 
     * @param xa x轴移动距离
     * @param ya y轴移动距离
     * 
     * @return 
     */
    void move(float xa, float ya)
    {
        x += xa;
        y += ya;
    }
};

/**
 * 玩家类，继承角色类以实现移动的基础功能
 */
class Player : public Entity
{
public:
    /* 玩家名 */
    const char* name;


    /**
     * 打印玩家名方法
     * 
     * @return 
     */
    void printName()
    {
        std::cout << name << std::endl;
    }
};

int main()
{
    Player player;

    /* 子类实例调用父类的移动方法 */
    player.move(5.0f, 5.0f);

    /* 子类实例访问父类属性 */
    player.x = 6.0f;

    /* 打印6，5 */
    std::cout << player.x << "," << player.y << std::endl;

    std::cin.get();
}
```

证明子类包含父类的所有公开属性/方法的另一种方式：打印类的大小

```c++
#include <iostream>

/**
 * 实体类，表示所有角色都具备的功能，例如移动
 */
class Entity 
{
public:

    /* 角色坐标 */
    float x = 0;
    float y = 0;

    /**
     * 角色移动方法
     * 
     * @param xa x轴移动距离
     * @param ya y轴移动距离
     * 
     * @return 
     */
    void move(float xa, float ya)
    {
        x += xa;
        y += ya;
    }
};

/**
 * 玩家类，继承角色类以实现移动的基础功能
 */
class Player : public Entity
{
public:
    /* 玩家名 */
    const char* name;

    /**
     * 打印玩家名方法
     * 
     * @return 
     */
    void printName()
    {
        std::cout << name << std::endl;
    }
};

int main()
{
    /* 8，两个float各占4个字节 */
    std::cout << sizeof(Entity) << std::endl;

    /* 16，父类的8加上64位下指针char* name的8 */
    std::cout << sizeof(Player) << std::endl;

    std::cin.get();
}
```



#### 6.5 虚函数

> 虚函数引入了一种叫做动态联编的东西，通过虚函数表来实现编译；
>
> 所以虚函数有额外的内存开销，因为单独维护一个虚函数表，用来根据不同的实例对象分配正确的函数。基类中要有一个成员指针，指向这个虚函数表；
>
> 每次调用虚函数时，需要遍历整个虚函数表，来确定需要映射到那个函数；
>
> 性能有要求的情况下，尽量避免使用虚函数。

##### 6.5.1 父子方法重载

类似于Java，父子类方法重名(重载)的时候，子类对象调用方法遵循就近原则，调用子类方法

**实例**

```c++
#include <iostream>
#include <string>

class Entity
{
public:
    std::string getName()
    {
        return "Entity";
    }
};

class Player : public Entity
{
private:
    std::string m_name;
public:
    /**
     * 构造函数
     * 构造函数的参数初始化列表(: 后面的部分)用于初始化 Player 类的成员变量 m_name，
     * 通过将传入的 name 参数赋值给 m_name 来初始化成员变量。
     */
    Player(const std::string& name)
        : m_name(name) {}

    std::string getName()
    {
        return m_name;
    }
};

int main()
{
    Entity* e = new Entity();
    /* 父类实例调用父类方法，输出Entity */
    std::cout << e->getName() << std::endl;

    Player* p = new Player("Blackhker");
    /* 子类实例调用子类方法，输出Blackhker */
    std::cout << p->getName() << std::endl;

    std::cin.get();
}
```



##### 6.5.2 向上转型

如果想要**调用父类方法**，可以模仿类似于Java的**向上转型**

```c++
#include <iostream>
#include <string>

class Entity
{
public:
    std::string getName()
    {
        return "Entity";
    }
};

class Player : public Entity
{
private:
    std::string m_name;
public:
    /**
     * 构造函数
     * 构造函数的初始化列表(: 后面的部分)用于初始化 Player 类的成员变量 m_name，
     * 通过将传入的 name 参数赋值给 m_name 来初始化成员变量。
     */
    Player(const std::string& name)
        : m_name(name) {}

    std::string getName()
    {
        return m_name;
    }
};

int main()
{
    Entity* e = new Entity();
    /* 父类引用调用父类方法，输出Entity */
    std::cout << e->getName() << std::endl;

    Player* p = new Player("Blackhker");
    /* 子类引用调用子类方法，输出Blackhker */
    std::cout << p->getName() << std::endl;

    /* 类似于Java向上转型，将子类引用赋值给父类引用，还是会调用父类方法 */
    Entity* entity = p;
    /* 输出Entity */
    std::cout << entity->getName() << std::endl;

    std::cin.get();
}
```



##### 6.5.3 虚函数

某个函数需要根据父子类的不同实例，决定调用不同的函数时，这种情况，就需要虚函数

使用virtual关键字，声明该函数为虚函数：

```c++
#include <iostream>
#include <string>

class Entity
{
public:
    virtual std::string getName()
    {
        return "Entity";
    }
};

class Player : public Entity
{
private:
    std::string m_name;
public:
    /**
     * 构造函数
     * 构造函数的初始化列表(: 后面的部分)用于初始化 Player 类的成员变量 m_name，
     * 通过将传入的 name 参数赋值给 m_name 来初始化成员变量。
     */
    Player(const std::string& name)
        : m_name(name) {}

    std::string getName()
    {
        return m_name;
    }
};

/* 父类实例作为调用该方法的参数，子类作为参数时，调用的却是父类的方法 */
void printName(Entity* entity)
{
    std::cout << entity->getName() << std::endl;
}

int main()
{
    Entity* e = new Entity();
    /* 通过父类指针调用printName()，输出Entity */
    printName(e);

    Player* p = new Player("Blackhker");
    /* 通过子类指针调用printName()，也输出Entity */
    printName(p);

    /* 虚函数调用，在父类函数上加关键字virtual，Player子类指针调用,输出Blackhker */
    std::cin.get();
}
```

在C++11中新增了`override`关键字，表示子类重写了父类的同名方法，这样子类实例/指针调用方法的时候，会优先调用子类自己的方法，<font color="#f40">它不具备功能，只检验函数名是否跟父类相同，增加可读性</font>。

```c++
class Player : public Entity
{
private:
    std::string m_name;
public:
    Player(const std::string& name)
        : m_name(name) {}

    std::string getName()
        override
    {
        return m_name;
    }
};
```





#### 6.6 纯虚函数(接口)

> 纯虚函数用于在基类中定义一个没有实现的方法，然后强制子类去实现该方法；
>
> 类似于Java的接口，增加可读性，用于规范子类方法的定义，方法实现由子类解决；
>
> 跟接口的区别是创建实例，有纯虚函数的类不能直接创建实例，而要有一个实现该类(接口)所有纯虚函数的子类，创建该子类的实例。C++中没有接口的概念，只有类。
>
> **接口必须被实现，才能创建实例。**

##### 6.6.1 定义

```c++
virtual 返回值 方法名(方法参数) = 0;
```

**实例**

```c++
#include <iostream>
#include <string>

class Entity
{
public:
    virtual std::string getName() = 0;
};

class Player : public Entity
{
private:
    std::string m_name;
public:
    /**
     * 构造函数
     * 构造函数的初始化列表(: 后面的部分)用于初始化 Player 类的成员变量 m_name，
     * 通过将传入的 name 参数赋值给 m_name 来初始化成员变量。
     */
    Player(const std::string& name)
        : m_name(name) {}

    std::string getName()
        override
    {
        return m_name;
    }
};

void printName(Entity* entity)
{
    std::cout << entity->getName() << std::endl;
}

int main()
{
    /* 有纯虚函数的类，就是接口了，不能创建实例 */
    /*
        Entity* e = new Entity();
        printName(e);
    */

    /* 实现该类(接口)所有纯虚函数的子类，创建该子类的实例 */
    Entity* e2 = new Player("Blackhker");
    printName(e2);

    std::cin.get();
}
```



##### 6.6.2 多接口实现

```c++
class A
{
public:
    virtual std::string getClassName() = 0;
};

class B
{
public:
    /* 虚函数，表示类B的子类可以重写该函数，调用的时候根据对象所属的类，调用对应方法 */
    virtual std::string getName()
    {
        return "Entity";
    }
};

/**
 * 多接口实现，类C实现类A、B的纯虚拟函数
 */
class C : public A, B
{
private:
    /* 字符串类型的变量 */
    std::string m_param;
public:
    ...实现类A(接口)中定义的纯虚函数
}
```



##### 6.6.3 多重继承

A、B、C三个类依次继承，类外部有一个方法，调用该方法需要一个最上层的类A的对象的情况

```c++
#include <iostream>
#include <string>

/**
 * Printable 最上级父类
 */
class Printable
{
public:
    /* 纯虚函数，获取类名 */
    virtual std::string getClassName() = 0;
};

/**
 * Entity 继承Printable
 */
class Entity : public Printable
{
public:
    /**
     * 实现父类(接口)Printable的纯虚函数
     * 
     * @return Entity
     */
    std::string getClassName()
        override
    {
        return "Entity";
    }
};

/**
 * Player 继承Entity
 */
class Player : public Entity
{
private:
    std::string m_name;
public:
    Player(const std::string& name)
        : m_name(name) {}
    
    /**
     * 重写父类实现的方法getClassName()
     *
     * @return Player
     */
    std::string getClassName()
        override
    {
        return "Player";
    }
};

void print(Printable* obj)
{
    std::cout << obj->getClassName() << std::endl;
}

int main()
{
    /* 两个都输出Entity，因为getClassName只有Entity实现了，子类Player没有 */
    Entity* e = new Entity();
    print(e);

    Player* p = new Player("Blackhker");
    print(p);

    std::cin.get();
}
```



---



### 七、关键字

#### 7.1 extern

声明变量/函数，表示该变量/函数是在外部定义的，编译器会去其他翻译单元寻找这个变量/函数的定义

num.cpp

```c++
int num = 8;

void function()
{
    ...
}
```

main.cpp

```c++
#include <iostream>

/* 声明该变量是外部(其他翻译单元)定义的 */
extern int num;

/* 声明该变量是外部(其他翻译单元)定义的 */
extern void function();
```



#### 7.2 static

被static修饰的变量，保存在静态区中，所以仅占用一次内存且仅有一份。

##### 7.2.1 不同使用场景的含义

###### 在类或结构体外部

可以理解为**全局变量/函数**，跟C类似，被修饰变量/函数的外部链接属性就变成内部链接属性，像是被私有化了，就只能在本源文件(翻译单元)中使用，不能在其他源文件内使用。

> 建议定义外部变量/函数(全局变量/函数)时，多使用static修饰，因为编译器会**跨编译单元**进行链接，项目很大的时候很容易造成命名冲突。

**实例**

全局变量不可以重复，编译链接会报错重复定义(已经在其他翻译单元中定义了)；

如果加上static，那么这个全局变量在编译后，将只跟当前源文件(.cpp翻译单元)内部进行链接，

可以理解为私有化了，只有当前源文件的函数能看到该变量，那么`s_variable`就不会冲突了

static.cpp

```c++
static int s_variable = 5;

void function()
{
    ...
}
```

main.cpp

```c++
#include <iostream>

int s_variable = 8;

void function()
{
    ...
}

int main()
{
    std::cout << s_variable << std::endl;
    std::cin.get();
}
```

或者使用`extern`关键字声明，也会提示找不到s_variable的定义：

```c++
#include <iostream>

extern int s_variable;

int main()
{
    std::cout << s_variable << std::endl;
    std::cin.get();
}
```

###### 在类或结构体内部

> 下方示例的变量都是静态的。

类中的**局部变量/方法**被修饰，类的所有实例都共享该属性的内存

**实例**

1. 类中的静态方法访问静态属性

```c++
#include <iostream>

extern int s_variable;

struct Entity
{
    /* 静态成员变量声明 */
    static int a;
    static int b;

    /*
        void print()
        {
            std::cout << a << "," << b << std::endl;
        }
    */
    static void print()
    {
        std::cout << a << "," << b << std::endl;
    }
};

/* 
    类的静态成员必须在类外部定义
    成员类型 成员所在类::成员名(不赋初值)
    成员类型 成员所在类::成员名 = 值(赋初值)
*/
int Entity::a;
int Entity::b;

int main()
{
    Entity entity;
    entity.a = 8;
    entity.b = 88;

    /*
        Entity entity2 = { 888, 8888 }
    */

    Entity entity2;
    entity2.a = 888;
    entity2.b = 8888;

    /*
        两个entity打印相同数值888，8888
        因为它们共享一个内存地址，所以后赋值的会覆盖掉前面的；
    */
    /*
        entity.print();
        entity2.print();
    */

    /* 第二种调用，类似于Java的静态方法调用 → 类名::方法名 */
    Entity::print();
    Entity::print();

    std::cin.get();
}
```

2. 静态方法访问非静态属性

因为静态方法**没有类实例**，所以方法中不能直接写类的属性，应使用对象.属性的方式；

本质上非静态方法总是获取当前类的一个实例作为参数，所以可以直接访问该类的属性，因为调用的时候是：实例名(对象名).方法名，而静态方法更像是在类的外部定义了一个普通方法

> <font color="#f40">注意</font>：类中的静态方法不能直接访问该类非静态属性，同Java，类属性需要使用对象获取；

**错误示例**：

```c++
struct Entity
{
    /* 非静态成员变量声明 */
    int a;
    int b;

    static void print()
    {
        /* 这里报错，非静态成员引用必须与特定对象相对 */
        std::cout << a << "," << b << std::endl;
    }
};

int main()
{
    Entity entity;
    entity.a = 8;
    entity.b = 88;
    
    Entity entity2;
    entity2.a = 888;
    entity2.b = 8888;
    
    /*
        entity.print();
        entity2.print();
    */
    
    /* 第二种调用，类似于Java的静态方法调用：类名::函数名() */
     Entity::print();
     ENtity::print();
}
```

类中的静态方法类似于在外面定义了一个函数：

```c++
struct Entity
{
    /* 非静态成员变量声明 */
    int a;
    int b;    
};

void print()
{
    std::cout << a << "," << b << std::endl;
}
```

它找不到a、b是什么，所以静态方法没法直接访问类的非静态属性

**正确示例**：

```c++
struct Entity
{
    /* 非静态成员变量声明 */
    int a;
    int b;    
    
    /* 这也是非静态方法在编译时的实际效果，有一个隐藏的Entity类型的实例当作参数 */
    static void print(Entity entity)
    {
        std::cout << entity.a << "," << entity.b << std::endl;
    }
};
```



##### 7.2.2 局部静态

以下是一个普通的单例模式：

```c++
#include <iostream>

class Singleton
{
private:
	/* 定义一个私有静态指针变量 */
	static Singleton* s_instance;
public:
	/**
	 * 获取实例指针的函数
	 * 
	 * @return 对象的引用
	 */
	static Singleton& getInstance()
	{
		return *s_instance;
	}

	void hello()
	{
		std::cout << "Hello World!" << std::endl;
	}
};

Singleton* Singleton::s_instance = nullptr;

int main()
{
	Singleton s = Singleton::getInstance();
	s.hello();
}
```

使用局部静态来简化：

```c++
#include <iostream>

class Singleton
{
public:
	/**
	 * 获取实例指针的函数
	 * 
	 * @return 对象的引用
	 */
	static Singleton& getInstance()
	{
		/* 定义一个局部静态变量 */
		static Singleton instance;
		return instance;
	}

	void hello()
	{
		std::cout << "Hello World!" << std::endl;
	}
};

int main()
{
	Singleton s = Singleton::getInstance();
	s.hello();
}
```



##### 7.2.3 总结

```
静态方法调用类中的非静态属性时，需要指定一个实例来调用，因为非静态属性每个实例都有各自的内存空间，它不知道你要调用的是哪个实例(对象)的属性。
```



---



### 八、枚举

> 最主要的作用是提供一个语义化的常量定义方式，避免了魔法数字(各种Integer数字)

#### 8.1 定义

##### 8.1.1 无类型枚举

> 枚举不指定类型，默认32位整型，不指定值，默认第一位为0，以此类推

```c++
enum 枚举类型(名)
{
    枚举1,
    枚举2,
    枚举3
};
```

**实例**

> 这里的A不赋值默认为0，B2C3

```c++
enum Example
{
    A,
    B,
    C
};
```



##### 8.1.2 有类型枚举

> 本质存储一个Integer类型的数据，不需要32位，使用8位的char，节省空间

```c++
enum 枚举类型(名) : 数据类型
{
    枚举1,
    枚举2,
    枚举3
};
```

**实例**

```c++
enum Example : unsigned char
{
    A,
    B,
    C
};
```



##### 8.1.3 Log类(v2)

```c++
#include <iostream>

class Log
{
public:
    /* 日志枚举 */
    enum Level
    {
        /* 日志等级为错误(0) */
        LevelError = 0,
        /* 日志等级为警告(1) */
        LevelWarning,
        /* 日志等级为信息(2) */
        LevelInfo
    };
private:
    /* 日志等级，私有的类成员变量用m当作前缀 */
    int m_LogLevel;
public:
    /**
     * 设置日志等级
     * @param level 代表等级的数字
     */
    void setLevel(Level level)
    {
        m_LogLevel = level;
    }

    /**
     * 错误日志
     *
     * @param message 日志信息
     */
    void error(const char* message)
    {
        /* 如果设置的日志级别大于等于当前日志的级别，才打印该日志 */
        if (m_LogLevel >= LevelError)
        {
            std::cout << "[ERROR]:" << message << std::endl;
        }
    }

    /**
     * 警告日志
     *
     * @param message 日志信息
     */
    void warn(const char* message)
    {
        if (m_LogLevel >= LevelWarning)
        {
            std::cout << "[WARNING]:" << message << std::endl;
        }

    }

    /**
     * 信息日志
     *
     * @param message 日志信息
     */
    void info(const char* message)
    {
        if (m_LogLevel >= LevelInfo)
        {
            std::cout << "[INFO]:" << message << std::endl;
        }
    }
};

int main()
{
    Log log;
    log.setLevel(Log::LevelError);
    log.error("Hello World!");
    std::cin.get();
}
```



---



### 九、可见性(作用域)

> 可见性提高了代码的可读性，主要跟性能无关，好的设计是和可见性有很大关系的；
>
> 一个类内部的、仅自己使用的属性/方法都设计成private，仅public对外供外部调用的接口，其他人就只需要看这些public的属性/方法的实现就可以。
>
> 类似于单例模式，仅public一个创建单例实例对象的方法——**封装**

#### 9.1 概念

##### 9.1.1 private

私有，**只有/仅有**当前类可以访问这个变量/方法，其他类无法访问。

除了使用关键字`friend`来解决这个问题，它可以让类或者函数成为类的朋友(友元)，可以从类中访问私有成员



##### 9.1.2 protected

受保护，**只有/仅有**当前类的内部及其子类可以访问这个变量/方法，其他类无法访问。



##### 9.1.3 public

公开的，所有类可以访问这个变量/方法，其他类无法访问。





#### 9.2 默认可见性

##### 9.2.1 属性/方法

C++中所有类的属性/方法，不指定可见性的情况下，默认私有。

```c++
#include <iostream>

/* 两个类的属性可见性是一样的，虽然没有private，但是默认是私有的 */ 
class Entity
{
	int x;
	int y;
};

class Player : public Entity
{
private:
	int a;
	int b;
};

int main()
{

	std::cin.get();
}
```



##### 9.2.2 结构体

结构体的属性，默认public。
