## Lambda表达式

> Lambda是简化接口实现类的语法糖，解决在使用匿名实现类的时候new接口的对象很长一段冗余代码，
>
> 使用Lambda表达式的接口必须是函数式接口：抽象方法有且最多只能1个。

### 匿名实现类

> 接口只有一个方法，但是还要写一个实现类，这种情况可以用匿名实现类来简化代码。
>
> 没有类名、创建匿名实现类的对象必须new关键字一起出现

#### 格式：

```java
// 通过匿名实现类创建一个接口的实例(对象)
接口名 对象名 = new 接口名(){		
    @Override
    原实现类类体；
}
```

##### 实例：

###### 原接口：

```java
interface Phone {
    // 抽象方法
		public void show();	
}
```

###### 原接口的实现类：

```java
// Phone的实现类XiaoMi:
class XiaoMi implements Phone {	
    // 继承并实现了手机的show方法
    @Override
    public void show() {
        System.out.println("我是小米手机");
    }
}
```

###### 原调用实现类里的方法：

```java
public class Test{
	public static void main(String[] args){
    	Phone phone = new XiaoMi();	// 先创建实现类的对象
        phone.show();	// 用对象调用方法，执行实现类中的show方法
	}	// 主函数
}	// 主类
```

###### 匿名实现类实现接口中的方法：

```java
// 1、将所有原实现类整体搬到创建对象这里
public class Test{
	public static void main(String[] args){
    	Phone phone = /*new XiaoMi()没了*/  
        class XiaoMi implements Phone {	
			@Override
			public void show() {
				System.out.println("我是小米手机");
			}
		};  
	}	// 主函数
}	// 主类

// 2、删除原实现类类名、实现了哪个接口也删除
public class Test{
	public static void main(String[] args){
    	Phone phone = 
        /*删除了这里*/{
			@Override
			public void show() {
				System.out.println("我是小米手机");
			}
		};  
	}	// 主函数
}	// 主类

// 3、new 接口的对象:new Phone()
public class Test{
	public static void main(String[] args){
    	Phone phone = new Phone(){	
			@Override
			public void show() {
				System.out.println("我是小米手机");
			}
		};  
		// 接下来就可以向之前一样调用方法了：
        phone.show();
	}	// 主函数
}	// 主类
```

> 直接new接口的对象，他会报错：接口不能直接创建实例，只能创建该接口的实现类的实例。
>
> 那么直接把实现类的类体写在new接口对象的后面，告诉接口这个就是实现类，这就是匿名实现类。







### 匿名实现类继续精简则使用lambda表达式：

#### 格式：

```java
接口名 对象名 = (/*参数列表*/) -> /*箭头操作符*/{
	// 方法体，写具体操作的;
};	
```

##### 实例：

```java
// 接口计算器(Calc)的对象 = () -> {}
Calc sum = (int a, int b) -> {
	return a+b;
};
```

> java本质是一个函数，Lambda可以替代匿名内部类来实现接口。
> 一般的函数有返回值、方法名、参数列表、方法体;
> 而lambda表达式只有参数列表和方法体：(参数列表) -> {方法体}，"->"箭头符号为lambda运算符。



##### 简化匿名实现类为Lambda表达式：

```java
// 1、删除new及方法体括号
public class Test{
	public static void main(String[] args){
    	Phone phone = /*new Phone(){*/	
			@Override
			public void show() {
				System.out.println("我是小米手机");
			}
		/*}*/;  
	}	// 主函数
}	// 主类

// 2、去掉方法体，留一个方法的参数列表(放参数的括号)
public class Test{
	public static void main(String[] args){
    	Phone phone = 	
			/*@Override
			public void show*/() {
				System.out.println("我是小米手机");
			};  
	}	// 主函数
}	// 主类

// 3、最后添加一个lambda运算符："->"就完事了
public class Test{
	public static void main(String[] args){
    	Phone phone = () -> {
				System.out.println("我是小米手机");
			};  
	}	// 主函数
}	// 主类

// 使用：
phone.接口方法名();
```



### Lambda表达式精简

#### 原Lambda表达式：

```java
// 接口计算器(Calc)的对象 = () -> {}
Calc sum = (int a, int b) -> {
	return a+b;
};
```





#### 简化Lambda：

##### 1.参数类型可以省略

```java
Calc sum = (a, b) -> {
	return a + b;
};
```



##### 2.假如只有一个参数,括号()可以省略

```java
Calc sum = a -> {
	return a;
};
```



##### 3.如果方法体只有一条语句，大括号可以省略

```java
Calc sum = a -> return a + b;	// 注意return是例外，有return的时候需要同时去掉return;
```



##### 4.如果方法体中唯一的语句是return，则需要把return同时省略

```java
Calc sum = a -> a + b;	// 有return是例外的正确写法
```







### Lambda表达式配合函数式接口

#### 五种情况：接口没有参数、只有一个参数、有多个参数、有返回值、非一行(多行)代码

##### 原接口：

```java
// 一般只有一个抽象方法的接口，我们可以统称为：“函数式接口”
interface Person {
    void show();
}
```



##### 接口没有参数：

```java
public class Test {
    
	// 写法一：通过定义实现类来完成。
	Person p = new PersonImpl();

    // 写法二：匿名实现类
    Person p2 = new Person() {
        @Override
        public void show() {}
    };
    
    // 写法三：通过Lambda表达式 -》优越而已
    Person p3 = () -> {
        System.out.println("hello Lambda");
    };
    
    // 执行接口Person中抽象方法show的匿名实现类
        p3.show();
}
```





---





## @FunctionalInterface：函数式接口

### 使用：

被@FunctionalInterface注解的接口，称为函数式接口，被声明的接口有且只能有一个抽象方法

例如：

```java
@FunctionalInterface
interface Animal {
    void eat(String food);
    // 两个抽象接口报错
    void walk(String time);
}
```





### 作用：

可以使用函数式接口作为方法的参数类型和返回值类型

参数和返回值就可以使用Lambda表达式简化代码了 Lambda表达式可以看成就是接口的实现类对象的一种

**可以理解为，不需要自己定义接口，需要什么类型的(有参无参、有无返回值)接口，直接用JDK现成的接口模板，然后我们定义JDK这些模板接口的实现类。而实现类可以通过Lambda表达式来简化不写，省略掉写接口实现类的过程，直接将方法体逻辑代码使用Lambda实现。方法引用则是使用Lambda写接口实现类的逻辑代码都不写了，直接引用别的方法的逻辑代码，来实现我们自己的接口(函数式接口)，作为接口中方法的逻辑**





### 接口类型

#### Consumer：消费型函数式接口

> 有一个参数，无返回值

```java
Consumer<传入参数的类型> consumer = (参数) -> {
     // 逻辑代码
};
```

##### 例如：

```java
public class Demo {
	public static void main(String[] args) {
        // 创建接口的实例，使用Lambda表达式，定义类型，表示传入参数的类型，不定义就是Object
		Consumer<String> consumer = (name) -> {
            // 将传入的姓名转成大写
            String upperName = name.toUpperCase();
            System.out.println("该姓名大写后：" + upperName);
        };
        // 用实例调用方法，执行Lambda表达式写的实现类的方法体
        // accept是该消费型函数式接口内部定义的抽象方法：void accept(T t);
        consumer.accept("user"); // 输出USER
	}
}
```



##### 创建接口实例(逻辑)可以通过方法引用进行实现，不自己写逻辑，直接引用别的方法的逻辑代码：

```java
public class Demo {
	public static void main(String[] args) {
        // 创建接口的实例，引用了println方法的方法体(逻辑)
        // 方法引用,普通方法用对象.方法名调用(out.println())
		Consumer consumer = System.out::println;
        // 用实例调用方法，执行println方法的逻辑
        // accept是该消费型函数式接口内部定义的抽象方法：void accept(T t);
        // 执行的方法体(逻辑)就是引用的PrintStream类的println方法的方法体(逻辑)
        consumer.accept("Success"); // 输出Success
	}
}
```

###### 引用的PrintStream中的方法：

```java
public void println(String x) {
    synchronized (this) {
        print(x);
        newLine();
    }
}
```





#### Supplier：供给型函数式接口

> 无参数有返回值

```java
Supplier supplier = () -> {
     // 逻辑代码
};
```

##### 例如：

```java
public class Demo {
	public static void main(String[] args) {
        // 创建接口的实例，使用Lambda表达式
		Supplier supplier = () -> {
            return "牛肉";
            // return 任意东西，也可以是对象
        };
        // 用实例调用方法，执行Lambda表达式写的实现类的方法体
        // get是该供给型函数式接口内部定义的抽象方法：T get();
        Object obj = supplier.get(); // 输出牛肉
	}
}
```





#### Predicate：断言型函数式接口

> 返回布尔，有参数，判断是否正确

```
Predicate<参数类型> predicate = (参数) -> {
     // 逻辑代码，返回布尔
};
```

##### 例如：

```java
// 断言型函数式接口
Predicate<Integer> predicate = (age) -> {
    return age > 18;
};
Integer age = 20;
// test是该断言型函数式接口内部定义的抽象方法：boolean test(T t);
boolean r = predicate.test(age));
```





#### Function：功能型函数式接口

> 有参数有返回值

```java
Function<参数类型,返回值类型> function = (参数) -> {
     // 逻辑代码
};
```

