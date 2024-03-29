## MySQL v8.0.15 安装配置

### 一、安装

#### 1.1 许可协议

勾选“I accept the license terms”，Next。

![QQ图片20230318225248](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326017.jpg)





#### 1.2 安装类型

这一步和MySQL5.X版本的有很的大区别，选择Custom(自定义)，可以将MySQL安装到非系统盘。

![QQ图片20230318225310](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326413.jpg)





#### 1.3 选择安装的功能

第一次进入到这个界面时，右边的框内可能什么也没有，需要不断点击“MySQL Servers”前的`+`，直到你看见`MySQL Server 8.0.xx-X64`单击它，然后点击向右的箭头添加到右边的框里，然后在右边的框里点击它，就会出现右下角的蓝字。

![QQ图片20230318225314](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326494.jpg)





#### 1.4 配置安装/数据路径

单击上一步出现的蓝字`Advanced Options`，出现下面的界面。

第一个位置是MySQL的安装路径，第二个位置是MySQL存放数据的路径，建议分开，不要放在一起。

路径下的感叹号是可以忽略的。直接点击`OK`。选好路径之后点击Next。

> 注意:路径不要有中文

![QQ图片20230318225816](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326888.jpg)





#### 1.5 路径冲突解决

因为两个路径(安装路径/数据存放路径)在同一个文件夹下，所以会警告，直接Next即可

![QQ图片20230318225910](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326703.jpg)

再次选择是

![QQ图片20230318225958](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326611.jpg)

可能弹出需要安装VS++(紫色)环境组件，点击`Execute`进行安装。





#### 1.6 安装

直接点击`Execute`进行安装。

![QQ图片20230318230154](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326544.png)

Complete后，Next。

![QQ图片20230318230214](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326659.png)



---



### 二、配置

#### 2.1 独立/集群安装

默认独立安装，直接Next即可。

![image-20230830142719937](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230830142719937.png)





#### 2.2 类型和网络

这一步建议什么也不要动，直接点击“next”。(详见后面的详细说明)

![QQ图片20230318230313](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326400.jpg)

##### 2.2.1 详细说明

其实在一步MySQL提供了3种可以选择的应用类型（见下图），那么这3种类型有什么区别呢：

`Development Computer`：开发机，该类型应用将会使用最小数量的内存。

`Server Computer`：服务器，该类型应用将会使用中等大小的内存。

`Dedicated Computer`：专用服务器，该类型应用将使用当前可用的最大内存。

在这里我们选择`Development Computer`开发机就足够我们使用了。

![QQ图片20230318230451](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326673.jpg)





#### 2.3 权限认证

要选择第二个，详见后续详细说明

这一步对以后使用图形化管理软件(Navicat等)有直接的影响

![QQ图片20230318230529](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326582.jpg)

##### 2.3.1 详细说明

第一个选项 Use Strong Password Encryption for Authentication(RECOMIMENDED)

使用强密码加密进行身份验证(已升级)

第二个选项 Use Legacy Authentication Method (Retain MySQL 5.x Compatibility)

使用传统身份验证方法(保留MySQL 5.x兼容性)

如果选择了强密码加密进行身份验证，虽然MySQL采用了强密码加密，但是图形化管理软件就不好连接了。

所以这里我们要选择传统的加密方法





#### 2.4 账户设置

给root用户设置密码，建议用Root，约定俗成；Next。

![QQ图片20230318230617](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326589.jpg)





#### 2.5 Windows服务配置

默认即可，如果“Windows Service Name”出现感叹号，说明有重名的服务，换一个名字即可，Next

![image-20230830143001030](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230830143001030.png)





#### 2.6 服务器文件权限

默认yes，grant... Next

![QQ图片20230318230847](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326730.jpg)





#### 2.7 应用设置(安装)

点击“Execute”进行安装。

![QQ图片20230318230940](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326520.jpg)

初始化数据库的时候会卡很久，等待

![QQ图片20230318230949](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326308.jpg)

安装完成，Finish

![QQ图片20230318231001](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326067.jpg)

Next

![QQ图片20230318231014](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326776.jpg)

finish，安装完成

![QQ图片20230318231033](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326443.jpg)



---



### 三、测试

安装完成后会在系统的开始菜单下出现下图所示的程序，随便打开一个，输入之前设置的密码。

![QQ图片20230318231113](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326325.png)

输入密码后，出现下面的界面，表示MySQL正常：

![QQ图片20230318231150](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326195.jpg)

然后输入“exit”，退出MySQL。

如果出现输入密码后闪退的情况：

1. 原MySQL没有卸载干净

   大概率需要搜索所有带MySQL的文件，删除，并对注册表做一些处理，甚至重装系统。

2. 没有开启服务，去服务里手动开启，并根据需求配置自动开启