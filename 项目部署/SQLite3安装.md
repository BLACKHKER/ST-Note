## SQLite3安装

### 一、下载

#### 1.1 官网

```http
https://www.sqlite.org/index.html
```

![image-20231017100203814](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231017100203814.png)





#### 1.2 安装步骤

1. 1. 选择Windows版，下载核心DLL，以及SQLite工具

![image-20231017100512580](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231017100512580.png)

2. 解压两个文件中的内容，即安装完成

![image-20231017100933454](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231017100933454.png)



---



### 二、配置

将SQLite3对应的位置添加到环境变量Path

![image-20231017101316856](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231017101316856.png)



---



### 三、测试

在CMD中输入命令，检查是否安装配置成功。

配置成功会出现版本号、安装时间等信息，注意必须有Tools中的文件才能执行成功。

```shell
sqlite3
```

![image-20231017101433152](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231017101433152.png)