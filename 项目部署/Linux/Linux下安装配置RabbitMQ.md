### 安装配置（低 20）

RabbitMQ安装、启动、停止服务、启用管理控制台

将以下几个rpm文件上传到centos上，放到自己的一个文件夹中

​	erlang-20.1.7-1.el7.centos.x86_64.rpm

​	rabbitmq-server-3.7.0-1.el7.noarch.rpm

​	socat-1.7.3.2-2.el7.x86_64.rpm



输入**<font color='red'>yum install *.rpm</font>**命令进行安装

<img src="https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/xiangwei/20210720220129.png" alt="image-20210720220129541" style="zoom:67%;" />

<img src="https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/xiangwei/20210720220139.png" alt="image-20210720220139303" style="zoom:67%;" />

启动rabbit mq

执行**<font color='red'>sudo service rabbitmq-server start</font>**

提示如图所示则表示启动成功

<img src="https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/xiangwei/20210720220154.png" alt="image-20210720220154184" style="zoom:67%;" />

配置rabbitmq管理账户。

执行命令 **<font color='red'>rabbitmqctl add_user admin admin</font>**，设置账户密码为admin admin

<img src="https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/xiangwei/20210720220211.png" alt="image-20210720220211182" style="zoom:67%;" />

执行命令 **<font color='red'>rabbitmqctl set_user_tags admin administrator</font>**，设置admin为管理员权限

<img src="https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/xiangwei/20210720220224.png" alt="image-20210720220224179" style="zoom:67%;" />

执行命令**<font color='red'> rabbitmq-plugins enable rabbitmq_management</font>**，打开rabbitmq web管理

<img src="https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/xiangwei/20210720220240.png" alt="image-20210720220240197" style="zoom:67%;" />

开放端口

firewall-cmd --zone=public --add-port=5672/tcp --permanent
firewall-cmd --zone=public --add-port=15672/tcp --permanent
sudo service firewalld restart



测试rabbit mq是否可以，打开浏览器在地址栏中输入：http://虚拟机ip:15672,出现登录页面，登陆账户密码为设置的admin admin

<img src="https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/xiangwei/20210720220254.png" alt="image-20210720220254230" style="zoom:67%;" />

查看用户权限,默认状态下权限是不允许访问(此时程序访问5672端口是连接被拒绝)

<img src="https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/xiangwei/20210720220306.png" alt="image-20210720220306204" style="zoom:67%;" />

点击用户名，进入用户页面，直接点击设置权限。此时刷新页面回到Users页面，权限变成可访问

<img src="https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/xiangwei/20210720220324.png" alt="image-20210720220324701" style="zoom:67%;" />

<img src="https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/xiangwei/20210720220333.png" alt="image-20210720220333577" style="zoom:67%;" />

<img src="https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/xiangwei/20210720220339.png" alt="image-20210720220339572" style="zoom: 67%;" />

<img src="https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/xiangwei/20210720220333.png" alt="image-20210720220333577" style="zoom:67%;" />

<img src="https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/xiangwei/20210720220339.png" alt="image-20210720220339572" style="zoom:67%;" />



#### 常见问题

 http://ip:15672不能访问，确认两点：

1、 添加用户、给用户设置管理员权限、rabbitmq-plugins这三步是否执行成功。

2、使用firewall打开5672/15672端口。具体步骤如下：

```
firewall-cmd --zone=public --add-port=5672/tcp --permanent
firewall-cmd --zone=public --add-port=15672/tcp --permanent
sudo service firewalld restart（如果系统不要求开启防火墙，可以在设置完以后再关闭它）
备注：即使防火墙处于关闭状态，也应该先打开端口再关闭，否则在有些机器上会仍然端口不通。
```

