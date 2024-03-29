## Java - API

### String：字符串

##### String转换为int:

```Java
String str = "123";
int num = Integer.presInt(str);
```


##### String转换为Integer：

```Java
Integer num = Integer.valueOf(str);
```



##### Integer转换为String：

```Java
num.toString();
```



##### split("字符")：切割字符串

```java
split("以什么为基准分割字符串")
字符串.split("以...切割的符号");  // 切割完是一个字符串数组
字符串.split("以...切割的符号")[下标];  // 切割完是一个字符串
String job = str[i].spilt("-")[1];	// 用String类型的job来装切割完的字符串数组的第一个字符串
```



##### substring(a,b)：截取字符串

```java
name.substring(起始位置(从零开始), 结束位置);	// 返回新的字符串
String name = "abcd";	
String nName = name.substring(1, name.length() - 1);	// 从1开始截取到字符串长度-1
System.out.println(nName);	// bc
```



##### equals("字符串") ：精确匹配字符串

```java
字符串.equals("要匹配的字符串")	// 返回布尔
String name = "刘备";
if(name.equals("刘备")) {
	System.out.println("全名匹配成功:)");
}
if(name.equals("备")) {
	System.out.println("名匹配成功:)");
}	// 输出全名匹配成功
```

> 只能匹配完全一样的，只能整体跟整体比。
> 例如字符串中国制造，中国用equals比永远是false，必须完全一致才是true。

##### contains("字符")：模糊查询字符串

```java
字符串.contains("要匹配的字符串")	// 返回布尔,可以用局部跟整体比。
String name = "刘备";
if(name.contains("刘备")) {
	System.out.println("全名匹配成功:)");
}
if(name.contains("备")) {
	System.out.println("名匹配成功:)");
}	// 输出全名匹配成功,名匹配成功
```



##### startsWith():对比字符串开头

```java
startWith(字符串)	// 返回布尔
String name = "abcdefg";
if (name.startsWith("a")) {
	System.out.println("匹配成功:)");	// 匹配成功:)
}
```

##### endWith("字符"):对比字符串结尾

```java
endWith(字符串)	// 返回布尔
String name = "abcdefg";
if (name.endWith("g")) {
    System.out.println("匹配成功:)");
}
```



##### toUpperCase()：字符/字符串转大写

```java
字符串.toUpperCase()	// 返回字符串
String name = "abcdefg";
String nName = name.toUpperCase();
System.out.println(nName);	// ABCDEFG
```

##### toLowerCase()：字符/字符串转小写

```java
字符串.toLowerCase()	// 返回字符串
String name = "ABCDEFG";
String nName = name.toLowerCase();
System.out.println(nName);	// abcdefg
```

> 注意：方法返回新字符串，不修改原字符串



##### toCharArray：将字符串变成字符型数组

```java
字符串名.toCharArray();	// 返回字符数组
String str = "at7cH63OPbQ81";
char[] charray = str.toCharArray();	// {'a','t','7','H','6','3','O','P','b','Q','8','1'}
```



##### replace：查找替换字符串

```java
字符串.replace(字符串a,字符串b);	// 查找字符串a,替换为字符串b
String name = "a-b-c";
String nName = name.replace("-", "");	// 返回新字符串
System.out.println(nName);	// abcs
```



### Math：大多返回Double

##### ceil()、floor()：取整

```java
Math.ceil(值);	//向上取整
Math.ceil(1.3) //2
Math.floor(值);	//向下取整
Math.floor(1.3) //1
```



##### random() ：随机数

```java
System.out.println(Math.random());  //返回 0.0~1.0随机数
System.out.println(Math.random() * 100);  //返回0.0~100.0随机数
```


### Arrays：数组

##### Arrays.copyOf：数组扩容、缩容(0-n)


```java
Arrays.copyOf(数组名，新数组长度)	// 返回新数组,数据类型为传入类型
int[] nums = {1, 2, 3};
int[] newNums = Arrays.copyOf(nums, nums.length - 1);// 数组缩容一位,缩容到数组最后一个数值减一
System.out.println(Arrays.toString(newNums));    // 1,2
```

##### Arrays.copyOfRange：可以同时从前面开始缩容(n-n)

```java
Arrays.copyOfRange(数组名,从第几位(下标),新数组长度);
int[] nums = {1, 2, 3};
// 新数组缩容一位,缩容到数组最后一个数值减一
int[] newNums = Arrays.copyOfRange(nums, 1, nums.length - 1);
System.out.println(Arrays.toString(newNums));    // 2
```



##### Arrays.sort()：排序

```java
Arrays.sort(数组名);	// 只能升序(从小到大)
int[] nums = {123,414,12,425,23,1};
Arrays.sort(nums);
System.out.println(Arrays.toString(nums));	// [1, 12, 23, 123, 414, 425]
```



##### Arrays.toString()：打印数组

```java
System.out.println(Arrays.toString(res))	//打印res数组
```



### randomUUID:生成一个随机ID，类型为UUID类型

```java
String id = UUID.randomUUID();	//生成的是UUID类型无法保存
```

###### 所以保存为String需要toString：

