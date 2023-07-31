## 安装erlang

> 双击otp_win6_21.0.1.exe安装到电脑，除了安装位置其他的都用默认选项

### 配置环境变量

##### 创建系统变量，值为erlang的安装位置

```
ERLANG_HOME
```

![image-20230417143428749](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304272009664.png)



##### 在系统的path变量中添加erlang的bin目录路径

```
%ERLANG_HOME%\bin;
```

![image-20230417143446701](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304272009931.png)





---





## 安装RabbitMQ

> 解压rabbitmq_server-xxx.xxx文件到安装目录

### 配置环境变量

##### 创建系统变量

```
RABBITMQ_SERVER
```

![image-20230417143502750](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304272009640.png)



##### 在系统的path变量中添加rabbitmq的sbin目录路径

```
%RABBITMQ_SERVER%\sbin;
```

![image-20230417143515368](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304272009374.png)





---





### 启动RabbitMQ，测试安装状态

##### 打开cmd将当前工作路径切换到rabbitmq的sbin目录下输入以下命令安装插件：

```shell
rabbitmq-plugins.bat enable rabbitmq_management
```

###### 显示以下内容表示安装成功

![image-20230417143310131](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304272009001.png)



##### 输入以下命令启动RabbitMQ

```shell
rabbitmq-server.bat
```

显示以下内容表示启动成功

![image-20230417143401962](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304272009118.png)



##### 新开一个dos窗口执行指令：添加一个用户，用户账号密码都是admin

```shell
rabbitmqctl add_user admin admin
```

![image-20230417143649605](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304272010287.png)



##### 设置该用户权限为管理员

```shell
rabbitmqctl set_user_tags admin administrator
```

![image-20230417143754663](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304272010379.png)



##### 访问RabbitMQ后台，看到rabbitmq管理登录页面

```http
http://localhost:15672
```



##### 输入账号：admin，密码：admin进入管理界面

![image-20230417144055828](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304272010966.png)



##### 登录成功之后点击“Admin”，进入系统管理页面

![image-20230417144204551](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304272010378.png)



##### 点击右侧的“Virtual Hosts”选项进入虚拟机管理页面

> 创建虚拟机的目的是为了避免不同用户在操作rabbitmq时互相影响

![image-20230417144226854](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304272010492.png)



##### 展开“Add a new virtual host”填写虚拟机名字最后点击“Add virtual host”按钮创建虚拟机

![image-20230417144312029](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304272010694.png)