##### 例如：

```java
// 传一个数字，返回该数字+10后的数
Function<Integer, String> function = (e) -> {
    String str = "计算结果是" + (e + 10);
    return str;
};
System.out.println(function.apply(5));	// 输出15
```



##### 第二个例子：

```java
// 传一个字符串，返回字符串的长度，这里是Lambda的简便写法，省略了参数列表的小括号、return、和大括号
Function<String, Integer> function = e -> e.length();
Integer len = function.apply("hello你好");
System.out.println(len);	// 输出7
```

###### 未省略版本：

```java
Function<String, Integer> function = (e) -> {
   return e.length();
}
```





---





## 方法引用：自己的接口引用其他类中方法的方法体

### 使用

通过映射操作符"::"，使用方法引用的时候，注意被引用方法的参数必须跟接口参数的类型、个数、顺序都一致

#### 引用方式：

instanceName::methodName：对象::方法名

ClassName::methodName：类名::普通方法

ClassName::staticMethodName：类名::静态方法

ClassName::new：类名::new 调用的构造器

TypeName[]::new String[]::new 调用数组的构造器

##### 总结：普通方法用对象和类名引用都可以，静态方法只能用类名引用，构造方法用类名::new关键字的方式引用







### 类型

#### 普通方法引用

> 接口名 接口实例 = 对象::方法名

##### 无返回值有参数：

```java
// 声明函数式接口注解
@FunctionalInterface
interface AAA {
	void hello(String str);
}
public class Demo {
    public static void main(String[] args){
		// System.out.println(String x); 该方法底层有参数String x
        AAA a = System.out::println;
        a.hello("刘备");	// 
    }
}
```





#### 静态方法引用

> 接口名 接口实例 = 类名::方法名

##### 无参数：

```java
// 声明函数式接口注解
@FunctionalInterface
interface AAA {
	void hello();
}
// 被引用方法体的Demo类
public class Demo {
	// 静态方法
	public static void hello(){
		System.out.println("执行Demo类的hello方法");				
	}
    
    public static void main(String[] args){
        // 静态方法引用(不是方法调用),类名::方法名，引用Demo类中的静态方法hello()
        AAA a = Demo::hello;
		// 方法调用，输出：执行Demo类的hello方法
        a.hello();
    }
}
```



##### 有参数：

```java
// 声明函数式接口注解
@FunctionalInterface
interface BBB {
	void hello(String str);
}

public class Demo {
	// 静态方法1
	public static void hello(){
		System.out.println("执行Demo类的hello方法");				
	}
    
    // 静态方法2
	public static void hello2(String str){
		System.out.println("执行Demo类的hello方法" + str);				
	}
    
    public static void main(String[] args){
        // 静态方法引用(不是方法调用),类名::方法名，引用Demo类中的静态方法hello()
        // 方法调用，输出：执行Demo类的hello方法
        BBB b = Demo::hello;	
        // 方法调用，输出：执行Demo类的hello方法
        b.hello("刘备");	
		/**=========================================================*/
        // 方法调用，输出：执行Demo类的hello，方法
        BBB b = Demo::hello;	
        // 正确，BBB有参数，输出：执行Demo类的hello方法 刘备
        b.hello2("刘备")	
    }
}
```



##### 有返回值，有参数：

```java
// 声明函数式接口注解
@FunctionalInterface
interface BBB {
	int hello(int x,int y);
}
public class Demo {
    public static void main(String[] args){
        // 静态方法引用，引用Integer中的静态方法compare
        // compare参数匹配(两个int)，返回值匹配(int)
        BBB b = Integer::compare;
    }
}
```





#### 构造方法引用

> 接口名 接口实例 = 类名::new
>

```java
interface DogFactory {
    Dog make();
    Dog make(String name)
}

public class Dog {
	String name;
    // 无参构造
    public Dog(){}
    // 有参构造
    public Dog(String name){
        this.name = name
    }
    
    public static void main(String[] args) {
		// 引用构造方法
        DogFactory dogFactory = Dog::new;
        // 接口调用：无参引用、有参引用，根据参数不同区分引用哪个构造方法
        Dog dog1 = dogFactory.make();
        Dog dog2 = dogFactory.make("多乐");
        // 打印多乐
        String dog2Name = dog2.getName();
	}
}
```





---





## Java8的Stream流编程

> Java8中引入了流（java.util.stream.Stream）的概念，流在编程中的写法类似于jQuery的链式编程。
>
> 它的功能主要是操作数据：从集合、数组或IO资源上进行数据操作。
>
> 例如：过滤(filter)、遍历(each)、查找(find)、排序(sort)、匹配(match)、映射(map)等。
>
> **注意：它只负责处理数据，不负责存储数据**

### 操作：

#### stream()：创建流

##### 将数组转换为流：

###### 写法一：Stream.of(参数值1,参数值2,...)

```java
Stream<限定参数类型(包装类型)> intsStream = Stream.of(参数值1,参数值2,...);
Stream<Integer> intsStream = Stream.of(1, 2, 3);	// 参数类型不能是int，包装类型
```

Stream.of底层就是Arrays. Stream()：

```java
public static<T> Stream<T> of(T... values) {
    return Arrays.stream(values);
}
```



###### 写法二：Arrays.stream(数组);

```java
int[] num = {1, 2, 3};
IntStream intStream = Arrays.stream(num);
```





#### close()：关闭流

```java
intsStream.close();
intStream.close();
```





#### count()：统计流个数(自动关闭)

```java
Long count = intsStream.count();
System.out.println("流intsStream的个数是" + count);
```





#### foreach()：遍历流(自动关闭)

##### 该方法需要传一个接口：函数式接口Consumer，有两种实现方式，Lambda和方法引用：

###### Lambda：

```java
intsStream.forEach(Consumer消费者接口);
// 写一个匿名实现类并通过Lambda简化
intsStream.forEach((e) -> {
    System.out.println(e);
});
```

###### 方法引用：

```java
// 普通方法用对象引用，静态方法用类名引用
// System类下有一个PrintStream类的公共静态对象out,PrintStream类有普通方法println
// 当前类没有对象out，用类名调用对象out，普通方法用对象引用，引用println方法(有一个参数，无返回值)
intsStream.forEach(System.out::println);	// println方法符合Consumer
```





#### limit()：截取流

```java
Stream<Integer> intsStream = Stream.of(3, 2, 1, 1, 2, 6);
intsStream.limit(3).forEach(System.out::println);	// 输出321,只保留3个，后面被截取了
```





#### filter()：过滤流

##### intsStream.filter(断言型函数式接口)：

```java
Stream<Integer> intsStream = Stream.of(3, 2, 1, 1, 2, 6);
// 实例1
intsStream.filter((num) -> {
    return num > 5;	// 返回布尔，过滤大于5的数字
}).forEach(System.out::println);	// 输出6

// 实例2
Long count = intsStream.filter((num) -> num > 5).count();	// 获取过滤符合条件数字个数
System.out.println(count);	// 输出1
```





#### ※有些方法会自动关闭流，所以操作流的时候必须一步完成

```java
// 以count方法为例
Stream<Integer> intsStream = Stream.of(1, 2, 3);
// 统计流个数
Long count = intsStream.count();
System.out.println("流intsStream的个数是" + count);

// 遍历流会报错,提示流已经在之前关闭，无法操作
intsStream.forEach((e) -> {
	System.out.println(e);
});
```

##### 报错：

```cmd
Exception in thread "main" java.lang.IllegalStateException: stream has already been operated upon or closed
at java.util.stream.AbstractPipeline.sourceStageSpliterator(AbstractPipeline.java:279)
at java.util.stream.ReferencePipeline$Head.forEach(ReferencePipeline.java:580)
at com.blackhker.study.StreamDemo.main(StreamDemo.java:30)
```





#### map()：映射流

##### beanStream.map(功能型函数式接口)：

```java
List<String> names = Stream.of(new Student(13, "刘备"), new Student(23, "关羽"), new Student(33, "张飞"))	// map传功能函数接口，有参有返回，传Student对象(e),返回对象的name属性(e.name)
	.map((Student e) -> {
		return e.name;	// 属性没私有、没写get、set 正常应该是 return e.getName()
	}).collect(Collectors.toList());	// collect()收集数据返回一个集合(student的name集合)
names.forEach(System.out::println);	// 遍历name，输出刘备关羽张飞
```

###### 简写：本例中私有属性，提供get、set方法

```java
// Lambda
List<String> names = Stream.of(new Student(13, "刘备"), new Student(23, "关羽"), new Student(33, "张飞")).map(e -> e.getName()).collect(Collectors.toList());
// 方法引用
List<String> names = Stream.of(new Student(13, "刘备"), new Student(23, "关羽"), new Student(33, "张飞")).map(Student::getName).collect(Collectors.toList());	// 类名引用
```





#### 其他方法：

##### distinct()：去重

```java
Stream<Integer> intsStream = Stream.of(1, 2, 3, 1, 2, 3);
// 去重后遍历
intsStream.distinct().forEach(System.out::println);	// 输出123
```



##### sorted()：排序(默认升序)

```java
Stream<Integer> intsStream = Stream.of(3, 2, 1, 1, 2, 3);
// 去重后排序再遍历
intsStream.distinct().sorted().forEach(System.out::println);	// 输出123(升序从小到大输出)
```

