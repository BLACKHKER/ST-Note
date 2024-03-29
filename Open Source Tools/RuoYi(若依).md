# RuoYi(若依)

## RuoYi-Vue

### RuoYi项目构建

#### 拉取代码

![image-20230815113908347](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230815113908347.png)





#### 搭建项目环境

##### 构建数据库

> 直接使用项目中的SQL建表(ry-date.sql)，先导入定时任务表、再导入基础表

![image-20230815114129743](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230815114129743.png)





##### 构建前端环境(下载依赖)

> 注意node版本，18及以上会报错	node -v 查看node.js版本，推荐使用node 14.19.3(NVM下载多个Node)

###### 在ruoyi-ui文件下打开cmd，下载依赖

![image-20230815115811267](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230815115811267.png)

```shell
npm install
```

![image-20230815115955537](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230815115955537.png)

###### 运行

```shell
npm run dev
```



##### 后端

###### 目录结构

![image-20230815143132917](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230815143132917.png)

###### 数据库

> 修改配置文件application-druid.yml

![image-20230815143333185](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230815143333185.png)







#### 启动注意事项

- 如果有Redis，项目才可以启动，没有Redis，需要先启动或修改配置application.yml中Redis的端口等信息

##### 启动成功

![image-20230815145944670](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230815145944670.png)







### RuiYi代码生成器

> 给一张数据库表，自动生成前后端代码，增删改查、根据主键查询、分页、导出Excel等方法
>

#### 定义表

> 注意表的字段以及表本身都要有注释，生成的前端会自动生成行头，表本身的注释在设计表里

##### 字段注释

![image-20230815151856009](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230815151856009.png)



##### 编写表注释

![image-20230815152105644](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230815152105644.png)





#### 导入表

##### 在前端页面导入表

![image-20230815152315959](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230815152315959.png)

选中要导入的表

![image-20230815152524332](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230815152524332.png)





#### 预览生成代码

![image-20230815152809134](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230815152809134.png)
