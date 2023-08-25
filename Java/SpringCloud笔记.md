## 微服务

### 架构演进

#### 单体架构

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305041542937.png" alt="image-20210802094515955" style="zoom:50%;" />

##### 集群解决单服务器负载问题：

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305041542485.png" alt="image-20210801172038458" style="zoom:50%;" />





#### SOA架构

> 面向服务的架构（SOA）是一个组件模型，它将应用程序的不同功能单元（称为服务）进行拆分，并通过这些服务之间定义良好的接口和协议联系起来。一个服务可能负责几个功能
>

<img src="https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305041542821.png" alt="image-20210801174815174" style="zoom: 50%;" />

##### SOA 设计原则

在 SOA 架构中，继承了来自对象和构件设计的各种原则，例如，封装和自我包含等。

那些保证服务的灵活性、松散耦合和复用能力的设计原则，对 SOA 架构来说同样是非常重要的。

但是这种集成方式开发代价大、通信效率低，且有单点故障的风险， 实际上在企业中并没有得到大规模应用。









#### 微服务架构

> 微服务由SOA的发展而来。就是很小的服务，所以它属于面向服务架构的一种。微服务类似于古代著名的发明，活字印刷术，每个服务都是一个组件，通过编排组合的方式来使用，从而真正做到了独立、解耦、组件化、易维护、可复用、可替换、高可用、最终达到提高交付质量、缩短交付周期的效果。

微服务的核心特点为：小, 且专注于做⼀件事情、轻量级的通信机制、松耦合、独立部署。微服务的核心特点为：小, 且专注于做⼀件事情、轻量级的通信机制、松耦合、独立部署。



##### 微服务设计原则

###### 单一职责原则

意思是每个微服务只需要实现自己的业务逻辑就可以了，比如订单管理模块，它只需要处理订单的业务逻辑就可以了，其它的不必考虑。

###### 服务自治原则

意思是每个微服务从开发、测试、运维等都是独立的，包括存储的数据库也都是独立的，自己就有一套完整的流程，我们完全可以把它当成一个项目来对待。不必依赖于其它模块。

###### 轻量级通信原则

首先是通信的语言非常的轻量，第二，该通信方式需要是跨语言、跨平台的，之所以要跨平台、跨语言就是为了让每个微服务都有足够的独立性，可以不受技术的钳制。

###### 接口明确原则

由于微服务之间可能存在着调用关系，为了尽量避免以后由于某个微服务的接口变化而导致其它微服务都做调整，在设计之初就要考虑到所有情况，让接口尽量做的更通用，更灵活，从而尽量避免其它模块也做调整。



##### 与SOA的主要区别

| 微服务                       | SOA                                       |
| ---------------------------- | ----------------------------------------- |
| 能拆分的就拆分               | 是整体的，服务能放一起的都放一起          |
| 业务逻辑存在于每一个服务中   | 业务逻辑横跨多个业务领域                  |
| 使用轻量级的通讯方式，如HTTP | 企业服务产总线(ESB)充当服务之间通讯的角色 |
| 细粒度                       | 粗粒度                                    |





---





## 分布式

### 分布式和微服务的区别

简单的说，微服务是架构设计方式，分布式是系统部署方式，两者概念不同





---





## SpringCloud

> Spring Cloud为开发人员提供了快速构建分布式系统中一些常见模式的工具（例如配置管理，服务发现，熔断器，智能路由，微代理，控制总线，一次性令牌，全局锁，领导选举，分布式会话，集群状态）

### SpringCloud常用工具

- Spring Cloud专注于提供良好的开箱即用典型用例和可扩展性机制覆盖。

- 分布式/版本化配置

- 服务注册和发现(Eureka注册中心)

- 路由

- service - to - service调用

- 负载均衡

- 熔断器/断路器

- 全局锁

- Leadership选举与集群状态

- 分布式消息传递







### Spring Cloud与Spring Boot的关系

Spring Boot用来开发项目，Spring Cloud用来管理项目，Spring Cloud管理的项目需要基于Spring Boot来开发

> Spring Cloud不是云计算解决方案，而是在Spring Boot基础之上构建的，用于快速构建分布式系统的通用模式的工具集。使用Spring Cloud开发的应用程序非常适合在Docker和PaaS(比如Pivotal Cloud Foundry)上部署，所以又叫做云原生应用(Cloud Native Application)。云原生可以简单地理解为面向云环境的软件架构。
>

 

#### 版本对应关系

| Spring Cloud              | Spring Boot                                    |
| ------------------------- | ---------------------------------------------- |
| Angel版本                 | 兼容Spring Boot 1.2.x                          |
| Brixton版本               | 兼容Spring Boot 1.3.x，也兼容Spring Boot 1.4.x |
| Camden版本                | 兼容Spring Boot 1.4.x，也兼容Spring Boot 1.5.x |
| Dalston版本、Edgeware版本 | 兼容Spring Boot 1.5.x，不兼容Spring Boot 2.0.x |
| Finchley版本              | 兼容Spring Boot 2.0.x，不兼容Spring Boot 1.5.x |
| Greenwich版本             | 兼容Spring Boot 2.1.x                          |
| Hoxton版                  | 兼容Spring Boot 2.2.x                          |

##### 在实际开发过程中，我们需要更详细的版本对应：

