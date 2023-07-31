# 4  分支操作（Git灵魂）

## 4.1 基本概念

假设你准备开发一个新功能，但是需要两周才能完成，第一周你写了50%的代码。

如果立刻提交，由于代码还没写完，不完整的代码库会导致别人不能干活了。

如果等代码全部写完再一次提交，又存在丢失每天进度的巨大风险。

![未命名文件](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212221607877.png)



这时可以创建一个属于你自己的分支，别人看不到，还继续在原来的分支上正常工作。

想提交就提交，直到开发完毕后，再一次性合并到原来的分支上，这样，既安全，又不影响别人工作。

![image-20221222160933691](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212221609748.png)



在实际工作过程中，同时推进多个分支是非常正常的。（我见过最多的是武汉智慧城市效果105个分支！！！）。

再比如比如项目有免费版和收费版，那么免费版为主分支，收费版作为子分支另外收费，这样好吃是可以灵活的切换。

![image-20221222161111833](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212221611981.png)





每次commit时，Git都把它们串成一条时间线，这条时间线就是一个分支。

截止到目前，只有一条时间线，在Git里，这个分支叫主分支，即`master`分支。

同时会有一个`HEAD`指针指向当前分支，而`master`指向最新的提交，所以代码是最新的

![git分支基本概念](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212221704105.png)





每次提交，`master`分支都会向前移动一步，这样，随着你不断提交，`master`分支的线也越来越长。



![git分支基本概念 (1)](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212221705379.png)





一个分支就是一个指针。

当我们创建新的分支，例如`dev`时，Git新建了一个指针叫`dev`，指向最新的提交。 

![image-20221222173043792](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212221730853.png)





从现在开始，针对`dev`分支新提交一次后，`dev`指针往前移动一步：

![image-20221222173342221](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212221733281.png)



![image-20230228113700367](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202302281137511.png)



假如我们在`dev`上的工作完成了，就可以把`dev`合并到`master`上。Git怎么合并呢？最简单的方法，直接把Head指针往前移动一下：



![image-20221222173424130](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212221734189.png)



合并完分支后，甚至可以删除`dev`分支。删除`dev`分支就是把`dev`指针给删掉

![image-20221222173520936](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212221735003.png)

| 命令                 | 作用                         |
| -------------------- | ---------------------------- |
| git branch 分支名    | 创建分支                     |
| git branch -v        | 查看分支                     |
| git checkout 分支名  | 切换分支                     |
| git merge 分支名     | 把指定的分支合并到当前分支上 |
| git branch -d 分支名 | 删除分支                     |



## 4.2 查看分支

~~~shell
$ git branch -v
* master 5499f3f 第四次提交
~~~



## 4.3 创建分支

*表示目前所在的分支

~~~shell

$ git branch dev

$ git branch -v
  dev    5499f3f 第四次提交
* master 5499f3f 第四次提交

~~~

![image-20221222174218806](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212221742840.png)



## 4.4 切换分支

~~~shell
$ git checkout dev
Switched to branch 'dev'

$ git branch -v
* dev    5499f3f 第四次提交
  master 5499f3f 第四次提交

~~~

![image-20221222174234908](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212221742941.png)







## 4.5 合并分支

在dev分支上修改`hello.txt`文件，添加如下内容

![image-20220223154524991](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212211732043.png)



添加至暂存区，并提交至本地版本库

~~~shell
$ git add hello.txt
$ git commit -m 'dev commit'
~~~



切换至master分支，在master分支上合并dev分支

~~~shell
$ git checkout master
$ cat hello.txt # 没有dev分支的内容
# 执行合并
$ git merge dev
# 查看文件内容
$ cat hello.txt # 此时可以看到dev分支修改的内容
~~~



强烈建议：

以后在开发项目的时候，如果有子分支，尽量不要去改主分支的代码。



# 5 远程仓库（码云）

点击右上角 “+” 选择新建仓库

![image-20220314094828224](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212211736434.png)

