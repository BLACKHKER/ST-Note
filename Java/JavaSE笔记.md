## 面向过程

### 基本数据类型和引用数据类型

#### 数据内部存储在栈区和堆区中：

栈里的叫做引用，堆里的叫做对象(属性部分)

```java
Person p1 = new Person("刘备",18,"男");	// =号左边保存在栈，=号右边保存在堆
// 对象p1实际上叫引用
```

> 基本数据类型的变量名和值都存储在栈区。
> ​引用数据类型是保存变量名和地址，地址指向堆区的一块区域；

###### 这块区域内保存的是该变量的值：

```java
int[] num = {1,2,3};
int[] num1 = num;
```

这样相当于把栈区num中保存的引用(地址)给了num1，num和num1保存的是一个地址。
​如果只想复制值，不想用一块堆区地址，可以用Arrays.copyOf：

```java
int[] num2 = Arrays.copyOf(num,num.length);
```

> String names = "";	是没有申请空间的；
> String names = null;	申请空间没有值；





#### 自定义数组长度大小：

##### 数组类型[] 数组名 = new 数组类型[大小]

```java
String[] names = new String[3]; 
```

> 数组删除可以通过对应的索引下标，把该下标对应的空间改成默认值即可。

###### 或者通过下标位移删除算法：

```java
int scanner = 2;	// 键盘输入的数
int xb = scanner - 1;	// 键盘输入的数的实际下标
int[] nums = {1, 2, 3, 4, 5};	//定义数组
for (int i = 0; i < nums.length - 1; i++) {	// 循环体是循环的数组下标
    if (i >= xb) {	// 如果循环的数组下标等于输入的下标
        nums[i] = nums[i + 1];	// 从这里开始循环下标i加1，覆盖掉当前的i下标的值
    }
}
```

###### 位移完数组倒数第一和第二位是同一个值，所以通过缩容删除最后一位：

```java
nums = Arrays.copyOf(nums, nums.length - 1);	
```



### 流程控制

##### if(!) && while(!):

!的意思是非(取反)：
​两种判断语句是括号内为真则执行，为假则不执行。
​加个！(非)则变成为假执行，为真不执行了。



##### while()死循环：	

```java
while(true) {	//一直循环		适用于界面菜单循环}
```

###### for循环也可以实现：	

```java
for(;;) {	//一直循环 }
```

##### break：跳出循环；

##### continue：终止此次循环



##### 冒泡排序：

```java
int lun = score.length - 1;	//轮数是被排序的数组长度减1，因为排序完最后一个就是最小的
for (int i = 0; i < lun; i++) {	//进行几轮
    for (int j = 0; j < lun - i; j++) {	//-i 外循环圈数越多，里循环圈数越少
        if (score[j] > score[j + 1]) {	//从小到大排序，从大到小就是:score[j] < score[j + 1]
            int change = score[j + 1];
            score[j + 1] = score[j];
            score[j] = change;
        }
    }
}	
//每轮的j < lun - i 是因为每轮排序完都有一个最大值或者最小值了，那么最后一个值就不用再进行比较了。
```







### 方法

> 无参的方法可以直接调用，有参的就需要调用时给到实参；

###### 无参方法调用：

```java
public calss Main{
	public static void main(String[] args){
		m1(); //无参直接调用
	}	//主函数
	public static void m1(){
		int a = 1;
		int b = 2;
		int c = a * b;
		System.out.println(c);
	}
}	//主类
```

###### 有参方法调用：

```java
public calss Main{
	public static void main(String[] args){
		m1(1，5); //有参要在调用时给到一个参数，给的就是实参
	}	//主方法
	public static void m1(int a,int b){//int a int b则是形参。
		int z = a * b;
		System.out.println(c);
	}
}	//主函数
```





#### return：返回值

> 查询方法一般是有返回的，非查询方法一般是无返回的。

```java
public calss Main{
	public static void main(String[] args){
		int res = m1(1，5); //用res接收返回值，或者说将返回的值赋值给res
		System.out.println(res);//输出res也就是返回的z的值
	}	//主方法
    
    //不再是void，变成int代表返回值的类型
	public static int m1(int a,int b){
		int z = a * b;
		return z;//返回z
	}
}	//主类
```







### 面向对象：

#### 创建对象

一个点打下去，能调用哪些方法，是受限于它的类型的：

```java
String hero = "";
// hero.方法		这里就只能打出String相关的内容。
```

我希望hero能调用别的方法，那么就hero就不能再是String类型了。
那么他应该是一个Hero类型：Hero hero；

但是没有这个类型，怎么办？自己建立一个类型。



##### 在主类外新建一个hero类(class)：

```java
class Hero{		//代表一个结构的定义，可以理解为英雄的图纸
	public String name;	//真正的英雄还不存在
	public String job;
	public int price;
}
Hero hero1 = new Hero();	//根据图纸造了第一个英雄java
String job = hero1.	//这回就可以点出属性了(name,job,price)	实体类
```



##### 类名 对象名 = new 类名(); 一个对象就出来了

```java
public class Main{
	public static void main(String[] args){
	//p1,p2,p3是我们造(new)出来的对象(实例)
	//对象首字母小写
		Person p1 = new Person();	//造的第一个人
		p1.id = 1;
		p1.age = 25;
		p1.name = "刘备";
		p1.sex = "男";
		Person p2 = new Person();	//造的第二个人
		p2.id = 1;
		p2.age = 35;
		p2.name = "杨光";
		p2.sex = "男";
		Person p3 = new Person();	////造的第三个人
		p3.id = 1;
		p3.age = 31;
		p3.name = "武广东";
		p3.sex = "男";
    }
}
```

###### 三人编队：

```java
Person[] persons = {p1,p2,p3};
```



##### 也可以在new对象的时候直接装在数组里：

###### 创建一个Person类

```java
//结构，图纸
class Person{	//Person是类，类名首字母大写
	int id;
	int age;		//id、age、name、sex都称为属性
	String name;	//一个类里可以有属性，也可以有方法
	String sex;		//属性就是字段、字段就是属性、方法就是函数、函数就是方法
}
```

###### 主类来调用Person类创建对象：