###### 降序：传一个比较器Comparator

```java
intsStream.distinct().sorted(new Comparator<Integer>() {
    @Override
    public int compare(Integer o1, Integer o2) {
        return o2 - o1;	// 返回降序
    }
}).forEach(System.out::println);	// 输出321

// Lambda简化
intsStream.distinct().sorted((Integer o1, Integer o2) -> {
    return o2 - o1;
}).forEach(System.out::println);

// 去掉参数类型、方法括号及return
intsStream.distinct().sorted((o1, o2) -> o2 - o1).forEach(System.out::println);
```

###### 学生对象排序：

```java
class Student {
    int age;
    String name;

    public Student() {
    }

    public Student(int age, String name) {
        this.age = age;
        this.name = name;
    }
}
```

```java
Stream.of(new Student(13, "刘备"), new Student(23, "关羽"), new Student(33, "张飞"))
	.sorted((o1, o2) -> o2.age - o1.age).forEach((stu) -> {	// 由大到小
    	System.out.println(stu.name);	// 输出张飞关羽刘备
	});
```



##### sum()：求和

```java
Stream<Integer> intsStream = Stream.of(3, 2, 1, 1, 2, 6);
int sum = intsStream.mapToInt((Integer e) -> {
    return e;
}).sum();
System.out.println(sum);	// 输出15
```

```java
int sum = intsStream.mapToInt(e -> e).sum();
```



##### average()：求平均值

```java
Stream<Integer> intsStream = Stream.of(3, 2, 1, 1, 2, 6);
double average = intsStream.mapToInt((Integer e) -> {
    return e;
}).average().getAsDouble();// average()方法返回OptionalDouble类型，getAsDouble()转换成double
System.out.println(average);	// 输出2.5
```

```java
double average = intsStream.mapToInt(e -> e).average().getAsDouble();
```





---





## 总结Lambda、函数式接口、方法引用、Stream流：

一个接口中只有一个抽象方法，称为函数式接口。

以往接口的实现要先创建一个类，然后去实现这个接口(implement)中的每个抽象方法，称为接口的实现类，但是函数式接口只有一个抽象方法，单独写一个实现类很麻烦，就有了匿名实现类的概念。

匿名实现类不需要单独写一个实现类去实现接口，只在需要执行接口方法的时候new一个匿名实现类就可以，但是匿名实现类写起来代码又太冗余，JDK1.8就推出了简化匿名实现类的语法糖：Lambda表达式。

Lambda表达式中定义接口的具体实现(逻辑代码)，虽然有Lambda极大简化了写接口实现类的过程，但是很多接口实现类的方法体内部的逻辑代码是重复的，每个Lambda表达式中重复写相同的逻辑代码，也很繁琐，那么对于重复的代码，可以使用方法引用来继续简化。

Lambda简化的接口，只能是只有一个抽象方法的接口(函数式接口)，而接口都是我们自己定义的，JDK根据参数类型、参数格式、有无返回值进行区分，推出了内置的函数式接口(消费型、断言型、供给型等)，需要使用只有一个方法的接口的时候，我们就可以根据参数类型等条件选择使用哪个内置的接口，不再需要自己再去定义一个接口。





---





## 微服务

### 架构的演变

![image-20230225162952366](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202302251630064.png)

#### 单体架构

##### 解释：

单体架构就好像一个巨石。

一个程序中包含所有系统的业务、功能。

比如一个电商系统，就包含了系统模块，商品模块、用户模块，订单模块，等等，这个程序在部署时就是一个进程，比如把war包部署到tomcat中。

![image-20230225164541056](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202302251645504.png)

##### 优缺点：

###### 优点：最稳定，最通用，最易于维护的。

- 经济层面：创业公司初期、客户业务单一、金额较少，研发资源缺少。
- 客户层面：上线时间要求紧张、客户二开需求较多，客户使用量较少

###### 缺点：大型项目有弊端

- 全部功能集成在一个工程中，对于大型项目不易开发、扩展和维护。
- 系统性能只能通过扩展集群结点，成本高，有瓶颈。
- 技术栈受限。
- 代码耦合度很高。
- 容错性差，比如用户管理出问题了，整个系统全部出问题，牵一发而动全身。





#### 垂直应用架构

##### 解释：

单体架构的优点和缺点都特别明显，网站的访问量越来越大，对于单体架构下的应用要想抗住如此大的访问量，那就得增加部署节点，通过负载均衡来分流承接访问量，但是并不是所有的模块都会有很大的访问量。

还是以电商系统为例，访问量比较大的模块可能只是商品模块、订单模块以及支付模块，但是对于消息模块的访问量就比较少了，那么此时我只想增加商品、订单以及及支付模块的部署节点，但对于消息模块则不增加，显然单体架构就不能实现了，这时候就有了垂直应用架构。

所谓的垂直应用架构，就是将原来的一个应用拆成互不相干的几个应用，以提升效率：

![image-20230225165029564](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202302251650827.png)



##### 优缺点：

###### 优点：

- 系统拆分后实现了流量分担，解决了并发问题，且可以针对特定模块进行性能优化以及水平扩容。
- 提升容错率，一个系统出现问题不会导致整个应用不可用。

###### 缺点：

- 系统之间相互独立，无法相互调用

- 系统之间相互独立，会出现重复的开发工作。。

  

#### 分布式架构

##### 解释：

随着业务需求量增多，需要的垂直应用也越来越多，对重复代码的拷贝也就越来越多，这时候就可以把重复的代码单独抽离出来，形成统一的业务层作为独立的服务，这时就出现分布式应用架构。

![image-20230225165223611](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202302251652799.png)



##### 优缺点：

###### 优点：

- 抽取公共的功能为服务层，提高代码复用性。

###### 缺点：

- 随着服务越来越多，系统间耦合度变高，调用关系错综复杂，后续难以维护。






#### SOA架构

##### 解释：

随着业务的发展，在分布式架构的基础上开发的服务越来越多，对于容量的评估，小服务资源的浪费等问题逐渐显现，需增加一个调度中心对集群进行实时管理。

此时，用于资源调度和治理中心(SOA Service Oriented Architecture)出现。

![image-20230225165458509](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202302251655563.png)



##### 优缺点：

###### 优点：

- 使用治理中心（ESB\dubbo）解决了服务间调用关系的自动调节。
- 在调用协议上实现了统一，屏蔽了异构系统间的调用细节。

###### 缺点：

- 使用中心化的ESB进行服务协调，容易出现服务雪崩。
- 服务关系复杂，测试、运维部署困难。





#### 微服务架构

##### 解释：

微服务架构在某种程度上是SOA架构继续发展的下一个方向，它强调将服务进行“彻底拆分”，去中心化，每个服务是独立部署的，可以单独运行。

![image-20230225165551399](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202302251655161.png)

![image-20230225165606296](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202302251656325.png)





---





## SpringBoot

### 通过SpringBoot搭建WEB项目

#### 新建项目：

![image-20230220150013461](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/lpogC2uVaFEdsbR.png)





#### 配置项目环境(场景器)：

> 区分场景器：maven中包含starter代表SpringBoot场景器

![image-20230220150326977](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/IgXUHSjwi7b6a8R.png)





#### 配置环境：

> ※WEB场景器引入了14个Jar包
>
> Maven中<parent>标签表示起步依赖，引用父类的配置

![image-20230220150702697](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/E8p5oX6clCQLaRb.png)

##### Maven：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.3.7.RELEASE</version> <!-- 改为2.3.7.RELEASE -->
        <relativePath/> <!-- lookup parent from repository -->
    </parent>

    <groupId>com.blackhker</groupId>
    <artifactId>music</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>music</name>
    <description>music</description>

    <properties>
        <java.version>1.8</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        
        <!--其他依赖(Lombok、Mybatis)-->
        
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>
```





#### (附加)获取SpringBoot启动时加载的组件名及对象名

##### SpringBoot环境搭建完自动生成的启动类中主函数会执行一个run方法：

```java
@SpringBootApplication
public class QqmastersApplication {
    // main方法
    public static void main(String[] args) {
        SpringApplication.run(QqmastersApplication.class, args);
    }
}
```



##### 该方法返回一个ConfigurableApplicationContext类型的对象：

![image-20230225200408094](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202302252004388.png)



##### 接收该对象，打印长度：

```java
// 创建的时候自动创建对象，上下文对象,可以通过上下文对象获取容器在启动时创建(注册)的对象
ConfigurableApplicationContext config = SpringApplication.run(启动类类名.class,args);
// 打印长度，输出137：启动SpringBoot项目，需要137个对象
System.out.println(context.getBeanDefinitionNames().length);
```



##### 通过流遍历该对象内的数据(展示详细信息)：

```java
Arrays.stream(config.getBeanDefinitionNames()).forEach(System.out::println);
```



##### 下图展示部分信息：

![image-20230225211549165](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230225211549165.png)







### @SpringBootApplication及其包含的三个注解

> 注解声明的类为SpringBoot启动类，自动去加载配置文件(application.properties)，启动SpringBoot服务器
>

#### @Configuration

> 这个注解等同于SpringBootConfiguration，相当于别名

Spring自动扫描到添加了@Configuration的类，会读取其中的配置信息，而@SpringBootConfiguration是来声明当前类是SpringBoot应用的主配置类。

SpringBootConfiguration注解的配置类在项目中只能有一个，只有一个类使用该注解，就是SpringBoot启动类。

这个注解的作用就是声明当前类是一个配置类，以往写在ApplicationContext.xml、springmvc-config.xml的配置文件在SpringBoot中变成Java类的形式，使用该注解声明该类是一个配置类。

##### 例如拦截器：

![image-20230227220941976](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202302272209244.png)





#### @EnableAutoConfiguration

开启自动配置，告诉SpringBoot基于所添加的依赖(Maven中的场景器)，去“猜测”你想要如何配置Spring。

比如我们引入了spring-boot-starter-web，而这个场景器中帮我们添加了Tomcat、SpringMVC的依赖，此时自动配置就知道你是要开发一个web应用，所以就帮你完成了web及SpringMVC的默认配置了，我们使用SpringBoot构建一个项目，只需要引入所需框架的场景器，配置该场景需要引入什么Jar包就可以交给SpringBoot处理了。





#### @ComponentScan

配置组件扫描的指令，提供了类似与原xml配置文件中context:component-scan标签的作用







### @Bean：手动注册实体到容器中

#### 实例

##### Student类：

```java
class Student {
    