| Spring Boot   | Spring Cloud            |
| ------------- | ----------------------- |
| 1.5.2.RELEASE | Dalston.RC1             |
| 1.5.9.RELEASE | Edgware.RELEASE         |
| 2.0.2.RELEASE | Finchley.BUILD-SNAPSHOT |
| 2.0.3.RELEASE | Finchley.RELEASE        |
| 2.1.0.RELEASE | Greenwich.SR1           |
| 2.2.0.M4      | Hoxton.SR9              |
| 2.3.7         | Hoxton.BUILD-SNAPSHOT   |
| 2.4.0.M1      | 2020.0.0-M3             |







### SpringCloud(微服务)基于Eureka的项目搭建

#### 父项目(Root)

##### 新建Maven项目

> idea某些版本，如果不选择archetype(模板)报错，就选择QuickStart

![image-20230504101140627](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305041542188.png)



##### 修改maven，项目打包方式为pom包

![image-20230505143533187](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305080925933.png)



##### 注意：

父项目引入的依赖，子项目会自动继承，从而实现依赖的版本统一管理

###### 如果想让某些依赖不自动继承，可以使用dependencyManagement标签来表示依赖，子项目就需要手动继承：

```xml
<!--可选继承，不会自动继承，需要子项目手动继承-->
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.30</version>
        </dependency>
    </dependencies>
</dependencyManagement>
```

![image-20230505144747905](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305080926795.png)

###### 手动继承示例：

> 没有版本号表示使用父项目版本号，有版本号表示重写父项目版本号，使用自定义版本号

![image-20230509162952799](S:/woniu/TypoaPicture/image-20230509162952799.png)



##### (可选)删除src目录

![image-20230505145348556](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305080926131.png)





#### 子项目(首先是注册中心，此处使用Eureka)

##### 在父项目的项目名上点击右键，新建一个Model(子项目)，创建SpringBoot项目

![image-20230505145810248](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305080926900.png)



##### 选择场景器(此处使用Eureka创建微服务项目)

![image-20230505164840038](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305080926678.png)



##### 修改(降低)SpringBoot、SpringCloud版本

![image-20230505165421595](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305080926660.png)

###### 修改为：

```xml
<spring-boot.version>2.3.7.RELEASE</spring-boot.version>
<spring-cloud.version>Hoxton.SR9</spring-cloud.version>
```

![image-20230505165608946](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305080926331.png)



##### 子项目模块继承父项目、父项目添加该模块为子项目

```xml
<!--子项目中继承父项目-->
<parent>
    <artifactId>springcloud-erp</artifactId>
    <groupId>com.woniuxy</groupId>
    <version>1.0</version>
</parent>
```

![image-20230505170112331](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305080926455.png)

```xml
<!--设置子项目(项目名)-->
<modules>
    <module>registcenter</module>
</modules>
```

![image-20230505170424910](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305080926703.png)



##### 在主启动类添加Eureka注解，声明当前模块为注册中心

```java
// 开启注册中心功能
@EnableEurekaServer
```

![image-20230505171121279](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305080926891.png)



##### 修改配置文件(首先将配置文件格式从application修改为yml，SHIFT+F6重命名)

![image-20230505172137110](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305080926648.png)

```yaml
spring:
  application:
    # 命名很重要，以及名字中不能包含下划线、特殊字符
    name: eureka-server
server:
  # 端口，8761是Eureka组件默认采用的端口，可以修改
  port: 8761
eureka:
  instance:
    # Eureka的主机名
    hostname: localhost
  client:
    # 是否将自己注册到Eureka，只有业务微服务模块需要注册，注册中心不需要
    register-with-eureka: false
    # 是否定时(间隔30s)拉取注册列表信息，注册列表中包含了所有业务微服务的基本信息(ip、端口、微服务名等)，获取别的微服务信息，注册中心已经有了，不需要开启
    fetch-registry: false
    service-url:
      # http://localhost:8761/eureka
      # 提供的注册接口，此处使用了${}表达式动态获取IP以及端口号，注意最后的‘/’必须加
      defaultZone: http://${eureka.instance.hostname}:${server.port}/eureka/
```



##### 启动注册中心

![image-20230505173254889](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305080926310.png)

###### 可以查看原生后台管理Web页面，即为部署成功

```http
localhost:端口号
```

![image-20230505173424962](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305080926144.png)





#### 子项目(业务模块)

##### 创建流程同注册中心，注意场景器是Discovery Client

![image-20230505175052325](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305080926499.png)



##### 创建后降低版本、配置父子模块之间的关系

```xml
<!--设置子项目-->
<modules>
    <module>registcenter</module>
    <module>goods</module>
</modules>
```

![image-20230505175308739](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305080926822.png)



##### 在主启动类添加Eureka注解，声明当前模块为服务端

```java
// 开启eureka客户端功能
@EnableDiscoveryClient
```

![image-20230505175721781](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305080926387.png)



##### 修改配置文件(同样yml格式)

```yaml
spring:
  application:
    # 微服务名，是SpringCloud中找到对应微服务(服务器)的标识，也是集群的标识，不能用下划线
    name: goods
server:
  port: 8080
eureka:
  client:
    service-url:
      # 向该接口注册
      defaultZone: http://localhost:8761/eureka/
  instance:
    # 服务器id，不可重复，用于区分同微服务下不同端口的项目
    instance-id: goods-8080
```