```java
Person[] persons = {new p1(),new p2(),new p3()}	//遍历输出
Person[] arr = { p1, p2, p3 };	//输出Person类型、名为arr的数组
for (Person p : arr){	//Person p 是因为数组是Person类型
	System.out.println(p);
}
```





#### 类和类不一样：

###### 有实体类(entity)、工具类(global)、数据访问类(Dao)等，例如：

```java
class Person {	// 实体类Person
	public int id;	//属性
	public int age;
	public String sex;
	public String name;
}
```

这种数据模型称为"实体类"：比如公司实体、员工实体、订单实体等。







### 构造函数：

> 调用构造函数必然出现new。构造函数没有返回，也没有void，且与类名同名，构造函数是可以有参数的。

###### 固定写法：

```java
public 方法名(与类同名)(参数列表){方法体}
```

实体类里不写构造函数,那么默认存在无参构造。
可以写一个有参构造。就是有一个有参构造，一个无参构造。
好处是：创建(new)一个对象的时候可以传参，直接给属性赋值。
但是写了有参构造,默认的无参构造就不存在了，new对象的时候就

需要自己写。



例如：

```java
Person p1 = new Person();
p1.id = 1;
p1.name = "富兰克林";
p1.age = 45;
p1.sex = "男";			//这样比较麻烦
```

###### 那在实体类里自定义一个有参构造函数：

```java
public Person(int id,String name, int age,String sex) {
	//有参构造
}
```

###### 之后，就可以直接在new一个对象的时候传参来赋值：

```java
Person p1 = new Person(1,"富兰克林",45,"男");
```

###### 但是这样会造成参数有值，但是属性没值：

```java
Person p1 = new Person(1,"富兰克林",45,"男");
Person p2 = new Person(2,"麦克",31,"男");
Person p3 = new Person(3,"崔佛",36,"男");

Person[] arr = { p1, p2, p3 };	//遍历打印输出
for (Person p : arr){
	System.out.println(p.toString());
}

public Person(int id,String name, int age,String sex) {
    //自定义有参构造函数
}
```

运行结果为： 0|null|0|null
						0|null|0|null
						0|null|0|null		没有值，这时候需要this关键字。



#### this 

在有参构造函数里使用表示当前对象的值：

```java
public Person(int id,String name, int age,String sex) {
    //自定义构造函数			
    this.id = id;			输出结果为：	1|富兰克林|45|男
    this.name = name;					2|麦克|31|男
    this.age = age;						3|崔佛|36|男 
    this.sex = sex;			恢复正常。
}	
```

###### 等号左边：this.id 代表属性id

```java
class Person {
	public int id;	//属性(字段)
	public int age;
	public String name;
	public String sex;
}
```

###### 等号右边：id代表参数

```java
public Person(int id,String name, int age,String sex){}	//构造函数
//例如里面的int id。
```





#### private/public ：权限修饰符

private表示私有，修饰方法则该方法只能在本类内部调用，public 公有，到处可以调用。





#### Static ：静态

static表示静态，静态的成员，用类名来调用：
	类名.方法()	 或者 类名.属性	静态方法可以用类名调用
非静态成员，用对象来调：
	对象.方法()	 或者	 对象.属性 

静态方法里只有静态对象才能打点调用 

静态的用对象访问、用类访问都行，非静态的，只能用对象访问。
静态的成员依附于类，与对象无关。
非静态的成员依附于对象。

例如：

当一个属性设置为静态，那么无论new出多少个对象，这个属性是共享的。

非静态的属性，要在new一个对象时才会存在，而static的属性，在new一个对象之前就已经存在了

在Java中可以通过类实例(对象)调用静态方法。

#### 总结：

##### 1.静态变量或方法可直接调用：

```java
static MethodName();
ClassName.staticMethodName();
```



##### 2.非静态方法必须通过类的实例(对象)来调用

###### 定义一个类的实例(对象)：

```java
HelloWorld helloWorld = new HelloWorld();
```

###### 通过实例调用：

```java
helloWorld.hello2();
```

> 注：如果把hello2方法定义为static，则会出现warnings
>

Scanner：Scanner scan = new Scanner(System.in).next();	//倒二视频44分钟开始





#### 多态：父类引用指向子类对象

```java
// p1就是父类引用，指向子类Teacher类，
Person p1 = new Teacher("刘备",18,"男"); 
```





#### 重写：

​	子类覆盖父类的同名方法，比如toString重写，把默认的覆盖掉





#### 重载：

​	同名不同参：方法名一样，参数列表不一样。(普通方法，构造方法)只有方法才能重载。

​	同名又同参，但返回值不同，不构成重载。





#### 装箱、拆箱：	

```Java
int a = 5;	//装箱的好处就是可以调用一些API
Integer num = a;	//装箱：int往Integer转
int b = num;	//拆箱	Integer往int转
```

>
> 基本数据类型赋给包装类就是装箱，包装类赋给基本数据类型就是拆箱



对比：		Person p1 = new Person(1,"富兰克林",45,"男");

相当于：		类型		类名	 类	属性
				int		x	=	Person.age	
			InputStream	input = System.in;
				输入类型
			Scanner scan = new Scanner(input);

同理：		类名.属性.方法
			System.out.println();





## ArrayList：

##### 不用扩容，底层是数组:String[] int[]等：

```java
ArrayList<泛型> 数组名 = new ArrayList<泛型>();
```

例如：

```java
ArrayList<String> str = new ArrayList<泛型>();
```

不写泛型默认Object：

```java
ArrayList list = new ArrayList();
ArrayList<Object> list = new ArrayList<Object>();	// 相等
```



##### 添加：

​	数组名.add			例如：list.add();

##### 删除：

​	数组名.remove		例如：list.remove();
​	removeAll("集合")：删除所有匹配该集合的数据。



遍历list可以但不建议用普通for：
	1.获取长度不再是length，是.size()方法。
	2.不用[]获取指定下标的信息，用.get()方法。



###### 删除要注意的问题：

```java
for (int i = 0; i < list.size(); i++) {
	if (list.get(i).getName().equals("刘")) {	// 删除指定匹配的姓的集合对象
		list.remove(i);
        i--;	// ※※※ i--;	
    }			// i要--，因为list的整体下标会自动前移。
				// 比如删除3号元素，下一轮四号会顶替3号，删四号实际上删的是五号元素。			
}
```

