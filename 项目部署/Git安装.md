## Git安装

### 一、官网

#### 1.1 地址

```http
https://git-scm.com/
```



---



### 二、下载

> 非Windows版本点击左下角<font color="#f40">Downloads</font>，官方提供三个版本：
>
> - Windows
> - MacOS
> - Linux

![image-20240320133248180](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240320133248180.png)



---



### 三、安装

> 以下基于Git 2.43.0版本 64位操作系统，且机器自带旧版Git的情况。
>
> 机器无Git时，本文档中某些步骤可能没有，跳过该步骤即可

1. 协议，Next

   ![image-20240112103518589](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240112103518589.png)

2. 按需选中，每日检查Git是否有更新，Next

   ![image-20240112103654353](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240112103654353.png)

3. 默认，Next

   第二个选项为：重写每个仓库的默认主分支名[^1]

   ![image-20240112103942843](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240112103942843.png)

4. SSH客户端，默认，Next

   > 使用默认的Git自带的SSH，第二个选项为配置自己的SSH客户端

   ![image-20240112104046687](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240112104046687.png)

5. 实验选项，不勾选，Next

   ![image-20240112104249079](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240112104249079.png)

6. 替换文件，Install

   > 替换正在使用的文件，也可能是没有关闭Git窗口，此时是不能安装的

   ![image-20240112104723455](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240112104723455.png)

7. 安装成功

   ![image-20240112104952471](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240112104952471.png)

---



### 四、测试

1. 右键桌面，查看是否有`git bash here`、`git GUI here`选项

   ![image-20240320134732276](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240320134732276.png)

2. 选中`git bash here`，测试该指令：

   ```shell
   git -v
   ```

   ![image-20240320134840443](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20240320134840443.png)



---



### 解释文档

[^1]:默认主分支名为master