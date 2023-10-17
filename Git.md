# Git

### 1 工作流程

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



### 2 基本命令

| 命令                                          | 作用                                               |
| --------------------------------------------- | -------------------------------------------------- |
| git clone <仓库地址>                          | 克隆仓库到本地                                     |
| git init                                      | 初始化本地库                                       |
| git remote <远程仓库别名> <远程仓库地址>      | 关联别名到远程库                                   |
| git remote -v                                 | 查看配置别名的所有远程库                           |
| git remote rm <远程仓库别名>                  | 删除别名与远程分支的关联                           |
| git add <文件名>                              | 添加到暂存区                                       |
| git reset <文件名> / *                        | 回滚指定文件 / 所有的git add                       |
| git commit -m "日志信息" <文件名>             | 提交到本地库                                       |
| git push <远程仓库别名> <本地分支名>          | 将本地仓库分支推送到远程仓库                       |
| git pull <远程仓库别名> <远程分支名>          | 拉取远程仓库的数据到本地远程分支，并进行merge合并  |
| git pull –-rebase <远程仓库别名> <远程分支名> | 拉取远程仓库的数据到本地远程分支，并进行rebase合并 |
| git status                                    | 查看本地库状态                                     |
| git diff                                      | 查看仓库改动                                       |
| git log                                       | 查看日志                                           |
| git reflog                                    | 查看历史记录                                       |
| git reset --hard <版本号>                     | 版本穿梭                                           |
| git merge / rebase <分支名>                   | 合并分支                                           |



---



### 3 基本使用

#### 初次配置

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





#### 版本控制

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

> 远程仓库别名一般为origin，约定俗成

```shell
git remote add 远程仓库别名 仓库地址
git remote add origin https://gitee.com/blackhker/git-study.git
```

![image-20231016221328919](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231016221328919.png)

###### 提交本地仓库中的代码到gitee

> `-u` 参数设置该远程仓库为默认的上游(关联分支)，以后就可以只git push; origin为Git默认的远程仓库名称

```shell
git push -u 远程仓库名 远程分支名
git push -u origin master
```

![image-20231016223459696](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231016223459696.png)

![image-20231016223022349](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231016223022349.png)

> 在git中,“push -u”的意思是将本地的分支版本上传到远程合并,并且记录push到远程分支的默认值
>
> 当添加“-u”参数时,表示下次继续push的这个远端分支的时候推送命令就可以简写成“git push”。





#### 克隆/拉取

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



##### 拉取远程仓库代码到本地

> 

```shell
git pull origin master
```



默认拉取远程master分支，如果需要单独拉取其他分支，执行以下命令

> 本地分支会基于远程origin/dev创建，并与之关联

```shell
git checkout -b dev origin/dev
```

TODO 图片



---



### 分支

#### 常用命令

| 命令                                             | 作用                             |
| ------------------------------------------------ | -------------------------------- |
| git branch <分支名>                              | 创建分支                         |
| git branch -v                                    | 查看分支(所有)                   |
| git checkout <分支名>                            | 切换分支                         |
| git checkout -b <分支名>                         | 创建并切换到分支                 |
| git checkout -b <分支名> <远程仓库别名>/<分支名> | 基于远程分支，关联到本地新建分支 |
| git merge <分支名>                               | 把指定的分支合并到当前分支上     |
| git branch -d <分支名>                           | 删除分支                         |

![image-20231017140215640](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231017140215640.png)





#### 常用分支

| 分支         | 含义                    |
| ------------ | ----------------------- |
| main(master) | 生产分支(V1.0、V2.0...) |
| release      | 测试分支                |
| bug          | BUG分支                 |
| develop      | 开发分支                |
| feature      | 需求分支(多个)          |





#### 概念

每次commit时，Git都把它们串成一条时间线，这条时间线就是一个分支。

如果只有一条时间线，在Git里，这个分支叫主分支，即`master`分支。

同时会有一个`HEAD`指针指向当前分支，而`master`指向最新的提交，所以代码是最新的：

![git分支基本概念](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202212221704105.png)

每次提交，`master`分支都会向前移动一步，这样，随着你不断提交，`master`分支的线也越来越长：

![git分支基本概念 (1)](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202212221705379.png)

一个分支就是一个指针，当我们创建并切换到新的分支，例如`dev`，Git新建一个指针`dev`，指向最新的提交：

![image-20221222173043792](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202212221730853.png)

从现在开始，针对`dev`分支新提交一次后，`dev`指针往前移动一步：