倒着删可以避免这种情况：

```java
注意 >= 0
for (int i = list.size(); i >= 0; i--){
	if (list.get(i).getID() == id){
        list.remove(i);	就不用自减了
	}
}
```





#### 迭代器：Iterator<>：

###### 高级for的底层，是一个类,也可以携带泛型<>

```
Iterator<被迭代的数据的数据类型> 自定义名 = 集合名.iterator();	//获取迭代器对象
```


​	Iterator<String> itr = list.iterator();	//命名为itr，用这个调用迭代器方法
​	itr.next();	//使构造器下移一位，默认位为第一个数据的上方，指向空白位。
​	比如:

```java
ArrayList<String> list = new ArrayList<String>();
Iterator<String> frt = list.iterator();
list.add("苹果");
list.add("香蕉");
list.add("菠萝");
String test =	itr.next();	//test的值是：苹果
itr.next();	//test的值是：香蕉
```



###### 迭代器方法：hasNext()

返回布尔，假如到了最后一位，它返回的就不是true了，返回false，表明读到底了。
可以用于while来遍历list:

```java
	while(itr.hasNext()){
        String test = itr.next();	//接收迭代器当前位置对应的值
		System.out.println(test)	//输出
	}
```





##### 重写

@Override：表示下面的方法是重写的方法
	

```java
public void hello(){
		System.out.println("123");	
}

//重写
@Override	//写hello1，Override就会报错
public void hello(){
	System.out.println("1234");	
}
```





##### final：

​	修饰属性不能修改值；
​	修饰方法不能被重写；
​	修饰类不能被继承；
​	修饰方法的参数，不能修改参数。





##### super：

​	子类构造方法调用父类构造方法；
​	super('值')	 //必须写在第一行	，没有值默认调用无参。
​	不同的值(类型、数量)决定调用哪个构造方法。
​	创建子类对象的时候会默认调用父类的构造方法。
​	所以即使不写super();也默认有。





##### 向上转型：

​	父类名 对象名 = new 子类构造();
​	Person stu = new Student();	//new一个子类的对象赋给父类。
但是执行的是子类的方法，假如父类和子类都有println方法：

​	stu.println():执行的是重写后子类Student里的println()

​	好处是节省了代码量：有一个Fruit类，类里有一个show方法；

​	Fruit有两个子类：Apple类、Orange类，都继承了show方法；

###### Fruit类：

```java
public class Fruit {
    public void show(){
        System.out.println("this is a Fruit");
    }
}
```

###### Apple类：

```java
public class Apple extends Fruit {
    @Override
    public void show(){
        System.out.println("this is a Apple");
    }
    public void color(){
        System.out.println("红色");
    }
}
```

###### Orange类：

```java
public class Orange extends Fruit{
    @Override
    public void show(){
        System.out.println("this is a Orange");
    }
}
```

###### Test类：

```java
public class Test {
    public static void main(String[] args) {
        Fruit fruit = new Fruit();
      	Apple apple = new Apple();
        Fruit orange = new Orange();
        run(fruit);		//可以接收任何类型的值
        run(apple);		//可以接收任何类型的值
        run(orange);	//可以接收任何类型的值
    }   //主方法
    public static void run(Fruit fruit) {
        fruit.show();
    }
}   //主类
```

Test类里面的run()方法可以接收任何类型的值，他都会调用对应类的show方法。

否则要写很多个对应类型的run()：

```java
public static void run(Apple apple) {
        apple.show();
}
public static void run(Orange orange) {
        orange.show();
}
```





##### 向下转型：

​	Person p1 = new Person();
​	子类名 对象名 = (父类名)父类对象；
​	Student stu1 = (Person)p1; //强转为stu1
​	目的是为了让父类对象调用子类方法。





##### 抽象类、抽象方法：abstract

###### 修饰类

 abstract class 类名
普通类里能写的抽象类也能写，但是抽象类可以多一种：抽象方法。



###### 修饰方法 

abstract void 方法名();	//没有方法体
抽象类调用方法必须用继承：
​	子类继承的父类如果是抽象类，必须重写父类的抽象方法。
​	除非子类也是抽象类，那么子类的子类必须重写，依次延申。
​	重写的方法且非抽象方法是带方法体的：{}

> 父类:

```Java
public abstract class Person{	//抽象类
	public abstract void show();	//抽象方法
}
```

> 子类：

```java
public class Student extends Person{
	//这样空白的会直接报错，因为没有重写父类的抽象方法 
	//重写：
	@Override
	public void show(){
		System.out.println("重写父类show方法");
	}			
}
```



抽象类不能直接实例(new一个对象)，例如：

```java
//创建一个动物类：
public abstract class Animal{}
//创建一个测试类：
public class Test{
	public static void main(String[] args){
		Animal animal1 = new Animal();	//报错
	}
}
```

需要一个继承该抽象类的子类来new一个对象：

```java
public class Dog extends Animal{}	//创建一个Dog类：
```

在测试类里new一个新的Dog类型：

```java
Animal animal1 = new Dog();	
```





##### 接口：interface	

就是class改成interface就可以了：

```java
public interface Father{}	//定义一个Father接口
```



接口里只能写抽象方法(JDK1.8之前)：

```java
public abstract void show();
```



接口里面的方法默认就是public(公开)、abstract(抽象)的，所以可以写成：

```java
void show();
```



接口定义了能做哪些功能，但是如何实现这些功能则需要实现类来做的。
一个实现类可以继承多个接口。





##### implements：实现

​	class 实现类类名(子类名) implements 被实现的类类名(父类){
​		继承类：
​		@override
​	}
用Father接口举例：
​	public interface Father{	//创建一个Father接口
​		void show();
​	}
​	class Child implements Father{	//创建一个Children类
​		对于这个Children类，我们一般称为Children类是Father接口的实现(实现类)。
​	}
跟抽象类的继承差不多，接口的实现只不过extends变成了implements。
一个接口可以有多个实现类。

创建接口的实例，不能直接实例，需要用实现类来完成：
	接口 对象名 = new 实现类;
用上面的Father举例：
	Father a = new Child();	//向上转型，这样就可以用Child实现类里面的方法。
	a.show();

