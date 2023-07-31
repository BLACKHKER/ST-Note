## MinIO安装部署

### 简介

Minio是GlusterFS创始人之一Anand Babu Periasamy发布新的开源项目。基于Apache License v2.0开源协议的对象存储项目，采用Golang实现，客户端支Java,Python,Javacript, Golang语言。

其设计的主要目标是作为私有云对象存储的标准方案。主要用于存储海量的图片，视频，文档等。非常适合于存储大容量非结构化的数据，例如图片、视频、日志文件、备份数据和容器/虚拟机镜像等，而一个对象文件可以是任意大小，从几kb到最大5T不等。

中文文档：http://docs.minio.org.cn/docs/







### 下载

#### Windows版下载地址：

```http
https://dl.min.io/server/minio/release/windows-amd64/
```

##### 在安装目录下新建minio，存放下载的MinIO.exe，并在该文件夹下创建data文件夹用于存储上传的文件

![image-20230427204306289](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304272104193.png)







### 配置MinIO

#### 通过cmd的方式打开minio.exe所在的文件夹

##### 设置管理员账号和密码

```shell
set MINIO_ACCESS_KEY=minioadmin
set MINIO_SECRET_KEY=minioadmin
```

![image-20221027171142224](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/xiangwei20221027171142.png)



##### 执行以下指令启动minio

```shell
minio.exe server D:\minio\data --console-address ":9001" --address ":9000"
```

![image-20221027171219683](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/xiangwei20221027171219.png)

默认情况下minio会生成一个管理员账号：minioadmin，密码也为minioadmin



##### 浏览器上访问9001端口，输入账号密码，完成

![image-20230315195900518](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303152032488.png)

###### 登录之后进入管理页面

![image-20230315200027243](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303152032809.png)







### 基本概念

| 术语   | 含义                                                         |
| ------ | ------------------------------------------------------------ |
| Object | 存储到MinIO的基本对象，如文件，字节流等。                    |
| Bucket | 存储Object的逻辑空间，每个Bucket之间的数据时相互隔离的。对于用户而言，相当于存放文件的顶层文件夹。 |
| Drive  | 存储Object的磁盘。在MinIO启动时，以参数的方式传入。          |
| Set    | 一组Drive的集合。                                            |

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303152032419.png" alt="image-20221008094400100" style="zoom: 67%;" />

如上图所示：在Erasure Set中有4个磁盘：Disk1，Disk2，Disk3，Disk4，四个磁盘组成一个Erasure Set。每个bucket对应一个相应桶名称的目录，每个对象对应bucket的一个目录：目录里保存着对应的数据和元数据文件。







### 基本使用

#### 创建bucket(桶)

![image-20230315201216703](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303152032742.png)



##### 输入桶名

![image-20230315201502243](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303152032058.png)



##### 创建完毕会跳转到该桶管理页面

![image-20230315201521135](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303152032176.png)



创建完成后服务器D:\minio\data下也会创建这个文件目录

![image-20230427205417718](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304272104420.png)





#### 设置访问规则

##### 点击右上角设置按钮，进入当前bucket设置界面

![image-20230315201656891](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304272104747.png)



##### 进入管理页面之后，找到“Access Rules”选项并点击“Add Access Rule”按钮添加访问规则

![image-20230315201753735](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303152032647.png)



##### 输入访问前缀、选择该前缀对应的访问权限，点击“Save”保存规则

![image-20230315201848825](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303152032539.png)



##### 创建成功之后会在规则列表中显示该规则

![image-20230315201938038](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303152032037.png)

> 注：一个桶可以创建多个规则，每一个前缀都可以有自己的权限





#### 上传文件

##### 点击Upload上传文件

![image-20230315202002863](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303152032471.png)



##### 上传之后会在当前桶的文件列表中看到文件信息

![image-20230315202031126](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303152032430.png)



##### 点击文件查看文件详细信息

![image-20230315202124932](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303152032010.png)



##### 点击“share”

![image-20230315202210708](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303152032382.png)



##### 复制文件url

![image-20230315202242825](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303152032210.png)



##### 将url放到浏览器地址栏中进行访问，该URL中有访问参数，minio需要对参数进行校验

> 默认情况下该URL有效期只有7天







### 安装mc客户端：设置永久访问链接

#### 下载

##### 下载地址：

```http
https://dl.min.io/client/mc/release/windows-amd64/
```



#### 部署

##### 将mc文件放到D:\minio目录下

![image-20230427210015745](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304272100656.png)



##### 设置永久访问链接

###### 基本格式：

```shell
mc.exe config host add minio ip:port 账号 密码 --api 签名
```

###### 输入：

```shell
mc.exe config host add minio http://192.168.2.163:9000 minioadmin minioadmin --api S3v4
```

![image-20221027174851823](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304272103106.png)



##### 设置某个桶(即文件目录)中的文件可直接下载的权限

```shell
./mc policy set download minio/桶名
```



##### 设置文件公共读

![image-20230315202716629](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303152033343.png)



操作完后这个桶下面的文件通过 http://服务器ip:端口/桶名称/文件名称 直接访问到了