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

> 注意：
>
> 1. sizeof()函数的打印，占位符最好用%zu
> 1. 将int以%c字符类型输出时，输出的是ASCII码中对应该数字的字符

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



##### 1.1.2 scanf()

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

基础接收

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

按宽度接收

```c
#include <stdio.h>

int main()
{
    int year = 0;
    int month = 0;
    int day = 0;

    /* 表示前四位存到year，后面的两位存到month，以此类推... */
    scanf_s("%4d%2d%2d", &year, &month, &day);

    printf("year = %d\n", year);

    /* 02d表示按两位输出，比如数字小于10的数，以01、02、03等表示 */
    printf("month = %02d\n", month);
    printf("day = %02d\n", day);

    return 0;
}
```



##### 1.2.3 getchar()

> 从标准输入缓冲区(通常是键盘)读取一个字符，返回输入字符的ASCII码值。
>
> 如果读取成功，返回值是非负整数；
>
> 如果发生错误或到达文件末尾，返回值是 `EOF`（End-of-File）。

```c
int getchar(void);
```

**实例**

```c
#include <stdio.h>

int main()
{
    int num = getchar();
    printf("num = %d", num);
    
    return 0;
}
```

> <font color="#f40">注意</font>：键盘把数据放到缓冲区，getchar()从缓冲区中拿一个字符，包括空格、换行等；
>
> 可以使用如下代码防止输入的回车影响后面的内容：
>
> ```
> #include <stdio.h>
> 
> int main()
> {
>     char password[20] = {0};
>     printf("请输入密码：");
>     scanf("%s", password);
>     
>     int ch = 0;
>     
>     /* 判断缓冲区的下一个字符是否是换行，是则继续读取，防止影响后面的判断 */
>     while((ch = getchar()) != '\n')
>     {
>         ;
>     }
>     
>     printf("请确认密码(Y/N):");
>     int ret = getchar();
>     if('Y' == ret)
>     {
>         printf("登录成功");
>     }
>     else
>     {
>         printf("登录失败");
>     }
>     
>     return 0;
>     
> }
> ```



##### 1.2.4 putchar()

> 将参数 `c` 所表示的字符输出到标准输出，并返回输出的字符作为整数。
>
> 如果输出成功，返回值是输出的字符的ASCII码值；
>
> 如果发生错误，返回值是 `EOF`（End-of-File）。

```c
int putchar(int c);
```

**实例**

```c
#include <stdio.h>

int main() {
    char c = 'A';

    printf("The character is: %c\n", c);
    putchar(c);

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

###### 相关问题

1. 无`\0`时的数组长度问题

   > 不完全初始化：数组大小大于元素个数，剩余元素赋值初始化为0
   >
   > <font color="#f40">'0'的ASCII码是48，'\0的ASCII码是0'</font>

   ```c
   #include <stdio.h>
   
   int main()
   {
       char arr[3] = {'1', '2', '3'};
       char arr2[3] = {'1', '2'};
       
       /* 打印随机数，因为没有结束符，会继续沿着内存向下找 */
       printf("%d\n", strlen(arr));
       
       /* 打印3，数组初始化大小为3，实际填充了两个字符，剩下的1个字符自动填充0，即为`\0` */
       printf("%d\n", strlen(arr2));
       
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
/* 4 */
printf("int占用的字节数为：%zu"sizeof(int));

/* 40，因为自动初始化为0，每个元素占四个字节 */
int arr[10] = {};
printf("%zu", sizeof(arr));

/* 4 */
printf("%zu", sizseof(arr[0]));

/* 求数组大小，用数组arr的整体占用内存(字节) / 每个数组元素占用的空间(字节) */
int size = sizeof(arr) / sizeof(arr[0]);
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

