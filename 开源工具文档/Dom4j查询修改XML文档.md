## Dom4j解析XML文档

### 一、XML解析的方式介绍

### 在日常开发中常见的XML解析方式有如下两种：

#### 1.DOM解析

##### DOM解析要求解析器将整个XML文件全部加载到内存中，生成一个Document对象。

优点：元素和元素之间保留结构，关系，可以针对元素进行增删改查操作。
缺点：如果XML文件过大，可能会导致内存溢出。





#### 2.SAX解析

##### SAX解析是一种更加高效的解析方式。

##### 它是逐行扫描，边扫描边解析，并且以时间驱动的方式进行具体的解析，每解析一行都会触发一个事件。

优点：不会出现内存溢出的问题，可以处理大文件。
缺点：只能读，不能写。







### 二、使用dom4j解析XML

#### 创建maven项目，引入依赖

##### Maven：

```xml
<!--dom4j编辑XML-->
<dependency>
    <groupId>org.dom4j</groupId>
    <artifactId>dom4j</artifactId>
    <version>2.1.1</version>
</dependency>
```





#### 使用dom4j解析user.xml

##### 1.在项目的resource目录下创建xml文件

在下面user.xml文件中，users是根标签，根标签是全局唯一的

在根标签下有两个user子标签，每一个user子标签都有两个属性，一个是country，另一个是source

在user标签下同样有三个子标签，分别是id，name以及password标签

###### user.xml：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!--文档声明
    XML的文档声明是可选的，也就是可以不写，但是日常生活开发中大家都会写
    XML文档声明如果写了,它必须放在XML文档的第一行第一列,必须以<?xml开头 以?>结尾,而且必须包含两个属性
    一个是version,表示XML的版本
    一个是encoding,表示XML的编码
-->
<!--
    元素是XML的重要组成部分，元素也被称为标签
    每个XML文件必须要有一个根标签
    标签有开始标签和结束标签组成,开始标签和结束标签可以写标签,也可以是文本字符串
    标签可以嵌套使用,但是不能随便嵌套
    标签名必须准守命名规则和命名规范
-->
<!--
    属性是标签的组成部分，属性只能定义在开始标签中，不能定义在结束标签中
    属性定义的格式:属性名=属性值，属性值需要使用""包含起来
    开始标签中可以定义多个属性，但是多个属性的属性名不能相同
    属性名必须准守命名规则和命名规范
-->
<users>
    <user id="10001" country="Chinese" source="Android">
        <id>10001</id>
        <name>admin</name>
        <password>111111</password>
    </user>

    <user id="10002" country="Chinese" source="ios">
        <id>10002</id>
        <name>tony</name>
        <password>666666</password>
    </user>
</users>
```



##### 2.在测试类创建解析器对象

```java
// 创建解析器对象
SAXReader saxReader=new SAXReader();
```



##### 3.使用解析器对象读取XML文档生成Document对象

```java
// 根据user.xml文档生成Document对象
Document document = saxReader.read(dom4jTest.class.getClassLoader().getResource("users.xml"));
```



##### 4.根据Document对象获取XML的元素(标签)信息

###### Dom4j的常用API说明

|            方法             |      返回值      |                      操作                      |
| :-------------------------: | :--------------: | :--------------------------------------------: |
|      getRootElement()       |     Element      |              获取XML文件的根节点               |
|          getName()          |      String      |                 返回标签的名称                 |
|         elements()          | List < Element > |             获取某标签所有的子标签             |
| attributeValue(String name) |      String      |            获取指定属性名称的属性值            |
|          getText()          |      String      |                 获取标签的文本                 |
|  elementText(String name)   |      String      | 获取指定名称的子标签的文本，返回子标签文本的值 |





#### 实例：

```java
package study;

import org.dom4j.Document;
import org.dom4j.DocumentException;
import org.dom4j.Element;
import org.dom4j.io.SAXReader;

import java.util.List;

/**
 * @Author BLACKHKER
 * @Date 2023/3/21 14:58
 * @ClassName: study.dom4jTest
 * @Description: TODO
 * @Version 1.0
 */
public class Dom4jTest {
    public static void main(String[] args) {
        SAXReader saxReader = new SAXReader();
        try {
            //根据user.xml文档生成Document对象
            Document document = saxReader.read(Dom4jTest.class.getClassLoader().getResource("user.xml"));
            System.out.println("=====================获取根节点=====================");
            // 获取XML文件的根节点
            Element rootElement = document.getRootElement();
            System.out.println("当前文件的根节点名字是：" + rootElement.getName());
            System.out.println("=====================获取根节点users的所有的子标签=====================");
            // 获取根节点的所有子节点
            List<Element> userList = rootElement.elements();
            // 遍历
            userList.forEach(user -> {
                System.out.println("当前循环的user标签内的id标签的内容是：" + user.elementText("id"));
                System.out.println("当前循环子标签标签的名字是：" + user.getName());
                System.out.println("====================获取指定属性名称的属性值======================");
                System.out.println("当前循环子标签标签的id属性值为：" + user.attributeValue("id"));
                System.out.println("当前循环子标签标签的country属性值为：" + user.attributeValue("country"));
                System.out.println("====================获取user标签的下的子标签=========================");
                // 获取遍历到的每个user标签的子标签
                List<Element> userChildrenList = user.elements();
                userChildrenList.forEach(userChildren -> {
                    System.out.println("当前循环子标签标签的名字是：" + userChildren.getName());
                    System.out.println("当前循环子标签的标签内容是：" + userChildren.getText());
                });
            });
        } catch (DocumentException e) {
            e.printStackTrace();
        }
    }
}
```

