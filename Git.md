# Git

### 一、工作流程

> 工作区(WorkSpace)→暂存区(Stage)→Git仓库(Repository)→远程库(Remote)

#### 提交流程

##### 工作区

正在编写代码的区域，通过add提交到暂存区



##### 暂存区

保存被add提交的代码，可以继续通过commit提交到本地库



##### 本地库

本地的最终保存位置，可以继续通过push提交到远程库

![image-20230321100339474](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303211004750.png)



---



### 二、基本命令

| 命令                                        | 作用                                               |
| ------------------------------------------- | -------------------------------------------------- |
| git clone 仓库地址                          | 克隆仓库到本地                                     |
| git init                                    | 初始化本地库                                       |
| git add 文件名                              | 添加到暂存区                                       |
| git commit -m "日志信息" 文件名             | 提交到本地库                                       |
| git push <远程仓库别名> <本地分支名>        | 将本地仓库分支推送到远程仓库                       |
| git status                                  | 查看本地库状态                                     |
| git diff                                    | 查看仓库改动                                       |
| git log                                     | 查看日志                                           |
| git reflog                                  | 查看历史记录                                       |
| git reset --hard 版本号                     | 版本穿梭                                           |
| git merge / rebase <分支名>                 | 合并分支                                           |
| git pull <远程仓库名> <远程分支名>          | 拉取远程仓库的数据到本地远程分支，并进行merge合并  |
| git pull –-rebase <远程仓库名> <远程分支名> | 拉取远程仓库的数据到本地远程分支，并进行rebase合并 |
| git reset 文件名/*                          | 回滚指定文件/所有的git add                         |



---



### 三、基本使用

#### 初次使用配置

##### 签名

> Git在进行commit时，必须进行签名，通过全局配置用户名和邮箱，作为身份标识
>
> 注意，此处设置的用户签名和远端代码托管中心的账号没有任何关系！

~~~shell
git config --global user.name 'username'
git config --global user.email 'email@163.com'
~~~

###### 实例：

```sh
git config --global user.name 'blackhker'
git config --global user.email 'bhkdos@qq.com'
```



##### 创建GIT仓库

> 在需要执行仓库目录执行CMD操作来Git，或者GitBashHere

![image-20230731102754118](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230731102754118.png)



##### 初始化本地仓库

> 会在当前目录中自动创建.git目录（隐藏），此目录用于Git跟踪管理版本库。

~~~shell
$ git init
~~~



![image-20221222150600600](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303211009698.png)





#### 使用版本控制

##### 添加

> 添加到暂存区(每次修改都需要add才能commit)

```shell
git add 文件名 / *(全部)
```

![image-20231016223217742](S:\TypoaPicture\image-20231016223217742.png)



##### 提交

> 提交暂存区中的修改，到本地仓库

```shell
git commit -m "本次提交的备注"
```

![image-20231016223301282](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231016223301282.png)



##### 推送

###### 获取仓库地址

> 在云仓库(GitHub、Gitee)创建仓库，会有仓库地址的链接
>

![image-20231016215954976](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231016215954976.png)

###### 本地仓库连接远程仓库

```shell
git remote add origin 仓库地址
git remote add origin https://gitee.com/blackhker/git-study.git
```

![image-20231016221328919](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231016221328919.png)

###### 提交本地仓库中的代码到gitee

> `-u` 参数设置该远程仓库为默认的上游，以后就可以只git push; origin为Git默认的远程仓库名称

```shell
git push -u 远程仓库名 远程分支名
git push -u origin master
```

![image-20231016223459696](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231016223459696.png)

![image-20231016223022349](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231016223022349.png)

> 在git中,“push -u”的意思是将本地的分支版本上传到远程合并,并且记录push到远程分支的默认值
>
> 当添加“-u”参数时,表示下次继续push的这个远端分支的时候推送命令就可以简写成“git push”。





#### 拉取

##### 克隆网络仓库到本地

> 在要克隆到的文件夹下打开cmd执行命令

```shell
git clone 仓库地址
git clone https://gitee.com/blackhker/git-study.git
```

![image-20231016221533345](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231016221533345.png)

###### 可能提示输入gitee的账号密码，输入后完成克隆(克隆了一个空的仓库会警告)，包含隐藏的git

![image-20231016221736496](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231016221736496.png)

![image-20231016221814722](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231016221814722.png)





#### 其他相关

##### 获取git状态

```shell
git status
```

###### 已经提交全部更改

> 没有需要提交的内容，工作树已清空

![image-20231016224029877](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231016224029877.png)

###### 有更改，但未添加到缓存区

> 使用git add 文件名 来进行添加

![image-20231016224122276](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231016224122276.png)

###### 已经添加到缓存区但未提交

![image-20231016224222901](S:\TypoaPicture\image-20231016224222901.png)



##### 获取修改的内容

```shell
git diff
```

> 查询到修改了文件TestC.txt，减一行，加零行，删除了ccc
>

![image-20231016224346602](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231016224346602.png)

 

##### 获取日志

> 每次提交都有一个ID，黄色字体：commit后面的字符串就是当前提交的ID，对应远程仓库的ID

```shell
git log
```

![image-20231016224546260](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231016224546260.png)

![image-20231016224639711](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231016224639711.png)

###### 显示当前指针的位置及历史记录

> HEAD代表指针，指针指向的位置代表当前版本所在位置(分支、版本)

```shell
git reflog
```

![image-20231016224754627](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231016224754627.png)



##### 版本回退(※谨慎使用)

> `-n` 参数告诉 Git 不要自动创建新的提交，而 `^..HEAD` 范围表达式指定了要撤消的提交范围

```shell
git revert -n 版本号^..HEAD		-- 移动指针到某版本号(注意^号)
git revert -n fe91f6642cc1128270384160c8026343d27b2535^..HEAD
```

###### 回退到历史版本，删除了Test.txt

![image-20231016225252706](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231016225252706.png)

###### 回退后的状态是待提交(删除了bbb.java)，未提交到本地库，重新add、commit并push

![image-20231016225323989](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231016225323989.png)
