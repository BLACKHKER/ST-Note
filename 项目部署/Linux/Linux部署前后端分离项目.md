# Linux项目部署

### 一、引入MySQL

##### 1.在Linux部署MySQL(参考部署文档：CentOS7安装MySQL)



##### 2.迁移数据库，导出原数据库数据

进入cmd (注意在系统cmd中 而不是在MySQLcmd中)

```shell
mysqldump -u 用户名 -p 数据库名 > 导出的文件名.sql
```

> 导出的文件就在当前工作目录中，xxx.sql



##### 3.登录Linux的数据库，创建一个数据库

###### 登录数据库：

```shell
mysql -u 账户名 -p
```

###### 创建数据库：

```mysql
create database 数据库名 default character set utf8;
```

![image-20230316162839870](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303161652972.png)



##### 4.导入数据到新数据库

利用xshell上传导出的sql文件到Linux