## 所有依赖(下载路径)都写在dependentcies标签里



### 更改获取资源的路径为阿里云

```xml
<modelVersion>4.0.0</modelVersion>	<!--写在Version后面，GruopId上面-->

	<repositories>
		<repository>
            <id>nexus-aliyun</id>
            <name>nexus-aliyun</name>
            <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
            <releases>
                <enabled>true</enabled>
            </releases>
            <snapshots>
                <enabled>false</enabled>
            </snapshots>
        </repository>
    </repositories>

    <pluginRepositories>
        <pluginRepository>
            <id>public</id>
            <name>aliyun nexus</name>
            <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
            <releases>
                <enabled>true</enabled>
            </releases>
            <snapshots>
                <enabled>false</enabled>
            </snapshots>
        </pluginRepository>
    </pluginRepositories>
    
	<groupId>groupId</groupId>
    <artifactId>cloud</artifactId>
    <version>1.0-SNAPSHOT</version>
```





#### Log4j:

##### 1.2.12:

```xml
<dependency>
    <groupId>log4j</groupId>
    <artifactId>log4j</artifactId>
    <version>1.2.12</version>
</dependency>
```





#### MySQL：

##### 5.1.47：

```xml
<!--MySQL-->
<!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.47</version>
</dependency>
```



##### 8.0.25：

```xml
<!--MySQL-->
<!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.25</version>
</dependency>
```



##### SpringBoot场景器：

```xml
<!--MySQL(常用)-->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
</dependency>

<!--MySQL-->
<dependency>
    <groupId>com.mysql</groupId>
    <artifactId>mysql-connector-j</artifactId>
    <scope>runtime</scope>
</dependency>
```



#### C3P0连接池：

##### 0.9.5.4：

```xml
<!-- c3p0 -->
<!-- https://mvnrepository.com/artifact/com.mchange/c3p0 -->
<dependency>
    <groupId>com.mchange</groupId>
    <artifactId>c3p0</artifactId>
    <version>0.9.5.4</version>
</dependency>
```





#### Druid连接池：

##### 1.1.10：

```xml
<!--druid连接池-->
<!-- https://mvnrepository.com/artifact/com.alibaba/druid -->
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid</artifactId>
    <version>1.1.10</version>
</dependency>
```

##### SpringBoot场景器：

```xml
<!--Druid连接池-->
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid-spring-boot-starter</artifactId>
    <version>1.1.20</version>
</dependency>
```



#### Junit单元测试：

##### 4.12：

```xml
<!--JUnit-->
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.12</version>
</dependency>
```



##### 4.9：

```xml
<!--Junit-->
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.9</version>
    <!--Scope-作用域:只在测试阶段可以使用，项目打包，不会添加这个，测试jar包建议使用test域-->
    <scope>test</scope>
</dependency>
```





#### lombok实体Get、Set、toString生成工具:

##### 1.18.20:

```xml
<!--lombok-->
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.20</version>
</dependency>
```



##### SpringBoot场景器：

```xml
<!--Lombok-->
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <optional>true</optional>
</dependency>
```





#### JSP:

##### 2.2:

```xml
<!-- JSP -->
<dependency>
    <groupId>javax.servlet.jsp</groupId>
    <artifactId>jsp-api</artifactId>
    <version>2.2</version>
    <scope>provided</scope>
</dependency>
```





#### JSTL标签库：

##### 1.2-1：

```jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>	<% 写在JSP声明下面%>	
```

```xml
<!-- JSTL -->
<!-- https://mvnrepository.com/artifact/javax.servlet.jsp.jstl/jstl -->
<dependency>
	<groupId>javax.servlet.jsp.jstl</groupId>
	<artifactId>jstl</artifactId>
	<version>1.2</version>
</dependency>

<!-- https://mvnrepository.com/artifact/javax.servlet.jsp.jstl/jstl-api -->
<dependency>
    <groupId>javax.servlet.jsp.jstl</groupId>
    <artifactId>jstl-api</artifactId>
    <version>1.2</version>
</dependency>

<!-- https://mvnrepository.com/artifact/taglibs/standard -->
<dependency>
    <groupId>taglibs</groupId>
    <artifactId>standard</artifactId>
    <version>1.1.2</version>
</dependency>
```

