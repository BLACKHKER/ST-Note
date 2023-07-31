### 一、NAS机(宿主机)创建访问账户

#### WIN + R 输入以下指令，打开用户账户控制

```apl
netplwiz
```

![image-20230705225642033](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230705225642033.png)





#### 添加用户

![image-20230705225851037](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230705225851037.png)





#### 不使用微软账户登录

![image-20230705225915578](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230705225915578.png)





#### 选择本地账户

![image-20230705230021334](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230705230021334.png)





#### 添加用户(Windows多用户)

> 其他终端通过该用户的账户信息进行登录访问共享磁盘

![image-20230705230046186](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230705230046186.png)







### 二、创建并给用户分配共享磁盘权限

#### 选中要共享的磁盘 → 属性 → 共享 → 高级共享 

![image-20230705230652210](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230705230652210.png)





####  勾选共享此文件夹 → 权限

![image-20230705230723338](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230705230723338.png)





#### 添加用户

![image-20230705230814486](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230705230814486.png)





#### 高级

![image-20230705230841625](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230705230841625.png)





#### 立即查找 → 在框里面找到刚才添加的用户 → 选中 → 点击确认添加该用户

![image-20230705231141721](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230705231141721.png)





#### 点击确定关闭窗口，在该页面分配刚刚添加的用户的权限(完全控制) → 一路确认即可

![image-20230705231306373](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230705231306373.png)







### 三、(可选)配置防火墙

> 访问不到共享磁盘时执行该流程

#### 控制面板 → 防火墙 → 高级设置

![image-20230705232009924](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230705232009924.png)





#### 添加入站规则

![image-20230705232053271](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230705232053271.png)





#### 端口

![image-20230705232116939](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230705232116939.png)





#### TCP → 自定义开放端口号

![image-20230705232222002](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230705232222002.png)





#### 允许连接 → 下一步(配置文件) → 最后随便取个名称

![image-20230705232343262](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230705232343262.png)







### 连接NAS机

#### 复制NAS共享磁盘网络路径(共享磁盘 → 属性 → 共享)

##### 一般格式如下：

```http
\\Zhao\s
```

![image-20230705232817689](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230705232817689.png)





#### 找到NAS机的IP地址

![image-20230705233302588](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230705233302588.png)





#### 映射网络驱动器

**![image-20230705232950274](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230705232950274.png)**





#### 配置NAS，连接

![image-20230705233508899](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230705233508899.png)

![image-20230705233553685](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230705233553685.png)





#### 配置成功

![image-20230705233643190](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230705233643190.png)

