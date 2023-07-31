# Wazuh-HIDS入门

### 一、安装Linux-CentOS 7.9

##### 下载：CentOS-7-x86_64-Minimal-2009.iso  这一版即可，大小为：973M。

```http
https://mirrors.aliyun.com/centos/7.9.2009/isos/x86_64/
```



##### 安装完成后，登录进Linux控制台，先停止系统防火墙，并禁用自启动：

```shell
systemctl stop firewalld
systemctl disable firewalld
```







### 二、单独安装Wazuh-Manager

> 准备一套干净的CentOS 7.9版本Linux服务器（不带UI界面），直接运行以下命令完成安装
>

##### 1.导入rpm源

```shell
rpm --import https://packages.wazuh.com/key/GPG-KEY-WAZUH
```

![image-20230306210211790](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201943747.png)

> 没有错误信息表示安装正确
>



##### 2.编写配置文件，添加以下内容

```shell
vi /etc/yum.repos.d/wazuh.repo
```

```properties
[wazuh]
gpgcheck=1
gpgkey=https://packages.wazuh.com/key/GPG-KEY-WAZUH
enabled=1
name=EL-\$releasever - Wazuh
baseurl=https://packages.wazuh.com/4.x/yum/
protect=1
```



##### 3.安装

```shell
yum -y install wazuh-manager
```

![image-20230306210302101](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201943762.png)

![image-20230306210322435](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201943042.png)



##### 4.启动

```shell
systemctl start wazuh-manager
```

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201944764.png" alt="image-20230306210415987" style="zoom:80%;" />

```shell
systemctl start wazuh-manager		-- 启动
systemctl stop wazuh-manager         -- 停止
systemctl restart wazuh-manager     -- 重启
systemctl status wazuh-manager      -- 查看状态
```



##### 5.查看状态

```shell
systemctl status wazuh-manager
```

![image-20230306210454967](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201944859.png)







### 三、安装Wazuh+Elastic整合环境（可选）

**注意：此操作需要至少消耗5.5G的内存，所以请准备至少6G以上内存，用于了解在Elastic中如何查看Wazuh预警日志，如何编辑Wazuh配置文件、解码器和规则库等。**

> 如果已经理解Elastic或理解本次项目大赛的需求后，也可以选择不安装整合环境。

##### 安装命令只需要一行：

```shell
curl -sO https://packages.wazuh.com/4.3/wazuh-install.sh && sudo bash ./wazuh-install.sh -a -o
```

![image-20230307211203044](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201944131.png)



**<font color='red'>注意：此条指令执行的时间比较长，如果出现安装失败（入下图）的情况，请多执行几次</font>**

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201944748.png" alt="image-20230307211331337" style="zoom:67%;" />

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201944875.png" alt="image-20230307211407251" style="zoom:67%;" />

```text
账号：admin
密码：y3nzNFiReNWpuLwv+v3YK0I8ByVduV7c
```



##### 安装结束后，注意一下生成的用户名 admin 和随机密码，如果无法知识随机密码，也可以使用以下命令找回：

```shell
sudo tar -O -xvf wazuh-install-files.tar wazuh-install-files/wazuh-passwords.txt
```



##### 直接访问： https://Wazuh-IP 即可进入Elastic 界面，在Web页面中查看日志。

```http
https://192....
```

![image-20230307211725926](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201946963.png)



##### 访问时会提示不是私密连接，点击“高级”，进去之后继续访问

![image-20230307211744097](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201946038.png)



##### 访问成功如下

![image-20230307211806129](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201946396.png)



##### 输入账号密码进入管理页面

![image-20230307211956271](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201946458.png)

##### 错误提示是显示的是索引的模板没找到，执行以下指令刷新模板

```shell
curl -X PUT "https://localhost:9200/_template/wazuh" -H 'Content-Type: application/json' -d @wazuh-template.json --key certificates/elasticsearch-ca.pem  -k  -u admin:iWSUeXX6Dp7o+aFKb745+a0KPydTf+Oj
```

![image-20230307212655369](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/xiangwei2/20230307212655.png)



##### 执行完毕之后刷新页面，得到以下界面表示成功

![image-20230307212744400](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/xiangwei2/20230307212744.png)







### 四、测试预警信息

##### 1、启动Wazuh服务器

```shell
systemctl start wazuh-manager
```



##### 2、实时监听预警信息

```shell
cd /var/ossec/logs/alerts/
tail -f alerts.log
```



##### 3、完成以下场景，测试是否出现预警

###### 在Windows环境(CMD)下登录该Linux(虚拟机IP)：

```http
ssh root@192.168.145.130
```

###### 并输入错误的密码，此时会出现类似预警：

