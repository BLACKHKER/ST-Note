## Vue脚手架安装&搭建Vue项目

### 一、环境配置

#### 1.1 NodeJS

##### 1.1.1 安装

> 这步骤可参考该Note项目其他笔记：根目录/项目部署/NodeJS、NodeVM安装.md，本文档略
>

###### 验证

```shell
npm -v
```

![image-20230301194255711](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035714.png)

###### 安装问题解决

> 清空npm缓存

```shell
npm cache clean --force
```

![image-20230301194526343](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035881.png)



##### 1.1.2 安装cnpm[^1]

> -g 表示全局安装，--registrty 同时设置cnpm镜像源为淘宝新的npm镜像站

```shell
npm install -g cnpm --registry=https://registry.npmmirror.com
```

![image-20230301100052417](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035504.png)

###### 验证

```shell
cnpm -v
```

![image-20230301194315573](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035994.png)



##### 1.1.3 检查镜像源

```shell
cnpm config list
```

如果刚才没配置成功镜像源，可以手动设置

###### 设置cnpm镜像源

```shell
cnpm config set registry https://registry.npmmirror.com
```

###### 设置npm镜像源

如果cnpm安装的脚手架路径有问题，放弃cnpm，使用npm设置淘宝的镜像源后安装脚手架

```shell
npm config set registry http://registry.npmmirror.com
```

![image-20230301194454136](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035277.png)

查看刚刚设置的npm的下载源

```shell
npm config get registry
```

![image-20230301194508273](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035107.png)



---



### 二、Vue脚手架

#### 2.1 安装脚手架

> 这步时间可能很长，取决于使用的镜像地址，国外官方npm站的包下载速度。

```shell
npm install -g @vue/cli
```

##### ![image-20230301194627876](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035806.png)

完成效果：

![image-20230301194709080](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035243.png)





#### 2.2 查看vue版本

```shell
vue -V
```

![image-20230301194740072](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035434.png)





#### 2.3 初始化脚手架

```shell
npm install -g @vue/cli-init
```

![image-20230301194814121](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035986.png)



---



### 三、脚手架搭建Vue项目

#### 3.1 初始化一个vue项目

```shell
vue init webpack xxx(自定义项目名)
```

##### 3.1.1 详细步骤

1. 下载模板

![image-20230301195021685](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035007.png)

2. 设置项目名，可以直接回车(默认demo)，也可以手动重写一个

![image-20230301200313814](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035893.png)

3. 项目描述，可以直接回车，不添加

![image-20230301200438564](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035932.png)

4. 作者是否是(xxx)，可以直接回车，手动输可以重定义作者

![image-20230301200612817](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035604.png)

5. 项目在运行(构建)时使用哪种方式，选择Runtime+，回车

> 区别就是占用存储，Runtime-only占用小，方向键上下选择

- Runtime+ 带编译器
- Runtime-only 不带编译器



![image-20230301201017547](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035610.png)

6. 是否安装Vue路由，是，回车

![image-20230301201110487](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035289.png)

7. 是否使用代码检测器，否，N

![image-20230301201235404](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035112.png)

8. 是否安装单元测试，否，N

![image-20230301201307774](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035941.png)

9. 是否使用e2e测试工具，否，N

![image-20230301201346484](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035553.png)

10. 使用什么管理方式管理，直接回车，使用NPM管理第三方插件

![image-20230301201509658](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035451.png)



##### 3.1.2 整体选择图示

![image-20230301201613512](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035032.png)

开始下载

![image-20230301201534141](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035852.png)



---



### 四、测试

#### 4.1 运行Vue项目

##### 4.1.1 目录切换

> 创建出的项目，一般在C:\Windows\System32下

```http
C:\Windows\System32
```

![image-20230301202403299](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035528.png)

```shell
cd 项目名
```

![image-20230301201724748](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035595.png)



##### 4.1.2 运行项目

```shell
npm run dev
```

![image-20230301201908599](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035276.png)



##### 4.1.3 端口号测试

```http
http://localhost:端口号/
```

![image-20230301202025020](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035211.png)



---



### 五、项目结构

#### 5.1 根目录

![image-20230301203309607](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035447.png)





#### 5.2 src源代码目录

![image-20230301203407912](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012036503.png)



---



### 解释文档

[^1]:`cnpm`是淘宝团队为了解决`npm`在国内下载速度慢的问题而推出的一个命令行工具。它是`npm`的一个镜像，提供了类似于`npm`的功能，但使用了淘宝的镜像源，从而加速了包的下载过程。默认地址：`https://registry.npm.taobao.org`