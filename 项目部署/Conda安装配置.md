## Conda安装配置

### 前言

Conda是一个包管理器，类似于Maven(Java依赖管理器)，同时包含了环境管理器，管理不同版本的Python。



---



### 一、下载

#### 1.1 官方站

##### 1.1.1 MiniConda

![image-20240409110827133](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240409110827133.png)

> 默认的是MiniConda[^1]，跟AnaConda[^2]的区别是，MiniConda只包含基本的内容。

```http
https://conda.io/projects/conda/en/latest/index.html
```



##### 1.1.2 AnaConda

```http
https://www.anaconda.com/download/
```





#### 1.2 三方站

##### 1.2.1 清华开源软件镜像站

![image-20240409110854966](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240409110854966.png)

```http
https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/?C=M&O=D
```



---



### 二、安装

#### 2.1 Conda

##### 2.1.1 安装步骤

1. Next。

![image-20240409134114005](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240409134114005.png)

2. 协议，I Agree。

![image-20240409134137161](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240409134137161.png)

3. 选择安装类型，所有用户都安装。

![image-20240409134232795](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240409134232795.png)

4. 配置安装路径。

![image-20240409134332931](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240409134332931.png)

5. 同时安装对应该Conda版本的Python，安装。

![image-20240409134422846](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240409134422846.png)

6. 安装成功，使用	

![image-20240409134538112](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240409134538112.png)



##### 2.1.2 测试

1. 打开Anaconda Prompt(不带PowerShell的)

2. 输入

   ```shell
   conda -V
   ```

   或

   ```shell
   conda --version
   ```




---



### 三、配置

#### 3.1 更改Conda虚拟环境安装路径

> 建议不更改虚拟环境的位置，除非Conda安装在了C盘，如果已经在其他盘了，就别动。
>
> conda虚拟环境一定要在安装目录的envs下

1. 展示所有配置。

```shell
conda config --show
```

![image-20240409135937102](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240409135937102.png)

2. 在想安装虚拟环境的路径下创建一个文件夹，示例在D盘创建了一个CondaEnvs的文件夹：

![image-20240409135422352](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240409135422352.png)

3. 使用以下命令将指定刚刚的文件夹为虚拟环境默认安装路径。

```shell
conda config --add envs_dirs D:\CondaEnvs
```

4. 重新查看是否设置成功，以下为成功的情况。

![image-20240409135852938](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240409135852938.png)





#### 3.2 配置到Pycharm中

> Conda的可执行文件(exe)在安装目录的`Scripts`里面

1. 右上角设置

![image-20240410100256510](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240410100256510.png)

2. Settings

![image-20240410100337943](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240410100337943.png)

3. Project:项目名 → Python Interpreter → Add Intedpreter → Add Local Interpreter

![image-20240410100700022](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240410100700022.png)

4. 选中Conda Environment，点击右面的文件夹，去找Conda的可执行文件，点击Load即可添加成功

![image-20240410100656969](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240410100656969.png)

5. 虚拟环境选择自己创建的，带路径的是默认的环境

![image-20240410101030498](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240410101030498.png)





#### 3.2 换源

##### 3.2.1 新增源

阿里源

> 可能失效

```shell
conda config --add channels https://mirrors.aliyun.com/anaconda/pkgs/free
conda config --add channels https://mirrors.aliyun.com/anaconda/pkgs/main
conda config --add channels https://mirrors.aliyun.com/anaconda/pkgs/msys2
conda config --add channels https://mirrors.aliyun.com/anaconda/pkgs/r
```

清华源

```shell
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/pro
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2  
```

设置运行conda命令时，是否显示远程仓库URL

```shell
conda config --set show_channel_urls yes
```



##### 3.2.2 删除源

```shell
conda config --remove-key channels
```



##### 3.2.3 查看源

```shell
conda config --show channels
```



---



### 四、命令

#### 4.1 基础命令

| 命令                | 操作                  |
| ------------------- | --------------------- |
| conda update conda  | 更新 Conda 到最新版本 |
| conda info          | 显示关于 Conda 的信息 |
| conda -V/ --version | 显示 Conda 版本       |





#### 4.2 库/包

| 命令                                         | 操作             |
| -------------------------------------------- | ---------------- |
| conda upgrade --all                          | 升级全部库       |
| conda update [packagename]                   | 升级一个包       |
| conda install [packagename]                  | 安装包           |
| conda installl [packagename1] [packagename2] | 安装多个包       |
| conda install [packagename]=[version]        | 安装固定版本的包 |
| conda remove packagename                     | 移除一个包       |
| conda list                                   | 查看所有包       |





#### 4.3 虚拟环境

> ENV(virtual environment)

| 命令                                               | 操作                         |
| -------------------------------------------------- | ---------------------------- |
| conda create --name [env-name]                     | 创建虚拟环境                 |
| conda create -n [env_name] python=[python_version] | 创建指定Python版本的虚拟环境 |
| conda activate [env-name]                          | 激活环境                     |
| conda deactivate                                   | 退出环境                     |
| conda env list                                     | 列出所有可用的环境           |



---



### 五、常见问题及解决方案

#### 5.1 Pycharm终端报错

##### 5.1.1 找不到Conda

**问题现象**

配置好Conda虚拟环境的项目，打开终端报错，提示`conda init powershell`

![](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240418151131260.png)

**报错原因**

1. 原先旧的Conda卸载了，重装了一个，或不在一个盘；
1. 未配置环境变量

**解决方案**

1. 在conda的Prompt窗口输入：

```shell
where conda
```

![image-20240419101343944](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240419101343944.png)

2. 将下列目录添加到环境变量中

![image-20240419101628536](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240419101628536.png)



##### 5.1.2 终端禁止执行脚本

**问题现象**

> File C:\Users\xxx cannot be loaded because running scripts is disabled on this system
>
> 无法加载文件xxx，因为在此系统上禁止运行脚本

**报错原因**

Windows自动配置了脚本执行策略，禁止三方执行脚本/受限.

该问题一般出现在Windows10上

**解决方案**

[可选]进入Powershell，查询执行策略，Restricted为限制了脚本执行的执行策略

```shell
get-ExecutionPolicy
```

![QQ_1722327412543](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/QQ_1722327412543.png)

管理员方式进入CMD，执行以下命令，解除脚本执行策略限制，Y同意执行

```shell
set-ExecutionPolicy RemoteSigned
```

![QQ_1722327554405](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/QQ_1722327554405.png)



----



### 解释文档

[^1]:只包含最基本的内容——Python与Conda，以及相关的必须依赖项，其他的包/库需要自己安装。
[^2]:打包的集合，里面预装好了Conda、Python、众多Packages、科学计算工具等等，包含所有包。