填写仓库名称，仓库路径会根据名称自动生成，最后点击创建。

![image-20221222194913045](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212221949123.png)





## 5.3. 设置SSH密匙

仓库创建后，默认提供了两种仓库地址：

![image-20220314095855168](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212211736834.png)

- 若使用HTTPS方式，后续在上传代码时，需要在本地输入码云的账号密码进行验证：
- 若使用SSH方式则需要在本地生成秘钥，并将生成的公钥信息上传至平台，后续上传代码时就不需要输入账号密码了，此种方式较为方便。
- 

需要在**Git Bash**中使用命令，如果在CMD中会出现不识别命令的情况。

~~~shell
ssh-keygen -t ed25519 -C "xxxxx@xxxxx.com" 
~~~



```shell
$ ssh-keygen -t ed25519 -C "434679924@qq.com"
Generating public/private ed25519 key pair.
Enter file in which to save the key (/c/Users/43467/.ssh/id_ed25519):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /c/Users/43467/.ssh/id_ed25519
Your public key has been saved in /c/Users/43467/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:25qlizQE48H9p8LA02PVafxAOh4ubs+Ahy+Df0se0yw 434679924@qq.com
The key's randomart image is:
+--[ED25519 256]--+
|          .      |
|   . .   = .     |
|    = . = *      |
|   o = = + o     |
|    = * S . .    |
|     X = =       |
|   .o E = o      |
|  . oB.@ =       |
|   ..+=.B.       |
+----[SHA256]-----+
```



<img src="https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212211736563.png" alt="image-20220314102649594" style="zoom:80%;" />

通过查看 `~/.ssh/id_ed25519.pub` 文件内容，获取到你的 public key。

~~~shell
cat ~/.ssh/id_ed25519.pub
~~~



复制生成后的公钥（id_ed25519.pub）信息，跳转到**个人设置**，注意不是仓库设置！点击SSH公钥，将本地生成的信息添加到码云中。

![image-20221222210912286](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212222109375.png)





![image-20221222210844941](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212222108039.png)



## 5.4 远程仓库操作

| 命令                               | 作用                                             |
| ---------------------------------- | ------------------------------------------------ |
| git remote -v                      | 查看当前所有远程地址别名                         |
| git remote add 别名 远程地址       | 将别名与远程地址关联                             |
| git push 别名 分支                 | 推送本地分支上的内容到远程仓库                   |
| git clone 远程地址                 | 将远程仓库的内容克隆到本地                       |
| git pull 远程库地址别名 远程分支名 | 将远程仓库对应分支内容拉下来后与当前本地分支合并 |
| git remote rm 别名                 | 删除别名与远程的关联                             |

## 5.5 添加远程仓库别名

~~~shell
$ git remote add origin git@gitee.com:dev-liuwei/webcode.git
~~~

添加后，远程库的名字就是`origin`，这是Git默认的叫法，也可以改成别的，但是`origin`这个名字一看就知道是远程库。

查看当前所有远程地址别名

~~~shell
$ git remote -v
origin  git@gitee.com:dev-liuwei/test.git (fetch)
origin  git@gitee.com:dev-liuwei/test.git (push)
~~~

## 5.6 推送分支

~~~shell
$ git push origin master
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 197 bytes | 197.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
remote: Powered by GITEE.COM [GNK-6.3]
To gitee.com:dev-liuwei/test.git
 * [new branch]      master -> master
~~~

如果要推送其他分支，比如`dev`，就改成：

```shell
$ git push origin dev
```

## 5.7 克隆远程仓库到本地

![image-20220314104814555](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212211736010.png)

~~~shell
$ git clone git@gitee.com:dev-liuwei/test.git
~~~

~~~shell
$ cd test
$ git remote -v
origin  git@gitee.com:dev-liuwei/test.git (fetch)
origin  git@gitee.com:dev-liuwei/test.git (push)
~~~

克隆操作会拉去远程仓库代码，并初始化本地仓库，同时建立别名。

## 5.8 拉取分支

