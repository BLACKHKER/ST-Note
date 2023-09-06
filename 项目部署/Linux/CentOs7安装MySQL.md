## 安装mysql 5.5

### 一、卸载centos7自带的数据库

> 在新版本的CentOS7中，默认的数据库已更新为了Mariadb，而非 MySQL，所以执行 yum install mysql 命令只是更新Mariadb数据库，并不会安装 MySQL 。

##### 1.查看已安装的 Mariadb 数据库版本。

```shell
rpm -qa|grep -i mariadb
```

![image-20230315170519444](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151838862.png)



##### 2.卸载已安装的 Mariadb 数据库。

```shell
rpm -qa|grep mariadb|xargs rpm -e --nodeps
```

 ![image-20230315170612368](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151838488.png)





### 二、离线安装MySQL

##### 1.卸载系统自带的Mariadb

```shell
rpm -qa|grep mariadb|xargs rpm -e --nodeps
```



##### 2.删除etc下的my.cnf配置文件

```shell
rm -f /etc/my.cnf
```

 

##### 3.创建MySQL用户组

```shell
groupadd mysql
```

 

##### 4.创建mysql用户并加入mysql用户组

```shell
useradd -g mysql mysql
```

![image-20230315170844760](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151838368.png)



##### 5.下载MySQL安装包

```http
https://downloads.mysql.com/archives/community/
```

![image-20230315175224656](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151838836.png)



##### 6.利用xshell将安装包上传到Linux的/usr/local目录下，解压并重命名为mysql

###### 切换到目录

```shell
cd /usr/local
```

###### 上传并解压MySQL安装包

```shell
tar -zxvf mysql-5.5.62-linux-glibc2.12-x86_64.tar.gz
```

###### 上传提示找不到命令，执行以下命令安装lrzsz

```shell
yum -y install lrzsz  
```

![image-20230315171118485](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151838121.png)

![image-20230315171315677](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151838627.png)

###### 重命名为mysql

```shell
mv mysql-5.5.62-linux-glibc2.12-x86_64 mysql
```



##### 7.在etc下新建配置文件my.cnf，并在该文件末尾添加以下代码 

###### 使用vi编辑器打开配置文件

```shell
vi /etc/my.cnf
```

###### 添加代码

```properties
[mysql]
# 设置mysql客户端默认字符集
default-character-set=utf8
socket=/var/lib/mysql/mysql.sock
[mysqld]
skip-name-resolve
#设置3306端口
port=3306
socket=/var/lib/mysql/mysql.sock
# 设置mysql的安装目录
basedir=/usr/local/mysql
# 设置mysql数据库的数据的存放目录
datadir=/usr/local/mysql/data
# 允许最大连接数
max_connections=200
# 服务端使用的字符集默认为8比特编码的latin1字符集
character-set-server=utf8
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
lower_case_table_names=1
max_allowed_packet=16M
```

 

##### 8.创建步骤9中用到的目录并授权mysql用户权限

```shell
mkdir /var/lib/mysql
mkdir /var/lib/mysql/mysql
```

###### 授权，授予mysql用户对/var/lib/mysql的读操作权限

```shell
chown -R mysql:mysql /var/lib/mysql   
chown -R mysql:mysql /var/lib/mysql/mysql
```

![image-20230315172204045](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151839849.png)



##### 9.进入**mysql主目录**执行以下操作

###### 进入目录

```shell
cd /usr/local/mysql
```

###### 修改当前目录拥有者为mysql用户

```shell
chown -R mysql:mysql ./
```

###### 安装autoconf库（在线）

```shell
yum -y install autoconf
```

###### 安装数据库

```shell
./scripts/mysql_install_db --user=mysql
```

![image-20230315172700039](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151839284.png)



##### 修改当前data目录拥有者为mysql用户

```shell
chown -R mysql:mysql data
```



##### 安装完毕，但此时还暂时不能使用



