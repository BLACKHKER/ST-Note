## C

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

> ##### 短整型

##### 2.1.2 int

> 整型

##### 2.1.3 long

> 长整型

##### 2.1.4 long long

> 长长整型

#### 2.2 浮点数



#### 2.3 字符型