    private int age;
    private String name;

    @Override
    public String toString() {
        return "Student{" +
                "age=" + age +
                ", name='" + name + '\'' +
                '}';
    }
}

@Log4j2 // 添加日志支持
@MapperScan("com.blackhker.mapper")
@SpringBootApplication
// SpringBoot启动类
public class QqmastersApplication {
    ...
}
```



##### 在启动类中使用@Bean注解注册实体：

```java
class Student {
    
    private int age;
    private String name;

    @Override
    public String toString() {
        return "Student{" +
                "age=" + age +
                ", name='" + name + '\'' +
                '}';
    }
}

@Log4j2 // 添加日志支持
@MapperScan("com.blackhker.mapper")
@SpringBootApplication
// SpringBoot启动类
public class QqmastersApplication {
    
    @Bean	// 手动注册
    public Student getStudent() {
        return new Student();
    }
    
    // main方法
    public static void main(String[] args) {
        ConfigurableApplicationContext config = 	
        SpringApplication.run(QqmastersApplication.class, args);
    }
}
```



##### 获取注册的对象(实体)：

```java
// ConfigurableApplicationContext类对象.getBean("注册的方法名",实体类名.class)
ConfigurableApplicationContext config = SpringApplication.run(启动类.class, args);
Student student = config.getBean("getStudent", Student.class);
System.out.println(student);	// Student{age=0, name='null'}
```







### @Component：自动注册实体到容器中

> 该注解是三层架构注解：@Controller`、`@Service`、`@Repository的父注解

##### 写在要注册的类上，标识该类是一个组件，交给Spring容器进行管理(将Java类标记为 bean)

```java
@Component
class Student {
    private int age;
    private String name;

    @Override
    public String toString() {
        return "Student{" +
                "age=" + age +
                ", name='" + name + '\'' +
                '}';
    }
}
```







### SpringBoot配置欢迎页(原web.xml下的welcome-file-list)

> 声明配置类,实现WebMvcConfigurer接口，重写方法addViewControllers

#### 配置类：

```java
@Configuration
public class WebMvcConfig implements WebMvcConfigurer {
    @Override
    public void addViewControllers(ViewControllerRegistry registry) {
        // 添加默认路径"/"所对应的视图， 重定向方式跳转到login.html 
        registry.addViewController("/").setViewName("redirect:login.html");
    }
}
```

##### 原配置欢迎页在web.xml下

```xml
<welcome-file-list>
    <welcome-file>login.jsp</welcome-file>
</welcome-file-list>
```







### SpringBoot拦截器

#### 拦截器类：

> 实现HandlerInterceptor接口，重写方法preHandle和postHandle，返回布尔，true放行，false不放行

```java
public class 类名 implements HandlerInterceptor {
    // 拦截请求，在Controller请求之前执行
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, 	Object handler) throws Exception {
        System.out.println("拦截器执行preHandle");
        return true;
    }
    // 拦截请求，在Controller请求之后执行
    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        System.out.println("拦截器执行postHandle");
       	return true;
    }
}
```





#### 配置类：

> 声明配置类，实现WebMvcConfigurer接口，重写方法addInterceptors，注册编写的拦截器

```java
@Configuration
public class 类名 implements WebMvcConfigurer {
    @Override
    public void addInterceptors(InterceptorRegistry 注册对象) {
        // 创建一个拦截器类的对象
        拦截器类类名 对象名 = new 拦截器类类名();
        // 1.addInterceptor()注册拦截器
        // 2.addPathPatterns()设置拦截哪些请求,/**表示拦截所有请求
        // 3.excludePathPatterns()设置放行(排除)哪些请求
        注册对象.addInterceptor(拦截器对象)
               .addPathPatterns(拦截哪些请求)
               .excludePathPatterns(排除请求地址);
    }
}
```





#### 实例

##### 拦截器类：

```java
package com.blackhker.interceptor;

import org.springframework.web.servlet.HandlerInterceptor;
import org.springframework.web.servlet.ModelAndView;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 * 用户认证鉴权的拦截器
 */
public class LoginInterceptor implements HandlerInterceptor {

    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        System.out.println("拦截器执行preHandle");
        System.out.println("去哪里" + request.getRequestURI());
        // 获取当前登录用户
        Object qqUser = request.getSession().getAttribute("qqUser");
        if (qqUser == null) {
            // 用户为空，未登录，重定向到登录页面
            response.sendRedirect("/login.html");
            return false;
        }
        // true放行，false不放行
        return true;
    }

    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        System.out.println("拦截器执行postHandle");
    }
}
```



##### 配置类：

```java
@Configuration
public class LoginInterceptorConfig implements WebMvcConfigurer {

    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        LoginInterceptor loginInterceptor = new LoginInterceptor();
        registry.addInterceptor(loginInterceptor)
                .addPathPatterns("/**")
                .excludePathPatterns("/login", "/login.html", "/element-ui/**", "/static/**", "/css/**", "/js/**", "/images/**");
    }
}
```







### SpringBoot监听器

> 创建监听器类，声明配置类，实现CommandLineRunner接口，重写run方法

```java
@Configuration
public class ApplicationLisener implements CommandLineRunner {
    @Override
    public void run(String... args) throws Exception {
        // 执行的操作
    }
}
```

#### 实例：

```java
package com.blackhker.listener;

import com.blackhker.service.IQQUserService;
import lombok.extern.log4j.Log4j2;
import org.springframework.boot.CommandLineRunner;
import org.springframework.context.annotation.Configuration;

import java.util.concurrent.Executors;

/**
 * 监听SpringBoot启动，监听器
 */
@Configuration
@Log4j2
public class ApplicationLisener implements CommandLineRunner {
    @Override
    public void run(String... args) throws Exception {
        System.out.println("监听到SpringBoot容器启动");
        // 线程池对象给IQQUserService中的线程池赋值
        IQQUserService.service = Executors.newCachedThreadPool();
        log.debug("线程池加载成功！");
    }
}
```







### SpringBoot过滤器

> 创建过滤器类，实现Filter接口(javax.servlet)，实现doFilter方法

```java
package com.blackhker.mall96.filter;

import org.springframework.stereotype.Component;

import javax.servlet.*;
import java.io.IOException;

@Component
public class FilterTest implements Filter {
    
    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        // 注意方法的参数是Servletxxx不是HttpServletxxx，使用时需要强转
        // 放行
        chain.doFilter(request, response);
    }
}
```





---





### CORS跨域问题(前后端分离)

> 浏览器拒绝非同源数据(同源策略)

#### 方案一：SpringBoot注解实现

> 只能实现被注解的接口跨域，没注解的无法跨域

##### Controller层在需要跨域的类或者方法上添加注解：@CrossOrigin

```java
// 允许跨域访问当前Controller的所有接口
@CrossOrigin
public class XxxController {
	...接口
}
```





#### 方案二：配置类

##### 编写跨域配置类，实现WebMvcConfigurer接口

```java
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.CorsRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

/**
 * 跨域配置类
 */
@Configuration
public class CrossOriginConfiguration implements WebMvcConfigurer {

    static final String ORIGINS[] = new String[]{"GET", "POST", "PUT", "DELETE"};

    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
                .allowedOrigins("*")
                .allowCredentials(true)
                .allowedMethods(ORIGINS)
                .maxAge(3600);
    }
}
```





#### 方案三：自定义过滤器

```java
import org.springframework.stereotype.Component;

import javax.servlet.*;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * 跨域过滤器
 */
@Component
public class CrossOriginFilter implements Filter {

    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
        HttpServletResponse res = (HttpServletResponse) response;
        // 添加响应头，允许跨域请求携带凭证（如Cookie）
        res.addHeader("Access-Control-Allow-Credentials", "true");
        // 添加响应头，允许所有来源的跨域请求
        res.addHeader("Access-Control-Allow-Origin", "*");
        // 添加响应头，允许的请求类型
        res.addHeader("Access-Control-Allow-Methods", "GET, POST, DELETE, PUT");
        // 添加响应头，允许的请求头参数，包括authorization等，用于Token验证
        res.addHeader("Access-Control-Allow-Headers", "Content-Type,X-CAF-Authorization-Token,sessionToken,X-TOKEN,authorization");