```shell
** Alert 1678038441.558040: - pam,syslog,authentication_failed,pci_dss_10.2.4,pci_dss_10.2.5,gpg13_4.3,gdpr_IV_35.7.d,gdpr_IV_32.2,hipaa_164.312.b,nist_800_53_AU.14,nist_800_53_AC.7,tsc_CC6.1,tsc_CC6.8,tsc_CC7.2,tsc_CC7.3,
2023 Mar 06 01:47:21 centqiang->/var/log/secure
Rule: 5557 (level 5) -> 'unix_chkpwd: Password check failed.'
Mar  6 01:47:20 centqiang unix_chkpwd[4207]: password check failed for user (root)

** Alert 1678038443.558457: - syslog,sshd,authentication_failed,gdpr_IV_35.7.d,gdpr_IV_32.2,gpg13_7.1,hipaa_164.312.b,nist_800_53_AU.14,nist_800_53_AC.7,pci_dss_10.2.4,pci_dss_10.2.5,tsc_CC6.1,tsc_CC6.8,tsc_CC7.2,tsc_CC7.3,
2023 Mar 06 01:47:23 centqiang->/var/log/secure
Rule: 5760 (level 5) -> 'sshd: authentication failed.'
Src IP: 192.168.112.1
Src Port: 20897
User: root
Mar  6 01:47:22 centqiang sshd[4203]: Failed password for root from 192.168.112.1 port 20897 ssh2
```

>也可以尝试多次登录失败，看看预警信息会有什么变化。



##### 4、在该服务器环境部署一套Java+Tomcat

###### 在线安装jdk1.8

```shell
yum -y install java-1.8.0-openjdk
```

![image-20230306211142924](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201949680.png)

###### 安装lrzsz文件传输工具

```shell
yum install lrzsz -y
```

![image-20230306211808696](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201949239.png)

###### 利用lrzsz将Tomcat9上传到/opt下，并解压文件

```shell
tar -zxvf tomcat-9.0.tar.gz
```

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201949674.png" alt="image-20230306214304011" style="zoom:80%;" />

###### 启动Tomcat

```shell
/opt/apache-tomcat-9.0.73/bin/startup.sh
```

![image-20230306214404572](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201949772.png)

###### 通过Windows浏览器访问Tomcat

```http
192.168.145.130:8080
```

![image-20230306214443653](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201949977.png)



##### 5、将Tomcat的日志包含进Wazuh监控范围

###### 进入目录：

```shell
cd /var/ossec/etc
```

###### 编辑文件：

```shell
vi ossec.conf
```

###### 在文件末尾添加以下内容：

```conf
<localfile>
    <log_format>syslog</log_format>
    <location>/opt/apache-tomcat-9.0.73/logs/localhost_access_log.*.txt</location>
</localfile>
```

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201950927.png" alt="image-20230306214746615" style="zoom: 67%;" />



##### 6、重启Wazuh，并完成以下操作，确认是否出现预警

```shell
systemctl restart wazuh-manager
```

###### 查看预警

```shell
cd /var/ossec/logs/alerts/
tail -f alerts.log
```

###### 访问一个不存在的URL地址，确认出现404错误预警：

```http
http://192.168.145.130:8080/index.jspx
```

![image-20230312151100740](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201951207.png)

###### 带SQL注入特征进行访问，会出现以下预警：

```http
http://192.168.112.215:8080/index.jspx?id=-1 union select 1,2,3
```

![image-20230312151207840](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201951767.png)

测试成功，现在，你已经基本上熟悉Wazuh的功能了，可以开始着手操作并进行项目开发准备了。







### 六、使用Wazuh日志测试功能

##### 切换工作目录

```shell
cd /var/ossec/bin
```



##### 启动测试功能

```shell
./wazuh-logtest
```

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201951055.png" alt="image-20230307201030494" style="zoom:67%;" />



##### 此时，该程序会等待我们输入，输入一段日志，确认是否能够触发预警，比如

```shell
192.168.73.1 - - [06/Mar/2023:02:10:18 +0800] "GET /index.jspx HTTP/1.1" 404 705
```

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201952919.png" alt="image-20230307201123001" style="zoom:67%;" />



##### 回车，则输出为以下内容，则说明预警规则成功捕获到404状态码异常。

```
**Phase 1: Completed pre-decoding.
	full event: '192.168.73.1 - - [06/Mar/2023:02:10:18 +0800] "GET /index.jspx HTTP/1.1" 404 705'

**Phase 2: Completed decoding.
	name: 'web-accesslog'
	id: '404'
	protocol: 'GET'
	srcip: '192.168.73.1'
	url: '/index.jspx'

**Phase 3: Completed filtering (rules).
	id: '31101'
	level: '5'
	description: 'Web server 400 error code.'
	groups: '['web', 'accesslog', 'attack']'
	firedtimes: '1'
	gdpr: '['IV_35.7.d']'
	mail: 'False'
	nist_800_53: '['SA.11', 'SI.4']'
	pci_dss: '['6.5', '11.4']'
	tsc: '['CC6.6', 'CC7.1', 'CC8.1', 'CC6.1', 'CC6.8', 'CC7.2', 'CC7.3']'
**Alert to be generated.
```

![image-20230307201256736](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303201952579.png)

> 该功能可用于编辑完规则后，在Web页面中对日志进行测试时调用。密码