##### 启动该模块，查看Eureka的Web后台，根据是否新增服务器来判断是否配置成功

###### 注意不要关闭注册中心(两个子模块都启动)

![image-20230505190453541](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305080926214.png)

###### 配置成功，Web页面显示子模块的微服务名(goods大写)：

![image-20230505190539790](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305080926880.png)





#### 子项目(公共工具模块)

##### 创建Maven项目，修改打包方式为jar包，配置父子模块之间的关系

> 没有packaging就手动添加

```xml
<packaging>jar</packaging>
```



##### 在需要公共模块的微服务引入Maven依赖

```xml
<dependency>
    <groupId>com.woniuxy</groupId>
    <artifactId>commons</artifactId>
    <version>1.0</version>
</dependency>
```



##### 通过Maven插件打包工具模块为jar包

> package打包，打的包只放在当前项目下，而install打包还会向Maven仓库存放一个包，就可以引入该依赖

![image-20230506150659230](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305080926612.png)

###### 注意：每次修改代码都要先clean再install







#### 创建某一微服务集群(副本)

##### 打开SpringBoot项目配置中心

![image-20230505191038582](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305080926824.png)



##### 选中要复制的微服务模块，点击上方复制图标，创建副本

![image-20230505191230849](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305080926302.png)



##### 选中副本，配置副本的VM options，输入以下指令

```shell
-Dserver.port=端口号 -Deureka.instance.instance-id=微服务唯一id
```

![image-20230505191704983](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305080926379.png)



##### 配置好运行副本，打开Eureka控制台页面，查看当前微服务的服务器数量是否增加变成2，即为成功

![image-20230505191914559](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305080926658.png)





#### 总结

首先创建父项目(Maven结构)，然后创建子项目(SpringBoot)，子项目分为微服务注册中心和微服务业务模块。

创建注册中心微服务时引入的场景器为Eureka Server，业务模块的场景器为Eureka Discovery Client。

每个子模块在创建后需要统一SpringBoot版本、配置父项目坐标，在父项目中引入该子项目(model)。

注册中心和业务模块的启动类要加上注解@EnableEurekaServer、@EnableDiscoveryClient声明该微服务





---





## 微服务调用

### 一、RestTemplate

> RestTemplate是SpringBoot内部集成的工具，用于微服务项目A发送HTTP请求调用项目B
>
> 就像是在Java内部通过Postman发送了一个请求获取数据

#### 创建配置类

```java
@Configuration
public class RestConfig {
	
    // 将RestTemplate注入到容器中
    @Bean
    public RestTemplate restTemplate() {
        return new RestTemplate();
    }
}
```





#### 调用其他微服务

##### IP + 端口号调用

```java
@RestController
@RequestMapping("/cart")
public class CartController {

    @Resource
    private RestTemplate restTemplate;

    /**
     * 添加商品到购物车，要调用微服务goods获取商品信息，再添加到购物车
     *
     * @return
     */
    @GetMapping("/add")
    public ResponseResult<Boolean> add() {

        // 定义URL，该URL调用微服务goods中的Controller方法：findById
        String url = "http://localhost:8080/goods/findById/2001";

        // 调用其他微服务，通过发送HTTP请求得到数据，restTemplate支持get、post、put、delete
        // 参数一是请求URL，参数二是返回类型的类文件
        ResponseResult forObject = restTemplate.getForObject(url, ResponseResult.class);
        System.out.println(forObject);

        return new ResponseResult<Boolean>().setCode(200);
    }
}
```



##### 微服务名调用

```java
String url = "http://微服务名(集群名)/requestMapping地址";

// 定义URL，该URL调用微服务集群goods中的Controller方法：findById
String url = "http://GOODS/goods/findById/2001";
```

###### 如果该微服务是一个集群，需要在RestTemplate配置类添加注解来配置负载均衡策略：

```java
@Configuration
public class RestConfig {

    // 将RestTemplate注入到容器中
    @Bean
    // 开启负载均衡器，默认轮询
    @LoadBalanced
    public RestTemplate restTemplate() {
        return new RestTemplate();
    }
}
```





#### 缺点

##### 调用方法的返回值是嵌套的，会出现问题：

比如ResponseResult的data中封装了Goods商品信息：

```java
ResponseResult forObject = restTemplate.getForObject(url, ResponseResult.class);
// 输出LinkedHashMap，不是Goods
System.out.println(forObject.getData().getClass());
```

###### 原因：

因为发送请求接收到的值是JSON，RestTemplate默认会使用LinkedHashMap去接收数据，造成数据转换问题





### 二、OpenFeign声明式通信

#### 引入依赖

##### commons公共模块(被调用方)

```xml
<!--openfeign-->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-openfeign</artifactId>
    <version>2.2.6.RELEASE</version>
</dependency>
```



##### cart-feign微服务(调用方)

```xml
<!--openfeign-->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-openfeign-core</artifactId>
    <version>2.2.6.RELEASE</version>
</dependency>

<dependency>
    <groupId>com.woniuxy</groupId>
    <artifactId>commons</artifactId>
    <version>1.0</version>
</dependency>
```





#### 在commons创建Feign的Service接口

