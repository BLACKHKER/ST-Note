## Linux问题日志

### 一、Ubuntu

#### 无法定位软件包build-essential

- 确认系统已经连接到互联网
- 可以访问软件源

执行以下命令更新软件源

```shell
sudo apt update
```

然后尝试再次安装build-essential软件包





#### Could Not find OpenSSL，try to set the path to OpenSSL root folder...

OpenSSL未安装，执行以下命令安装

```shell
sudo apt install libssl-dev
```





#### 移动或复制文件权限不够

执行以下命令，打开一个带权限的文件管理器，注意不要关闭终端

```shell
sudo nautilus
```





#### sudo vim common not found

执行以下命令，安装vim

```shell
sudo apt-get install vim-gtk
```

安装完毕验证是否成功

```shell
vi + <tab>
```

