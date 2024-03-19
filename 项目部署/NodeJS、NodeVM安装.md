## NodeJS、NodeVM安装

### 一、NodeJS

#### 1.1 官网

```http
https://nodejs.org/en
```





#### 1.2  配置下载源

> npm包管理器进行下载时，获取数据的资源地址，国内地址访问速度较快

##### 1.2.1 镜像地址

###### 官方源

```http
https://registry.npmjs.org/
```

###### 淘宝源

```http
https://registry.npm.taobao.org/
```

###### cnpm源

```http
http://r.cnpmjs.org/
```

###### 阿里源

```http
https://npm.aliyun.com/
```



##### 1.2.2 配置方式

```shell
npm config set registry “源地址”
```





----



### 二、NodeVM

> NodeVM是NodeJS的版本管理器(node version manager)，便于切换NodeJS不同版本
>
> 在安装版本管理器之前，需要删除已安装的 Node.js 或 npm 的程序

#### 2.1 下载

```http
https://github.com/coreybutler/nvm-windows/releases
```

![image-20230815122011806](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230815122011806.png)

- nvm-noinstall.zip： 这个是绿色免安装版本，但是使用之前需要配置
- nvm-setup.zip：这是一个安装包，下载之后点击安装，无需配置就可以使用，方便。
- Source code(zip)：zip压缩的源码
- Sourc code(tar.gz)：tar.gz的源码，一般用于linux系统



##### 2.1.1 安装

> 16.20.2安装后的npm-v版本是8.19.4

```shell
nvm install 16.20.2
```

使用nvm命令查看是否安装成功：

![image-20230815124400199](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230815124400199.png)





#### 2.2 NVM for Windows的使用

> 安装后打开PowerShell，尝试使用 windows-nvm 来列出当前安装的 Node 版本（此时应为无）
>
> **注意安装后需要新开一个dos窗口执行nvm命令，否则不识别！**

##### 2.2.1查看node版本

![image-20230815125013851](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230815125013851.png)



##### 2.2.2 命令

> 依次执行install → use才能切换到指定版本

|          含义           |           命令           |
| :---------------------: | :----------------------: |
|           nvm           |       查看NVM详情        |
|         nvm ls          |  列出当前安装的Node版本  |
|   nvm list available    | 查找当前支持的Node版本号 |
|  nvm install <version>  |    安装指定版本的Node    |
|    nvm use <version>    |    切换指定版本的Node    |
| nvm uninstall <version> |    卸载指定版本的Node    |