##### 原生GoodsController(原被调用方)

```java
@RestController
@RequestMapping("/goods")
public class GoodsController {

    @Resource
    private GoodsService goodsService;

    @GetMapping("/findById/{id}")
    public ResponseResult<Goods> findById(@PathVariable("id") int id) {
        System.out.println(id);
        return goodsService.findById(id);
    }
}
```



##### Feign的Service接口(调用GoodsController中的方法，新被调用方)

> 直接将原生Controller方法的方法头(前两行)引用过来，映射地址需要注意一下
>
> 接口中的方法要求与要调用的Controller方法完全一致，除了Mapping映射的地址需要修改为完整的地址

```java
// 指定接口(客户端)调用哪些微服务
@FeignClient(name = "微服务名")
public interface FeignXxxService {

    // 原方法映射地址(全路径，就是Postman里怎么调用这里就写什么)
    @XxxMapping("xxx/xxx/{xxx}")
    public 返回值 findById(形参);
}
```

###### 实例：

```java
// 指定接口(客户端)调用哪些微服务
@FeignClient(name = "GOODS")
public interface FeignGoodsService {

    // 这里地址多了一个goods，因为原生的Controller上方有全局映射地址
    @GetMapping("/goods/findById/{id}")
    public ResponseResult<Goods> findById(@PathVariable("id") int id);
}
```





#### 调用方在启动类添加注解

```java
// 开启eureka客户端功能
@EnableDiscoveryClient
// 开启Feign的客户端们,扫描Feign接口所在的包，创建接口对象
@EnableFeignClients(basePackages = "com.woniuxy.commons.service")
@SpringBootApplication
public class CartFeignApplication {

    public static void main(String[] args) {
        SpringApplication.run(CartFeignApplication.class, args);
    }
}
```





#### 调用方调用Feign接口

```java
@RestController
@RequestMapping("/cart")
public class CartController {

    @Resource
    private FeignGoodsService feignGoodsService;

    @RequestMapping("/add")
    public void add() {
        // 调用微服务Goods的接口，得到商品数据
        ResponseResult<Goods> responseResult = feignGoodsService.findById(1);

        System.out.println(responseResult);
        System.out.println(responseResult.getData());
    }
}
```





#### 总结









---





## 负载均衡(Ribbon)

> RestTemplate、Eureka内置的负载均衡都是Ribbon，导入了其他就导入了Ribbon，不需要单独再导入

### 负载均衡策略

| 策略                                               | 解释                                                         |
| -------------------------------------------------- | ------------------------------------------------------------ |
| com.netflix.loadbalancer.RandomRule                | 随机，在服务实例中随机选择请求                               |
| com.netflix.loadbalancer.RoundRobinRule            | 轮询，根据服务列表轮流请求                                   |
| com.netflix.loadbalancer.RetryRule                 | 在RoundRobinRule的基础上添加重试机制，即在指定的重试时间内，反复使用线性轮询策略来选择可用实例 |
| com.netflix.loadbalancer.WeightedResponseTimeRule  | 对RoundRobinRule的扩展，响应速度越快的实例选择权重越大，越容易被选择 |
| com.netflix.loadbalancer.BestAvailableRule         | 选择并发较小的实例                                           |
| com.netflix.loadbalancer.AvailabilityFilteringRule | 先过滤掉故障实例，再选择并发较小的实例                       |
| com.netflix.loadbalancer.ZoneAwareLoadBalancer     | 采用双重过滤，同时过滤不是同一区域的实例和故障实例，选择并发较小的实例 |

#### OpenFeign配置全局负载均衡策略(单一微服务)

##### 在Feign微服务(调用方)中添加配置类

> IRule是一个接口，里面有很多实现类，就是不同的负载均衡策略

```java
// 微服务名.src.main.java.com.xxx.微服务名.config.RibbonConfiguration.java
@Configuration
public class RibbonConfiguration {

    @Bean
    public IRule rule(){
        // 返回策略，这里是RandomRule，随机访问该微服务下的集群服务器
        return new RandomRule();
    }
}
```

这样实现的效果就是在当前微服务调用其他任何微服务时采用随机的方式访问





#### 局部设置

**<font color='red'>注意：全局与局部同时存在，ribbon优先使用全局设置，因此需要先注释掉全局设置才有用</font>**

```yaml
# 名字必须大写，和Eureka保持一致
微服务名字:
  ribbon:
  	# 配置负载均衡策略
    NFLoadBalancerRuleClassName: com.netflix.loadbalancer.策略名
    # ReadTimeout: 1000
    
    # 连接超时时间
	# ConnectTimeout: 1000

	# 切换实例后重试最大次数 默认0
	# MaxAutoRetries: 1
	
	#对所有超时的请求启用重试机制  默认false
	# OkToRetryOnAllOperations: true
	
	# 切换重试实例的最大个数	默认1
	# MaxAutoRetriesNextServer: 1
GOODS:
  ribbon:
  	# 使用随机访问
    NFLoadBalancerRuleClassName: com.netflix.loadbalancer.RoundRobinRule
```







### 读取超时问题

> Ribbon调用其他微服务，默认等待两秒钟，超时则返回500：connect time out 超时错误

#### 配置Ribbon超时时间

