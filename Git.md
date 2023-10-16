## Git

> 学习网址：https://learngitbranching.js.org

### 工作流程

#### Git分区

> 工作区(WorkSpace)→暂存区(Stage)→Git仓库(Repository)→远程库(Remote)

##### 工作流程

###### 工作区

正在编写代码的区域，通过add提交到暂存区

###### 暂存区

保存被add提交的代码，可以继续通过commit提交到本地库

###### 本地库

本地的最终保存位置，可以继续通过push提交到远程库

![image-20230321100339474](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303211004750.png)





#### 基本命令

##### 主要流程

| 命令                                        | 作用                                               |
| :------------------------------------------ | :------------------------------------------------- |
| git clone 仓库地址                          | 克隆仓库到本地                                     |
| git init                                    | 初始化本地库                                       |
| git add 文件名                              | 添加到暂存区                                       |
| git commit -m "日志信息" 文件名             | 提交到本地库                                       |
| git remote add origin <仓库地址>            | 将本地库连接到远程仓库地址                         |
| git push <远程主机名> <本地分支名>          | 将本地仓库分支推送到远程仓库                       |
| git pull <远程仓库origin> <远程分支 master> | 拉取远程仓库的数据到本地远程分支，并进行merge合并  |
| git pull –-rebase <远程仓库> <远程分支>     | 拉取远程仓库的数据到本地远程分支，并进行rebase合并 |
| git reset 文件名/*                          | 回滚指定文件/所有的git add                         |



##### 分支

| 命令                                | 作用               |
| :---------------------------------- | :----------------- |
| git branch <分支名>                 | 创建分支           |
| git reset --hard 版本号             | 版本穿梭           |
| git merge / rebase <分支名>         | 合并分支           |
| git checkout <分支名>               | 切换分支           |
| git checkout -b <分支名>            | 创建并切换到该分支 |
| git branch -m <原分支名> <新分支名> | 分支更名           |



##### 日志信息

| 命令       | 作用           |
| :--------- | :------------- |
| git status | 查看本地库状态 |
| git diff   | 查看仓库改动   |
| git log    | 查看日志       |
| git reflog | 查看历史记录   |



---



### 基本使用

#### 初始化

##### 初次使用配置

> git在进行commit时，必须进行签名，通过全局配置用户名和邮箱，作为身份标识
>
> **注意：此处设置的用户签名和远端代码托管仓库的账号没有任何关系**

~~~shell
git config --global user.name '用户名'
git config --global user.email '邮箱'
~~~

###### 实例：

```shell
git config --global user.name 'blackhker'
git config --global user.email 'email@xxx.com'
```



##### 创建Git仓库

> 在需要使用git的目录，通过cmd操作来git，或者Git Bash Here

![image-20230911152234563](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230911152234563.png)



##### 初始化本地仓库

> 会在当前目录中自动创建.git目录（隐藏），此目录用于Git跟踪管理版本库。

~~~shell
$ git init
~~~

![image-20230731102754118](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230731102754118.png)

![image-20221222150600600](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303211009698.png)





#### 本地仓库

##### 添加到暂存区

> 每次修改都需要add才能commit

```shell
git add 修改的文件名
```

![image-20230321195155770](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303211952393.png)



##### 提交暂存区中的修改，到本地仓库

```shell
git commit -m "本次提交的备注"
```

![image-20230321195208907](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303211952028.png)



##### 提交本地仓库中的代码到gitee

```shell
git push -u origin master
```

![image-20230321200043565](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303212000134.png)

![image-20230321200109830](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303212001382.png)

> 在git中,“push -u”的意思是将本地的分支版本上传到远程合并,并且记录push到远程分支的默认值
>
> 当添加“-u”参数时,表示下次继续push的这个远端分支的时候推送命令就可以简写成“git push”。





#### 远程仓库

##### 获取仓库地址

> 在远程仓库(GitHub、Gitee)创建仓库，会有仓库地址的HTTPS链接
>

![image-20230322093538626](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303220935178.png)



##### 推送内容到远程仓库

```shell
git remote add origin 仓库地址
git remote add origin https://gitee.com/blackhker/note.git
```

![image-20230731103136165](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230731103136165.png)



##### 克隆远程仓库内容到本地

> 在要克隆到的文件夹下打开cmd执行命令

```shell
git clone 仓库地址
git clone https://gitee.com/blackhker/java96-test.git
```

![image-20230321192245535](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303211952012.png)

###### 提示输入gitee的账号密码，输入后完成克隆(警告是克隆了一个空的仓库)，生成一个新的文件夹，包含隐藏的git

![image-20230321192552957](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303211952775.png)

![image-20230321192600473](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303211952293.png)





#### 版本控制

##### 版本回退(※谨慎使用)

```shell
git revert -n 版本号^..HEAD		-- 移动指针到某版本号(注意^号)
git revert -n fe91f6642cc1128270384160c8026343d27b2535^..HEAD
```

###### 回退到历史版本，删除了bbb.java

![image-20230322095320305](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303231532576.png)

###### 回退后的状态是待提交(删除了bbb.java)，未提交到本地库，重新add、commit并push

![image-20230322095533844](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303231532182.png)





#### 日志相关

##### 获取git状态

```shell
git status
```

###### 已经提交全部更改

> 没有需要提交的内容，工作树已清空

![image-20230321200757325](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303212007683.png)

###### 有更改，但未添加到缓存区

> 使用git add 文件名 来进行添加

![image-20230321200843337](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303212011074.png)

###### 已经添加到缓存区但未提交

> 使用git commit 提交缓存区中的内容到本地仓库

![image-20230321201149248](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303212011962.png)



##### 获取修改的内容

```shell
git diff
```

查询到修改了文件bbb.java修改了Public Test1为Test2

![image-20230321214707836](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303212217534.png)

 

##### 获取日志

```shell
git log
```

![image-20230321221715493](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303212217767.png)

> 每次提交都有一个ID，黄色字体：commit后面的字符串就是当前提交的ID，对应远程仓库的ID

![image-20230321222125166](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303212221193.png)

###### 显示当前指针的位置及历史记录

```shell
git reflog
```

![image-20230321222645631](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303212226912.png)

> HEAD代表指针，指针指向的位置代表当前版本所在位置(分支、版本)