        // 判断请求类型是否为OPTIONS，如果是则直接返回响应"ok"，用于预检请求
        if (((HttpServletRequest) request).getMethod().equals("OPTIONS")) {
            response.getWriter().println("ok");
            return;
        }

        // 继续执行后续的过滤器链或Servlet处理
        chain.doFilter(request, response);
    }
}
```





#### 总结

##### Session和Cookie

> Cookie里建议不放重要信息，有可能伪造

###### 前后端不分离

客户端浏览器向服务器发送一个请求，服务器会生成一个Session，Session是保存在服务器的，在响应给客户端浏览器数据的时候，服务器会将SessionID作为一个名为"JSESSIONID"的Cookie发送给客户端浏览器，浏览器会将Cookie保存到本地，每次请求的时候，携带着这个Cookie(SessionID)，服务器收到一个包含SessionID的HTTP请求时，会去查找与该SessionID相对应的用户会话，并将请求路由到正确的会话。通过Cookie存储SessionID，服务器可以在不同的HTTP请求之间跟踪用户的会话状态。

###### 前后端分离

> 可以在前端设置一下，强行让浏览器携带Cookie，但是可能会收到伪造Cookie的攻击

不同源(跨域)的情况下，浏览器不会自动携带Cookie发送下一个请求，所以服务器会认为这是第一次请求，重新生成一个Session。所以后端不能用Session做登录鉴权，因为每次请求都是一个新的Session





---





## JWT(JSON Web Token)

> 两个工具类：JWTUtil、TokenEnum参阅工具类笔记

### 介绍

#### 结构

> JWT由三部分组成：头部(header)、载荷(payload)、签名(signature)
>

<font color="red">eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9</font>.<font color="green">eyJ1aWQiOjEwMDEsImlzcyI6Imlzc3VlciIsImV4cCI6MTY5MjQzMjE1OSwiaWF0IjoxNjkwOTYwOTMwfQ</font>.<font color="blue">ffL72VG-OqLxvDEXkG84cNt5TQYx77hY6hauHBrY1LQ</font>

##### Header

header包含两部分信息：声明类型、声明加密的算法，通常直接使用HMAC、SHA256或RSA

###### 完整的头部示例：

> 将头部加密就构成了第一部分：eyJOeXAiOjKV1QiLcIhbGciojlU2l1Ni)9

```json
{
  "typ": "JWT",
  "alg": "HS256"
}
```



##### Payload

payload也称为JWT Claims，包含用户的一些非隐私数据(如用户id)

###### 完整的payload示例:

> 将payload进行base64加密，得到JWT的payload：eyJVc2vySWQiojEyMywiVXNIck5hbwuioijhZG1pbij9

```json
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
```



##### Signature

signature是一个签证信息，这个签证信息是由三部分组成：header、payload(base64之后)、secred

这个部分需要base64编码(序列化)之后的header和payload使用.连接组成的字符串，然后通过header中声明的加密方式进行secred组合加密构成JWT的第三部分，三部分用.作为连接符，构成了最终的JWT





#### 用途

解决前后端分离，HttpSession失效的问题，前后端分离的情况下，因为浏览器在不同源(前后端分离)发送请求时，不会自动携带保存上一次请求SessionID的Cookie，所以每次请求都会产生一个新的Session，造成了上一次请求保存到Session中的用户信息等权限验证内容在过滤器验证的时候获取不到，就有了JWT







### 使用

#### 登录流程

##### 后端将token保存到请求头

```java
/**
 * 登录接口
 *
 * @param user
 * @param response
 * @return
 */
@PostMapping("/login")
public ResponseResult<Boolean> login(@RequestBody User user, HttpServletResponse response) {

    // 根据账户查询用户信息
    User findUser = userService.findByAccount(user.getAccount());

    // 判断账户查询的对象不为空，且查询出的用户信息密码跟前端的密码对应上
    if (findUser != null && findUser.getPassword().equals(user.getPassword())) {
        // 登录成功，根据uid生成Token
        String token = JWTUtil.generateToken(findUser.getId());

        // 将Token放到响应头
        response.setHeader("authorization", token);

        // 暴漏响应头，暴漏给浏览器(告诉前端头没问题)
        response.setHeader("Access-Control-Expose-Headers", "authorization");

        // 响应
        return new ResponseResult<Boolean>()
                .setCode(200)
                .setState(ResponseState.LOGIN_SUCCESS)
                .setMessage("登录成功！")
                .setData(true);
    } else {
        // 账户不存在|密码错误
        return new ResponseResult<Boolean>()
                .setCode(500)
                .setState(ResponseState.LOGIN_FAIL)
                .setMessage("用户名或密码错误！")
                .setData(false);
    }
}
```

###### 暴漏响应头的解释

在跨域请求中，浏览器会发送OPTIONS请求进行预检，以确保实际请求是安全的。在OPTIONS请求中，浏览器会检查响应头中的Access-Control-Expose-Headers字段，以确定允许暴露的响应头。

如果你想在实际请求的响应头中暴露自定义的头部信息，例如authorization token，你需要在服务端的响应头中加入Access-Control-Expose-Headers字段指定允许暴露的头部信息。这样，浏览器就能够在实际请求的响应头中获取到该信息。

因此，当你在服务端添加Token到请求头时，需要在响应头中添加Access-Control-Expose-Headers字段，以确保浏览器能够获取到该信息。具体来说，设置Access-Control-Expose-Headers字段的值为"authorization"，表示允许暴露authorization头部信息。这样，浏览器就可以在实际请求的响应头中获取到该信息，从而完成跨域请求的授权验证。





##### 前端获取请求头中的Token

```js
// 登录方法
login: function () {
  this.$axios.post("/user/login", this.user).then(res => {
    // token保存在请求头中的"authorization"头中
    console.log(res);
    let token = res.headers.authorization;
    // 保存到LocalStorage||SessionStorage
    // 保存Token到本地，方便其他页面携带Token发送请求
    window.sessionStorage.setItem("token",token)
  })
}
```



##### 前端携带Token发送请求

> 携带头向后端发请求，必须配置后端，让后端知道这个头是可以接的

```js
this.$axios.post("/cart/add", cart,{
    // 保存Token到请求头，再发送请求
	headers:{
  		"authorization":window.sessionStorage.getItem("token")
	}
}).then(res => {
	console.log(res.data);
})
```

###### 配置authorization头后端可以正常识别

```java
import org.springframework.stereotype.Component;

import javax.servlet.*;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * 跨域过滤器
 */
@Component
public class CrossOriginFilter implements Filter {

    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
        HttpServletResponse res = (HttpServletResponse) response;
        // 添加响应头，允许跨域请求携带凭证（如Cookie）
        res.addHeader("Access-Control-Allow-Credentials", "true");
        // 添加响应头，允许所有来源的跨域请求
        res.addHeader("Access-Control-Allow-Origin", "*");
        // 添加响应头，允许的请求类型
        res.addHeader("Access-Control-Allow-Methods", "GET, POST, DELETE, PUT");
        // 添加响应头，允许的请求头参数，包括authorization等，用于Token验证
        res.addHeader("Access-Control-Allow-Headers", "Content-Type,X-CAF-Authorization-Token,sessionToken,X-TOKEN,authorization");

        // 判断请求类型是否为OPTIONS，如果是则直接返回响应"ok"，用于预检请求
        if (((HttpServletRequest) request).getMethod().equals("OPTIONS")) {
            response.getWriter().println("ok");
            return;
        }

        // 继续执行后续的过滤器链或Servlet处理
        chain.doFilter(request, response);
    }
}
```









---





## MyBatisPlus

### 使用

#### 引入场景器：

MybatisPlus、Druid连接池(参考Maven文档)





#### 配置数据源：

> SpringBoot默认自动化配置数据源，如果没有配置数据源直接启动，会报错

```java
// 启动SpringBoot启动类报错
@SpringBootApplication
public class QqmastersApplication {
    // main方法
    public static void main(String[] args) {
        SpringApplication.run(QqmastersApplication.class, args);
    }
}
```

##### 配置application.properties

```properties
# 配置数据源为阿里巴巴的德鲁伊，这是一款史上最强的连接池
spring.datasource.type=com.alibaba.druid.pool.DruidDataSource
# 线程池初始大小50个连接
spring.datasource.initialSize=50
# 线程池最小50个连接
spring.datasource.minIdle=50
# 线程池最多100个连接
spring.datasource.maxActive=100
# 配置获取连接等待超时的时间，60秒
spring.datasource.maxWait=60000
# 配置间隔多久才进行一次检测，检测需要关闭的空闲连接，60秒检测一次
spring.datasource.timeBetweenEvictionRunsMillis=60000
# 配置驱动类
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
# 配置数据库账号
spring.datasource.username=账号
# 配置数据库密码
spring.datasource.password=密码
# 配置数据库连接URL
spring.datasource.url=jdbc:mysql://localhost:3306/数据库名?characterEncoding=utf-8&useSSL=true
# 配置打印到控制台的日志组件
mybatis-plus.configuration.log-impl=org.apache.ibatis.logging.stdout.StdOutImpl
# 自动开启驼峰命名法映射 user_name - > userName
mybatis-plus.configuration.map-underscore-to-camel-case=true
```





```
@TableName("users")
@TableId("user_id")
@TableField("user_id")
@TableLogic 逻辑删除字段
```





### MyBatisPlus代码生成器

> 基于MyBatisPlus，必须先有MyBatisPlus

#### 引入依赖：

```xml
<!--mybatisPlus代码生成器-->
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