```yaml
ribbon:
  # 启用Eureka客户端，从Eureka获取可用服务的信息进行负载均衡
  eureka:
    enabled: true
  http:
    client:
      # 开启超时管理
      enabled: true
  # 请求超时
  ReadTimeout: 10000
  # 连接超时
  ConnectTimeout: 10000
```







---





## 熔断器(Hystrix)

> OpenFeign内置了Hystrix，只要引入OpenFeign依赖，自动引入

![image-20230508152519608](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305081529679.png)

### RestTemplate与Hystrix整合实现服务降级

#### 在调用方模块中导入Hystrix依赖

```xml
<!--hystrix-->
<dependency>
     <groupId>org.springframework.cloud</groupId>
     <artifactId>spring-cloud-starter-netflix-hystrix</artifactId>
</dependency>
```





#### 再导入公共模块

```xml
<!--公共模块-->
<dependency>
    <groupId>com.woniuxy</groupId>
    <artifactId>commons</artifactId>
    <version>1.0</version>
</dependency>
```





#### 在主启动类上添加@EnableCircuitBreaker注解开启熔断器

```java
@SpringBootApplication
@EnableEurekaClient
@EnableRetry
@EnableCircuitBreaker  // 开启降级
public class ConsumerApplication {

    public static void main(String[] args) {
        SpringApplication.run(ConsumerApplication.class, args);
    }
}
```





#### 在controller需要降级的方法上添加@HystrixCommand注解，并指定fallback方法

```java
@RestController
public class ConsumerController {
    @Resource
    private RestTemplate restTemplate;

    @RequestMapping("/all")
    @HystrixCommand(fallbackMethod = "fallback")
    public List<Goods> all(){
        String url = "http://PROVIDER/all";
        //
        List<Goods> goods = restTemplate.getForObject(url,List.class);
        //
        return goods;
    }
    //返回值、参数必须与对应的方法保持一致
    public List<Goods> fallback(){

        List<Goods> goods = Arrays.asList(
                new Goods(4001,"fallbackA"),
                new Goods(4002,"fallbackB")
        );
        //
        return goods;
    }
}
```







### OpenFeign整合Hystrix实现服务降级

#### 新增fallback Factory

##### 在Feign的Service接口(新被调用方)修改Feign注解

```java
// Feign接口的FeignClient注解新增一个fallbackFactory参数，参数值为降级工厂类.class
@FeignClient(name = "GOODS",fallbackFactory = xxx.class)
public interface FeignGoodsService {

    @GetMapping("/goods/findById/{id}")
    public ResponseResult<Goods> findById(@PathVariable("id") int id);
}
```

###### 实例

```java
@FeignClient(name = "GOODS",fallbackFactory = FeignGoodsServiceFactory.class)
public interface FeignGoodsService {

    @GetMapping("/goods/findById/{id}")
    public ResponseResult<Goods> findById(@PathVariable("id") int id);
}
```





#### 创建降级工厂类

##### 实现FallbackFactory，泛型为要配置降级工厂的Service接口，然后实现里面的方法

```java
@Component
public class Feign的Service接口Factory implements FallbackFactory<Feign的Service接口> {

    @Override
    public FeignXxxService create(Throwable throwable) {
        // 这里的idea自动生成的实现是return null，手动修改为new FeignxxxService，自动实现所有方法
        return new FeignXxxService() {
            @Override
            public ResponseResult<Xxx> 方法名(形参) {
                return new ResponseResult<Xxx>().xxx;
            }
        };
    }
}
```

###### 实例：

```java
@Component
public class FeignGoodsServiceFactory implements FallbackFactory<FeignGoodsService> {

    @Override
    public FeignGoodsService create(Throwable throwable) {
        return new FeignGoodsService() {
            // 服务降级方法
            @Override
            public ResponseResult<Goods> findById(int id) {
                return new ResponseResult<Goods>()
                        .setCode(500)
                        .setMessage("触发降级熔断");
            }
        };
    }
}
```



##### 项目结构，工厂的存放位置

![image-20230508162429526](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305081624163.png)





#### 调用方配置SpringBoot启动扫描路径

##### 需要调用commons中Feign接口的微服务，在SpringBoot启动类配置注解扫描的范围

> 因为调用方(xxx微服务)与降级工厂(commons)不在一个包下，想要扫描到降级工厂类的注解：@Component需要扩大SpringBoot启动时扫描的范围，所以要求两者的包路径必须一致：com.xxx.xyz，xyz可以不一致

```java
// 开启eureka客户端功能
@EnableDiscoveryClient
// 开启Feign的客户端们,扫描Feign接口所在的包，创建接口对象
@EnableFeignClients(basePackages = "com.xxx.commons.service")
// 配置注解扫描的范围，要求所有微服务都有统一的前缀com.xxx
@SpringBootApplication(scanBasePackages = "com.xxx")
public class XxxApplication {

    public static void main(String[] args) {
        SpringApplication.run(XxxApplication.class, args);
    }
}
```





#### 开启熔断器

##### 调用方在配置文件中将熔断器开启

```yaml
spring:
  application:
    # 微服务名，是SpringCloud中找到对应微服务(服务器)的标识，也是集群的标识，不能用下划线
    name: cart-feign
server:
  port: 8091
eureka:
  client:
    service-url:
      # 向该接口注册
      defaultZone: http://localhost:8761/eureka/
  instance:
    # 服务器id，不可重复，用于区分同微服务下不同端口的项目
    instance-id: cart-feign-8091
feign:
  hystrix:
    # 开启熔断器，默认关闭
    enabled: true
```