##### 1.2-2：

###### 李老师

```xml
<!-- JSTL -->
<dependency>
    <groupId>jstl</groupId>
    <artifactId>jstl</artifactId>
    <version>1.2</version>
</dependency>

<dependency>
    <groupId>taglibs</groupId>
    <artifactId>standard</artifactId>
    <version>1.1.2</version>
</dependency>
```



#### FastJSON阿里工具：

##### 2.0.12：

```xml
<!--fastJSON-->
<!-- https://mvnrepository.com/artifact/com.alibaba.fastjson2/fastjson2 -->
<dependency>
    <groupId>com.alibaba.fastjson2</groupId>
    <artifactId>fastjson2</artifactId>
    <version>2.0.12</version>
</dependency>
```





#### CGLIB代理：

##### 3.3.0：

```xml
<dependency>
    <groupId>cglib</groupId>
    <artifactId>cglib</artifactId>
    <version>3.3.0</version>
</dependency>
```





#### Commons(文件上传)：

```xml
<!--文件上传-->
<!-- https://mvnrepository.com/artifact/commons-fileupload/commons-fileupload -->
<dependency>
    <groupId>commons-fileupload</groupId>
    <artifactId>commons-fileupload</artifactId>
    <version>1.3.3</version>
</dependency>

<!-- https://mvnrepository.com/artifact/commons-io/commons-io -->
<dependency>
    <groupId>commons-io</groupId>
    <artifactId>commons-io</artifactId>
    <version>2.6</version>
</dependency>
```





#### ASPECTJ(for Java)：

##### 1.8.13：

```xml
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjrt</artifactId>
    <version>1.8.13</version>
</dependency>
```





#### Servlet：

##### 3.1.0:

```xml
<!--Servlet-->
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>3.1.0</version>
    <scope>provided</scope>
</dependency>
```



##### 4.0.1：

```xml
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>4.0.1</version>
</dependency>
```





#### MyBatis：

##### 3.5.2：

```xml
<!--MyBatis-->
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.2</version>
</dependency>
```



##### SpringBoot场景器：

```xml
<!--MyBatis-->
<dependency>
    <groupId>org.mybatis.spring.boot</groupId>
    <artifactId>mybatis-spring-boot-starter</artifactId>
    <version>2.2.2</version>
</dependency>
```





#### MyBatisPlus(SpringBoot场景器)：

##### 3.5.1：

```xml
<!--Mybatis-Plus-->
<dependency>
    <groupId>com.baomidou</groupId>
    <artifactId>mybatis-plus-boot-starter</artifactId>
    <version>3.5.1</version>
</dependency>
```





#### MyBatisPlus代码生成器

```xml
<!-- mybatis plus 代码生成器 -->
<dependency>
    <groupId>com.baomidou</groupId>
    <artifactId>mybatis-plus-generator</artifactId>
    <version>3.4.1</version>
</dependency>
<dependency>
    <groupId>org.freemarker</groupId>
    <artifactId>freemarker</artifactId>
    <version>2.3.28</version>
</dependency>
```





#### MyBatis-Spring：整合SqlSessionFactory

##### 2.0.7：

```xml
<!--mybatis-Spring-->
<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis-spring -->
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis-spring</artifactId>
    <version>2.0.7</version>
</dependency>
```





#### Mybatis-Generator-Core(逆向工程)：

##### 1.4.0：

```xml
<!--MyBatis-Generator-->
<!-- https://mvnrepository.com/artifact/org.mybatis.generator/mybatis-generator-core -->
<dependency>
    <groupId>org.mybatis.generator</groupId>
    <artifactId>mybatis-generator-core</artifactId>
    <version>1.4.0</version>
</dependency>
```