##### 10.授予my.cnf权限

```shell
chmod 644 /etc/my.cnf
```

 

##### 11.设置启动脚本、启动MySQL

```shell
#复制启动脚本到资源目录
cp ./support-files/mysql.server /etc/rc.d/init.d/mysqld
#增加mysqld服务控制脚本执行权限
chmod +x /etc/rc.d/init.d/mysqld
#将mysqld服务加入到系统服务
chkconfig --add mysqld
#启动msql
service mysqld start
```

![image-20230315172832245](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151839528.png)



##### 12.将mysql的bin目录加入PATH环境变量

###### 使用vi编辑器编辑profile文件

```shell
vi /etc/profile
```

###### 在文件添加如下信息

```shell
export PATH=$PATH:/usr/local/mysql/bin
```

![image-20230315172946184](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151839858.png)



##### 13.保存退出，使用以下命令使配置生效

```shell
source /etc/profile
```

 

##### 14.以root账户登陆mysql，默认是没有密码，直接回车

```shell
mysql -u root -p
```

 

##### 15.为MySQL设置密码

```mysql
set password for 'root'@'localhost'=password('你的密码');
```

 

##### 16.设置开机启动

> 输入exit退出mysql

###### 执行以下命令，让mysql服务可用

```shell
systemctl enable mysqld
```

![image-20230315173054195](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151839412.png)

###### 让mysql以后台任务的方式执行

```shell
systemctl daemon-reload
```



##### 17.开放3306端口

```shell
firewall-cmd --zone=public --add-port=3306/tcp --permanent
```

![image-20230315173129207](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151839326.png)

###### 重启防火墙

```shell
systemctl restart firewalld.service
```





##### 18.开启远程访问权限

###### 登录MySQL：

```shell
mysql -u root -p
```

![image-20230315173246260](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151839320.png)

###### 切换到四个内置数据库之一(mysql)：

```mysql
use mysql;
```

![image-20230315173406355](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151839382.png)

###### 开启远程访问权限：

```mysql
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '你的密码' WITH GRANT OPTION;
```

![image-20230315173835144](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151839332.png)

###### 刷新数据库

```mysql
FLUSH PRIVILEGES;
```

![image-20230315173446014](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303151839801.png)











项目部署

1、将写好的项目打成war包

2、利用xshell将war上传到tomcat的webapps目录下

3、启动tomcat

4、打开浏览器访问项目

 



4、在Linux上创建一个与Windows上名字一模一样的数据库

 

5.退出数据库，输入

mysql -u 用户名 -p 数据库名 < 文件名

![img](S:/woniu/TypoaPicture/clip_image014.jpg)

 

**问题1**

项目部署起来之后无法访问数据库，可能有两种原因

原因一：数据库没有授权

解决办法

对于mysql数据库没有授权，只需要用一条命令就可以了。

mysql>GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '123456' WITH GRANT OPTION;

 

//远程连接数据库的时候需要输入用户名和密码

用户名：root

密码:123456

 

输入后使修改生效还需要下面的语句

mysql>FLUSH PRIVILEGES;

 

原因二：没有开放3306端口

解决办法

firewall-cmd --zone=public --add-port=3306/tcp --permanent

systemctl restart firewalld.service

 

**问题2：**

验证码无法显示

原因：java在图形处理时调用了本地的图形处理库。在利用Java作图形处理（比如：图片缩放，图片签名，生成报表）时，如果运行在windows上不会出问题。如果将程序移植到Linux/Unix上的时候有可能出现图形不能显示的错误。

 

解决办法：

编辑Tomcat下的bin/catalina.sh文件

vi /usr/local/tomcat/bin/catalina.sh

在文件中添加如下命令，（解决LINUX字符模式无法支持java图形处理问题） （大概位置在392行）

-Djava.awt.headless=true \

![img](S:/TypoaPicture/clip_image016.jpg)

 

 