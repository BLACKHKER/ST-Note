### IDEA自动化部署

> 当我们进行服务器部署到调试时，每次都需要上传，停止再启动，操作繁琐。
>
> 其实我们再idea中就可以进行快速部署，启动项目
>

##### 1.在idea软件商店中搜索 Alibaba Cloud Tookit 插件，并进行安装

![image-20230319165832376](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303202135933.png)



##### 2.搜索：Alibaba Cloud Toolkit，然后进行安装

![image-20230319170011972](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303202135522.png)



##### 3.点击“Accept”

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303202135052.png" alt="image-20230319170033453" style="zoom:50%;" />



##### 4.重启IDEA

![image-20230319200213123](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303202135514.png)

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303202135001.png" alt="image-20230319200225520" style="zoom:50%;" />



##### 5.编辑当前项目配置

![image-20230319200255808](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303202135017.png)



##### 6.点击“+”添加Deploy to Host配置

![image-20230319200341233](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303202135373.png)



##### 7.给配置取一个名字

![image-20230319200434784](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303202136121.png)



##### 8.添加服务器IP地址信息

![image-20230319200503207](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303202136793.png)



##### 9.点击“Add Host”

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303202136597.png" alt="image-20230319200616175" style="zoom:50%;" />



##### 10.设置服务器IP、指定端口号22、填写账号密码之后可以测试是否能连接上服务器

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303202136787.png" alt="image-20230319200849812" style="zoom:67%;" />

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303202136274.png" alt="image-20230319200900581" style="zoom:50%;" />



##### 11.添加完毕之后选择刚才添加的服务器

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303202136312.png" alt="image-20230319200925189" style="zoom:50%;" />



##### 12.指定项目jar包上传之后的路径

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303202136854.png" alt="image-20230319201009638" style="zoom: 50%;" />



##### 13.在jar上传路径的下面创建start.sh脚本文件，用于编写在上传完jar之后进行的操作，主要是用来启动项目

###### start.sh

```shell
# jar包的文件名，根据自己的进行修改
RESOURCE_NAME=xxx-0.0.1-SNAPSHOT.jar

tpid=`ps -ef|grep $RESOURCE_NAME|grep -v grep|grep -v kill|awk '{print $2}'`
if [ ${tpid} ]; then
echo 'Stop Process...'
kill -15 $tpid
fi
sleep 5
tpid=`ps -ef|grep $RESOURCE_NAME|grep -v grep|grep -v kill|awk '{print $2}'`
if [ ${tpid} ]; then
echo 'Kill Process!'
kill -9 $tpid
else
echo 'Stop Success!'
fi

tpid=`ps -ef|grep $RESOURCE_NAME|grep -v grep|grep -v kill|awk '{print $2}'`
if [ ${tpid} ]; then
    echo 'App is running.'
else
    echo 'App is NOT running.'
fi

rm -f tpid
nohup java -jar ./$RESOURCE_NAME  & tail -f nohup.out
echo $! > tpid
echo Start Success
```



##### 14.添加执行权限

```shell
chmod +x start.sh
```



##### 15.添加完start.sh文件之后在配置窗口中点击“Select Command”

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303202136581.png" alt="image-20230319201448278" style="zoom:67%;" />



##### 16.点击“Add Command”(启动时执行的指令---执行脚本)

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303202136172.png" alt="image-20230319201517355" style="zoom:50%;" />



##### 17.输入./start.sh点击OK即可(./脚本文件全名)

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303202136370.png" alt="image-20230319201548265" style="zoom:50%;" />

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303202136386.png" alt="image-20230319201609336" style="zoom:50%;" />



##### 18.点击“+”配置在jar包上传之前的操作

![image-20230319201733201](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303202136492.png)



##### 19.选择“Run Maven Goal”

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303202136152.png" alt="image-20230319201754228" style="zoom:67%;" />



##### 20.填写“clean package”点击OK即可

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303202136505.png" alt="image-20230319201825861" style="zoom:67%;" />



##### 21.最后点击“OK”完成配置

![image-20230319201907455](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303202136609.png)



##### 22.点击运行按钮测试是否能够正常部署

![image-20230319201928864](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303202136454.png)



##### 23.如果在控制台中能看到以下信息，表明自动部署成功

![image-20230319201954544](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303202136338.png)



##### 24.在服务器上查看项目是否运行

```shell
ps aux|grep *.jar
```

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303202136522.png" alt="image-20230319203505307" style="zoom:80%;" />