#### 编写配置类：

```java
package com.blackhker.config;

import com.baomidou.mybatisplus.core.exceptions.MybatisPlusException;
import com.baomidou.mybatisplus.core.toolkit.StringUtils;
import com.baomidou.mybatisplus.generator.AutoGenerator;
import com.baomidou.mybatisplus.generator.config.*;
import com.baomidou.mybatisplus.generator.config.rules.NamingStrategy;
import com.baomidou.mybatisplus.generator.engine.FreemarkerTemplateEngine;

import java.util.Scanner;

/**
 * 自动生成mybatisplus的相关代码
 */
public class GeneratorCodeConfig {

    public static String scanner(String tip) {
        Scanner scanner = new Scanner(System.in);
        StringBuilder help = new StringBuilder();
        help.append("请输入" + tip + "：");
        System.out.println(help.toString());
        if (scanner.hasNext()) {
            String ipt = scanner.next();
            if (ipt != null) {
                return ipt;
            }
        }
        throw new MybatisPlusException("请输入正确的" + tip + "！");
    }

    public static void main(String[] args) {
        // 创建全局配置对象
        GlobalConfig gc = new GlobalConfig();
        // 创建代码生成器对象
        AutoGenerator mpg = new AutoGenerator();
        
        /**配置全局配置对象*/
        // 配置输出路径，指定生成代码文件的位置(Java蓝色文件夹)
        gc.setOutputDir("路径");
        // 开发人员姓名(作者信息)
        gc.setAuthor("作者名");
        // 是否打开输出目录
        gc.setOpen(false);
        // 是否配置实体属性的Swagger2注解
        gc.setSwagger2(true);
        // 将全局配置对象给到代码生成器
        mpg.setGlobalConfig(gc);
        
        /**配置数据源对象*/
        // 创建数据源对象
        DataSourceConfig dsc = new DataSourceConfig();
        // 配置数据源
        dsc.setUrl("jdbc:mysql://localhost:3306/数据库名?serverTimezone=UTC");
        dsc.setDriverName("com.mysql.cj.jdbc.Driver");
        dsc.setUsername("账号");
        dsc.setPassword("密码");
        // 将数据源对象给到代码生成器
        mpg.setDataSource(dsc);

        /**配置自己开发环境的包配置*/
        // 创建包配置对象
        PackageConfig pc = new PackageConfig();
        // 设置包名
        pc.setParent("com.blackhker");
        pc.setEntity("entity");
        pc.setMapper("mapper");
        pc.setService("service");
        pc.setServiceImpl("service.impl");
        // 将包配置对象给到代码生成器
        mpg.setPackageInfo(pc);

        // 配置模板
        TemplateConfig templateConfig = new TemplateConfig();
        templateConfig.setXml(null);
        mpg.setTemplate(templateConfig);

        /**策略配置*/
        StrategyConfig strategy = new StrategyConfig();
        // 数据库下划线自动转换，驼峰命名法(表名转实体类名、列名转属性名)
        strategy.setNaming(NamingStrategy.underline_to_camel);
        strategy.setColumnNaming(NamingStrategy.underline_to_camel);
		// 配置提示语句
        strategy.setInclude(scanner("表名，多个英文逗号分割").split(","));
        strategy.setControllerMappingHyphenStyle(true);
        mpg.setStrategy(strategy);
        mpg.setTemplateEngine(new FreemarkerTemplateEngine());
        mpg.execute();
    }
}
```





#### 注意事项：

> ##### ※使用代码生成器时，先备份项目！如果配置的包路径(com.xxx)不对，会将该项目清空重写！

##### 配置全局配置对象的路径时，路径的复制方式：

###### 右键蓝色Java文件夹，选中CopyPath/Reference

![image-20230227233453537](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230227233453537.png)

###### 选中Absolute Path，生成绝对路径

![image-20230227233554049](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230227233554049.png)





##### 配置全局配置对象时，使用Swagger2注解要导包(Swagger2)：

> 请求地址为:http://localhost:8080/doc.html，进入Swagger页面

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





---





## Swagger2：自动生成接口(API)文档







---





## Vue Application(Vue.js)

### 通过脚手架生成Vue项目

#### 项目结构

##### 根目录目录结构：

![image-20230301203309607](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012035447.png)



##### src源代码目录结构：

![image-20230301203407912](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303012036503.png)





#### 启动项目

```shell
npm run dev
```

##### 报错可以输入：

```shell
npm run install
```







### 语法：取值、遍历、筛选

#### v-for

##### 遍历商品列表

```vue
<div v-for="(goods, index) in goodsList" :key="index">
  <!-- 从后端获取图片，先在配置文件中配置后端的静态资源获取路径 -->
  <img :src="'http://localhost:8080/' + goods.image" alt="该商品未添加图片">
  <p>{{ goods.price }}</p>
  <p>{{ goods.name }}</p>
</div>
```







### Components：组件

> 将界面的一部分抽成组件形式，就可以复用组件来减少代码量

#### App.vue：根组件

是整个Vue应用程序的根组件，因此不能删除。如果删除它，整个应用程序将无法正常运行。

在Vue.js中，组件是应用程序的基本构建块，用于将用户界面拆分成可重用的部分。通常情况下，我们将组件放在一个components文件夹中，并在需要使用它们的地方引入。

但是，App.vue作为根组件，它不属于components文件夹中的任何一个组件。它是一个独立的文件，并且在Vue应用程序启动时会自动加载和渲染。

因此，App.vue文件通常位于Vue应用程序的根目录中，作为整个应用程序的入口点。





#### 编写组件

##### 统一格式：xxx.vue

```vue
<template>
	<div>
        <!--组件代码-->
    </div>
</template>
<script>
	// export:公开当前组件中的属性、方法 
    // default:默认，可以更换别的名字，例如export aaa，别的地方就可以导入，但是手动命名可能会冲突
	export default {
        // script代码
    }
</script>
<style scoped>
    /*
    	一般情况下用来编写当前组件的CSS
    	样式，scope属性使当前组件的样式不会和其它组件冲突,类似作用域，限制只在当前页面生效
    */
</style>
```





#### 使用(引入)组件

##### main. Vue

```vue
<template>
	<div>
        <!-- 3.使用组件：自定义组件名作为标签名 -->
        <Header></Head>
        <Top></Top>
        // 主页面代码
        <Footer></Footer>
    </div>
</template>
<script>
// 1.引入组件页面
import 自定义组件名 from '组件路径/vue文件(组件).vue'
import Top from '../Top.vue'
import Header from '../common/header.vue'
import Footer from '../common/footer.vue'
export default {
	// 2.注册组件
    components: {
        自定义组件名，Top, Header, Footer
    },
}
</script>
<style scoped>
	/* 样式 */
</style>
```







### data()：在Vue中保存的数据

> 保存Vue页面中使用的插值表达式、单向绑定、双向绑定等使用的数据

#### 保存数字、字符串、对象(JSON)、数组

```vue
<template>
  <div>
    <!-- 插值表达式 -->
    <span>{{ id }}</span>
    <span>{{ name }}</span>
    <hr>
    <span>{{ student.id }}</span>
    <span>{{ student.name }}</span>
    <hr>
    <span v-for="student in students" :key="student">{{ student }}</span>
    <hr>
    <button @click="test1(1, '刘备')">test1</button>
    <button @click="test2(2, &quot;关羽&quot;)">test2</button>
  </div>
</template>

<script>
export default {
  // 将data写成一个函数(方法)，在return中编写参数
  data() {
    // data必须返回一个对象：return
    return {
      // 数字
      num: 0,
      // 字符串
      str:"",
      // 对象: {属性1:属性值,属性2:属性值}
      student: {
        name:"刘备",
        age: 12
      },
      // 数组
      students: [
        { id: 1, name: "刘备" },
        { id: 2, name: "关羽" },
        { id: 3, name: "张飞" }
      ]
    }
  }
}
</script>
```

> 如果我们的data不是一个函数，函数不返回一个对象
> 不同复用处的组件的数据，都会随着一处的更改而全部都改，就没有独立性。
>
> 如果组件data使用函数，返回一个对象，对象中装数据。这样的话，每次复用引入该组件时，该组件的数据在都会独立开辟一个空间存储自己的数据，组件间相同数据，互不影响







### methods：函数(事件---@xxx)

> 页面元素添加@click、@change等属性，用于触发methods事件

#### 按钮触发事件

```vue
<button @click="事件名(参数)"></button>
<script>
export default {
	// 注册组件
    components: {
        自定义组件名
    },
    methods: {
        事件名: function (参数) {
            // 事件(方法)实现
        }
    }
}
</script>
```

##### 实例

```html
<template>
  <div>
    <button @click="hello()"></button>
  </div>
</template>

<script>
export default {
  methods: {
    hello: function () {
      alert("success!")
    }
  }
}
</script>

<style scoped></style>
```







### Vue生命周期函数(钩子函数)

```js
mounted : function () {
	// 页面加载前执行，可以反复执行多次
}
created : function () {
    // 页面创建时执行，只执行一次
}
```

