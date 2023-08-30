# MySQL8.0.15安装

### 一、安装

##### 双击安装程序，就会出现下面的界面，勾选“I accept the license terms”，然后点击next

![QQ图片20230318225248](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326017.jpg)



##### 这一步和MySQL5.X版本的有很的大区别，直接选择“Custom（自定义）”，就可以将MySQL安装到非系统盘。

![QQ图片20230318225310](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326413.jpg)



##### 进行安装功能的选择当你第一次进入到这个界面时，右边的框内可能什么也没有，你需要不断点击“MySQL Servers”前的“+”，直到你看见“MySQL Server 8.0.xx-X64”，单击它，然后点击向右的箭头添加到右边的框里，然后在右边的框里点击它，就会出现右下角的蓝字。

![QQ图片20230318225314](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326494.jpg)



##### 接下来就是选择安装路径了，单击上一步出现的蓝字“Advanced Options”，出现下面的界面。第一个位置就是MySQL的安装路径，第二个位置是存放数据用的，建议两个路径分开，不要放在一起。路径下出现的感叹号不要去管它。直接点击“OK”。选好路径之后点击“next”。

> 注意:路径不要有中文。

![QQ图片20230318225816](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326888.jpg)



##### 继续next

![QQ图片20230318225910](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326703.jpg)



##### 选择是

![QQ图片20230318225958](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326611.jpg)



##### 可能弹出需要安装VS++(紫色)环境组件，点击“Execute”进行安装





##### 直接点击“Execute”进行安装

![QQ图片20230318230154](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326544.png)



##### 等待30s左右，点击“next”。

![QQ图片20230318230214](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326659.png)



##### 这里是独立安装\集群安装，默认独立，next

![image-20230830142719937](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230830142719937.png)



##### 这一步建议什么也不要动，直接点击“next”。(详见后面的详细说明)

![QQ图片20230318230313](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326400.jpg)

###### 详细说明：

> 其实在一步MySQL提供了3种可以选择的应用类型（见下图），那么这3种类型有什么区别呢：
>
> Development Computer：开发机，该类型应用将会使用最小数量的内存。
>
> Server Computer：服务器，该类型应用将会使用中等大小的内存。
>
> Dedicated Computer：专用服务器，该类型应用将使用当前可用的最大内存。
>
> 在这里我们选择“Development Computer”就足够我们使用了。

![QQ图片20230318230451](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326673.jpg)



##### 这一步对以后我们使用图形化管理软件(SQLyog)有直接的影响，所以在这一步我们要选择第二个。

![QQ图片20230318230529](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326582.jpg)

###### 详细说明：

> 在这里解释一下第13步为什么要强调选择第二个选项，先来给大家翻译一下两个选项的中文意思：
>
> Use Strong Password Encryption for Authentication(RECOMIMENDED)：
>
> 使用强密码加密进行身份验证（已升级）
>
> Use Legacy Authentication Method (Retain MySQL 5.x Compatibility)：
>
> 使用传统身份验证方法（保留MySQL 5.x兼容性）
>
> 如果我们选择了强密码加密进行身份验证，虽然MySQL采用了强密码加密，但是我们的图形化管理软件（SQLyog）却没有采用强密码加密，这回直接导致SQLyog访问不了我们的MySQL，所以这里我们要选择传统的加密方法（选择了第一种也有解决办法，在这里就不详细说明了）。



##### 然后next 给root用户设置密码，设置完点击next

![QQ图片20230318230617](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326589.jpg)



##### 这一步是服务名称 默认不用管就行了，如果“Windows Service Name”出现感叹号，那你就随便换一个别的名字就行了，然后点击“next”

![image-20230830143001030](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230830143001030.png)



##### 配置权限，直接默认yes，grant... next下一步

![QQ图片20230318230847](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326730.jpg)



##### 点击“Execute”进行安装。

![QQ图片20230318230940](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326520.jpg)



##### 安装过程中 这个地方会卡一会

![QQ图片20230318230949](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326308.jpg)



##### 安装完成之后的样子 单击Finish

![QQ图片20230318231001](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326067.jpg)



##### 点击next

![QQ图片20230318231014](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326776.jpg)



##### 点击“finish”,安装完成

![QQ图片20230318231033](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326443.jpg)







### 二、登录MySQL进行测试。

##### 安装完成后会在系统的开始菜单下出现下图所示的程序，随便打开一个，输入之前设置的密码。

![QQ图片20230318231113](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326325.png)



##### 输入密码后，出现下面的界面，表示MySQL正常，如果出现输入密码后闪退的情况

1. 是原来的mysql没有卸载干净 举个例子 我的是5.0 之前没有安装 就是一个文件夹 然后把服务停止后 直接把文件夹删除了 就没有了

2. 安装mysql8.0之后 没有开启服务 把服务停止了 忘记开启了 也会如此 但是没有1.的可能性大 毕竟是第一次刚安装好

![QQ图片20230318231150](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303182326195.jpg)

然后输入“exit”，退出MySQL