~~~shell
$ git pull origin master
~~~

克隆时，默认只会拉取远程的master分支，如果需要在其他分支上工作，则需要单独拉取，执行以下命令，本地分支会基于远程origin/dev创建，并与之关联。

~~~shell
$ git checkout -b dev origin/dev
~~~

上述操作因为非常常见，当checkout的分支不存在且与远端分支名字相同时，则可以进行简化：

~~~shell
$ git checkout dev
~~~

现在，就可以在`dev`上继续修改，然后，时不时地把`dev`分支`push`到远程：

```shell
$ git push origin dev
```

## 5.9 分支关联

如果本地的分支是直接创建出来的（git branch 分支名称）,则本地的分支与远程的分支默认是无关联的，若只使用`git pull` 或 `git push`，没有指定分支，则会提示先进行分支关联，

~~~shell
$ git push
fatal: The current branch dev has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin dev
~~~

可以建立本地分支和远程分支的关联

~~~shell
# git branch --set-upstream branch-name origin/branch-name
$ git branch --set-upstream dev origin/dev
$ git push --set-upstream origin test
~~~

这样后续就可以直接使用`git pull` 或 `git push`进行操作了

也可以在push时，添加`-u`参数，如：

```shell
$ git push -u origin dev
```

查看本地分支与远程分支的关联关系：

~~~shell
$ git branch -vv
~~~

## 5.10. 注意事项

从本地推送分支，如果远端已经有了新的提交，则使用git push时，会推送失败

![image-20220317161442577](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212211736719.png)

此时应该先`git pull`，拉取远端新的提交至本地。

`git pull`命令相当于`git fetch`+`git merge`，也就是将远程分支内容拉取到本地，再与本地分支进行合并，因此如果远端有新的提交，本地也有新的提交，则需要以提交的方式进行合并，有可能会产生冲突，需要手动解决（参考分支合并章节）。

# 6 idea编程工具Git操作

## 6.1. 环境准备

#### 检查Git环境

![image-20221222225954459](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212222259579.png)

#### 初始化本地库

![image-20220223173107642](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212211736055.png)



#### 添加Gitee插件

用户支持码云远程仓库提交代码

![image-20221222235244380](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212222352479.png)



#### 配置gitignore文件

.gitignore用于指定哪些文件不需要添加到版本管理中

```swift
/mtk/ 过滤整个文件夹
*.zip 过滤所有.zip文件
/mtk/do.c 过滤某个具体文件
```

![image-20220223180831947](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212211736160.png)

![image-20220223182120455](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212211736451.png)

## 6.2. 常见操作

#### 添加到暂存区

![image-20220223173643823](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212211736799.png)

#### 提交到本地库

![image-20220223173737733](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212211736121.png)

#### 查看历史提交信息

![image-20220223173905030](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212211736665.png)

#### 创建及切换分支

![image-20220223174108783](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212211736355.png)

![image-20220223174652066](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212211736496.png)

#### 合并分支

![image-20220223174749598](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212211736410.png)

## 6.3. 远程仓库操作

#### 关联远程仓库

![image-20220223174926865](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212211736193.png)

![image-20220223175033717](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212211735789.png)

#### 推送与拉取

![image-20220223175751568](git的使用.assets/image-20220223175751568.png)

![image-20220223175835474](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212222356633.png)

![image-20220223180059474](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212211735822.png)

#### 克隆

<img src="https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202212211735918.png" alt="image-20220223180225580" style="zoom:67%;" />







# 二 Vue组件化开发



## 2.1 组件基本概念

![27c00f153a898e17ee65a3964b3641ce](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202302272336175.jpeg)



![2da125afb0ed0dfdc0c8e8f2c183e8fa](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202302272336284.jpeg)







![123c67309a84b222330209184c617574](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202302272336293.jpeg)





![5d7dc7bc889f7b1d6a7006d8f67cc471](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202302272336075.jpeg)







## 2.2 传统方式的弊端



