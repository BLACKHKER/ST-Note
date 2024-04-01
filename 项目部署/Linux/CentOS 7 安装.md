## CentOS 7 安装

### 一、镜像下载

#### 1.1 官方镜像站

##### 1.1.1 CentOS

```http
https://centos.p2hp.com/
```

CentOS Linux和CentOS Stream的区别：

Linux是稳定版，最完善的版本(CentOS 7)，Stream是RedHat最新版(发行版)



#### 1.2 三方镜像站

##### 1.2.1 I Tell You

```http
https://next.itellyou.cn/Original/
```



---



### 二、系统安装

> 以下安装基于虚拟机软件 `VMWare 16`

#### 2.1 简易安装

##### 2.1.1 虚拟机创建

1. 新建虚拟机，选择典型。

![image-20230314173936763](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303141953992.png)

2. 选择`安装程序光盘映像文件`的方式，高版本VMWare会自动执行简易安装，下一步。

![image-20230314174517448](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303141953924.png)

3. 配置简易安装信息，下一步

![image-20230314184550672](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303141953041.png)

4. 给虚拟机命名，选择系统的安装位置

![image-20230314184630578](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303141953339.png)

5. 指定磁盘容量，建议50GB，内存吃紧可以20。(后期需要可以改)

![image-20230314184639160](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303141953387.png)

6. 自定义硬件，配置虚拟机的性能(处理器核心数、内存大小、网络等)，完成

![image-20230314184713029](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303141953345.png)



##### 2.1.2 虚拟机系统安装

> 需要时双击enter(回车)

1. 自动开启CentOS7系统

![image-20230314184937326](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303141953796.png)

2. 自动下载系统文件(1382)

![image-20230314190027836](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303141953344.png)

3. 安装完毕

![image-20230314193322244](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303141953672.png)





#### 2.2 非简易安装

> VMware14及以下不支持简易安装

##### 2.2.1 虚拟机系统安装

1. 自动启动后进入该界面，连续两次回车，开始安装系统

![image-20230314194004347](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303141954064.png)

2. 选择语言，继续

![image-20230314194043595](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303142001170.png)

3. 设置日期和时间

![image-20230314194108708](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303142001074.png)

![image-20230314194127396](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303142001269.png)

4. 选择安装类型，选择GNOME桌面，否则不是图形化界面(命令行)

![image-20230314194215168](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303142001102.png)

5. 完成，选项暂时变成灰色，等待配置检查完成变成黑色

![image-20230314194257400](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303142001730.png)

6. 选择安装位置，完成

![image-20230314194338092](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303142001568.png)

7. 开始安装

![image-20230314194356921](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303142001319.png)

8. 安装过程中，设置root密码

![image-20230314194428958](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303142002419.png)

![image-20230314194437427](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303142002557.png)

9. 完成，等待系统完成安装

![image-20230314194509120](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303142002076.png)

10. 重启

![image-20230314194534885](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303142002085.png)

11. 自动选择启动项，未接受许可

![image-20230314194631208](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303142002519.png)

12. 同意许可协议，完成

![image-20230314194659891](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303142002302.png)

13. 完成配置

![image-20230314194718365](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303142002778.png)

14. 语言设置为中文

![image-20230314194741554](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303142002918.png)

![image-20230314194757468](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303142002549.png)

![image-20230314194815745](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303142002166.png)

15. 选择时区

![image-20230314194838719](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303142002192.png)

16. 配置在线账号，没梯子(VPN)，跳过

![image-20230314194917308](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303142002388.png)

17. 设置用户名和密码

![image-20230314194957003](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303142002197.png)

![image-20230314195002846](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303142002385.png)

18. 开始使用，进入完成页面

![image-20230314195017488](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303142002018.png)

![image-20230314193322244](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303141953672.png)