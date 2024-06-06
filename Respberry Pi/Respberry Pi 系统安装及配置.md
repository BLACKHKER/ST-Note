## Respberry Pi系统安装及环境配置

### 一、板载结构

#### 1.1 Respberry Pi 4B

![树莓派4B板载结构](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/%E6%A0%91%E8%8E%93%E6%B4%BE4B%E6%9D%BF%E8%BD%BD%E7%BB%93%E6%9E%84.jpg)





#### 1.2 Respberry Pi 5

TODO



---



### 二、镜像下载

> 镜像下载配合第三方烧录工具(官方镜像、第三方烧录工具)，官方的烧录工具可以直接烧录，不需要额外下载

#### 2.1 官方站(Raspberry Pi OS)

```http
https://www.raspberrypi.com/software/operating-systems/
```

![image-20231030095257243](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231030095257243.png)



---



### 三、系统安装

#### 3.1 SD卡格式化工具

##### 3.1.1 SD Card Formatter

```http
https://www.sdcardformatter.com/
```

![image-20231225100134736](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231225100134736.png)



#### 3.2 烧录工具

##### 3.2.1 官方安装工具(Raspberry Pi Imager)

```http
https://www.raspberrypi.com/software/
https://downloads.raspberrypi.org/imager/imager_latest.exe
```

![image-20231030095126372](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231030095126372.png)



##### 3.2.2 第三方安装工具

###### Win32 Disk Imager

```http
https://sourceforge.net/projects/win32diskimager/
```

###### USB Image Tool

```http
https://www.alexpage.de/
```





#### 3.3 SD卡格式化

> 以下使用SD Card Formatter为例

![image-20231225103923736](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231225103923736.png)





#### 3.4 安装系统/烧录镜像

##### 3.4.1 官方工具安装

选择运行设备

![image-20231225104037304](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231225104037304.png)

操作系统，这里选择x64位

![image-20231225104147954](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231225104147954.png)

要烧写的SD卡，Next

![image-20231225104239064](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231225104239064.png)

按需选择是否个性化安装的系统如何设置

![image-20231225104343268](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231225104343268.png)

主要设置

![image-20231225104530814](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231225104530814.png)

开启SSH

![image-20231225104550136](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231225104550136.png)

其他配置默认即可

![image-20231225104648008](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231225104648008.png)

安装

![image-20231225104737761](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231225104737761.png)

![image-20231225104746588](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231225104746588.png)

开始写入

![image-20231225104806550](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231225104806550.png)



---



### 四、蓝牙

#### 4.1 更新/升级系统软件包

```shell
-- 更新软件包列表
sudo apt update
-- 升级已安装软件包
sudo apt upgrade
```





#### 4.2 安装蓝牙软件包

1. `bluetooth`：蓝牙相关的核心库和工具
2. `pi-bluetooth`：用在树莓派上的支持蓝牙功能的软件包
3. `bluez`：管理蓝牙设备和协议的库和工具
4. `blueman`：图形界面的蓝牙管理器，可以管理蓝牙设备以及链接
5. `mplayer`：多媒体播放器，支持音视频播放，用于测试蓝牙功能(蓝牙耳机)

```shell
sudo apt install bluetooth pi-bluetooth bluez blueman mplayer
```





#### 4.3 蓝牙命令行工具

```shell
-- 启动命令行工具 全称bluetooth contrl
bluetoothctl
-- 告诉蓝牙管理器开启代理功能，自动处理蓝牙设备的配对和认证
agent on
-- 扫描设备，扫描蓝牙设备，显示MAC地址
scan on/off
-- 配对设备，根据扫描到的MAC进行配置
pair MAC地址
-- 连接设备，可能会自动连接，就不需要这条命令，输入quit退出
connect MAC地址
```

##### 4.3.1 扫描实例

```
[bluetooth]# scan on
Discovery started
[CHG] Controller E4:5F:01:26:55:90 Discovering: yes
[NEW] Device 4A:E4:8E:E3:BC:54 4A-E4-8E-E3-BC-54
[CHG] Device 9C:19:C2:4D:88:DC Name: Redmi Buds 3
```



##### 4.3.2 配对示例

```shell
[bluetooth]# pair 9C:19:C2:4D:88:DC
Attempting to pair with 9C:19:C2:4D:88:DC
[CHG] Device 9C:19:C2:4D:88:DC Connected: yes
```



##### 4.3.3 连接示例

```shell
[Redmi Buds 3]# connect 9C:19:C2:4D:88:DC
Attempting to connect to 9C:19:C2:4D:88:DC
[CHG] Device 9C:19:C2:4D:88:DC Connected: yes
Connection successful
quit
```





#### 4.4 测试

```shell
mplayer xxx.mp3
```



---



### 五、输入法

> 输入法有三种：谷歌拼音、云拼音、太阳拼音
>
> 输入法有BUG，跟内置的Chroium有冲突，打不了中文

#### 5.1 apt安装

```shell
-- fcitx是个框架，同时安装其他软件包用空格分隔
sudo apt install fcitx fcitx-googlepinyin fcitx-module-clouldpinyin fcitx-sunpinyin
-- 重启生效
sudo reboot
```



---



### 六、SSH