现在有一个页面需求，引用了3个样式文件，3个js文件



![网页原型 (1)](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202302272336160.png)









多个网页复用的情况

![网页原型](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202302272336347.png)





## 2.3 组件开发优势

组件就是一块砖，哪里需要哪里搬：

人家写好的组件直接copy过来用， 比如element-ui ，很多........

把你写的组件，分享给整个小组

1、开箱即用（反正，组件之间东西写一套，哪个要用直接引用组件即可）

2、互相协作（组件之间既可以相互独立，又可以相互独立）

3、方便定位问题

4、组件可以嵌套（小零件组装成一个完整的系统）

5、复用

![网页原型](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202302272336753.png)



VUE官方：推荐我们要有一个root组件

![f5b10df64683dc6743023951cabc8dce](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202302272336980.jpeg)

![963fda136dabee4dd07cc5e1d280180f](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202302272336137.jpeg)





用户的姓名是：xxx

用户的年龄是：xxx



## 2.4 组件的定义Vue.extend

组件为了复用，在定义上不能写el，因为组件是拿来用的，哪里需要哪里搬。

另外data必须用函数返回，因为多个地方使用同一个组件，数据必须独立。

组件的命名规则有讲究，用帕斯卡命名法，除非用了脚手架

```js
var Person = Vue.extend({
        template:`
          <div>
            <p>学生姓名：{{name}}</p>
            <p>学生年龄：{{age}}</p>
            <button @click="show">点击中大奖</button>
          </div>
        `,
        data() {
            return {
                name:'张三',
                age:20
            }
        },
        methods:{
            show() {
                alert(this.name)
            }
        }
    })

```



## 2.4 局部组件注册compoents

把组件主动添加到vm上，想给哪个容器用就给哪个用。

如果组件没有添加到vm上，直接使用的话会报错

```js
let vm = new Vue({
    el:'#root',
    components:{
        person:person
    }
})
```

![image-20221208114017951](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202302272336044.png)



## 2.4 全局组件注册Vue.compoent

全局组件相对于局部组件来说，范围更大，不需要每个vm实例单独写一份

```js
Vue.component('person' , person);

let vm = new Vue({
    el:'#root',
})
```





## 2.5 组件使用

编写组件名称就可以了

```html
<div id="root">
   <person></person>
    <person></person>
</div>
```





## 2.6 组件嵌套

![image-20221208135819195](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202302272336200.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
<body>

<div id="root">
    <person></person>

</div>

<script src="js/vue.js" type="text/javascript"></script>
<script>


    let student = Vue.extend({
        template:`
          <div>
            <p>学生姓名：{{name}}</p>
            <p>学生年龄：{{age}}</p>
          </div>
        `,
        data() {
            return {
                name:'小名',
                age:20
            }
        }
    })


    var person = Vue.extend({
        template:`
          <div>
            <p>人员姓名：{{name}}</p>
            <p>人员年龄：{{age}}</p>
            <student></student>
          </div>

        `,
        data() {
            return {
                name:'张三',
                age:20
            }
        },
        components:{
            student:student
        }
    })



    // Vue.component('person' , person);

    let vm = new Vue({
        el:'#root',
        components:{
            person:person
        }
    })

    console.log(vm)
</script>
</body>
</html>
```





## 2.7 组件上下级传值

![image-20230103231636670](https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/wenjian/202302281252706.png)

### 2.7.1 向下传递



父组件通过属性名=属性值来传递

```html
 <StudentApp name="李四" age="20"></StudentApp>
  </div>
```



子组件添加属性props

```js
 {
 ....
  props:{
    name:{
      type:String,
      required:true
    },
    age:{
      type:Number,
      required:true
    }
  }
}
```



### 2.7.2 向上传递



子组件：

```html
 <button @click="setData">传递到父组件</button>
```



```js
  methods: {
     setData() {
       this.$emit("getData", this.msg);
     }
   }
```



父组件：

```js
methods: {
     getData(data) {
       this.msg = data;
     }
  },
```



