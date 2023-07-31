## ElasticSearch安装步骤

```http
https://www.elastic.co/cn/downloads/elasticsearch
```

### 1、将elasticsearch-7.6.2-windows-x86_64.zip解压到安装位置

![image-20230420101108941](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304201019058.png)







### 2、修改elasticsearch.yml配置文件

#### 进入到elasticsearch-7.6.2的config文件夹中

![image-20230420101151094](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304201019235.png)





#### 编辑配置文件

![image-20230420101235254](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304201019383.png)





#### 配置如下内容

```yaml
#集群名称
17  cluster.name: my-application
#节点名称
23  node.name: node-1
#将来访问elastic的话，都是通过API访问，在这我们要提供一个http主机地址，这里就是本机IP
55  network.host: 192.168.2.171  
#默认端口
59  http.port: 9200
#指定集群节点列表
72 cluster.initial_master_nodes: ["node-1"]

末尾增加
#开启跨域访问
http.cors.enabled: true
http.cors.allow-origin: "*"
#是否能成为master节点
node.master: true
#该节点能存储数据
node.data: true 
```







### 3、运行ElasticSearch

#### 通过dos打开elasticsearch-7.6.2的bin文件夹

![image-20230420101406042](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304201020732.png)





#### 输入elasticsearch.bat运行程序，出现以下信息(disabled)表示运行成功

![image-20230420100945680](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304201020940.png)

##### 也可以通过浏览器访问以下URL进行测试：本机IP:9200，运行结果如下所示，表明运行成功

![image-20230420101903795](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304201020016.png)