接口里面可以定义属性，但是要注意：
	接口里面的属性默认且必须为public static final的。
	所以也可以省略不写。(公开的静态常量)

##### enum:枚举

###### 创建一个枚举类：

```java
public enum FistRules(类名){
	石头，剪刀，布	 //常量1,常量2,常量3;
}
```

###### 调用枚举：新建Test类创建枚举对象

```java
FirstRules st = FirstRules.石头(枚举类里的某个值)
FirstRules st = FirstRules.剪刀(枚举类里的某个值)
FirstRules st = FirstRules.布(枚举类里的某个值)
```

###### 获取枚举值的String：

```java
System.out.println(st.name());	//调用name方法;
```

###### 获取索引下标：

```java
System.out.println(st.ordinal());	//调用oridnal方法;
```

###### 拿到FirstRules枚举类里的所有值：

​	FirstRules[]  str(数组名) = FirstRules.values();	//调用value方法，返回一个数组;

###### 遍历输出：

​	for (int i = 0; i < str.length; i++){
​		sout(str[i]);
​	}

###### Random:随机数

创建一个随机数对象:
	Random (对象名) = new Random();	
	Random randomNum = new Random();
划定随机数范围(从零开始数)，返回一个随机数：
	对象名.nextInt(范围上限，不包括),点不止Int，也有Double、Long;	
	randomNum.nextInt(3);	//代表随机0，1，2 到3结束
用int类型变量来接随机数：
	int randomNumber = randomNum.nextInt(3);

###### 匿名实现类：

接口只有一个方法，但是还要写一个实现类，这种情况可以用匿名实现类来简化代码。
没有类名、创建匿名实现类的对象必须new关键字一起出现:
	接口名 对象名 = new 接口名(){		//就创建了一个匿名实现类对象
		@Override
		原实现类类体；
	}

> 原接口：
>

```java
interface Phone {
		public void show();	//抽象方法
}
```

> 原接口的实现类：
>

```java
//calc的实现类JiSuan:
	class XiaoMi implements Phone {	
		@Override
		public void show() {
			System.out.println("我是小米手机");
		}
	}
```

> 原调用实现类里的方法：

```java
public class Test{
	public static void main(String[] args){
    	Phone phone = new XiaoMi();	//先创建对象
        phone.show();	//用对象调用方法
	}	//主函数
}	//主类
```

> 匿名实现类：

```java
//1、将所有原实现类整体搬到创建对象这里
public class Test{
	public static void main(String[] args){
    	Phone phone = /*new XiaoMi()没了*/  
        class XiaoMi implements Phone {	
			@Override
			public void show() {
				System.out.println("我是小米手机");
			}
		};  
	}	//主函数
}	//主类
```
```java
//2、删除原实现类类名、实现了哪个接口也删除
public class Test{
	public static void main(String[] args){
    	Phone phone = 
        /*删除了这里*/{
			@Override
			public void show() {
				System.out.println("我是小米手机");
			}
		};  
	}	//主函数
}	//主类
```

```java
//3、new 接口的对象:new Phone()
public class Test{
	public static void main(String[] args){
    	Phone phone = new Phone(){	
			@Override
			public void show() {
				System.out.println("我是小米手机");
			}
		};  
//接下来就可以向之前一样调用方法了：
        phone.show();
	}	//主函数
}	//主类
```

> 就相当于直接new接口的对象，他会报错：接口不能直接创建实例，需要先创建该接口的实现类。
>
> 那么直接把实现类的类体写在new接口对象的后面，告诉接口这个就是实现类，就是匿名实现类。
>

###### 继续精简则使用lambda表达式：

##### lambda表达式：

接口名 对象名 = (// 参数列表)->{
	//方法体，写具体操作的;
};	

例如：

```java
Calc sum = (int a, int b) -> {
	return a+b;
};
```

java本质是一个函数，可以替代匿名内部类来实现接口。
一般的函数有返回值、方法名、参数列表、方法体;
而lambda表达式只有参数列表和方法体;(参数列表) -> {方法体} "->"为lambda运算符。

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
```

```java
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
```

```java
// 3、最后添加一个lambda运算符："->"就完事了
public class Test{
	public static void main(String[] args){
    	Phone phone = () -> {
				System.out.println("我是小米手机");
			};  
	}	// 主函数
}	// 主类
```

###### 表达式精简,以上方表达式为基础：

1、参数类型可以省略;

```java
Calc sum = (a, b) -> {
	return a+b;
};
```

2、假如只有一个参数,括号()可以省略;

```java
Calc sum = a -> {
	return a+b;
};
```

3、如果方法体只有一条语句，大括号可以省略;

```java
Calc sum = a -> return a+b;	// 注意return是例外，有return的时候需要同时去掉return;
```

4、如果方法体中唯一的语句是return，则需要把return同时省略;

```java
Calc sum = a -> a+b;
```

注意lambda表达式方法体里只能有一个方法。

##### lambda表达式方法引用：

​	多个lambda表达式实现函数是一样的话，可以封装成通用方法
lambda可以用方法引用实现:
​	对象 :: 方法
如果是static静态方法，可以直接用类名：
​	类名 :: 方法

##### 内部类：

​	写在主类里面的类，或定义在方法里面的类，称为内部类。
​	内部类添加static和不添加，在new对象的时候是有区别的：
添加了static的内部类new对象时：
​	主类名.内部类名 对象名 = new 内部类构造方法();
没添加的new内部类对象时：
​	主类名.内部类名 对象名 = new 主类构造方法().内部类构造方法();
​	要先调用主类的构造方法，再调用内部类的构造方法：

```java
class Person{
	static class Student{	
		//添加了static的内部类
	}	
	class Teacher{
		//没有添加static的内部类
	}
	public static void main(String[] args){
		Person.Student stu1 = new Student();	//new添加了static的
		Person.Teacher tea1 = new Person().Teacher();	//new没添加的
	}
}	//主类
```

###### 使用场景：

​	1、当一个类需要多个父类的时候，可以借助内部类来实现这个缺点。
​	2、用过内部类，来包装外部类的数据结构，加以隐藏封装
​	3、当某个方法计算很复杂，需要一个A类来完成．
​	但是这个A类和它的外部类B耦合度很高．那就定义为内部类。
​	比如LinkedList底层，把我们的数据通过Node类来进行包装了。

##### 静态代码块：在类里面添加static：

```java
static{
	//代码
}	//静态代码块比构造方法还要先执行。
```

##### 泛型类：只在编译期间有效果，泛型在运行的时候会被擦除。

```java
class 类名<参数名(占位符)>{}
class Student<T>{
	//T为占位符，什么都可以
}
```

使用：

```java
class Student<T>{
	T name;	//传进来的类型可以用来定义变量的数据类型
	void show(){
		System.out.println(name.getClass());
	}
}
```

主函数：

```java
Student<String> stu = new Student<String>();	//将上面的占位符T定义为String
stu.name = "赵云";	//Student泛型是String，所以可以给name传字符串
stu.show();
```





### 排序 两大家族：

​	数组工具类：Arrays

​	集合工具类：Collections

#### 1、List(有序的 -> 本质是一个数组)

##### 	ArrayList:

```java
ArrayList<泛型> 对象名 = new ArrayList<泛型>();	
```

##### 	LinkedList：

```java
LinkedList<泛型> 对象名 = new LinkedList<泛型>();	
```

###### List排序可以用Collections下的sort():

```java
List<类名> list = new ArrayList<类名r>();
List<Integer> list = new ArrayList<Integer>();	// 假设list里有1，5，3，11，9

