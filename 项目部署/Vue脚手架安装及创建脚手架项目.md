## 安装vue-cli3

> 首先安装NodeJS

### 判断NodeJs是否安装完毕

```shell
npm -v
```

![image-20230301194255711](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035714.png)





### 设置镜像源(安装cnpm)

```shell
npm install -g cnpm --registry=https://registry.npmmirror.com
```

![image-20230301100052417](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035504.png)

##### 查看镜像源是否安装成功

```shell
npm config list
```



##### 切换新的镜像源

```shell
npm config set registry https://registry.npmmirror.com
```





### 查看版本号判断是否安装成功

```shell
cnpm -v
```

![image-20230301194315573](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035994.png)





### 设置下载源

> 因为cnpm安装的脚手架路径有问题，所以设置npm使用cnpm的下载源，这样就还是使用npm安装脚手架

```shell
npm config set registry http://registry.npmmirror.com
```

![image-20230301194454136](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035277.png)





### 查看刚刚设置的npm的下载源

```shell
npm config get registry
```

![image-20230301194508273](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035107.png)





### 安装出现问题，清空npm缓存

```shell
npm cache clean --force
```

![image-20230301194526343](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035881.png)





### 安装vue脚手架

```shell
npm install -g @vue/cli
```

##### 开始下载：

##### ![image-20230301194627876](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035806.png)



##### 下载完毕：

![image-20230301194709080](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035243.png)





### 查看vue版本

```shell
vue -V
```

![image-20230301194740072](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035434.png)





### 初始化脚手架

```shell
npm install -g @vue/cli-init
```

![image-20230301194814121](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035986.png)





### 利用脚手架搭建项目

##### 初始化一个vue项目

```shell
vue init webpack xxx(自定义项目名)
```



##### 会自动下载模板：

![image-20230301195021685](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035007.png)



##### 下载完毕提示设置项目名：

> 可以直接回车也可以手动重写一个

![image-20230301200313814](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035893.png)



##### 添加项目描述：

> 可以直接回车，不填加

![image-20230301200438564](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035932.png)



##### 作者是否是(xxx)？

> 可以直接回车，是，手动输，重定义作者

![image-20230301200612817](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035604.png)



##### 项目在运行(构建)时使用哪种方式？

> 区别就是占用存储，Runtime-only占用小，方向键上下选择

1.Runtime+

2.Runtime-only

###### 选择Runtime+，回车

![image-20230301201017547](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035610.png)



##### 是否安装Vue路由？

> 是，回车

![image-20230301201110487](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035289.png)



##### 是否使用代码检测器？

> 否，n

![image-20230301201235404](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035112.png)



##### 是否安装单元测试？

> 否，n

![image-20230301201307774](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035941.png)



##### 是否使用e2e测试工具？

> 否，n

![image-20230301201346484](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035553.png)



##### 使用什么管理方式管理？

> 直接回车，使用Node管理第三方插件

![image-20230301201509658](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035451.png)



##### 整体选择图示：

![image-20230301201613512](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035032.png)



##### 开始下载

![image-20230301201534141](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035852.png)





### 测试运行Vue项目

##### 切换到刚才搭建的项目目录

```shell
cd 项目名
```

![image-20230301201724748](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035595.png)



##### 运行项目

```shell
npm run dev
```

![image-20230301201908599](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035276.png)



##### 根据端口号测试

```http
http://localhost:端口号/
```

![image-20230301202025020](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035211.png)





##### 创建出的项目在C:\Windows\System32下

```http
C:\Windows\System32
```

![image-20230301202403299](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035528.png)



### 项目结构

##### 根目录目录结构：

![image-20230301203309607](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035447.png)



##### src源代码目录结构：

![image-20230301203407912](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012036503.png)