#### 钩子函数表

| 函数          | 解释                                                        |
| ------------- | ----------------------------------------------------------- |
| beforeCreate  | 组件实例刚被创建，组件属性计算之前，如data属性等            |
| created       | 组件实例创建完成，属性已绑定，但DOM还未生成,$el属性还不存在 |
| beforeMount   | 模板编译/挂载之前                                           |
| mounted       | 模板编译/挂载之后(不保证组件已在document中)                 |
| beforeUpdate  | 组件更新之前                                                |
| updated       | 组件更新之后                                                |
| activated     | for keep-alive ，组件被激活时调用                           |
| deactivated   | for keep-alive，组件被移除时调用                            |
| beforeDestory | 组件销毁前调用                                              |
| destoryed     | 组件销毁后调用                                              |







### Router：路由

> 解决前后端分离后，Vue前端页面之间的跳转

#### 路由位置

```
/Vue根目录/router/index.js
```

![image-20230712135911018](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230712135911018.png)





#### 路由模式

> Vue.js提供了两种路由模式：hash模式和history模式

##### hash模式：

在hash模式中，URL中会带有`#`符号，例如http://example.com/#/home。#后面的内容称为hash值，由浏览器负责处理，不会发送到服务器。



##### history模式：

在history模式中，URL中不会带有#符号，例如http://example.com/home。这种模式需要服务器正确配置，以便在访问不存在的路由时，返回正确的页面。



##### 更改路由模式：

```js
export default new Router({
  routes: [
    {
      path: '/',
      name: 'Index',
      component: Index
    }
      // 更改为history模式，没有#号
  ], mode: 'history'
})
```





#### 编写路由

##### 一级路由：

> 通过路由跳转页面

```js
{
    path："请求路径",
 	name：自定义路由名,
    component: 自定义组件名
}
```

###### 实例：

```js
// 导入组件页面到路由，供路由操作实现跳转
// import 自定义组件名 from '@/components/组件路径'
import Vue from 'vue'
import Router from 'vue-router'
import Index from '@/components/index'
Vue.use(Router)

export default new Router({
  // 可以配置多个路由
  routes: [
    {
      // 映射地址，对应前端的内容
      path: '/',
      // 路由名称，可以通过名称跳转解决path地址比较长的问题(可有可无)
      name: 'Index',
      // 组件名称
      component: Index
    }
    // 表示路由模式(方式)，history地址不带#号
  ], mode: 'history'
})
```



##### 二级路由(children)：

> /一级路由/二级路由，就可以实现iframe的父子页面嵌套效果(点击左边菜单栏右面区域页面发生改变)

```js
{
	path："请求路径",
	name：自定义路由名,
	component: 自定义组件名
  	children: 属性配置子路由，可以有多个
  children: [
    // 商品管理页面
    {
      // 二级路由的path不能加斜杠"/"
      path: "goodsManage",
      component: GoodsManage
    },
    // 评论管理页面
    {
      path: "comment",
      component: Comment
    }
  ]
}
```

###### 实例：

```js
// 导入组件页面到路由，供路由操作实现跳转
// import 自定义组件名 from '@/components/组件路径'
import Vue from 'vue'
import Router from 'vue-router'
Vue.use(Router)

export default new Router({
  routes: [
    {
      // 后台管理页面
      path: "/manage",
      name: "Manage",
      component: Manage,
      // children属性配置子路由，可以有多个
      children: [
        // 商品管理页面
        {
          // 二级路由的path不能加斜杠"/"
          path: "goodsManage",
          component: GoodsManage
        },
        // 评论管理页面
        {
          path: "comment",
          component: Comment
        }
      ]
    }
  ]
})
```



##### 动态路由：带参数的路由

> /:参数名(匹配参数)

```js
{
  path: '/路由地址/:参数名',
  name: 'Xxx',
  component: Xxx
}
```

###### 实例：商品列表，根据商品分类id获取商品列表

```vue
<img class="transform" src="../assets/images/computer.png" @click="goodsList(541)" />
<script>
export default {
  methods: {
    // 点击调用该方法，跳转到goodsList，携带参数categoryId
    goodsList: function (categoryId) {
      this.$router.push("/goodsList/" + categoryId)
    }
  }
}
</script>
```

```js
// 路由
{
  path: '/goodsList/:categoryId',
  name: 'goodsList',
  component: GoodsList
}
```

```vue
<template>
  <div>
    <!-- 获取动态路由参数 -->
    <h2>{{ categoryId }}</h2>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // 获取动态路由中的参数(获取路由(this.$route)中所有参数(params)中的参数(categoryId))
      categoryId: this.$route.params.categoryId
    }
  }
}
</script>
<style scoped></style>
```





#### 路由跳转

> 需要先配置路由

```js
this.$router.push("/detail")
```

##### 点击跳转

```vue
<template>
<!-- 点击图片调用detail()方法 -->
<img src="../assets/images/huawei.png" @click="detail()" />
</template>

<script>
   export default {
       data(){},
       methods:{
           detail: function () {
               // 跳转页面
               this.$router.push("/detail")
           }
       }
   }
</script>
```



##### router-link

```vue
<router-link to="/path" tag="button">Link Text</router-link>
```







### 动态配置

#### 属性

##### 给Vue对象动态添加一个属性\方法(main.js)

```js
Vue.prototype.$eat = function () {
  // 有$符号，可以认为他是属性
}
Vue.prototype.eat = function () {
  // 没有$符号，可以认为他是方法
}
```









### Axios

#### 安装(为当前项目安装)

##### 关闭项目后，控制台安装axios

```shell
npm install --save axios
```





#### 配置Axios

##### main.js：

> 相当于给Vue这个对象添加一个属性，这个属性就是$axios，属性来自于导入下载的插件(import axios)

```js
// 导入axios插件
import axios from 'axios'

// 动态配置属性：将axios设置为vue的元属性(到处都可以用axios发请求)
Vue.prototype.$axios = axios
```

![image-20230712200822047](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230712200822047.png)



##### 检测Axios是否成功

```js
// 钩子函数
mounted: function () {
    console.log("mounted方法在组件被挂载时执行");
    this.$axios.get("http://www.baidu.com").then(res => {
      // 接口成功执行后执行的方法
      console.log("Success！");
    })
}
```





#### 请求示例

##### GET

```js
this.$axios.get("/goods/findById/" + this.gid).then(res => {
  this.goods = res.data.data
})
```



##### POST

> 以下示例，后端使用对象接收时需要加@RequestBody，否则后端的对象参数为空

###### 传递对象

```js
addCart: function () {
// 定义购物车实体
  let cart = {
    id: this.goods.id,
    num: this.num,
    price: this.goods.price
  }

  // 发送请求，添加到购物车
  this.$axios.post("/cart/add",cart).then(res => {
	console.log(res.data.data)
  })
}
```

###### 传递多参

```js
addCart: function () {
  // 发送请求，添加到购物车
  this.$axios.post("/cart/add", {
    gid: this.goods.id,
    num: this.num,
    price: this.goods.price
  }).then(res => {
    console.log(res.data);
  })
}
```





#### 设置Axios请求全局前缀

> main.js中配置，配置后图片地址就不需要配置了，默认携带这部分

```js
// 设置axios请求全局前缀，注意这里的8080后面没有/，如果配置了‘/’，则请求前面就不需要写了
axios.defaults.baseURL = "http://localhost:8080"
```

##### 修改前：

```js
mounted: function () {
    this.$axios.get("http://localhost:8080/goods/findByCategoryId/" + this.categoryId).then(res => {
      // 接口成功执行后执行的方法
      this.goodsList = res.data.data
    })
}
```



##### 修改后：

```js
mounted: function () {
    // 前面不需要拼全路径了
    this.$axios.get("/goods/findByCategoryId/" + this.categoryId).then(res => {
      // 接口成功执行后执行的方法
      this.goodsList = res.data.data
    })
}
```





#### Axios拦截器

##### 请求拦截器

> main.js配置Axios

```js
// 设置Axios的请求拦截器：在每个Axios的请求发送之前，对请求做处理
// 将本地(sessionStorage)的token放到每一个Axios请求的请求头中
// 1.创建一个Axios对象
let sentder = axios.create({});

// 2.给对象添加请求拦截器并配置
sentder.interceptors.request.use(config => {
  // 从本地获取Token
  let token = window.sessionStorage.getItem("token")

  // 判断token是否存在
  if (token) {
    // 有则放入请求头
    config.headers.authorization = token;
  }

  // 放行
  return config;
})

// 将配置好的sentder设置为Vue的元属性
Vue.prototype.$axios = sentder;
```



##### 响应拦截器

> 验证登录状态

```js
// 设置响应拦截器：会在每次请求返回到浏览器，但是还没有执行到then回调函数时执行
// 此处用于判断每一个响应中是否有token，如果有则得到token并放到本地
sentder.interceptors.response.use(response => {

  // 判断返回结果
  if (response.data.state == "NO_LOGIN") {
    // 没登录,跳转到登录页
    // 不能使用this,这里的this不是Vue对象，无法跳转
    // this.$router.push("/login");
    window.location.href = "/login"
    return response;
  }

  // 从响应头中获取token
  let token = response.headers.authorization;

  // 判断token是否存在
  if (token) {
    // 有token,放到本地
    window.sessionStorage.setItem("token", token)
  }

  // 放行
  return response;
})

// 将配置好的sentder设置为Vue的元属性
Vue.prototype.$axios = sentder;
```







