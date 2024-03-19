## MongoDB、MongoSH安装配置

> 示例版本：7.0.0

### 一、MongoDB

#### 1.1 自定义安装

##### 1.1.1 选中Custom

![image-20230822110937954](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230822110937954.png)



##### 1.1.2 选择路径

![image-20230822111123574](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230822111123574.png)



##### 1.1.3 配置服务账户，Next

![image-20230822111156729](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230822111156729.png)



##### 1.1.4 勾选安装图形化界面

![image-20230822111301472](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230822111301472.png)



##### 1.1.5 安装

![image-20230822111317145](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230822111317145.png)



##### 1.1.6 安装成功

> 安装完会有两个软件：MongoDB数据库、MongoDBCompass图形化界面(类似于Navicat、Postage小海豚)

![image-20230822112004365](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230822112004365.png)



##### 1.1.7 测试

使用MongoDBCompass，默认即可，直接连接

![image-20230822112417589](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230822112417589.png)



##### 1.1.8 成功页

![image-20230822112457563](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230822112457563.png)



---



### 二、MongoSH

> MongoDB6开始数据库和图形界面分离，需要去官网下载MongoSH

```http
https://www.mongodb.com/try/download/shell
```

下载好解压到文件夹，打开Bin文件夹下的mongosh.exe，启动

![image-20230822115433049](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230822115433049.png)



----



### 三、配置环境变量

#### 3.1 配置Path

![image-20230822115819904](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230822115819904.png)

点击浏览添加两个bin文件夹

![image-20230822120017663](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230822120017663.png)





#### 3.2 测试

##### 3.2.1 CMD连接MongoDB

```shell
mongosh
```

示例：![image-20230822120213305](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230822120213305.png)



##### 3.2.2 退出

```shell
quit
```



##### 3.2.3 指令集

|       命令       |                作用                |
| :--------------: | :--------------------------------: |
|  show databases  | 显示当前数据库服务器上的所有数据库 |
|  use <database>  |          切换指定的数据库          |
| show collections |     显示当前数据库中的所有集合     |
|                  |                                    |
|                  |                                    |
|                  |                                    |
|                  |                                    |
|                  |                                    |
|                  |                                    |