### Hystrix超时配置

> Hystrix也会超时，超时后会自动执行降级方法，默认两秒

```yaml
hystrix:
  command:
    default:
      # 指定执行策略
      execution:
        timeout:
          # 开启超时管理
          enabled: true
        # 指定隔离策略
        isolation:
          # 采用线程池隔离
          thread:
          	# 设置超时时间为10秒
            timeoutInMilliseconds: 10000
```

#### Ribbon和Hystrix的超时降级的区别

Ribbon：只能在客户端进行处理，即当请求无响应时，客户端会马上返回错误信息，无需等待服务端处理完成

Hystrix：在服务端实现，当服务端被请求后无响应，Hystrix会等待一定时间后再进行熔断操作，同时执行服务降级策略，直到服务端恢复正常。

Ribbon和Hystrix适用于不同的场景，Ribbon适用于轻量级的负载均衡，主要解决服务发现的问题；

而Hystrix则是一种熔断器，主要用于增强系统的稳定性并降低系统的故障率，适用于复杂的微服务架构中。





---





## 网关/路由/过滤器(Gateway)

> 直接请求各个微服务的Controller，存在以下问题：
>
> 1. 跨域问题：直接从客户端请求微服务，可能会涉及到跨域问题，需要处理跨域资源共享，增加了开发难度和复杂度。
> 2. 安全性问题：直接请求微服务，可能会暴露微服务的真实地址和提供的接口，存在安全隐患。
> 3. 单一入口问题：如果直接从客户端请求微服务，那么客户端需要知道每个微服务的地址，这增加了客户端的复杂度，同时也使得后端微服务集群变得不透明。
> 4. 路由问题：在服务拆分后，微服务为了提高服务性能通常部署在多台机器上，客户端无法直接指定微服务的实例，需要通过某种方式进行路由，大量的重复代码使得会增加复杂度。
>
> 而通过Gateway，可以将微服务的请求转发到统一的入口进行集中管理，它为客户端和微服务之间建立了一个中间层，负责所有的请求转发和路由，这样做的好处有：
>
> 1. 解决安全问题：Gateway可以处理权限和身份认证，为微服务提供安全保障。
> 2. 解决跨域问题：Gateway可以处理跨域资源共享，让客户端更方便地访问服务。
> 3. 解决单一入口问题：Gateway充当了所有微服务的入口，将之前分散的逻辑进行整合，使客户端更方便地使用和访问所有的微服务。
> 4. 提高可扩展性：Gateway可以通过负载均衡功能来控制流量，并将请求路由到不同的实例，提高可扩展性。

### Gateway环境搭建

#### 一、创建SpringBoot项目

##### 引入场景器：

> 因为gateway是基于webflux，与spring web不兼容，因此不要导入spring web

![image-20230508185810861](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305090956042.png)



##### 降低SpringBoot、SpringCloud版本、配置父子模块之间的关系

###### gateway：

```xml
<!--子项目中继承父项目-->
<parent>
    <artifactId>springcloud-erp</artifactId>
    <groupId>com.woniuxy</groupId>
    <version>1.0</version>
</parent>
```

###### 父项目：

```xml
<!--设置子项目-->
<modules>
    <module>registcenter</module>
    <module>goods</module>
    <module>cart</module>
    <module>commons</module>
    <module>cart-feign</module>
    <module>gateway</module>
</modules>
```





#### 二、新建配置文件，将该模块添加到注册中心

###### 右键main文件夹

![image-20230508190945946](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305090956240.png)



###### 选中resources

![image-20230508190955515](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305090956992.png)

###### 在resources下创建application核心配置文件

![image-20230508191054275](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305090956597.png)

![image-20230508191108584](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305090956390.png)



###### 修改配置，将gateway添加到注册中心

```yaml
spring:
  application:
    # 微服务名，是SpringCloud中找到对应微服务(服务器)的标识，也是集群的标识，不能用下划线
    name: gateway
server:
  port: 9400
eureka:
  client:
    service-url:
      # 向该接口注册
      defaultZone: http://localhost:8761/eureka/
  instance:
    # 服务器id，不可重复，用于区分同微服务下不同端口的项目
    instance-id: gateway-9400
```





#### 配置Gateway路由

> 匹配特定请求，成功就将该请求转发给配置文件中指定的微服务去处理

```yaml
cloud:
    gateway:
      routes:
        # 路由的id，随意取，不可重复
        - id: aaa
          # lb：负载均衡单词的缩写  aaa:微服务的名字
          uri: lb://aaa
          # 是否是以/xxx开头的请求(uri)，只要匹配上了，就将该请求转发给aaa微服务去处理
          predicates:
            - Path=/xxx/**
```

##### 实例(多个路由)：

