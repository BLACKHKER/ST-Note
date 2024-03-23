## C++ VS环境搭建与调试运行

### 一、环境搭建

#### 1.1 配置编译生成的程序类型

右键项目，属性

![image-20231211104457951](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231211104457951.png)

配置编译后生成的程序类型为二进制可执行文件

![image-20231211104750848](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231211104750848.png)





#### 1.2 添加编译命令按钮到控制台

> 编译默认快捷键是Ctrl + F7

操作台下拉菜单，选择添加或移除按钮

![image-20231211110400525](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231211110400525.png)

自定义

![image-20231211110452628](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231211110452628.png)

命令 → 标准 → 添加命令

![image-20231211110905458](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231211110905458.png)

生成 → 编译

![image-20231211110614678](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231211110614678.png)

界面会多一个按钮，可以自己移动位置

![image-20231211111011707](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231211111011707.png)





#### 1.3 配置输出目录

##### 1.3.1 过滤器目录

VS原生的目录是过滤器目录，他是一个模拟的目录，文件实际在同一目录下：

![image-20231218111105567](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231218111105567.png)

可以在上方切换成实际目录：

![image-20231218111258037](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231218111258037.png)

默认是没有src文件夹的，一般需要创建src保存cpp文件：

![image-20231218111409971](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231218111409971.png)



##### 1.3.2 输出目录

> 包含中间文件和exe可执行程序

生成的.exe可执行文件目录一般放在Debug目录(解决方案-项目名 → 平台-x64 → 配置-Debug)下，更改这个目录为其他目录：

右键项目 → 属性 → 要改成的目录

![image-20231218111832332](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231218111832332.png)

设置为全局配置

![image-20231218112813994](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231218112813994.png)

所有平台应用这套配置

![image-20231218133018819](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231218133018819.png)

修改输出目录，对应为解决方案(项目名) → bin → 平台(x64、x86) → 编译配置(Debug、Release)

```
$(SolutionDir)\bin\$(Platform)\$(Configuration)\
```

![image-20231218133724251](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231218133724251.png)

修改中间目录

```
$(SolutionDir)\bin\intermediates\$(Platform)\$(Configuration)\
```

![image-20231218134526716](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231218134526716.png)

右键解决方案 → 清理解决方案

![image-20231218134638792](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231218134638792.png)

手动去项目文件夹删除旧的Debug文件夹(src里面是.cpp、.h)

![image-20231218135203235](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231218135203235.png)

回到VS → 右键项目 → build

![image-20231218135341884](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231218135341884.png)

最终的项目结构

![image-20231218135810797](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231218135810797.png)

![image-20231218135751575](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231218135751575.png)





#### 1.4 配置格式化和自动代码样式

##### 1.4.1 缩进制表符改为空格

工具 → 选项

![image-20231229143846219](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231229143846219.png)

文本编辑器 → C/C++ → 制表符，改为插入空格

![image-20231229143943242](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231229143943242.png)



##### 1.4.2 配置左大括号的位置

文本编辑器 → C/C++ → 代码样式 → 格式设置 → 新行

![image-20231229144536884](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231229144536884.png)



##### 1.4.x 其他配置

![image-20231211105020465](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231211105020465.png)





---



### 二、编译/运行

#### 2.1 模板

```c++
/* IO输入输出，同C语言的引入头文件<stdio.h> */
#include <iostream>

int main()
{
    /* `<<`在C++中不是运算符，可以理解为一个函数：*/
    /* 
        表示将字符串`Hello World`推送到cout流中，然后打印到终端，然后推送一个行结束符(endLine)
        endl告诉终端跳到下一行，等同于C的`\n`
    */
    std::cout << "Hello World!" << std::endl;
    
    /* 上面这句等同于(2022不支持print，没有这个成员)： */
    std::cout.print("Hello World!").printf(std::endl);
    
    /* 
        cin.get()函数是等待状态，等待终端按下Enter，在前往下一句代码之前等待，此时程序暂停执行 
        目的是为了解决exe执行完自动退出导致的“闪退”现象
    */
    std::cin.get();
    ...
    /* main函数在没有return的情况下，默认返回0，代表程序执行完毕，仅针对main函数 */
}
```





#### 2.2 编译

##### 2.2.1 单个文件

在想要编译的文件点击编译按钮或快捷键(Ctrl + F7)，执行编译

编译后会生成`.obj`文件，项目中的每个C++文件，都会生成对应的obj文件

![image-20231211143004748](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231211143004748.png)



##### 2.2.2 整个项目编译

解决方案资源管理器中右键项目 → 生成

![image-20231211143213106](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231211143213106.png)

生成后文件夹下会多一个可执行文件xxx.exe，可直接双击执行：

![image-20231211143254934](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231211143254934.png)





#### 2.3 调试

##### 2.3.1 VS断点调试

给某个变量打一个断点

![image-20231229140157522](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231229140157522.png)

F5运行或以调试模式运行

![image-20231229140115229](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231229140115229.png)

调试 → 窗口 → 内存 → 内存1

![image-20231229140351502](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231229140351502.png)

上方即显示内存

![image-20231229140426156](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231229140426156.png)

地址窗口可以直接搜索变量名(int4字节，16进制数表示)，F11指定到下一个断点

![image-20231229141711480](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231229141711480.png)