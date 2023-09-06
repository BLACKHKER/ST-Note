## Linux安装Redis

> 下载地址：http://redis.io/download，下载最新稳定版本
>

##### 1.在/opt下创建redis文件夹，通过XShell将redis-5.0.7.tar.gz拷贝到该目录下，最后解压

```shell
mkdir /opt/redis
cd /opt/redis
```

###### 拷贝Redis安装压缩包到当前目录：

```shell
tar -zxvf xxx.tar.gz
```

![image-20230315191811984](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151940594.png)

###### 解压：

![image-20230315191829662](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151940065.png)





##### 2.安装gcc编译器

```shell
yum -y install gcc gcc-c++ kernel-devel
```

安装成功：

![image-20230315192038769](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151940971.png)

如果出现下图所示的错误:

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151940115.png" alt="image-20211018171641105" style="zoom:50%;" />

可能是系统自动升级正在运行，yum在锁定状态，可以输入以下命令强制关闭yum，然后重新执行指令安装gcc

```shell
rm -f /var/run/yum.pid
```

结束后会自动生成一个Redis-版本号的目录：

![image-20230315192357607](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151940844.png)



##### 3.进入自动生成的目录，安装Redis

###### 进入目录：

![image-20230315192416245](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151940332.png)

###### 输入以下指令安装Redis：

```shell
make MALLOC=libc
```

![image-20230315192921816](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151940042.png)



##### 4.安装redis服务

```shell
make install
```

![image-20230315192954588](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151941332.png)

###### 创建存储redis文件目录

```shell
mkdir -p /usr/local/redis
```

###### 复制redis-server redis-cli redis-sentinel到新建立的文件夹

```shell
cp /opt/redis/redis-5.0.7/src/redis-server /usr/local/redis/
cp /opt/redis/redis-5.0.7/src/redis-cli /usr/local/redis/
cp /opt/redis/redis-5.0.7/src/redis-sentinel /usr/local/redis
```

###### 将redis配置文件复制一份到redis目录

```shell
cp /opt/redis/redis-5.0.7/redis.conf /usr/local/redis/
```

###### 然后切换到该目录下，编辑redis配置文件

```shell
cd /usr/local/redis/
vi /usr/local/redis/redis.conf
```

###### 在bind 127.0.0.1前加“#”将其注释掉（如果有注释）

![image-20230315193213955](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151941512.png)

###### 默认为保护模式，把 protected-mode yes 改为 protected-mode no

![image-20230315193355816](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151941569.png)

###### 默认为不守护进程模式，把daemonize no 改为daemonize yes

![image-20230315193502800](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151941642.png)



##### 5.启动redis

```shell
redis-server redis.conf
```

![image-20230315193707054](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151941949.png)



##### 6.通过客户端连接redis

```shell
redis-cli -h 127.0.0.1 -p 6379
```

keys *测试一下Redis是否可用

![image-20230315193836880](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151941390.png)