#### SpringMVC：

##### 5.3.22：

```xml
<!--下载主依赖自动下载子依赖-->
<!--SpringMVC-->
<!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>5.3.22</version>
</dependency>
```





#### Jackson(@ResponseBody)：

> jackson-databind依赖于Streaming和Annotations包
>
> 因此，引入jackson-databind相当于引入了jackson-core和jackson-annotations。

##### 版本号：

```
2.14.4	2.11.4
```



##### 2.11.4：

###### Jackson Databind：

```xml
<!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-databind -->
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.14.4</version>
</dependency>
```

###### Jackson Core：

```xml
<!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-core -->
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-core</artifactId>
    <version>2.14.4</version>
</dependency>
```

###### Jackson Annotations：

```xml
<!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-annotations-->
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-annotations</artifactId>
    <version>2.14.4</version>
</dependency>
```





#### Thymeleaf：

##### 3.0.12：

```xml
<!--thymeleaf-->
<dependency>
    <groupId>org.thymeleaf</groupId>
    <artifactId>thymeleaf-spring5</artifactId>
    <version>3.0.12.RELEASE</version>
</dependency>
```

##### SpringBoot场景器：

```xml
<!--thymeleaf-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>
```

添加thymeleaf默认的资源路径，以及资源的前缀和后缀

```properties
spring.mvc.static-path-pattern=/**
spring.web.resources.static-locations=classpath:/static/
spring.thymeleaf.prefix=classpath:/static/
spring.thymeleaf.suffix=.html
spring.thymeleaf.cache=false
```





#### Spring：spring-context会引入其他三个子包(Beans、Core、SpEL)

##### 5.2.15.RELEASE：

```xml
<!--Spring(IOC、AOP)-->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>5.2.15.RELEASE</version>
</dependency>
```



##### 5.2.10.RELEASE：

```xml
<!--在properties中统一版本号-->
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.7</maven.compiler.source>
    <maven.compiler.target>1.7</maven.compiler.target>
    <!--统一版本号 标签可以自定义-->
    <spring.version>5.2.10.RELEASE</spring.version>
</properties>

<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>${spring.version}</version>
</dependency>

<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-beans</artifactId>
    <version>${spring.version}</version>
</dependency>

<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-core</artifactId>
    <version>${spring.version}</version>
</dependency>
```





#### pagehelper分页插件：

版本号：

```
4.1.4(李老师)、5.1.2
```

```xml
<!--pagehelper分页插件-->
<dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper</artifactId>
    <version>5.1.2</version>
</dependency>
```

##### SpringBoot场景器

```xml
<!--pagehelper分页插件-->
<dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper-spring-boot-starter</artifactId>
    <version>1.2.10</version>
</dependency>
```





#### hutool验证码：

```xml
<!--验证码-->
<!--hutool-->
<dependency>
    <groupId>cn.hutool</groupId>
    <artifactId>hutool-all</artifactId>
    <version>4.6.8</version>
</dependency>
```





#### 热部署：

```xml
<!-- devtools 热部署 -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <optional>true</optional>
</dependency>
```





#### Swagger：

```xml
<!--Swagger2 -->
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger2</artifactId>
    <version>2.7.0</version>
</dependency>
<!--引入外部的Swagger页面美化包，必须配合版本为2.7.0的Swagger2-->
<dependency>
    <groupId>com.github.xiaoymin</groupId>
    <artifactId>swagger-bootstrap-ui</artifactId>
    <version>1.9.6</version>
</dependency>
```





#### JWT：

```xml
<!-- JWT -->
<dependency>
	<groupId>com.auth0</groupId>
	<artifactId>java-jwt</artifactId>
	<version>3.4.0</version>
</dependency>
```





#### Redis:

```xml
<!--Redis-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```





#### MinIO:

```xml
<!--MinIO-->
<dependency>
    <groupId>io.minio</groupId>
    <artifactId>minio</artifactId>
    <version>8.0.0</version>
</dependency>
```

