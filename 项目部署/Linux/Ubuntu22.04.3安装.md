## Ubuntu 22.04.3安装

### 一、下载

#### 1.1 网址

##### 1.1.1 Ubuntu 官方

```http
https://cn.ubuntu.com/download/desktop
https://ubuntu.com/download/desktop
```



##### 1.1.2 国内/外第三方镜像网址：

```http
https://launchpad.net/ubuntu/+cdmirrors
```





#### 1.2 通过镜像站下载

##### 1.  在页面找到对应的国家(中国)

![image-20230906200840868](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230906200840868.png)



##### 2. 选择院校

> 这里选择上海交通大学

![image-20230906201046152](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230906201046152.png)



##### 3. 选择镜像源网址

![image-20230906201128298](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230906201128298.png)



##### 4. 选择版本

> 版本的命名为：ubuntu-版本号-desktop-amd64.iso

![image-20230906201303597](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230906201303597.png)



---



### 二、安装

> 本范例使用VMWare的版本为17Pro

#### 1. 创建新的虚拟机

![image-20230906201448490](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230906201448490.png)





#### 2. 选择典型

![image-20230906201809858](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230906201809858.png)





#### 3. 稍后安装操作系统

![image-20230906201824505](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230906201824505.png)





#### 4. 选择Linux，Ubuntu64位

![image-20230906201942904](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230906201942904.png)





#### 5. 选择安装位置

![image-20230906202049945](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230906202049945.png)





#### 6. 磁盘容量、拆分方式

> 自己决定，容量最好在50GB

![image-20230906202154266](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230906202154266.png)





#### 7. 点击完成创建虚拟机

![image-20230906202229486](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230906202229486.png)





#### 8. 编辑虚拟机设置

- 内存：主机内存32G就设置8G，16G就设置4G
- 处理器：数量1，内核4
- CD/DVD：使用ISO映像文件，文件就是下载的ISO文件
- 网络适配器：安装时关闭网络

![image-20230906202935953](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230906202935953.png)

![image-20230906203018912](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230906203018912.png)





#### 9. 开启虚拟机，选择第一项，尝试或者安装Ubuntu

![image-20230906203217811](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230906203217811.png)





#### 10. 进入章鱼界面会卡一会，等待

![image-20230906203805491](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230906203805491.png)





#### 11. 选择中文简体，安装Ubuntu

![image-20230906204231514](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230906204231514.png)





#### 12. 键盘选择Chinese

> 此处会卡一会，不要动

![image-20230906204311332](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230906204311332.png)





#### 13. 选择最小安装

![image-20230906204817846](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230906204817846.png)





#### 14. 选择清除整个磁盘并安装Ubuntu

![image-20230906204922229](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230906204922229.png)





#### 15. 继续

![image-20230906204949994](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230906204949994.png)





#### 16. 地址选择上海

![image-20230906205000022](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230906205000022.png)





#### 17. 配置用户名、密码

> 此处配置的是默认用户，Ubuntu默认不创建root用户

![image-20230906205039222](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230906205039222.png)





#### 18. 安装过程

![image-20230906205102327](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230906205102327.png)



---



### 三、系统配置

#### 3.1 Root用户的创建

默认已经有root用户了，但是没有密码，使用普通用户的密码是不行的，这时候需要给root用户设置一个密码，就可以使用`su`进入管理员模式了

```shell
sudo passwd root -- 设置root用户密码
```





#### 3.2 删除系统自带软件

1. ```shell
   sudo apt-get remove libreoffice-common
   ```

2. ```shell
   sudo apt-get remove thunderbird totem rhythmbox simple-scan gnome-mahjongg aisleriot gnome-mines cheese transmission-common gnome-sudoku
   ```

3. ```shell
   sudo apt autoremove simple-scan gnome-mahjongg aisleriot gnome-mines cheese transmission-common gnome-sudoku
   ```





#### 3.3 安装开发环境

##### 3.3.1 QT

```http
https://kevinglaser.blog.csdn.net/article/details/117202517
```



##### 3.3.2 Clion和C/C++环境，以及OpenGL

```http
https://kevinglaser.blog.csdn.net/article/details/117531615
```



##### 3.3.3 JAVA和IDEA

```http
https://kevinglaser.blog.csdn.net/article/details/116334487
```





#### 3.4 删除多余的垃圾缓存文件

##### 3.4.1 清理旧版本的软件缓存

```shell
sudo apt-get autoclean
```



##### 3.4.2 清理所有软件缓存

```shell

```

