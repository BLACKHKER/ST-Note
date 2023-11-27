## C - API

### 一、输入输出IO/字符串相关

#### 1.1 输入输出IO

##### 1.1.1 printf()

> 基础输出(打印)，打印数据到终端(控制台)
>
> - `*format`：格式控制字符串，可以理解为占位符，表示这里要输出的数据类型
>
>   占位符有%d|%f|%s|%p|%u|%c|%x...等很多，对应int、float、char[]、*p(指针)

```c
printf(const char *format, ...)
```

**实例**

> 注意：sizeof()函数的打印，占位符最好用%zu

```c
/* 字符数组(字符串) */
char name[] = "John";
/* 整型 */
int age = 25;
/* 单精度浮点 */
float height = 1.75;
/* 字符型 */
char grade = 'A';
/* 指针 */
int* ptr = &age;

/* \n为换行符 */
printf("Name: %s\n", name);
printf("Age: %d\n", age);
printf("Height: %f\n", height);
printf("Grade: %c\n", grade);
printf("Pointer: %p\n", (void*)ptr);

/* sizeof() */
printf("int 占用的字节为：%zu",sizeof(int));
```



##### 1.2.1 scanf()

> 基础输入(从键盘输入终端)，一般用于给变量赋值
>
> - format：格式控制字符串，可以理解为占位符，表示这里要输出的数据类型
>
>   以下是常用占位符：
>
>   - `%d`：读取一个整数，并将其存储到 `int` 类型的变量中。
>   - `%f`：读取一个浮点数，并将其存储到 `float` 或 `double` 类型的变量中。
>   - `%c`：读取一个字符，并将其存储到 `char` 类型的变量中。
>   - `%s`：读取一个字符串，并将其存储到字符数组（或字符串指针）中。
>   - `%lf`：读取一个双精度浮点数，并将其存储到 `double` 类型的变量中。
>
> <font color="#f40">注意：</font>scanf()函数在使用时，需要定义一个宏，否则需要使用`scan_f()`函数，是VS提供，但是不能跨平台
>
> ```c
> #define _CRT_SECURE_NO_WARNINGS
> ```

```c
int scanf(const char *format, ...);
```

**实例**

```c
#include <stdio.h>

int main() {
    int age;
    float height;
    char name[20];

    printf("请输入您的年龄：");
    scanf("%d", &age);

    printf("请输入您的身高（米）：");
    scanf("%f", &height);

    printf("请输入您的姓名：");
    scanf("%s", name);

    printf("您的姓名是：%s\n", name);
    printf("您的年龄是：%d\n", age);
    printf("您的身高是：%.2f 米\n", height);

    return 0;
}
```





#### 1.2 字符串

##### 1.2.1 strncpy()

> 将一个字符串的一部分或整个字符串复制到另一个字符串中
>
> - `destination`：目标字符串的指针，用于存储复制后的字符串
> - `source`：源字符串的指针，即要复制的字符串
> - `num`：要复制的字符数

```c
char* strncpy(char* destination, const char* source, size_t num);
```



##### 1.2.2 strlen()

> 计算给定字符串的长度，即字符串中的字符个数（不包括字符串末尾的空字符 '\0'），返回无符号整型
>
> - `*str`：要获取长度的字符串

```c
size_t strlen(const char *str);
```

**实例**

输出strlen:6

```c
#include <stdio.h>

int main()
{
    size_t length = 0;
    char str[] = "String";

    length = strlen(str);
    printf("strlen:%d",length);

    return 0;
}
```

输出strlen:3：遇到结束符即结束，d、e、f都不会读到

> <font color="#f40">注意：</font>空格正常计数

```c
#include <stdio.h>

int main()
{
    size_t length = 0;
    char str[] = {'a', 'b', 'c', '\0', 'd', 'e', ' '};

    length = strlen(str);
    printf("strlen:%d",length);

    return 0;
}
```



---



### 二、数学/计算

#### 2.1 sizeof()

> 计算变量或数据类型的大小/所占字节
>
> - `type`：变量、数据类型

```c
size_t sizeof(type);
```

**实例**

> 该函数返回的值，建议占位符用%zu表示

```c
ptintf("int占用的字节数为：%zu"sizeof(int));
```





#### 2.2 pow()

> 计算底数的指数幂，返回一个浮点数double
>
> - `base`：底数
> - `exponent`：指数幂
>
> 注意：参数可以是整数，但返回的依旧是double类型

```c
double pow(double base, double exponent);
```



---



### 三、内存/指针

#### 3.1 malloc()

> 申请一块连续的指定大小(字节)的内存块(堆)区域，以void*类型返回分配的内存区域地址
>
> - `size`: 字节数

```c
void* = malloc(size_t size);
```

**实例**

```c
// 定义一个int类型的指针p
int *p;
// 强制类型转换为int类型的指针，sizeof(数据类型)返回size_t类型的值，表示申请int大小(四个字节)的空间
p = (int *)malloc(sizeof(int));
```



---



### 四、文件IO

#### 4.1 fread()

> 从文件读取数据到内存，注意配合fclose(文件指针)
>
> - `*ptr`：指向存储读取数据的内存指针
> - `size`：数据项大小(单位字节)
> - `count`：读取数据项数量
> - `*stream`：要读取文件的指针

```c
size_t = fread(void *ptr, size_t size, size_t count, FILE *stream);
```

**实例**

```c
/* 初始化整型变量n为500kb */
int n = 500 * pow(2, 10);

/* 定义char指针res */
char* res;

/* 打开名为test.txt的文件 */
FILE* file = fopen("test.txt", "r");

/* 异常处理，判断是否成功打开该文件 */
if (file == NULL) {
	printf("文件未找到\n");
}

res = (char*)malloc(n);

/* 从file指针指向文件中读取n个字节，保存到指针res指向的内存地址 */
fread(res, sizeof(char), n, file);

/* 关闭流 */
fclose(file);
```