```yaml
spring:
  application:
    # 微服务名，是SpringCloud中找到对应微服务(服务器)的标识，也是集群的标识，不能用下划线
    name: gateway
  cloud:
    gateway:
      routes:
        # 路由的id，随意取，不可重复
        - id: goods
          # lb：负载均衡单词的缩写  goods微服务的名字
          uri: lb://goods
          # 是否是以/goods开头的请求(uri)
          predicates:
            - Path=/goods/**
        - id: cart
          uri: lb://cart-feign
          predicates:
            - Path=/cart/**
server:
  port: 9400
eureka:
  client:
    service-url:
      # 向该接口注册
      defaultZone: http://localhost:8761/eureka/
  instance:
    # 服务器id，不可重复，用于区分同微服务下不同端口的项目
    instance-id: gateway-9400
```







### 路由断言

> Predicate（谓语、断言）：路由转发的判断条件，目前SpringCloud Gateway支持多种方式，常见如：Path、Host、Method、Query等。
>

#### Path 方式匹配转发

```yaml
routes:
   - id: provider  
     uri: lb://provider
     predicates:
        - Path=/goods/**
```





#### Host 方式匹配转发

根据Host主机名进行匹配转发，如果我们的接口只允许**.aaa.com域名进行访问，那么配置如下所示：

```yaml
routes:
   - id: provider  
     uri: lb://provider
     predicates:
        - Host=**.aaa.com
```





#### Method断言

这个断言是专门验证HTTP Method的，在下面的例子中，当访问“/gateway/sample”并且HTTP Method是GET的时候，将适配下面的路由

```yaml
routes:
   - id: provider  
     uri: lb://provider
     predicates:
        - Path=/goods/**
        - Method=GET
```





#### Query断言

请求断言，从ServerHttpRequest中的Parameters列表中查询指定的属性，有如下两种不同的使用方式

```yaml
routes:
   - id: provider  
     uri: lb://provider
     predicates:
        - Path=/goods/**
        - Query=name,zhangsan*
```

Query=name表示只要请求中包含 name 属性的参数即可匹配路由

两个参数：Query=name，zhangsan，表示请求中必须包含name属性而且值必须是zhangsan才能匹配路由





#### 通配符

| 通配符 | 解释         |
| ------ | ------------ |
| .      | 任意一个字符 |
| *      | 任意多个字符 |







### 基于Gateway过滤器+数据库实现认证、鉴权

#### 具体实现思路

> 网关(gateway)做认证(验证Token)，各个微服务通过拦截器做鉴权(查询数据库判断权限)

Gateway接收到请求，判断该请求是否需要认证之后才能访问，如果不需要直接放行

如果需要，判断请求头中是否存在Token，检验Token是否过期

通过，判断当前用户是否有权限(将项目中所有URI及访问该URI所需的权限保存至数据库)

在过滤器中得到URI，再以URI作为条件去数据库查询访问需要的权限信息、通过当前用户信息查询到当前用户的所有权限，然后比对，成功放行，不成功返回没有权限的信息，返回登录页

不通过，返回登录页





#### 在Gateway微服务创建过滤器

##### 实现GlobalFilter和Ordered

```java
package com.xxx.gateway.filter;

import org.springframework.cloud.gateway.filter.GlobalFilter;
import org.springframework.core.Ordered;

@Component
public class AuthFilter implements GlobalFilter, Ordered {
    @Override
    public Mono<Void> filter(ServerWebExchange exchange, GatewayFilterChain chain) {
        return null;
    }

    @Override
    public int getOrder() {
        return 0;
    }
}
```









---





## SpringCloudAlibaba

### Nacos

> 替代Eureka

#### 安装

##### 将压缩包解压到想要安装的位置(全英文路径)

![image-20230509101303739](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305091013909.png)



##### 通过CMD打开bin文件夹，输入以下指令启动Nacos

###### 以单机模式运行，非集群模式

```shell
startup.cmd -m standalone
```

![image-20230509101619172](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305091602321.png)

###### 出现successfully表示运行成功

![image-20230509101640519](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305091602110.png)





#### Discovery(服务注册和服务发现)

##### 在项目中添加依赖(降低微服务SpringCloud版本)

```xml
<!--nacos注册中心-->
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
    <version>2.1.0.RELEASE</version>
</dependency>
```



##### 修改配置文件

###### 配置Nacos地址(与spring.Application、Datasource平齐)

```yaml
# 配置nacos地址
cloud:
  nacos:
    discovery:
      # 对应的IP:端口号就是前面启动的Nacos的IP和端口号，避免localhost
      server-addr: IP:端口号
```

###### 暴露端口(与spring平齐，靠最左，可以直接复制到最后面)

```yaml
management:
  endpopints:
    web:
      exposure:
        # 暴露端口方便nacos监控微服务
        include: '*'
```

###### 实例：

```yaml
spring:
  application:
    # 微服务名，是SpringCloud中找到对应服务器的标识，也是集群的标识
    name: address
  # 数据源
  datasource:
    # 8.x选择带cj的，5.x选择不带的
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/mall?useUnicode=true&characterEncoding=utf8&serverTimezone=UTC
    username: root
    password: root
  # 配置nacos地址
  cloud:
    nacos:
      discovery:
        server-addr: 192.168.15.167:8848
server:
  port: 8084
# MyBatis
mybatis:
  # 实体类前缀(别名)
  type-aliases-package: com.woniuxy
  # 配置mapper.xml文件路径
  mapper-locations: classpath:mapper/*.xml
# eureka
eureka:
  client:
    service-url:
      # 向该接口注册
      defaultZone: http://localhost:8761/eureka/
  instance:
    # 服务器id
    instance-id: address-8084
# 配置SpringBootActuator的端点访问暴露方式，暴露端口方便nacos监控微服务
management:
  endpopints:
    # 暴露的端点类型
    web:
      # 指定 Spring Boot Actuator 的端点是否暴露
      exposure:
        # 需要暴露的端点，默认可以为 "*"，此时所有端点均对外开放
        include: '*'
```





