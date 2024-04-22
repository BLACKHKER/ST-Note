## Aliyun-OSS 对象存储开通&配置

### 一、开通阿里云OSS服务

产品中选择对象存储OSS

![image-20230413121741144](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304131327121.png)

立即开通

![image-20230413121948209](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304131327549.png)



---



### 二、创建桶

bucket列表 → 创建bucket

![image-20230413130421995](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304131327068.png)

开通

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304131327712.png" alt="image-20210718203922369" style="zoom:33%;" />

指定桶名字以及存储区域

![image-20230413130858725](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304131327530.png)

![image-20230413130921785](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304131327139.png)



---



### 三、设置AccessKey

![image-20230413131032553](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304131327849.png)

点击“开始使用子用户AccessKey”

![image-20230413131315229](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304131328721.png)

点击前往治理

![image-20230413131619895](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304131328579.png)

点击“创建用户”

![image-20230413131710509](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304131328614.png)

指定登录名和显示名称，选择“Open API调用访问”，点击“确定创建”

![image-20230413131902739](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304131328912.png)

**<font color='red'>创建完毕之后，在用户列表下有用户信息和AccessKey ID和Accesskey Secret，请立即将Access Key保存</font>**

![image-20230413132256264](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304131328975.png)



---



### 四、指定用户权限

点击用户信息

![image-20230413132515936](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304131328102.png)

选择”权限管理“选项卡，点击”添加权限“

![image-20230413132603427](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304131328251.png)

授予全部权限

![image-20230413132646734](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304131328194.png)

