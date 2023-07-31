# Docker

## Linux部署Docker容器

### 一、卸载Docker

##### 1.卸载老版本的Docker：如果安装过Docker，卸载Docker：

```shell
sudo yum remove docker docker-common docker-selinux docker-engine
```

![image-20230316195649357](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101009154.png)

![image-20230316195702344](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101009419.png)

> 显示Complete表示成功



##### 2.可能卸载失败，检查当前安装了哪些跟docker有关的软件包：

```shell
yum list installed | grep docker
```

###### 如果有，使用以下命令删除这些包：

```shell
yum -y remove docker...
```







### 二、部署Docker

##### 1.切换到用户目录，创建docker文件夹，通过XShell将两个Docker的rpm软件包上传到docker文件夹

```shell
cd /home/用户名
mkdir docker
cd docker/
```

![image-20230316202157210](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101009932.png)



##### 2.切换到root用户，安装两个软件包

> Tab补全

```shell
rpm -ih container-selinux-2.95-2.el7_6.noarch.rpm
rpm -ih docker-ce-18.06.3.ce-3.el7.x86_64.rpm
```

![image-20230316203738619](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101009839.png)



##### 3.查看docker是否安装成功，检查docker版本

```shell
docker -v
```

![image-20230316203804300](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101009826.png)



##### 4.启动docker

```shell
sudo systemctl start docker
```

![image-20230316204316603](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101010532.png)



##### 5.配置开机启动

```shell
sudo systemctl enable docker
```

![image-20230316204325633](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101010114.png)







### 三、配置阿里云镜像加速器

##### 1.打开阿里云网页，找到容器镜像服务ACR

```http
https://cr.console.aliyun.com/cn-shanghai/instances/mirrors
```

![image-20230316205727011](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101010843.png)



##### 2.进入管理控制台

![image-20230316205830043](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101010502.png)



##### 3.找到镜像工具，镜像加速器，选择CentOS，获取加速地址及配置文件

![image-20230316210125628](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101010038.png)



##### 4.复制整个配置文件，每个人的链接地址不一致注意使用自己的地址

```shell
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://dw88ht5n.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

![image-20230316210551156](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101010657.png)

###### 检查是否成功：

```shell
cat /etc/docker/daemon.json
```

![image-20230316210725759](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101010906.png)







### 四、Docker常见指令

```shell
docker ps 											   -- 查看当前运行的容器
docker ps -a										   -- 查看所有容器(历史容器)
docker search 镜像名									 -- 搜索镜像
docker pull 镜像名										 -- 通过名字拉取镜像
docker load -i xxx.tar								   -- 通过压缩文件导入镜像
docker save -o xxx.tar 镜像名:tag(TAG标签下的版本名)		-- 将镜像导出为压缩文件
docker images										   -- 查看本地仓库中的镜像
docker rmi -f 镜像id								  	  -- 通过镜像id删除镜像
docker rm 自定义容器名								   -- 通过容器名删除容器
docker run -d -p 8090:8080 --name 自定义容器名 镜像名	 -- 启动镜像(创建容器)
docker start 容器名									 -- 启动docker容器
docker stop 容器名										 -- 关闭docker容器
docker logs 容器名										 -- 查看某容器运行日志
docker exec -it 容器名 bash							 -- 进入容器(系统)
```

##### 搜索镜像

![image-20230316211725748](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101010858.png)



##### 拉取镜像

![image-20230316103841289](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101010622.png)



##### 导出镜像(先拉取后导出，导出的格式为xxx.tar，就是可以导入的镜像)

从Docker导出(拉取)Redis(导出到当前目录)示例：

![image-20230316104047030](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101010759.png)



##### 导入镜像

导入tar包到Docker(java、MySQL、Tomcat、nginx)：

![image-20230316212341499](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101010046.png)

tomcat示例：

![image-20230316105128127](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101010027.png)



##### 启动镜像(创建容器，就是镜像的实例)

> 每个docker镜像其实都是一个独立的操作系统，这个系统中包含所需的运行环境(装好了对应的软件)
>
> 启动镜像就相当于启动配置好环境的系统，可以理解为这个系统寄生在Linux操作系统中。

```shell
docker run -d -p 8090:8080 --name tomcat8090 tomcat
```

> -d 代表在后台运行，
> -p 指定端口映射，指定Linux系统的8090端口映射docker容器---tomcat系统的8080端口
> --name 给这个启动的镜像命名，最后的tomcat表示要启动的镜像名

![image-20230316105757625](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101010334.png)



##### 查看运行的容器

```shell
docker ps
```

![image-20230316105811864](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101010274.png)



##### 查看所有容器(历史容器)

```shell
docker ps -a
```

![image-20230316112725190](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101010598.png)



##### 关闭容器

```shell
docker stop 容器名
```

![image-20230316112348678](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101010260.png)



##### 删除容器

```shell
docker rm 容器名
```

![image-20230316112852231](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101010510.png)



##### 启动容器

```shell
docker start 容器名
```

![image-20230316113122817](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101010321.png)



##### 查看运行日志

```shell
docker logs 容器名
```

![image-20230316235602607](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101011517.png)



##### 进入容器(镜像)

```shell
docker exec -it 容器名 bash			-- bash是一种模式
```

![image-20230316113426409](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101011262.png)



##### 退出容器(镜像)

```shell
exit
```

![image-20230316113619155](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101011770.png)





### 五、部署Docker项目

##### 1.启动Docker镜像(容器)

##### 2.开启Linux的防火墙对应端口(暴漏给Windows使用)

```shell
firewall-cmd --zone=public --add-port=8090/tcp --permanent
```

![image-20230316110012287](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101011952.png)



##### 3.重启Linux的防火墙

```shell
systemctl restart firewalld.service
```

![image-20230316110024485](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101011205.png)



##### 4.测试是否可以在Windows打开对应容器服务的首页即为成功(Linux主机IP:8090)





































![img](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305101011315.png)