![image-20221222173342221](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202212221733281.png)

假如我们在`dev`上的工作完成了，就可以把`dev`合并到`master`上，Git底层是直接把Head指针往前移动一下：

![image-20230228113700367](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202302281137511.png)

![image-20221222173424130](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202212221734189.png)

合并完分支后，甚至可以删除`dev`分支。删除`dev`分支就是把`dev`指针给删掉：

![image-20221222173520936](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202212221735003.png)





#### 关联分支

> 如果本地的分支是直接创建出来的（git branch 分支名称）,则本地的分支与远程的分支默认是无关联的，若只使用`git pull` 或 `git push`，没有指定分支，则会提示先进行分支关联

TODO 图片

##### 本地分支关联远程分支

```shell
git branch --set-upstream <分支名> <远程仓库别名>/<远程分支名>
git branch --set-upstream dev origin/dev
```

###### -u参数关联远程分支

```shell
$ git push -u origin dev
```





#### 合并分支

> 在Git中，`merge`和`rebase`是两种常用的代码合并策略，它们有一些区别和适用场景

##### Merge（合并）

Merge是将一个分支的更改合并到另一个分支上的操作。
在合并过程中，Git会创建一个新的合并提交，将两个分支的更改合并在一起。
合并保留了原始分支的完整历史记录和提交信息，可以清晰地看到哪些更改来自哪个分支。
Merge适用于合并公共分支、团队合作和保留完整的历史记录。

![img](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/v2-1ab32e79dc84b38d9d8044968c5c1dbd_720w.webp)



##### Rebase（变基）

Rebase是将一个分支的更改应用到另一个分支上的操作
在变基过程中，Git会将一系列提交复制到目标分支上，并创建新的提交
变基后的提交历史线是线性的，看起来像是按顺序提交的，没有合并提交的存在
Rebase可以使提交历史保持整洁和线性，避免了合并提交的杂乱
Rebase适用于在本地分支上进行提交整理、保持干净的提交历史和与上游分支同步

![img](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/v2-165bfe942dfbe93aa14d0ee7743f2050_720w.webp)



##### 主要区别

1. merge 会多出一次 merge commit，rebase不会
2. merge 的提交树是非线性的，rebase 的提交树是线性的（通过重写提交历史）
3. Merge会创建一个新的合并提交，保留了原始分支的完整历史记录，而Rebase会创建新的提交，并将原始分支的提交复制到目标分支上
4. Merge保留了分支之间的分叉结构和合并提交，而Rebase会将提交历史线变成线性的，像是按顺序提交的

选择合适的合并策略取决于具体情况和需求

如果希望保留完整的分支历史记录和合并信息，使用Merge

如果更关注提交历史的整洁性和线性，以及与上游分支的同步，使用Rebase



---



### 其他相关

#### 获取git状态

```shell
git status
```

##### 已经提交全部更改

> 没有需要提交的内容，工作树已清空

![image-20231016224029877](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231016224029877.png)



##### 有更改，但未添加到缓存区

> 使用git add 文件名 来进行添加

![image-20231016224122276](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231016224122276.png)



##### 已经添加到缓存区但未提交

TODO

![image-20231016224222901](S:\TypoaPicture\image-20231016224222901.png)





#### 获取修改的内容

```shell
git diff
```

> 查询到修改了文件TestC.txt，减一行，加零行，删除了ccc
>

![image-20231016224346602](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231016224346602.png)

 



#### 获取日志

> 每次提交都有一个ID，黄色字体：commit后面的字符串就是当前提交的ID，对应远程仓库的ID

```shell
git log
```

![image-20231016224546260](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231016224546260.png)

![image-20231016224639711](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231016224639711.png)

##### 显示当前指针的位置及历史记录

> HEAD代表指针，指针指向的位置代表当前版本所在位置(分支、版本)

```shell
git reflog
```

![image-20231016224754627](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231016224754627.png)





#### 版本回退(※谨慎使用※)

> `-n` 参数告诉 Git 不要自动创建新的提交，而 `^..HEAD` 范围表达式指定了要撤消的提交范围

```shell
git revert -n 版本号^..HEAD		-- 移动指针到某版本号(注意^号)
git revert -n fe91f6642cc1128270384160c8026343d27b2535^..HEAD
```

回退到历史版本，删除了Test.txt：

![image-20231016225252706](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231016225252706.png)

回退后的状态是待提交(删除了Test.txt)，未提交到本地库，重新add、commit并push：

![image-20231016225323989](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231016225323989.png)
