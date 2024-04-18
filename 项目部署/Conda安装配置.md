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

#### 5.1 Pycharm打开终端报错

**问题现象**

配置好Conda虚拟环境的项目，打开终端报错，提示`conda init powershell`

![image-20240418151131260](A:\Typora\TyporaPicture\image-20240418151131260.png)

**报错原因**

重装过Conda，例如第一次安装不在C盘，后面卸载安装到了D盘

**解决方案**

打开C盘的该文件：

```http
C:\用户\用户名\文档\WindowsPowershell\profile.ps1
```

修改Conda可执行文件的目录，改为安装Conda的实际目录即可。一般是在AnaConda下的Scripts下。

如果依然失效，使用以下命令以允许本地计算机运行本地脚本

```shell
set-executionpolicy remotesigned
```



----



### 解释文档

[^1]:只包含最基本的内容——Python与Conda，以及相关的必须依赖项，其他的包/库需要自己安装。
[^2]:打包的集合，里面预装好了Conda、Python、众多Packages、科学计算工具等等，包含所有包。