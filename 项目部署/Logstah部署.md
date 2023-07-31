## Logstah安装部署

Logstash是一个开源数据收集引擎，具有实时管道功能。

Logstash可以动态地将来自不同数据源的数据统一起来，并将数据标准化到你所选择的目的地进行存储。

Logstash的早期目标是搜集日志，现在它的功能已完全不只于此。任何事件类型都可以加入分析，通过输入、过滤器和输出插件进行转换。

Logstash还提供了很多原生编解码工具简化消息处理。

### 运行原理

##### 1、Logstash使用管道方式进行日志的搜集处理和输出

Logstash管道有两个必需的元素，输入和输出，以及一个可选元素过滤器。输入插件从数据源那里消费数据，过滤器插件根据你的期望修改数据，输出插件将数据写入目的地。在logstash中，包括了三个阶段:输入input --> 处理filter（不是必须的） --> 输出output

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304201734763.png" alt="image-20210816203601489" style="zoom:50%;" />



##### 2、Logstash 支持各种输入选择 ，可以在同一时间从众多常用来源捕捉事件。能够以连续的流式传输方式，轻松地从日志、指标、Web 应用、数据存储以及各种 AWS 服务采集数据

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304201734667.png" alt="image-20210816203618897" style="zoom: 50%;" />

目前，logstash主要支持的数据输入方式为：标准输入、文件输入、TCP输入、syslog输入、http_poller

抓取、kafka消息队列输入等。

 

##### 3、过滤器：数据从源传输到存储库的过程中，Logstash 过滤器能够解析各个事件，识别已命名的字段以构建结构，并将它们转换成通用格式，以便更轻松、更快速地分析和实现商业价值。Logstash 能够动态地转换和解析数据，不受格式或复杂度的影响。

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304201734048.png" alt="image-20210816203634605" style="zoom:50%;" />

目前，logstash过滤器支持的功能有：date时间处理、GROK正则捕获、dissect解析、GeoIP地址查询、Json编解码、metrics数据修改、splite拆分事件、交叉日志合并等

 

##### 4、Logstash 提供众多输出选择，可以将数据发送到您要指定的地方，并且能够灵活地解锁众多下游用例。

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304201734531.png" alt="image-20210816203650736" style="zoom:50%;" />

目前，logstash主要支持的输出方式：输出到Elasticsearch、发送email、调用系统命令执行、保存成文件、报警发送到Nagios、标准输出stdout、TCP发送数据、输出到HDFS。







### 安装使用

#### 下载地址：

```http
https://www.elastic.co/cn/downloads/past-releases#logstash
```

##### 1、将logstash-7.6.2.zip解压到安装目录

![image-20230420173436268](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304201848429.png)



##### 2、进入该文件中，在该文件夹下创建logstash.conf文件

![image-20230420173554440](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304201848960.png)

###### 在该文件中添加以下信息

```yaml
input{
        stdin {
        }

        jdbc {
                jdbc_connection_string => "jdbc:mysql://localhost:3306/woniumall"
                jdbc_user => "root"
                jdbc_password => "root"
                #驱动类
                jdbc_driver_class => "com.mysql.jdbc.Driver"
                codec => plain { charset => "UTF-8"}

                #主键
                tracking_column => "id"
                #是否记录上次执行结果
                record_last_run => "true"
                #是否需要记录某个column 的值
                use_column_value => "true"
                #代表最后一次数据记录id的值存放的位置，必填不然启动报错
                last_run_metadata_path => "D:\logstash-7.6.2\last_id.txt"
                #是否清除 last_run_metadata_path 的记录
				#如果为真那么每次都相当于从头开始查询所有的数据库记录
                clean_run => "false"
                #是否分页
                jdbc_paging_enabled => "true"
                jdbc_page_size => "100000"
                #进行同步数据时，执行的SQL
                statement => "select * from mall_order where id > :sql_last_value"
				#定时字段 各字段含义（由左至右）分、时、天、月、年，全部为*默认含义为每分钟都更新
                #"*/2 * * * * *"        表示每两秒同步一次
                schedule => "*/2 * * * * *"
         		#当前jdbc的类型，自定义，可以看做是当前jdbc的名字
         		type => "order"
        }
}
filter{
}
output{
        elasticsearch {
                hosts => "localhost:9200"
                #索引名字
                index => "order"
                #文档类型
                document_type => "order"
                #文档id，唯一，避免数据重复
                document_id => "%{id}"
        }
        stdout {
                #以json格式查看数据同步情况，生产环节关闭，提升效率
                codec => json_lines
        }
}

```

###### 因为配置同步数据时要用到数据库驱动，所以需要将数据库连接包放到：安装目录\logstash-core\lib\jars下

![image-20230420173821985](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304201848783.png)

> 注意：如果同步的数据库是8.x版本的，除了连接包要换成8.x的，logstash.conf中的驱动名得加上cj，连接数据库的url得加上字符编码、时区等参数
>

![image-20230420174801605](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304201848270.png)

```conf
jdbc_connection_string => "jdbc:mysql://localhost:3306/woniumall?useUnicode=true&characterEncoding=utf8&serverTimezone=UTC"
jdbc_user => "root"
jdbc_password => "root"
#驱动类
jdbc_driver_class => "com.mysql.cj.jdbc.Driver"
codec => plain { charset => "UTF-8"}
```

###### 其他需要修改的值：

![image-20230420175711595](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304201848915.png)





##### 3、进入安装目录\config文件夹，修改pipelines.yml文件，将9-15行的注释打开

![image-20230420175331097](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304201848977.png)



##### 4、进入bin文件夹，并通过dos打开该文件夹，在dos中通过以下指令执行数据同步

```shell
logstash.bat -f 安装路径logstash.conf
```

![image-20230420175910223](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304201848115.png)

###### 看到以下情景表示同步数据成功

![image-20230420184810233](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304201848212.png)

**<font color='red'>注意：如果报以下错误信息</font>**

![image-20221201212448057](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202304201848439.png)

```shell
[ERROR] 2022-12-01 21:10:38.307 [main] Logstash - java.lang.IllegalStateException: Logstash stopped processing because of an error: (EACCES) Permission denied - NUL
```

###### 在安装目录\config\jvm.options中添加以下JVM配置信息

```
-Djdk.io.File.enableADS=true
```

