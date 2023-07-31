## Nginx安装

### 下载

#### 官网：

```http
http://nginx.org/
```

##### 注意是windows版本的：

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304271907158.png" alt="image-20221019115053127" style="zoom:67%;" />





#### 自己指定的安装目录解压缩

![image-20230427191025450](S:/woniu/TypoaPicture/image-20230427191025450.png)







### 启动Nginx

#### 进入nginx文件夹，在DOS中打开该文件夹，执行以下指令启动nginx

![image-20230427195904059](S:/woniu/TypoaPicture/image-20230427195904059.png)

```shell
start nginx
```

![image-20230427195925313](S:/woniu/TypoaPicture/image-20230427195925313.png)

##### 可以通过以下指令查看nginx是否启动成功

```shell
tasklist /fi "imagename eq nginx.exe
```

![image-20230427200215575](S:/woniu/TypoaPicture/image-20230427200215575.png)



##### 如果什么都没有，就要检查一下日志，在nginx目录中的logs文件夹下error.log

常见的错误：

- 端口号被占用
- nginx文件夹路径含中文
- 其他错误就详细看log中的描述



##### 如果错误是80端口被占用导致启动不成功，修改Nginx端口：

在conf目录下找到nginx.conf文件打开，找到server这个节点，修改端口号， 改为其他没被占用的端口即可。

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304271916676.png" alt="image-20221019115914630" style="zoom:67%;" />

修改完成后保存再次到dos命令窗口，重新启动，并检查是否启动成功，之后打开浏览器访问刚才的域名及端口，出现欢迎页就说明部署成功了。

```http
http://127.0.0.1:8800
```

###### 如果用的是8800端口注意修改地址后面的端口号

![image-20230427200357890](S:/woniu/TypoaPicture/image-20230427200357890.png)







### 常用命令：

|             命令             |                功能                 |
| :--------------------------: | :---------------------------------: |
|         start nginx          |            启动nginx服务            |
|        nginx -s stop         |            停止nginx服务            |
|       nginx -s reload        |              重载配置               |
| taskkill /f /t /im nginx.exe | 关闭nginx其他服务，这样才能彻底关闭 |

