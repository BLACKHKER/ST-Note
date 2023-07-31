## Redis主从复制+哨兵模式

> 在一台电脑上模拟多个redis服务器

### 主从复制

#### 一、复制配置文件

##### 将redis.conf拷贝两份，分别打开修改以下内容

92行：修改Redis端口prot	主：6379	从：6380、6381

158行：修改从Redis的保存进程ID文件的文件名(防止启动多个Redis失败)	pidfile /var/run/redis_6379.pid 

171行：修改日志文件名	logfile "redis6379.log"

253行：修改Redis持久化文件名	dbfilename dump6379.rdb





#### 二、分别启动三台服务器

##### 通过三个配置文件启动服务器

```shell
redis-server redis6379.conf
redis-server redis6380.conf
redis-server redis6381.conf
```



##### 开启三个终端连接不同的redis服务器

```shell
redis-cli -h 127.0.0.1 -p 6379		或者		redis-cli -p 6379

redis-cli -h 127.0.0.1 -p 6380		或者		redis-cli -p 6380

redis-cli -h 127.0.0.1 -p 6381		或者		redis-cli -p 6381
```



##### 查看服务器角色

> 目前三个服务器都是role：master，表示自己就是主服务器

```shell
info replication
```

![image-20230417110406939](S:/woniu/TypoaPicture/image-20230417110406939.png)





#### 三、设置两个服务器为从服务器

##### 在想设定为从服务器的dos下输入： 设置当前服务器的隶属于哪个主服务器

```shell
slaveof 127.0.0.1 6379
slaveof 主服务器IP	主服务器端口
```



##### 效果

###### 主服务器：

![image-20230417111325406](S:/woniu/TypoaPicture/image-20230417111325406.png)

###### 从服务器(down则是表示主机离线)：

![image-20230417111415676](S:/woniu/TypoaPicture/image-20230417111415676.png)



SLAVEOF NO ONE
执行该命令后，该 Redis 服务器将不再是任何其他 Redis 服务器的从服务器。



#### 测试

##### 主机中存放内容时，会自动将数据同步到从机上

###### 主机



###### 从机





##### 在从机上不能进行set key value的操作，因为在redis中主从策略为主机做写的操作，从机做读的操作

###### 从机执行set：

<img src="https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/xiangwei/20211019171925.png" alt="image-20211019171925713" style="zoom:50%;" />

当从机关闭然后重新启动时，不会自动变成从机，还是需要再次指定其为从机

6380/6381

<img src="https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/xiangwei/20211019171943.png" alt="image-20211019171943033" style="zoom:50%;" />

当主机关闭或遇到问题停止运行，然后再次启动之后还是会做为主机，同时与从机保持主从关系

6379

<img src="https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/xiangwei/20211019171959.png" alt="image-20211019171959397" style="zoom:50%;" />

#### 主从复制原理

<img src="https://woniumd.oss-cn-hangzhou.aliyuncs.com/java/xiangwei/20211019172013.png" alt="image-20211019172013563" style="zoom:50%;" />







### 哨兵模式

##### 单个哨兵配置操作步骤

- 所有redis配置文件中的bind 127.0.0.1中的IP地址改为0.0.0.0

- 分别在所有的redis配置文件中搜索查看是否包含有 slave xxx.xxx.xxx.xxx的配置，如果有则删除。搜索字符串方式：在命令模式下输入”/要搜索的字符串”，按n搜索下一个

- 启动主机6379

<img src="S:/woniu/TypoaPicture/20211019172147.png" alt="image-20211019172146924" style="zoom:50%;" />

启动从机6380

<img src="S:/woniu/TypoaPicture/20211019172157.png" alt="image-20211019172157594" style="zoom:50%;" />

启动从机6381

<img src="S:/woniu/TypoaPicture/20211019172209.png" alt="image-20211019172209103" style="zoom:50%;" />



分别在从机6380、6381中设置主机

<img src="S:/woniu/TypoaPicture/20211019172221.png" alt="image-20211019172221283" style="zoom:50%;" />

- 在redis目录下创建sentinel6379.conf，并添加以下内容

```
protected-mode no				# 关闭保护模式，方便测试
port 26379						# 哨兵的端口
sentinel monitor mymaster 192.168.41.226 6379 1		# 192.168.41.226：主机ip 6379：端口 1：至少几个哨兵认为主机下线时进行故障切换
```

注意：不要添加注释

- 输入redis-sentinel sentinel6379.conf 启动哨兵，看到以下界面表示成功

<img src="S:/woniu/TypoaPicture/20211019172325.png" alt="image-20211019172325633" style="zoom:50%;" />

此时哨兵已经对主机以及从机进行监控

- 在主机6379中输入shutdown命令关闭主机，然后注意观察哨兵的反应（反应会有点慢）

- 哨兵

<img src="S:/woniu/TypoaPicture/20211019172343.png" alt="image-20211019172343834" style="zoom:50%;" />

可以看到现在的主机已经变成6381了，我们可以在6381上查看一下自己的身份

<img src="S:/woniu/TypoaPicture/20211019172355.png" alt="image-20211019172355607" style="zoom:50%;" />

可以看到身份已经是master了

那么如果现在原来的主机6379又重新启动，会是什么样的情况呢？

<img src="S:/woniu/TypoaPicture/20211019172408.png" alt="image-20211019172408476" style="zoom:50%;" />

可用看到原来的主机现在变为从机了

保存，并重新启动6379

<img src="S:/woniu/TypoaPicture/20211019172421.png" alt="image-20211019172421310" style="zoom:50%;" />

此时查看6380的身份，可以看到6379已经成为它的从机了

<img src="S:/woniu/TypoaPicture/20211019172434.png" alt="image-20211019172433972" style="zoom:50%;" />

##### 多哨兵操作步骤：

- 拷贝两份sentinel6379.conf，分别为命名为sentinel6380.conf、sentinel6380.conf

- 分别打开两个文件，修改sentinel的运行端口为26380、26381，同时将选举哨兵数修改成2

- 分别运行两个哨兵