### Local/SessionStorage

> 浏览器提供的两个给用户存储东西的地方

#### SessionStorage

只在会话期间有效，浏览器关闭就消失

##### 使用场景

1. 在多个页面之间共享临时数据，如表单数据。
2. 记录用户操作的状态，以便在页面刷新时恢复数据。
3. 保存用户购物车信息，在结账前保持选购的商品。



##### 使用

###### 新增

```js
// 存数据
window.sessionStorage.setItem("token",token)
```

###### 查询

```js
// 取数据
window.sessionStorage.getItem("token")

// 获取sessionStorage中索引为0的键名
var key = window.sessionStorage.key(0)

// 获取sessionStorage中的数据项数量
var count = window.sessionStorage.length
```

###### 删除

```js
// 删除数据
window.sessionStorage.removeItem("token")

// 清除所有sessionStorage数据
window.sessionStorage.clear()
```





#### LocalStorage

只要不主动删除、卸载浏览器，数据就会一直存在

##### 使用场景

1. 保存用户偏好设置，如主题、语言等。
2. 持久保存用户登录凭证，以实现“记住我”功能。
3. 缓存静态资源，以减少服务器请求

##### 使用

###### 新增

```js
// 存数据
window.localStorage.setItem("token",token)
```

###### 查询

```js
// 取数据
window.localStorage.getItem("token")

// 获取localStorage中索引为0的键名
var key = window.localStorage.key(0)

// 获取localStorage中的数据项数量
var count = window.localStorage.length
```

###### 删除

```js
// 删除数据
window.localStorage.removeItem("token")

// 清除所有localStorage数据
window.localStorage.clear()
```













### Element UI

#### 安装

> 提示 added 6 packages in 5s

```shell
npm i element-ui -S
```





#### 导入

> 在main.js引入Element UI，可以参考官网的快速上手模块

```js
// 导入ElementUI
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
Vue.use(ElementUI);
```





#### 布局

##### 结构

```vue
<!-- 每行默认24等分，手动分配 -->
<el-row>
  <!-- 每行展示4条数据，span就是6(24/4=6) -->
  <el-col :span="6" v-for="(goods, index) in goodsList" :key="index">
    <img :src="'http://localhost:8080/' + goods.image" alt="该商品未添加图片">
    <p>{{ goods.price }}</p>
    <p>{{ goods.name }}</p>
  </el-col>
</el-row>
```







##### 布局空白

> 可能是文字超出长度，占了位置

![image-20230715113311648](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230715113311648.png)

###### 给文字添加CSS：

```css
<p class="title">{{ goods.name }}</p>
.title {
  display: block;
  overflow: hidden;
  white-space: nowrap;
  /* 将多余的文字用...表示 */
  text-overflow: ellipsis;
}
```









---





## Security权限控制











----





## Linux

### 基本命令

```shell
su root		-- 切换root用户(密码隐藏，且不显示长度)
clear		-- 清空当前控制台历史信息
===================================切换目录========================================
cd 当前目录下的目录(相对路径)/目录全地址(绝对路径)		-- 切换到指定目录地址
cd ..		-- 切换到当前目录的上一级
cd ~		-- 切换到当前用户的主目录(/home/用户名)	等同于 cd什么都不写
cd /		-- 切换到根目录
pwd			-- 查看当前所在目录位置
===================================显示文件========================================
ls			-- 显示当前所在目录下的文件(不包含隐藏文件)
ls -a		-- 查看当前所在目录下的所有文件(包含隐藏文件)
ls -la		-- 查看当前所在目录下的所有文件(包含隐藏文件)详细信息(权限、创建人、创建时间)
蓝色:文件夹，黑色:文件，绿色:可执行文件，红色:压缩包
===================================新增目录========================================
mkdir 文件夹名	-- 在当前目录创建一个文件夹
mkdir 文件夹1 文件夹2 文件夹3 -- 创建多个文件夹
mkdir 文件夹名1/文件夹2 ...	-- 在文件夹1下创建文件夹2，同样支持多个(文件夹1必须存在)
mkdir -p 文件夹名1/文件夹2/文件夹名3/文件夹4	-- 一次性创建多个文件夹
===================================新增文件========================================
touch 文件名	-- 在当前目录创建指定文件名的文件
===================================复制文件========================================
cp 文件名 复制出新文件的文件名 	-- 复制一个文件，重命名为新文件名
cp 文件名 文件夹名		-- 将一个文件复制到指定文件夹
cp 文件名 文件夹名/复制出新文件的文件名		-- 将一个文件复制到指定文件夹并重命名
===================================删除文件========================================
rm 文件名(包括后缀)		-- 删除指定文件
rm -r 文件夹名		-- 删除指定文件夹
rm -f 文件名	-- 删除文件没有提示y/n
rm *.后缀		-- 删除指定后缀的文件 
===================================移动文件========================================
mv 文件名 文件夹名		-- 将文件移动到指定文件夹
mv 
mv 文件名(包括后缀) 新文件名(包括后缀)		-- 重命名文件(可以修改后缀)
===================================查看内容========================================
cat 文件名(含后缀)	-- 显示文件内容
===================================管道操作========================================

===================================文件查询========================================
find / -name '文件夹名' -type d		-- 从根目录开始查询名为xxx的文件夹
find /起始目录 -name '文件夹名' -type print 		-- 从起始目录目录开始查询名为xxx的文件
find /起始目录 -name '*.后缀' -type print 		-- 从起始目录开始查询.java后缀的文件
===================================权限修改========================================
权限名：r：read读，w：write写，x：execute执行
chmod +权限名 文件/文件夹名
chmod -权限名 文件/文件夹名
chmod 三位二进制权限数 文件名
文件没有读权限，打开文件不显示文件内容，没有写权限，可以通过!强制写入
===================================文件压缩========================================
tar -cf 压缩后文件名 被压缩文件/文件夹	-- 压缩指定文件/文件夹为.tar文件
tar -xf 压缩文件名	-- 解压文件
tar -czf 压缩后文件名.tar.gz 被压缩文件/文件夹	-- 压缩指定文件/文件夹为.tar.gz文件
```







### 常用命令

```shell
ip addr										-- 查看IP信息
sudo yum install net-tools					-- 安装netstat包(才能使用sudo netstat -tlnp)
sudo netstat -tlnp							-- 查看进程占用的所有端口
systemctl stop firewalld					-- 先停止系统防火墙
systemctl disable firewalld					-- 并禁用自启动
```

##### 编辑网卡设置

```shell
cd /etc/sysconfig/network-scripts		-- 切换到网卡配置文件所在目录
vi ifcfg-ens33		-- 使用vi编辑器编辑网卡配置文件
esc		-- 进入打开状态
:wq		-- 退出
sudo service network restart	-- 重置/重启网络设置
```







### 功能

#### vi编辑器的使用

##### vi编辑器有三种工作状态：

###### 正常状态(打开时状态)：

打开文件时的状态，不能编辑文件，按i进入编辑状态，输入":"进入命令状态

```shell
yy(快速双击y)	-- 复制当前光标所在行
数字yy(2、3..)yy	-- 从当前光标所在位置开始复制2行
p	-- 粘贴刚才复制的行
dd	-- 剪切当前行
u	-- 撤销
ctrl+r	-- 恢复上一次撤销的动作
/ 关键字	-- 查询关键字(高亮，按n切换下一个高亮)
:s/str1/str2/	-- 替换当前行第一个str1为str2
:s/str1/str2/g	-- 替换当前行中所有str1为str2
:%s/str1/str2/g	-- 替换所有行中的str1为str2
:ms/str1/str2/	-- 替换第m行的第一个str1为str2
:m,ns/str1/str2/g	-- 替换第m行开始到第n行中所有的str1为str2
(注: m和n为数字，若m为.，表示为当前行开始;若n为$，则表示到最后一行结束)
```

###### 编辑状态：

可以对文件进行编辑，按esc切换成打开状态

###### 命令状态：

用来输入一些指令对文件进行保存、退出、查询、替换等操作

```shell
w	-- write，写入、保存(等同ctrl+s)
q	-- quit,退出
wq	-- 写入并退出
!	-- 强制
q!	-- 强制退出
set nu	-- 显示行号(临时设置，关闭文件后消失)
```

###### 设置永久行号

```shell
cd ~ cd 空格	-- 切换到用户目录
vi .vimrc	-- 创建并编辑文件vimrc
set nu	-- 在文件中设置行号
```



##### 使用vi编辑器进入指定文件：

```shell
cd 文件名 
```



##### 命令：

```shell
输入模式：i切换到INSERT编辑状态
退出:输入":"光标移到下面，输入以下指令：
q:不保存退出
wq:写入并退出
```





---





## Docker

### Docker三大核心概念

##### 镜像(image)：

​	是特殊的文件系统，包含程序、配置、资源等

##### 容器(Container)：

​	镜像的实例。就像Java中类和对象一样，镜像是定义的一个类，容器则是镜像的实体。

​	容器可以被创建、启动、停止、删除、暂停等。

##### 仓库(Repository)：

​	用于保存镜像的服务

  