sort(list,比较器对象)	// 比较器：Comparator，是一个接口，有一个抽象方法compare(T o1,T o2);
Comparator<Integer> cmp = new Comparator<Integer>(){
    @Override	// 继承并实现Comparator里的抽象方法
    public int compare(Integer o1, Integer o2) {
        return o1 - o2;	//1，3，5，9，11 o2 - o1 就是从大到小
    }
};
Connections.sort(list,cmp)
System.out.println(list);

// 也可以用匿名实现类：
	Collections.sort(list, new Comparator<类名>(){
        @Override	// 继承并实现这个抽象方法
        public int compare(类名 o1, 类名 o2) {	// 要对比的对象属于哪个类
            return 0;	//return正数、负数、0
        }
    });
// Lambda简写：
	Collections.sort(list,(o1,o2) -> {return o1-o2;});
```





#### 2、Set(无序的 -> 内存层面)

##### HashSet:

​	HashSet<泛型> 对象名 = new HashSet<泛型>();
​	HashSet每条数据是唯一的，存入相同的数据值只保留一条。
​	存入的数据会给一个HashCode码，是唯一的，每个码对应一条数据，实现去重。

向上转型：ArrayList、HashSet等方法继承自Set接口，可以向上转型，例如：
	Set<泛型> 对象名 = new HashSet<泛型>();

##### TreeSet:

​	TreeSet<泛型> 对象名 = new TreeSet<泛型>();

TreeSet自带排序，但是不能排序对象，排序对象要让想排序的对象所对应的类，实现一个接口：Comparable

###### Comparable接口：

​	接口里面有一个方法，实现这个接口就要继承compareTo(T o)方法。
​	是一个泛型接口:<>，该接口对实现他的每个类的对象强加一个整体排序。
​	泛型里添加被排序的类。
​	这个排序称为类的自然排序，类的compareTo()方法被称为自然比较方法。

```java
class Student implements Comparable <Student>{	//实现Comparable接口
		int num;
		int age;
		String name;
		public Student(num,name,age){}	//有参构造
}
```

###### 继承并重写Comparable接口的抽象方法：compareTo(T o)

​	T是泛型占位符，o是要比较的对象的对象名

这个方法不需要主动调用，方法会在add的时候自动调用：
	会从treeSet里获取第一个对象，这个对象就是o，跟要添加的对象进行比较。

```Java
public int compareTo(T o){	//T，比较对象的类型 o，要比较的对象
    if(this.age > o.age){	//如果(当前添加的对象的age大于数组获取的对象的age)
        return 1;	//1代表添加的对象比数组对象大，放在后面	从小到大123
    } else if (this.age < o.age){	       		
        return -1;	//-1代表添加的对象比数组对象小，放在前面	从大到小(冒泡)321
    }								
		return 0;	//0代表已经有这个对象了，就不会再去加了 
}
```

简写方式：

```java
public int compareTo(T o){	//(升序 -> 从大到小，降序 -> 从小到大)
    //升序算法	当前对象this - 数组对象o
	int shengXu = this.age - o.age;		//添加的对象比数组里的对象大，正数，往后排。
    									//添加的对象比数组里的对象小，负数，往前排。
    //降序算法	数组对象o - 当前对象this
    int jiangXu = o.age - this.age;
	return result;					
}
```



##### Map：







##### 单例设计模式(饿汉)：

​	构造方法私有化(private)，外部就不能创建对象了。
class Person{	
​	String name;
​	Person p1 = new Person();	//在类内部创建对象
​	private person(){}	//私有构造方法
}
外部调用对象：
​	Person.p1.name = "赵云";

final修饰的数据：
基础数据类型值不能变：
	final int a = 5;
	a = 10;	//报错

引用数据类型的地址不能变，但是值可以：
	final int[] nums = {1,2,3};
	nums = new nums[4]	//报错
	nums[0] = 0;	//修改数组里1的值

对象地址也不能变，值可以：
	final	Person p1 = new Person("刘备");
	p1 = new Person();	//报错，创建一个新的对象地址赋给p1
	p1.name = "关羽";	 //可以修改值

var(JDK17通用类型)：
	会自动确认自己的数据类型：
	var id = 10;	//int
	var name = "刘备";	//String





#### 异常：day0916

Throwable:异常的根类，有两个子类：Error类、Exception类。
	Error是严重错误，无法处理。例如内存溢出；
	Exception是异常错误，可以处理。例如数组下标越界；
程序在运行时，JVM会开一个Exception Thread(异常线)线程，来监听程序。
如果程序出现问题，它会立即终止程序并记录问题位置、问题原因(属于哪种异常)，
接着封装成一个异常对象，将对象输出给控制台，控制台解析信息并打印输出。
如果出现问题但是不想终止程序，java提供了一种结构：try catch；
try catch:
	try{
		可能出异常的代码；
	} catch"捕获"(接收传回的异常对象：对象(异常)类型 对象名){	//接收Exception Thread传回的异常对象；
		//触发异常后的代码;
	}
	//继续往下；
try里面的没有出现异常，	则不执行catch里面的代码。
触发异常，执行完catch，继续向下。
catch可以写多个：
	catch(下标越界异常类 xbyj){System.out.println("触发下标越界异常！");}
	catch(空指针异常类 kzz){System.out.println("触发下标越界异常！");}
那么返回什么类的异常，就执行对应类分支的catch。
如果一个对象的方法可能触发多种异常，不想写这么多catch，
那么可以写所有异常的父类：Exception
	catch(Exception allExcption) {
		//触发异常后运行的代码;
	}

printStackTrace() 打印异常相关信息:
	(异常类)对象名.printStackTrace();
	catch(Exception allException){
		System.out.println("触发异常！);
		allExcption.printStackTrace();	//打印异常信息
	}

printStackTrace() 接收返回异常对象的值，在抛出异常里使用；

finally{} 不管是否出现异常，都要执行：
	try{
		//正常运行	|	//运行异常
	} catch() {
		//不触发异常or	 |	//触发异常
	} finally {
		//执行	|	//执行
	}								//异常应用场景：Scanner；

抛出异常：
创建对象，throw对象；卸载try里，catch会在下面捕获异常，捕获到触发catch
	Expection 对象名 = new Expection();
	Expection exp = new Expection("对不起您输入有误");
	throw 异常类对象;
	throw exp;
可以简化为：throw new Expection("对不起您输入有误");
throw 挨着下面不能写语句，执行throw会自动跳转到catch;
无论是执行异常还是抛异常都会执行catch语句；

throws关键字 声明一个异常：
如果没有trycatch，需要在方法后面声明此方法会抛出什么类型的异常；
抛出的异常要交给调用者来捕获，谁调用的方法，谁来处理:
main 方法里面调用t()方法，t里面抛出了异常并且没有try catch：
	t() throws Expection{	//声明会抛出Expection类型的异常
		throw new Expection("输入有误，请重新输入！");
	}	
main方法{	//需要处理t()方法抛出的异常；
	try{
		t();
	} catch(Expection exp) {
		//printStackTrace()获取t()抛出的("输入有误，请重新输入！")
		System.out.println(exp.printStackTrace()); 
	}
}

如果mian调用了也不想处理：可以继续throws；
	mian方法 throws Expection{} 这样就交给控制台来处理；





Dao层异常处理：

```java
try {
    Goods goods = goodsMapper.findById(id);
    return goods;
} catch (DataAccessException d) {
	// 数据访问异常，Spring内置的Dao层通用异常，是Spring在处理数据访问时的异常基类
} catch (PersistenceException p) {
    // 持久性异常，Java Persistence API (JPA)中定义的异常
}
```







### IO流：(带有Reader，Writer的是字符流，反之是字节流)

![IO流](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202303271138537.png)

I：input; O:output，所以IO流可以称为输入输出流
内存和磁盘进行数据交换的时候需要一个管道，这个管道就是IO流的对象；



#### Reader/Writer字符流：

```java
// 输入
Reader 对象名 = new FileReader("文件地址/文件名");
Reader input = new FileReader("d:/stu.obj")
// 输出
Writer 对象名 = new FileWriter("文件地址/文件名");
Writer output = new FileWriter("d:/stu.obj")
```



##### FileReader：读取文件

```java
Reader input = new FileReader("s:/素材/素材1/人员名单.txt")		 //读取文件
```

###### read() ：一次读取一个字符

​	管道对象.read();	//每执行一次，读取一个字符。
返回int，返回值如果为-1，表明读到底了，跟迭代器Iterator的hasNext()一致。

就可以用while来循环:

```java
int len = 0;
while((len = input.read()) != -1){	// len为每次实际读取的长度
	System.out.println((char)len);
}	
```



###### read(char[] 缓冲区)：一次读取多个字符

​	read()方法可以传参，传一个char[]数组(容器)缓冲区，缓冲区的大小决定一次读取的数据量。

```java
char[] buf = new char[1024];	//定义数组长度为1024 buf是缓冲区
int len = 0;
while((len = input.read(buf)) != -1){	// len为每次实际读取的长度
	System.out.println(new String(buf));	//强转成字符串
}	
```





##### FileWriter：写入文件

```java
Writer output = new FileWriter("s:/素材/素材1/新人员名单.txt")	//写入新文件
```

###### write(char[] 缓冲数组 起始位置 结束位置)：写入多个字符

```java
char[] buf = new char[1024];	//定义数组长度为1024 buf是缓冲区
int len = 0;
while((len = input.read(buf)) != -1){	// len为每次实际读取的长度
	output.write(buf,0,len);	//将缓冲区保存的数据写入到文件，从0开始，写入读取的长度
    output.flush();	//刷新缓冲区
}	
```





##### close() 关闭流(管道)：

​	IO对象名.close;
​	output.close; //释放资源，必须调用
适合写在finally里。注意out报红是因为声明的时候在try里，作用域作用不到。

可以在trycatch外面写好：
	ObjectoutputStream output = null;

注意关闭流也需要写一个catch：

```java
try {
    
} catch(Expection exp) {
 
} finally {
	try {
		out.close()	//close方法会抛出一个异常:用trycatch接收；
	} catch(Expection exp) {	
 	  }
  }
