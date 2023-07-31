## 安装kibana

> 因为kibana基于node.js，所有需要先安装node.js
>
> node下载地址：https://nodejs.org/en/download/
>
> 安装方法参考：https://blog.csdn.net/Soinice/article/details/87793793
>
> kibana下载地址：https://www.elastic.co/cn/downloads/kibana

### 1、将kibana-7.6.2-windows-x86_64解压到安装目录

![image-20230420105114685](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304201101656.png)







### 2、修改kibana.yml配置文件

#### 进入kibana的config文件夹配置kibana.yml

![image-20230420105135260](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304201101729.png)





#### 第2、7、28行设置以下内容

```yaml
server.port: 5601
server.host: "本机IP"
elasticsearch.hosts: ["http://192.168.2.171:9200"]
```







### 3、运行Kibana

#### 通过CMD打开kibana的bin文件夹，输入kibana.bat运行

![image-20230420105502576](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304201101345.png)

##### 出现以下内容表明运行成功

![image-20230420105715879](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304201101316.png)



##### 在浏览器上访问http://localhost:5601，出现以下界面也可以表示运行成功

![image-20230420105902216](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304201101669.png)







### 基本使用

##### 点击“Try our sample data”进入kibana

![image-20230420105925344](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304201101832.png)



##### 选择kibana的开发工具

![image-20230420110042625](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304201101942.png)



##### 出现如下界面就可以通过相关指令操作es了

![image-20230420110019974](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304201101002.png)