##### 在主启动类上添加注解(跟Eureka一致)

```java
@EnableDiscoveryClient
```





#### Config(配置中心)

##### 引入依赖

```xml
<!--nacos配置中心-->
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-nacos-config</artifactId>
    <version>2.1.0.RELEASE</version>
</dependency>
```



##### 迁移配置文件内容到Nacos

> 执行后可以选择删除或者注释掉原配置文件

###### 复制application.yml中所有内容，切换到Nacos后台，新建配置

![image-20230509110021717](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305091602234.png)

###### 修改配置文件格式为YAML

![image-20230509110155193](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305091602115.png)

###### 添加配置文件名

格式需要按照官方取名：${spring.application.name}-${spring.profiles.active}.${file-extension}

​	${spring.application.name}：bootstrap.yml中指定的微服务名

​	${spring.profiles.active}：bootstrap.yml中指定的配置信息环境

​	${file-extension}：后缀名格式，nacos只支持properties和yaml两种格式

例如：address-dev.yaml



##### 在项目新建bootstrap配置文件

> SpringBoot有两种配置文件：application，bootstrap，可以同时存在，bootstrap优先级高于application
>
> bootstrap通常用于配置项目启动时需要额外加载或配置的信息

```yaml
# nacos配置
# ${spring.application.name}-${spring.profiles.active}.${file-extension}
spring:
  application:
    name: address
  profiles:
    # 环境，配置信息的环境：dev开发、test测试、produce生产
    active: dev
  cloud:
    nacos:
      config:
        # 配置中心的地址
        server-addr: 192.168.15.167:8848
        # 配置文件的后缀名
        file-extension: yaml
```



##### Nacos配置热部署(在Nacos修改配置，不重启服务器自动生效)

```java
// 开启Nacos自动刷新功能
@RefreshScope
public class AddressController {...}
```

@RefreshScope注解是Spring Cloud提供的一个用于动态更新配置的注解，它可以让Spring容器中的Bean在配置信息更新时自动进行刷新。当配置信息发生变化时，@RefreshScope注解会触发Spring容器重新实例化被注解的Bean，从而使得新的配置信息生效。

一般需要将@RefreshScope注解加在Bean的类定义上，以便在配置信息发生变化重新实例化这个Bean。

###### 例如：

```
@Service
@RefreshScope
public class MyService {
    @Value("${config.key}")
    private String configKey;
    // ...
}
```

在这个例子中，@RefreshScope注解被加在MyService类上，表示这个类需要支持动态更新配置。当配置信息中的`config.key`键值发生变化时，Spring容器会重新实例化MyService类，并注入新的配置值。

需要注意的是，@RefreshScope注解只会生效在Spring容器管理的Bean中，如果我们使用new关键字手动创建了Bean对象，则@RefreshScope注解会失效。同时，@RefreshScope注解的Bean不能使用final修饰，否则会导致无法重新实例化。



##### group分组配置

###### 在新增配置时，Group的值不再是DEFAULT_GROUP，修改为其他组名

![image-20230509114230558](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305091602738.png)

```yaml
# nacos配置
# ${spring.application.name}-${spring.profiles.active}.${file-extension}
spring:
  application:
    name: address
  profiles:
    # 环境，配置信息的环境：dev开发、test测试、produce生产
    active: dev
  cloud:
    nacos:
      config:
        # 配置中心的地址
        server-addr: 192.168.15.167:8848
        # 配置文件的后缀名
        file-extension: yaml
        # 指定nacos中同名但不同组的配置，指定分组，默认DEFAULT_GROUP
        group: first_group
        # group: DEFAULT_GROUP
```



##### 命名空间配置

> Nacos的配置文件数量有上限，每个命名空间中可以保存的配置信息是200个，创建多个配置需要命名空间

###### 创建命名空间

![image-20230509114616384](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305091602357.png)

###### 命名空间ID在命名空间列表

![image-20230509114752862](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305091602194.png)

###### 在bootstrap.yml通过命名空间ID指定其他命名空间的配置

```yaml
# nacos配置
# ${spring.application.name}-${spring.profiles.active}.${file-extension}
spring:
  application:
    name: address
  profiles:
    # 环境，配置信息的环境：dev开发、test测试、produce生产
    active: dev
  cloud:
    nacos:
      config:
        # 配置中心的地址
        server-addr: 192.168.15.167:8848
        # 配置文件的后缀名
        file-extension: yaml
        # 指定nacos中同名但不同组的配置，指定分组
        # group: first_group
        group: DEFAULT_GROUP
        # 配置命名空间
        namespace: e5fd44a1-30e1-4032-8549-6de3a55a3e10
```







### Sentinel(替代Hystrix熔断器，服务降级)

> Hystrix是在服务器出问题后执行相应的操作，Sentinel是通过限流等操作在服务器出问题之前就执行操作
>