```





#### InputStream/OutputStream 字节流：

字节流可以读取写入任何文件

###### 字节流输入输出：

```java
// 输入
inputStream 对象名 = new FileinputStream("文件地址/文件名");
inputStream input = new FileinputStream("d:/stu.obj")
// 输出
OutputStream 对象名 = new FileOutputStream("文件地址/文件名");
OutputStream output = new FileOutputStream("d:/stu.obj")
```

读取输出图片：

```java
public class InputAndOutputPicture {
	public static void main(String[] args) {
		try {
			InputStream input = new FileInputStream("s:/素材/素材2/images/大乔.jpg");
			OutputStream output = new FileOutputStream("s:/素材/素材2/images/新大乔.jpg");
			byte[] buf = new byte[1024];	//跟字符流的区别就是字节流缓冲区为byte[]
			int len = 0;
			while ((len = input.read(buf)) != -1) { // len为每次实际读取的长度
				output.write(buf,0,len);
				output.flush();
			}
			output.close();
			input.close();
			System.out.println("写入成功！");
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
}
```





#### BufferedReader/BufferedWriter缓冲流(管道)：

需要把FileReader/FileWriter包进去；

##### BufferedReader：读取

```java
BufferedReader 对象名 = new BufferedReader(FileReader对象);
Reader reader = new FileReader("s:/素材/Person.txt");
BufferedReader buffread = new BufferedReader(reader);
```



##### BufferedWriter：写入

```java
BufferedWriter 对象名 = new BufferedWriter(FileWriter对象);
Writer writer = new FileWriter("s:/素材/Person.txt");
BufferedWriter output = new BufferedWriter(writer);
```

> 问题1：写入会将原本的文本覆盖掉，如果不想覆盖，需要在创建FileWriter的地址后面写一个true：

```java
Writer writer = new FileWriter("s:/素材/Person.txt"， true);	// 在后面写，不覆盖
```

> 问题2：每次写入都是写在一行，没有换行，BufferWriter对象调用newLine()方法：

```java
Writer writer = new FileWriter("s:/素材/Person.txt", true);
BufferedWriter output = new BufferedWriter(writer);
output.write(name);	//写入新名字
output.newLine();	//写入后换行
output.close();	//关闭BufferWriter流
```



###### readLine(): 一次读取一行

返回String，如果返回null，表明读到底了

```java
String s = bufferedReader.readLine();	//将读取的一行文字保存到Stirng s中。
System.out.println(s);	//输出第一行
System.out.println(bufferedReader.readLine());	//读取下一行并输出。
```

while循环遍历：

```java
String x = "";
while((String x = bufferedReader.readLine()) != null){
	System.out.println(x);
}
```

bufferedReader.close(): 关闭buffer的管道，里面的fileReader管道会被自动关闭。





##### Properties：配置文件(文件名.properties) 93-0810-2 00:20:00

配置文件示例：

```java
curr = com.bhk.pack01.Cat
```

方法调用配置文件：

```java
// 自动获取配置文件位置并转换为流
InputStream input = 类名.class.getResourseAsStream("配置文件名");
InputStream input = AnimalFactory.class.getResourseAsStream("setting.properties");

// 这个类用来读取配置文件
Properties p = new Properties();	// 创建properties对象
p.load(input);	//获取到的输入流
```

可以不用InputStream：

```java
Properties p = new Properties();	// 创建properties对象
p.load(AnimalFactory.class.getResourseAsStream("setting.properties"));	//获取到的输入流
```

```java
// 获取类名：就是配置文件里的Cat
String clazz = p.getPeoperty("key");	//key就是curr，一个key对应一个Value key可以是别的
String clazz = p.getPeoperty("curr");	//curr的Value就是
// 反射：根据类名获取类的对象				获取到的clazz就是com.bhk.pack01.Cat
Class.forName(clazz).newInstance();
```







### 反射：根据名称解析这个类的结构

> 一个类在内存中只有一个Class对象
>
> 一个类被加载后，整个类的结构都会被封装在Class对象中。

##### forName()：根据文件路径获取类Class对象

```java
Class 对象名 = Class.forName("包名(类的地址)类名");
Class c1 = Class.forName("com.bhk.entity.Student");
```



##### getClass()：根据对象获取类Class对象，返回Class类型的对象

```java
Student s = new Student();	// 创建Student类型的对象s
Class c = s.getClass();	// 
```



#### 类对象对应的方法：

##### Class.forName(类名).newInstance()：根据类Class对象获取该Class对应类的对象

但是是Object类型的对象。

```java
Class.forName(Cat).newInstance();	// 获取Cat类的对象
Object obj = Class.forName(Cat).newInstance();	// 用Object类接收
(Cat)obj;	// 强转Object类的对象为Cat类的对象
```

> 注意newInstance会去调用该类的无参构造方法。如果只有一个有参构造那么无法创建对象。



##### getDeclaredField()：返回Field(属性)类型的对象，根据字符串返回匹配该类对象的Field(属性)对象

```java
Field 对象名 = 类对象.getDeclaredField(匹配的字符串);
Field f = c.getDeclaredField("name");	// 返回Field类型的Student类的属性name 用f接收
```

> 同样的，在Java中所有属性为Field，所有方法也有一个对象可以表示：Method

###### setAccessible(true)：关闭访问权限

```java
属性对象/方法对象.setAccessible(true);
f.setAccessible(true);	// 关闭f属性对象的访问权限(private)
```

###### set()：给属性赋值

```java
Field(属性)类对象.set(对象名，值);
f.set(s, rs.getObject(columnLabel)); // 结果集rs中获取当前该行对应列名columnLable的值
```





#### 获取该类注解的参数：

##### 定义一个注解：

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
public @interface Proxies {
    Class c();	// 注解属性c，Class类型
}
```

##### 获取注解属性值：

```java
该类的Class.getAnnotation(注解名.class); 返回注解类型的对象(Annotation)
// 假设该注解为Proxies
Proxies annotation = (Proxies) target.getAnnotation(Proxies.class);	// 获取注解对象并强转

注解对象.注解属性(); 返回该属性的数据类型
Class c = annotation.c();	// 获取该注解的属性c的值，c数据类型是Class，用Class类型接收
```









##### String.valueOf ()： 将字符数组转换为字符串

​	String.valueOf(数组,起始位置,转换多少个);
​	String.valueOf(china,0,n);	//n是上面获取的一共有多少个数据的int返回值。

同样可以while循环：

```java
int sum = 0;
while((n = reader.read(china)) != -1){
	String ch = String.valueOf(china,0,n);
	System.out.println(ch);
}
reader.close();
```

通过设置china数组的长度(new[10])每次读取个数相加：
	sum += n	//获取总共读取了多少字符





##### File：File类

​	File f = new File("D:/存数据/china");	//将文件夹转换成File对象
方法:
​	File file = new File("d:/123.txt");   //创建一个File(文件)类对象file
返回布尔：

```JAVA
boolean x = file.mkdir();   //在对象地址创建文件夹
boolean u = file.delete();  //删除文件/文件夹，如果文件夹里面有内容，则不能删除
boolean y = file.isFile();  //判断是否是文件
boolean z = file.isDirectory(); //判断是否是文件夹
boolean q = file.createNewFile();   //当且仅当不存在具有此路径名指定名称的文件时，创建一个新的空文件
boolean r = file.exists();  //判断某个文件在磁盘中是否存在
```

其他：
	getName();   //获取 文件名，返回String。
	length();    //获取文件的字节数，返回Long。

​	File[] subFiles = file.listFIles();	//返回当前对象file的值，文件地址所对应的所有文件。

​	

//  以下三个方法后缀都有path  （和路径相关），返回String。
	getPath();      //文件对应字符串
	getAbsolutePath();   //文件对应物理文件的路径
	getCanonicalPath();  // 完整写法，标准写法，盘符是大写的





#####  @FunctionalInterface：声明函数式接口 

​	被声明的接口只能有一个抽象方法，配合lambda表达式非常好用



---



### 线程

Java中创建线程主要有三种方式：

一、继承Thread类创建线程类

（1）定义Thread类的子类，并重写该类的run方法，该run方法的方法体就代表了线程要完成的任务。因此把run()方法称为执行体。

（2）创建Thread子类的实例，即创建了线程对象。

（3）调用线程对象的start()方法来启动该线程。

二、通过Runnable接口创建线程类

（1）定义runnable接口的实现类，并重写该接口的run()方法，该run()方法的方法体同样是该线程的线程执行体。

（2）创建 Runnable实现类的实例，并依此实例作为Thread的target来创建Thread对象，该Thread对象才是真正的线程对象。

（3）调用线程对象的start()方法来启动该线程。

三、通过Callable和Future创建线程

（1）创建Callable接口的实现类，并实现call()方法，该call()方法将作为线程执行体，并且有返回值。

（2）创建Callable实现类的实例，使用FutureTask类来包装Callable对象，该FutureTask对象封装了该Callable对象的call()方法的返回值。

（3）使用FutureTask对象作为Thread对象的target创建并启动新线程。

（4）调用FutureTask对象的get()方法来获得子线程执行结束后的返回值



---



## JDBC

##### 1、Class.forName()：反射驱动

```java
Class.forName(反射的驱动)
Class.forName("com.mysql.jdbc.Driver");	//try catch
```

###### 可以拿到外面，定义为私有、最终、静态变量：

```java
private final static String driver = "com.mysql.jdbc.Driver"
Class.forName(driver);	//try catch
```



##### 2、get Connection()：获取连接

```java
Connection 连接对象名 = DriverManager.getConnection("jdbc:mysql://本机地址","账号","密码");
//	本机地址：jdbc:mysql://localhost/数据库名
//	例如：	  jdbc:mysql://localhost/myschool
Connection conn = DriverManager.getConnection("jdbc:mysql://localhost/myschool","root","root");
//	注意导包是java.sql.Connection，不是com.mysql.jdbc
```

###### URL、数据库账号、密码也可以定义到外面：

```java
private final static String url = "jdbc:mysql://localhost/myschool","root","root";
private final static String user = "root";
private final static String pwd = "root";
Connection conn = DriverManager.getConnection(url,user,pwd);
```



##### 3、createStatement()：获取Statement对象

```java
连接名.createStatement() //连接名调用creatStatement返回一个Statement类型对象
Statement st = conn.createStatement()	//创建并接收Statement对象
//	注意导包java.sqlStatement
```



##### 4、用Statement对象调用execute()方法执行SQL语句

```java
Statement对象.execute(sql语句)	//返回布尔，说明执行增删改语句，查询返回值布尔装不了
Statement对象.executeQuery(sql语句)	//返回ResultSet(结果集)	执行查询语句
    
String sqlInsert = "INSERT INTO subject(SubjectId,SUbjectName,ClassHour,GradeId)
    				VALUES (21,"Java从放弃到入门",58,1)"
String sqlSelect = "SELECT * FROM student";	//单独定义一个变量保存SQL语句

boolean x = st,excute();	//返回布尔
ResultSet rs = st.executeQuery(sql);	//返回ResultSet(结果集)类型的数据
```

###### 遍历ResultSet类型的值不能用forEach，用类似迭代器的东西：

```java
while (ResultSet对象.next()) {
	列名类型 变量名 = ResultSet对象.get列名类型(列名)	//接收返回值
}

while (rs.next()){
    int id = rs.getInt("id")	//获取int类型的字段：id
    String cname = rs.getString("cname");	//获取String类型的字段：cname公司名
    System.out.println(id + cname);	//每遍历一次输出一次
}
```



#### ResultSet(结果集)对象对应的方法：

##### getMetaData()：获取表头，返回ResultSetMetaData类型的对象 metadata(元数据)

```java
ResultSetMetaData metaData = rs.getMetaData();	// metaData对象接收
```



##### ResultSetMetaData 可以调用数据库表相关的方法：

###### getColumnCount()：获取该表一共有多少列，返回int行数

```java
int columnCount = ResultSetMetaData对象.getColumnCount();
int columnCount = metaData.getColumnCount();
```

###### getColumnLabel()：获取该表每列的建议列名(字段名)，返回String

```java
String columnLabel = ResultSetMetaData对象.getColumnLabel(第几列);
String columnLabel = metaData.getColumnLabel(1);	// 返回第一列的列名
```



##### 4-1 PreparedStatement：占位符形式写SQL语句

```java
Connection conn = JDBCUtil.getConnection();	//从连接池获取连接对象
String sql = "INSERT INTO account(user_name,user_pwd) VALUES(?,?)";	//SQL语句，？为占位符
PreparedStatement cmd = conn.prepareStatement(sql);// 创建PrepareStatement对象cmd
cmd.setObject(1, name);	//填充第一个占位符，把name填充进SQL
cmd.setObject(2, DigestUtils.md5Hex(pwd));	//填充第二个占位符
int i = cmd.executeUpdate();    //拿到数据库返回的，受影响行数 PrepareMent方法executeUpdate
if (i > 0) {
    return true;
}
return false;
```