```java
String id = UUID.randomUUID().toString;
System.out.println(id);	// b67d4acd-5cb7-49c7-8790-47520f1be35c，随机，想去掉"-"，需要replace
```





    filter：对数组进行过滤
    
    Objects.isNull:Object是官方的类，isNull是方法，可以进行对象的非空判断
    Book book1 = new Book();
    Book book2 = new Book();
    Book book3 = new Book();
    Book[] books = new Book[10]
    books[0] = book1;....	//三个都存进去
            for (int i = 0; i < books.length; i++) {	//遍历
        if(Objects.isNull(books[i])){	//判断数组books该位置是否为空，为空就是true
            return i;	//返回数组值为空的位置下标
        }
    }
    lambda表达式遍历：
            Arrays.stream(txs).forEach((s) -> {
        System.out.println(s);
    })
    
    lambda表达式的方法引用遍历：
            Arrays.stream(txs).forEach(System.out::println);
    
    ArrayList：
    泛型限定List数组存储的元素；
    ArrayList<泛型> 对象名 = new ArrayList<泛型>();
    ArrayList<String> names = new ArrayList<String>();
    
    添加：
            对象名.add();
    names.add("刘备");
    
    删除：
            对象名.remove();
    names.remove("刘备");
    
    获取指定下标元素：
            对象名.get();
    name = names.get(0);
    
    判断元素在集合中是否存在：
            对象名.contains();
    boolean x = names.contains("刘备");	 //返回布尔，x = true;
    
    查找某个元素内容对应的位置：
            对象名.indexOf();	 //从前往后走
    对象名.lastIndexOf();	//从后往前走
    int num = names.indexOf("刘备");	 //返回int，num = 0,没有返回-1;
    
    替换数组内某一元素：
            对象名.set(下标，新的值)
            names.set(0,张飞);
    
    清空数组：
            对象名.clear();
    names.clear;

instanceof 判断值的类型：
    int a = 0;
	if (a instanceof int){
        System.out.println("是int类型");
    }

    getClass() 判断对象所属的类型：
    Stirng name = "赵云"
    System.out.println(name.getClass());	// 输出class java.lang.String
    
    HashSet：
    
    日期API：
    Date,LocalDate,LocalTime,LocalDateTime
    创建日期对象，创建时间对象，创建日期时间对象
    
    Date：表示日期的数据类型。
    private Date birthday;	//Date类型的birthday Date是数据类型
    Date birthday = time.parse("1992-10-11");	//创建一个日期(Date)对象
    
    parse()：转换为日期对象
    parse("日期，以-分隔")
    parse("1999-1-1")
    
    LocalDate:
    创建实例对象1：
    LocalDate localDate = LocalDate.now();	//获取当前的时间
    创建实例对象2：
    LocalDate localDate2 = LocalDate.of(1999,1,1);
    创建实例对象3：
    LocalDate localDate3 = LocalDate.parse("2022-1-1");
    SimpleDateFormat:获取当前日期：
    格式：
    //创建一个日期对象
    Date 对象名 = new Date();
    Date withdrawalTime = new Date();
    //创建格式对象						//年-月-日 时:分:秒
    SimpleDateFormat 对象名 = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
    SimpleDateFormat time = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
    //转换保存为字符串，输出：
    String 字符串名 = 格式对象名.format(日期对象名);
    String thisTime = time.format(withdrawalTime);
    System.out.println(thisTime);
    
    Calendar类 获取日期：
    Calendar date = Calendar.getInstance();
    int year = date.get(1);	//已经写在类里面，收到1返回年份
    int month = c.get(Calendar.MONTH);
    int hour = c.get(Calendar.HOUR);
    int minute = c.get(calendar.MINUTE);
    int second = c.get(calendar.SECOND);
    
    String.valueOf 将字符数组转换为字符串：
            String.valueOf(数组,起始位置,转换多少个);
    //将char数组data中，由data[offset]开始取count个元素，转换成字符串。
    String.valueOf(data,0,n);	//n是上面获取的一共有多少个数据的int返回值。

System.currentTimeMillis()：显示当前毫秒数,返回long
    获取该代码块运行时间：起始记录一次，末尾记录一次，两次相减。
    接收并输出：
    long time = System.currentTimeMillis();
	System.out.println(time);


    FileReader：抓取文件数据
    FileReader reader = new FileReader(文件地址、文件名);
    
    read():每执行一次，读取一个字符
    管道对象.read();
    返回int，如果为-1，表明读到底了
    需要将返回值强转成char才能获取读到的字符：
    char c = 管道对象.read();
    
    read(char[]):设定读取多少个字符，字符数为数组大小。
    char[] num = new char[10];
    read(num);	//读取十个字符


    bufferedReader缓冲流(管道)：
    需要把FileReader包进去：	// 需要先有FileReader
    BufferedReader 对象名 = new BufferedReader(FileReader对象);
    BufferedReader buffread = new BufferedReader(reader);
    
    readLine(): 一次读取一行
    方法返回一个String，如果返回null，表明读到底了
    String s = bufferedReader.readLine();	//将读取的一行文字保存到Stirng s中。
    System.out.println(s);	//输出第一行
    System.out.println(bufferedReader.readLine());	//读取下一行并输出。
    
    close():关闭管道
    会将里面的FileReader一并关闭。