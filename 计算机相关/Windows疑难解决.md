## Windows疑难解决

### 微软系统工具安装问题

#### 错误0xC1800103–0X90002

##### 问题现象

制作u盘启动盘，提示错误0xC1800103–0X90002

u盘曾经被制作成过windows 10的启动盘，使用完后仅作格式化，没有删除分区彻底恢复成普通盘。



##### 解决方案

CMD管理员

![image-20231215150120953](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231215150120953.png)

进入磁盘管理

```shell
diskpart
```

![image-20231215150333598](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231215150333598.png)

查看磁盘列表

```shell 
list disk
```

![image-20231215150456391](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231215150456391.png)

选中要格式化的磁盘

```shell
select disk 1
```

![image-20231215150623941](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231215150623941.png)

清空该磁盘所有分区， 提示成功地清除了磁盘为成功

```shell
clean
```

进入磁盘管理，给硬盘分配驱动器号、简单分区(新建简单卷)

![image-20231215150903404](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20231215150903404.png)

再次尝试即成功