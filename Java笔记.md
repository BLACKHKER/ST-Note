# JavaSE

## 基本/引用数据类型

### String、StringBuffer、StringBuilder的区别

#### String 类：

String 类是一个不可变的字符串类型，它的实现原理是使用一个 final 修饰的字符数组来存储字符串。

一旦字符串被初始化后，其内容就不能再被修改，如下所示：

```java
String str = "Hello World!";
str = str + "Welcome to Java!";
```

在上述示例中，变量 str 虽然通过 "+" 操作符连接了两个字符串，但其实它仍然代表了一个新的字符串对象，原来的字符串对象已经被释放，每次对字符串进行操作(如追加、替换等)，都会生成一个新的字符串对象。String 类中的所有方法都不会修改原来的对象，而是返回一个新的对象。

因此，若需要频繁对字符串进行操作，使用 String 类会带来性能问题。





#### StringBuffer 类：

StringBuffer线程安全，每个 StringBuffer 方法上添加 synchronized 关键字来保证方法的原子性和同步性。

StringBuffer 允许修改里面的内容，实现原理是除了使用了一个字符数组来存储字符串的值，还有两个变量：表示字符数组的长度 length，表示字符数组的容量 capacity。

当 StringBuilder 的 length 超过其 capacity 时，其会自动扩容，重新分配更大的内存空间来存储新增加的字符。扩容的方式可以通过指定初始容量和增长因子(JDK8默认2倍，JDK9为约1.5倍)来实现，示例如下：

```java
StringBuffer sb = new StringBuffer(10); // 初始容量为10
sb.append("Hello");
```

##### 注意：

StringBuffer是线程安全的，每次使用都要加载锁，因此在并发高的场景中，建议使用 StringBuilder。





#### StringBuilder 类：

StringBuilder 与 StringBuffer 类似，也支持修改存储在其中的字符串。不同的是，它并不是线程安全的，因此在单线程环境下运行时，拼接字符串时使用 StringBuilder 会比 StringBuffer 更高效。

StringBuilder 在实现上与 StringBuffer 基本相同，有两个变量：表示字符数组的长度 length，表示字符数组的容量 capacity。



以下是一个简化的扩容算法示例，用于说明这个过程：

1. 计算新容量：`newCapacity = oldCapacity + (oldCapacity >> 1)`（即原始容量的 1.5 倍）
2. 如果新容量小于所需的最小容量（即新字符串长度），则将新容量设置为最小容量。
3. 扩容数组以容纳新字符串。





#### 总结：

String、StringBuffer、StringBuilder 在实现时，都使用了char类型的字符数组来存储字符串，不同之处在于它们是否支持修改以及线程安全等问题。

String 适用于需要对字符串进行读取、比较、哈希等操作的场景。由于 String 对象是不可变的，因此可以被多个线程安全地共享和重用。

StringBuffer 适用于多线程环境下的字符串处理，例如在多线程环境下进行字符串拼接、修改等操作时，可以使用 StringBuffer 来保证线程安全。

StringBuilder 适用于单线程环境下的字符串处理，例如在单线程环境下进行字符串拼接、修改等操作时，可以使用 StringBuilder 来获得更好的性能。





---





## List&Map

### ArrayList和LinkedList的区别

#### 数据结构

ArrayList是基于动态数组的数据结构，它的内部实现是一个数组，通过下标来访问元素，它支持随机访问，但在插入和删除时比较慢。

LinkedList是基于链表的数据结构，它的内部实现是一个双向链表，通过前驱和后继节点来访问元素，它支持插入和删除操作比较快，但在随机访问时比较慢。





#### 插入和删除操作

ArrayList在插入和删除操作时需要移动数组中的元素，这样的操作比较耗时，特别是在数组中间插入或删除元素时更为明显。

LinkedList在插入和删除操作时只需要改变前驱和后继节点的指针即可完成，因此在链表中间插入或删除元素时比较快。





#### 内存分配

ArrayList需要预分配一定大小的内存空间，当元素数量超过预分配的大小时，需要重新分配更大的内存空间，然后将原来的元素复制到新的数组中，这样大量的内存复制操作比较耗时。

LinkedList在新增元素时只需要申请一个新节点的内存空间，因此它比ArrayList更适合频繁的新增和删除操作。





#### 随机访问

ArrayList通过下标来访问元素，因此支持随机访问，可以通过get方法快速获取元素，但在插入和删除时需移动数组元素，比较耗时。

LinkedList不支持随机访问，因为它是基于链表的数据结构，只能从头节点或尾节点开始顺序访问元素，因此访问元素比较耗时。





#### 功能区分

LinkList实现了堆栈和队列的功能，堆栈是一种后进先出(LIFO)的数据结构，可以通过 push() 方法将元素压入堆栈中，通过 pop() 方法将元素从堆栈中弹出。在 LinkedList 中，可以通过 push() 方法将元素添加到链表的头部，通过 pop() 方法从链表的头部删除元素，从而实现堆栈的功能：

```java
LinkedList<String> stack = new LinkedList<>();
stack.push("A");
stack.push("B");
stack.push("C");
String top = stack.pop(); // "C"
```

队列是一种先进先出(FIFO)的数据结构，可以通过 offer() 方法将元素添加到队列尾部，通过 poll() 方法从队列头部获取并删除元素。在 LinkedList 中，可以通过 offer() 方法将元素添加到链表的尾部，通过 poll() 方法从链表的头部获取并删除元素，从而实现队列的功能：

```java
LinkedList<String> queue = new LinkedList<>();
queue.offer("A");
queue.offer("B");
queue.offer("C");
String head = queue.poll(); // "A"
```

ArrayList并没有实现堆栈、队列的功能





#### 总结：

当需要随机访问和读取时，或者数据量不大的情况下，使用ArrayList比较合适；当需要频繁插入、删除或者数据量较大时，使用LinkedList比较合适。

 





### HashTable、HashMap、ConcurrentHashMap的区别

> 功能性、线程安全性和性能等方面存在不同

#### HashTable

HashTable是Java中最早的用于实现Map接口的类，在Java 1.0中就已经存在。它可以保证存储的数据不会出现空值（null）。HashTable内部实现了线程安全的机制，但在多线程环境下，其同步操作是在整个集合对象上进行的，因此效率较低，而且并发性能不如ConcurrentHashMap。





#### HashMap

HashMap是Java中最常用的Map实现类，采用了一种称为"拉链法"的实现方式。HashMap支持空值的存储，可以存储多个null值。HashMap的实现不是线程安全，因此在并发环境下需要加锁或者使用synchronized关键字进行同步处理，因此在高并发情况下性能差于ConcurrentHashMap。





#### ConcurrentHashMap

ConcurrentHashMap是线程安全的HashMap实现类，它采用了锁分段机制，将整个Map划分为多个小的segment区域，在每个segment区域内部可以保证线程安全。并发性能相对于Hashtable和HashMap要高(尤其对于写多读少的并发情形)，且无需像HashTable那样对整个Map进行同步加锁操作，因此在高并发情况下其性能更优。





#### 总结：

HashTable、HashMap和ConcurrentHashMap这三个集合类的主要区别在于线程安全性和性能上，具体在不同场景下应选取不同的数据结构进行使用，在考虑线程安全和性能的基础上选择性能最优的Map集合类可以提升程序的执行效率。







### HashMap底层实现(如何解决Hash冲突)

> 从JDK8开始，底层保存数据变成了数组+链表/数组+红黑树

#### 数组+链表

数组中元素的位置在算法中一般叫做桶，通过pull方法向HashMap存放数据的时候，HashMap会根据Key的Hash值，进行取模的运算，取模的结果就是放到哪一个桶中，或者数组元素存放的位置，但是存在Hash冲突的问题。就是不同的Hash值取模后可能结果一致，那么就会导致数据存放到了一个数组下标(桶)上，在这种情况下，HashMap会将这些具有相同index的元素组织成链表，链表中的每个节点都包含一个Key-Value对。





---





## 线程

### 线程的创建方式

#### 继承Thread类

创建线程的最简单方式是继承Thread类，重写它的run()方法，并创建一个Thread对象来启动线程：

```java
public class MyThread extends Thread {

    /**
     * 线程执行的方法体
     */
    @Override
    public void run() {
        System.out.println("MyThread is running.");
    }

    public static void main(String[] args) {
        // 创建子类(继承了Thread的类)对象，用该对象调用start方法启动线程
        MyThread thread = new MyThread();
        thread.start();
    }
}
```





#### 实现Runnable接口

创建线程的第二种方式，将一个Runnable实现类的实例传递给Thread类的构造函数并调用start()方法启动线程：

```java
public class MyRunnable implements Runnable {

    /**
     * 线程执行的方法体
     */
    @Override
    public void run() {
        System.out.println("MyRunnable is running.");
    }

    public static void main(String[] args) {
        // 将Runnable实现类的实例传递给Thread类的构造函数并调用start()方法启动线程
        MyRunnable runnable = new MyRunnable();
        Thread thread = new Thread(runnable);
        thread.start();
    }
}
```





#### 实现Callable接口

Callable接口与Runnable接口的主要区别在于它可以返回一个值并且可以抛出异常。

实现Callable接口，可以在执行完毕后通过Future对象获取线程的结果，也可以利用该接口实现线程的异常处理：

```java
public class MyCallable implements Callable<Integer> {

    /**
     * 线程执行该方法方法体中的内容,该方法包含返回值(Integer类型)
     */
    @Override
    public Integer call() throws Exception {
        // 计算1-10的和
        int sum = 0;
        for (int i = 1; i <= 10; i++) {
            sum += i;
            // 模拟耗时操作
            Thread.sleep(100);
        }
        return sum; // 返回结果
    }

    public static void main(String[] args) {
        // 创建Callable实现类的实例
        MyCallable myCallable = new MyCallable();

        // 将实现类的实例放入FutureTask中，用于获取执行结果
        // FutureTask是一种可以获取Callable执行结果的容器
        FutureTask<Integer> task = new FutureTask<Integer>(myCallable);

        // 开启一个新的线程，该线程会在后台执行call方法中的代码，并返回call方法的执行结果
        new Thread(task).start();
        try {
            // 调用get()方法获取FutureTask实例中存储的计算结果，该方法会阻塞当前线程，
            // 直到后台线程执行结束并返回结果。
            // 由于在MyCallable中的计算过程中执行了Thread.sleep(100)语句，
            // 因此get()方法会阻塞至少100毫秒以等待计算结果。
            Integer result = task.get(); // 获取执行结果
            System.out.println("Result is " + result);  // 55
        } catch (InterruptedException | ExecutionException e) {
            // 捕获可能抛出的异常，并打印栈信息
            e.printStackTrace();
        }
    }
}
```

MyCallable实现了Callable接口，重写了call()方法以执行线程所需的操作，并返回计算结果。

在主线程中，通过创建FutureTask的对象task，并将实例作为Thread的参数，启动线程；

最后通过调用task对象的get()方法，获取线程执行的结果。

需要注意的是，get()方法会阻塞当前线程，直到线程执行完毕并返回结果。如果线程在执行期间抛出了异常，则该异常将被封装并抛出ExecutionException异常。





#### 通过线程池启动多线程

通过Executor的工具类可以创建三种类型的普通线程池：

|            类型             |       解释       |
| :-------------------------: | :--------------: |
|    FixThreadPool(int n)     | 固定大小的线程池 |
|  SingleThreadPoolExecutor   |     单线程池     |
|     CashedThreadPool()      |    缓存线程池    |
| ScheduledThreadPoolExecutor |    定时线程池    |

需要注意的是，Java中的线程是轻量级的，通过创建低级别的操作系统语言来实现，创建线程的成本较低。

但是，创建过多的线程会产生额外的消耗，从而导致系统性能下降。

在实际应用中，建议使用线程池来管理线程以提高性能和可维护性。







### synchronized(/sɪŋkrənaɪzd/)实现原理

synchronized的底层实现是使用了一种叫做“内部锁”或“监视器锁”的机制，用来实现多线程之间的同步。

具体来说，当一个线程进入synchronized修饰的方法或代码块时，会尝试获取对象锁或类锁(静态synchronized方法)，如果锁没有被其他线程获取，则该线程获取锁，并继续执行方法或代码块中的内容；如果锁已经被其他线程获取，则该线程会进入阻塞状态，等待锁的释放。

内部锁的实现基于Java中每个对象都有一个头信息，用来存储对象的hashcode、锁标记、GC标记等信息。当一个线程进入synchronized块时，会尝试获取对象的锁标记，如果标记为0，则表示未被获取，当前线程获取到锁，并将该标记设置为线程ID；否则表示锁已经被其他线程获取，当前线程进入阻塞状态，等待锁的释放。

当一个线程执行完synchronized块中的内容，会将锁标记释放，并唤醒等待此锁的其他线程，此时其他线程又可以尝试获取锁。

需要注意的是，由于每个对象都有一个自己的内部锁，因此synchronized的同步粒度是对象级别的，也就是说对于同一个对象，不同的synchronized代码块之间仍然是互斥的，而对于不同的对象，synchronized代码块之间则不存在互斥关系。







### wait与sleep的区别

wait和sleep都是Java中用来控制线程执行流程的关键字，但它们有以下几个不同点：

#### 所属包及其功能

wait()是Object类中的方法，用于线程间的通信，而sleep()是Thread类中的方法，用于控制线程的休眠。





#### 锁的释放机制

wait()函数会释放当前线程持有的锁，进入等待状态，直到其他线程调用notify()或notifyAll()唤醒线程，或者等待时间到期，自行唤醒线程。而sleep()函数则不会释放当前线程持有的任何锁，执行过程中，其他任何线程都无法获得该锁。





#### 调用方法

wait()函数只能在synchronized块或者synchronized方法中调用，否则会抛出IllegalMonitorStateException异常，而sleep()则可以在任何地方调用，不会抛出该异常。





#### 唤醒方式

wait()函数执行后只有在等待期间其他线程通过notify()或notifyAll()方法唤醒了当前线程，该线程才能继续执行。而sleep()函数则不受其他线程的干扰，到时间后自动唤醒当前线程。



#### 总结：

在线程间通信时应该使用wait()方法，而在控制线程休眠时应该使用sleep()方法。在使用wait()方法时，应该注意在synchronized块或者synchronized方法中调用，并且在调用前获取到相应的锁，否则会抛出IllegalMonitorStateException异常。而使用sleep()方法时，应该意识到当前线程并未释放任何锁，因此应该避免在多线程环境中使用sleep()方法。







### 阻塞与非阻塞

> 阻塞和非阻塞是指一个线程执行操作时，如果操作不能完成，线程是等待还是继续执行的两种不同方式
>
> 阻塞式 IO 每个连接需要一个线程进行处理，而非阻塞式 IO 可以使用单一的线程来处理多个通道的 IO 请求

#### 阻塞式调用

在阻塞式调用中，如果被调用的函数没有得到结果之前，那么该函数会一直等待，当前线程会被阻塞。

在等待的时间内，线程不能执行其他的操作。当被调用的函数完成操作后，这个线程才会继续执行任务。





#### 非阻塞式调用

在非阻塞式调用中，如果被调用的函数不能立即得到结果，该函数也并不会一直等待，而是立即返回，当前线程可以继续执行其他操作。同时被调用的函数会通过异步的方式来完成操作，完成之后再通知当前线程。

##### 底层原理：

非阻塞式IO在 Java 中通常使用 NIO(New IO)技术实现，其核心是 Selector(选择器)和 Channel(通道)两个概念。

在 NIO中，Selector可以注册多个Channel，并监听这些Channel上是否有事件就绪，从而实现非阻塞式IO。

当一个Channel执行非阻塞式 IO 操作时，如果该操作不能得到结果，该方法会立即返回，并不会一直等待。

在未来某个时间，当 Channel 上发生了 IO 事件时，Selector 会通知 Channel 对应的线程，该线程再从 Channel 中读取或写入数据。

在 NIO 中，不会为每个 Channel 创建一个独立的线程来执行 IO 操作。相反，可以使用单一的线程来处理多个 Channel 上的事件，这可以避免线程数量的增长和上下文切换的开销，提高程序的并发性和效率。

非阻塞式 IO 不一定会为每个调用创建一个新的线程。通常情况下，只需要一个线程来处理多个通道的 IO 请求。这也是非阻塞式 IO 与阻塞式 IO 的最大区别之一。





#### 总结：

可以将阻塞和非阻塞方式类比于排队和取号，阻塞式调用就像是排队，如果前面的任务没有完成，你就必须等待；而非阻塞式调用就像取号，你可以自由地选择不等待，继续做其他事情，等结果出来后再取回结果。

阻塞一般会造成进程或线程的挂起，会浪费 CPU 等资源，因此在编写高并发程序和网络通信程序时，通常会采用非阻塞IO等技术来提高程序的性能和效率。







### 死锁

> 互持资源、相互等待就是死锁

#### 概念

当一组进程或线程中的每一个都在等待一个只有该组中另一个进程才能引起的事件时，我们就说这组进程或线程 死锁了。死锁的最简单情形是：线程 A 持有对象 X 的独占锁，并且在等待对象 Y 的锁，而线程 B 持有对象 Y 的独占锁，却在等待对象 X 的锁。除非有某种方法来打破对锁的等待（Java 锁定不支持这种方法），否则死锁的线程将永远等下去。





#### 触发死锁的必要条件

##### 互斥条件（Mutual Exclusion）

指某个资源在任一时刻只能被一个线程（或进程）占用。如果其他线程请求该资源，请求者必须等待，直到资源被占有的线程释放为止。



##### 占有且等待（Hold and Wait）

指一个线程已经占有一些资源，但又提出了新的资源请求。由于新请求的资源已被其他线程占用，因此该线程被迫等待。在等待期间，仍继续占有已获得的资源。



##### 不可抢夺（No Preemption）

指已经占有资源的线程无法被强制释放资源，除非该线程主动释放资源。



##### 循环等待（Circular Wait）

指存在一个线程等待序列（如线程A等待线程B，线程B等待线程C，线程C等待线程A），这些线程之间形成一种循环链，其中的每个线程都在等待其他线程释放资源。





#### 避免死锁的方法

> 打破四个必要条件之一即可

##### 互斥条件

互斥条件不可打破，因为线程本身就是通过互斥保证线程安全的，不可打破



##### 占有且等待(占且)

一次性申请所需的所有资源，就不存在占有且等待的情况了



##### 不可抢夺

使用已经占用部分资源的线程进一步去申请其他资源的时候，如果申请不到资源，则释放当前线程的所有资源



##### 循环等待

通过申请资源的流程进行预防，按顺序申请资源。

可以为资源分配一个唯一的序号，确保线程根据资源序号的递增顺序申请资源。

资源是有线性顺序的，可以先申请序号比较小的，再申请序号比较大的线性之后就不存在循环等待的问题。





#### 实例

```java
package com.blackhker.study.javase.thread;

/**
 * @Author BLACKHKER
 * @Date 2023/6/10
 * @ClassName: DeadlockExample
 * @Description: 死锁
 * @Version 1.0
 */

/**
 * DeadlockExample类有两个方法 method1() 和 method2()，分别需要获取 lock1 和 lock2 两个对象的锁。
 * 当线程1执行 method1() 方法时，首先获取 lock1 的锁，然后尝试获取 lock2 的锁；
 * 而线程2执行 method2() 方法时，则是相反的顺序，首先获取 lock2 的锁，然后尝试获取 lock1 的锁。
 * 当线程1获取了 lock1 的锁之后，线程2获取了 lock2 的锁，但是由于两个线程都需要获取对方持有的锁，因此两个线程都无法继续执行下去，形成死锁。
 */
public class DeadlockExample {

    private static final Object lock1 = new Object();
    private static final Object lock2 = new Object();

    public static void main(String[] args) {
        
        Thread thread1 = new Thread(new Runnable() {
            @Override
            public void run() {
                method1();
            }
        });

        Thread thread2 = new Thread(new Runnable() {
            @Override
            public void run() {
                method2();
            }
        });

        thread1.start();
        thread2.start();
    }

    public static void method1() {
        synchronized (lock1) {
            System.out.println("线程一获取到锁1");

            try {
                // 休眠1秒
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

            synchronized (lock2) {
                System.out.println("线程二获取到锁2");
            }
        }
    }

    public static void method2() {
        synchronized (lock2) {
            System.out.println("线程二获取到锁2");

            try {
                // 休眠1秒
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

            synchronized (lock1) {
                System.out.println("线程二获取到锁1");
            }
        }
    }
}
```







### start()方法和run()方法的区别

> Thread 类提供了两个方法可以用于启动线程：start() 和 run() 方法
>
> start() 方法会启动一个新线程并执行run()方法中的代码，而run()方法则是某个线程的执行体入口点。

#### start() ：

用于启动一个新线程，并使新线程开始执行 run() 方法中的代码。当 start() 方法被调用时，它会在后台启动一个新的线程并立即返回，不会等待该线程执行完毕。在新线程启动后，系统会自动调用 run() 方法，并在新线程中执行 run() 方法中的代码。





#### run()：

 方法是线程执行体的入口点。当一个线程被启动后，它会执行 run() 方法中的代码。

如果直接调用 run() 方法而不使用 start() 方法启动一个新线程，那么 run() 方法就普通地运行在当前线程中，而不会开启一个新线程。





#### 示例：

```java
public class MyThread extends Thread {
    public void run() {
        System.out.println("线程执行");
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread t = new MyThread();
        t.start(); // 启动一个新线程
    }
}
```

在上述代码中，MyThread 继承了 Thread 类并定义了它的线程执行体，当启动线程时，使用 start() 方法来启动一个新线程，run() 方法中的代码会在新线程中执行。

如果直接调用run方法，相当于在当前线程执行，不会去新开辟一个线程去执行run方法了

```java
MyThread t = new MyThread();
t.run(); // 直接调用 run() 方法，不会开启新线程
```

那么线程将不会开启新线程，run() 方法中的代码会在当前线程中直接执行。





#### 总结：

调用 start() 方法会开启一个新线程，而直接调用 run() 方法则不会。

尝试直接调用start()方法会抛出 IllegalThreadStateException 异常。

需要注意的是，Thread 类中的 run() 方法只是一个普通的方法，不具备多线程的特性。只有通过 start() 方法来启动线程，才能使线程具有并发执行的能力，并改变线程的执行状态（如阻塞、等待等）。







### happens-before(之前发生)

Happens-before是Java内存模型中的一个关键概念，在多线程编程中用于描述并发执行的顺序，它是指在一个线程中，如果一个操作A先于另一个操作B执行，那么操作B一定能看到操作A的结果。

如果事件A Happens-Before事件B，那么A所执行的所有操作的结果对其他线程（或JVM）是可见的，并且在B所执行的所有操作之前可见。换句话说，线程中执行操作A的所有结果对该线程中执行B操作的结果产生了影响，确保了多线程程序的正确性。

#### Happens-Before关系的几种情况

##### 程序的顺序规则：

在一个线程中，按照程序顺序，前面的操作Happens-Before后面的操作



##### volatile(关键字)变量规则：

对一个volatile变量的写操作Happens-Before于对它的任何读操作。



##### 传递性规则：

如果操作AHappens-Before操作B，操作BHappens-Before操作C，那么操作AHappens-Before操作C。



##### 管程(lock)规则：

一个unlock操作Happens-Before与之前的lock操作。



##### 线程启动规则：

Thread.start()的方法Happens-Before于新线程中任何操作。



##### 线程终止规则：

一个线程的终止Happens-Before于其他线程检测到该线程已经终止的事件。意思是，在一个线程结束后，其他线程可以看到该线程的终止标志，以确保线程的正确关闭。







### volatile实现原理

##### 基本概念：

volatile是一个关键字，用来标记一个变量，告诉编译器这个变量可能会被多个线程同时访问，并且在访问时不要进行优化。

volatile的作用是让程序员明确地告诉编译器，这个变量可能发生变化，需要注意其可见性和顺序性。



##### 具体实现：

编译器在处理volatile变量时，会尽量避免对其进行优化。在多线程环境下，每个线程访问volatile变量时，会将其值从内存中读取，并在修改后立即写回内存，以保证线程之间的正确性和一致性。此外，在编译器生成的汇编代码中，对volatile变量的读取和修改指令会被声明为“volatile读”和“volatile写”，保证了其可见性和顺序性。

总之，volatile关键字的实现原理是通过告诉编译器该变量可能被多个线程同时访问，并将其可见性和顺序性保障在编译器生成的汇编代码中，以确保程序的正确性和一致性。







### ThreadLocal

##### 概念

ThreadLocal是Java中的一个类，用于创建线程范围内的变量。它可以让每个线程都拥有一个独立的变量副本，避免了线程间的数据共享和竞争，在多线程编程中起到了很大的作用。ThreadLocal常用于需要跨多个方法和类传递数据的场景，例如Web应用程序中的用户身份验证和事务管理等。



##### 具体使用方式

可以通过ThreadLocal类的set()方法来设置变量的值，通过get()方法获取变量的值。每个线程都可以通过一次set()方法调用来设置自己的变量副本的值，并且获取的值也仅仅是自己的变量副本的值。当线程结束时，它持有的变量也随之消失，不会影响其他线程。如果线程在使用完ThreadLocal变量后没有清除它，可能会导致内存泄漏的问题。

另外，需要注意的是，ThreadLocal是线程安全的，但是它并不是用来解决多线程并发问题的。它只是提供了一种线程范围内的数据共享方式，用于不同线程之间进行数据隔离，要解决线程安全问题还需要使用其他方式。







### Java常见的线程池及使用场景

#### 概念

线程池就是首先创建一些线程，它们的集合称为线程池。使用线程池可以很好地提高性能，线程池在系统启动时即创建大量空闲的线程，程序将一个任务传给线程池，线程池就会启动一条线程来执行这个任务，执行结束以后，该线程并不会死亡，而是再次返回线程池中成为空闲状态，等待执行下一个任务。

 



#### 工作机制

在线程池的编程模式下，任务是提交给整个线程池，而不是直接提交给某个线程，线程池在拿到任务后，就在内部寻找是否有空闲的线程，如果有，则将任务交给某个空闲的线程。

 一个线程同时只能执行一个任务，但可以同时向一个线程池提交多个任务。

 



#### 使用线程池的原因

多线程运行时间，系统不断的启动和关闭新线程，成本非常高，会过渡消耗系统资源，以及过渡切换线程的危险，从而可能导致系统资源的崩溃。这时，线程池就是最好的选择了。





#### ExecutorService

##### SingleThreadExecutor（单线程池）

> 该线程池只有一个线程，适用于需要顺序执行任务的情况

###### 优点

1. 重用线程：单线程池可以重用线程，避免了频繁创建和销毁线程的开销。如果使用直接创建线程的方式，每次需要执行任务时都需要创建一个新的线程，执行完成后再销毁线程，这样会产生较大的开销。使用线程池可以避免这种开销，提高程序的执行效率。
2. 线程管理：线程池可以更好地管理线程，包括线程的创建、销毁、调度等。单线程池只维护一个工作线程，因此可以更好地控制线程的执行顺序和状态，避免出现竞态条件和死锁等问题。
3. 提供任务队列：线程池可以提供任务队列，用于存储尚未执行的任务。当工作线程正在执行任务时，可以将后续的任务存储在任务队列中，等待工作线程空闲时再执行。这样可以避免任务的丢失和延迟执行的问题，提高程序的稳定性和可靠性。
4. 提供线程池管理功能：线程池还可以提供线程池管理功能，包括线程池的创建、销毁、大小调整等。这样可以更好地管理程序中的线程池，避免出现线程池大小不合适、线程池满载等问题。

###### 实例：

```java
/**
 * 单一线程池
 */
public static void singleThreadExecutor() {

    // 创建单一线程池
    ExecutorService singleThreadExecutor = Executors.newSingleThreadExecutor();

    // 循环提交10个任务执行
    for (int i = 0; i < 10; i++) {
        final int index = i;
        singleThreadExecutor.execute(new Runnable() {
            @Override
            public void run() {
                try {
                    System.out.println(index);
                    Thread.sleep(2000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });
    }

    // 关闭线程池
    singleThreadExecutor.shutdown();
}
```



##### FixedThreadPool（固定大小线程池）

> 提高程序效率和节省创建线程时所耗的开销的线程池。但是，在线程池空闲时，即线程池中没有可运行任务时，它不会释放工作线程，还会占用一定的系统资源。

该线程池固定线程数量，当任务提交到线程池中时，如果当前线程池中的线程数小于指定数量，就会创建新的线程来执行任务。如果线程池中的线程数已经达到指定数量，那么该任务就会等待线程池中有空闲的线程才会执行。适用于任务量稳定的情况。

###### 实例：

```java
/**
 * 固定大小的线程池
 */
public static void fixedThreadPool() {
    // 创建一个固定大小为3的线程池
    ExecutorService fixedThreadPool = Executors.newFixedThreadPool(3);

    // 循环提交10个任务给线程池执行
    for (int i = 0; i < 10; i++) {
        final int index = i; // 定义一个final变量存储i的值
        // 将任务提交给线程池执行
        fixedThreadPool.execute(new Runnable() {
            // 实现Runnable接口的run方法来定义任务的具体执行逻辑
            @Override
            public void run() {
                try {
                    System.out.println(index); // 输出任务编号
                    Thread.sleep(2000); // 模拟任务执行需要2秒的时间
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });
    }

    // 关闭线程池
    fixedThreadPool.shutdown();
}
```



##### CachedThreadPool（缓存线程池）

> 在使用时，一定要注意控制任务的数量，否则，由于大量线程同时运行，很有会造成系统瘫痪。

该线程池不限制线程数量，当有新的任务提交到线程池中时，如果当前线程池中有空闲的线程，就会直接使用空闲的线程来执行任务。如果没有空闲的线程，就会创建新的线程来执行任务。当线程空闲时间超过60秒，则会被销毁。适用于任务量较小且需要快速响应的情况。

###### 实例：

```java
/**
 * 缓存线程池
 */
public static void cachedThreadPool() {

    // 创建一个可缓存的线程池
    ExecutorService cachedThreadPool = Executors.newCachedThreadPool();

    // 循环创建10个任务
    for (int i = 0; i < 10; i++) {
        // 为每个任务创建一个索引
        final int index = i;
        try {
            // 让线程休眠一段时间，以便观察执行顺序
            Thread.sleep(index * 1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        // 提交任务到线程池中
        cachedThreadPool.execute(new Runnable() {
            @Override
            public void run() {
                // 输出任务的索引
                System.out.println(index);
                // 输出当前线程池中的线程数
                ThreadPoolExecutor executor = (ThreadPoolExecutor) cachedThreadPool;
                System.out.println("当前线程池中线程的数量：" + executor.getPoolSize());
            }
        });
    }

    // 关闭线程池
    cachedThreadPool.shutdown();
}
```



##### ScheduledThreadPool（定时任务线程池）

该线程池用于执行定时任务和周期性任务，可以指定线程数，任务被放入一个任务队列中，由线程池中的线程按照指定的时间执行任务。适用于需要定时执行任务的情况。

###### 实例1：

```java
/**
 * 计划线程池，延迟x秒执行线程
 */
public static void scheduleThreadPool1() {

    System.out.println("延迟3秒执行");

    // 创建一个大小为5的ScheduledExecutorService线程池
    ScheduledExecutorService scheduledThreadPool = Executors.newScheduledThreadPool(5);

    // 延迟3秒后执行任务
    scheduledThreadPool.schedule(new Runnable() {
        @Override
        public void run() {
            System.out.println("执行线程");
        }
    }, 3, TimeUnit.SECONDS);

    // 关闭线程池
    System.out.println("关闭线程");
    scheduledThreadPool.shutdown();
}
```

###### 实例2：

```java
/**
 * 延迟x秒-间隔y秒执行一次
 */
// 定义一个方法，用于示例定时任务和周期性任务
public static void scheduleThreadPool2() {

    System.out.println("延迟1秒后，每隔3秒执行一个任务");

    // 创建一个大小为5的ScheduledExecutorService线程池
    ScheduledExecutorService scheduledThreadPool = Executors.newScheduledThreadPool(5);

    // 延迟1秒后，每隔3秒执行一个任务
    scheduledThreadPool.scheduleAtFixedRate(new Runnable() {
        int i = 0;

        @Override
        public void run() {
            // 判断计数器是否小于3
            if (i < 3) {
                i++;
                System.out.println("执行线程");
            } else {
                // 如果计数器大于等于3，则关闭线程池，并打印关闭线程的消息
                scheduledThreadPool.shutdown();
                System.out.println("关闭线程");
            }
        }
    }, 1, 3, TimeUnit.SECONDS);
}
```





#### ThreadPoolExecutor

> 实现线程池的一个类，它提供了一系列的方法和参数来控制线程池的大小、任务队列、线程池饱和策略等
>

ThreadPoolExecutor 类可以自定义线程池的核心线程数、最大线程数、线程空闲时间和任务队列等参数，以满足不同的业务需求。同时，ThreadPoolExecutor 类还提供了一系列的方法来提交任务、关闭线程池、获取线程池状态等操作。

###### 常用的 ThreadPoolExecutor 方法：

|          方法名           |                  功能                  |
| :-----------------------: | :------------------------------------: |
| execute(Runnable command) |        提交一个任务给线程池执行        |
|        shutdown()         |  关闭线程池，等待已提交的任务执行完毕  |
|       shutdownNow()       | 立即关闭线程池，尝试终止正在执行的任务 |
|     getActiveCount()      |  获取当前线程池中正在执行任务的线程数  |
|  getCompletedTaskCount()  |       获取线程池中已完成的任务数       |
|       getPoolSize()       |        获取线程池中当前的线程数        |
|        getQueue()         |   获取线程池中正在等待执行的任务队列   |

通过使用 ThreadPoolExecutor 类，我们可以更加灵活地控制线程池的大小和行为，从而避免线程创建和销毁的开销，提高应用程序的性能和稳定性。

###### 实例：

> 最大线程 - 核心线程 = 非核心线程
>
> 任务队列有很多种：new ArrayBlockingQueue<>(num)、new LinkedBlockingQueue<Runnable>()等

```java
/**
 * 使用 ThreadPoolExecutor 创建线程池
 */
public static void threadPoolExecutor() {

    int corePoolSize = 5;	// 核心线程池大小(5个线程)
    int maxPoolSize = 10;	// 最大线程池大小(10个线程)
    long keepAliveTime = 60L;	// 空闲线程保持存活时间(60)
    TimeUnit unit = TimeUnit.SECONDS;	// 存活时间的单位(秒)
    BlockingQueue<Runnable> workQueue = new ArrayBlockingQueue<>(10);	// 任务队列

    // 创建一个包含1个线程的线程池
    ThreadPoolExecutor executor = new ThreadPoolExecutor(corePoolSize, maxPoolSize, keepAliveTime, unit, workQueue);

    // 循环创建10个任务
    for (int i = 1; i <= 10; i++) {
        // 为每个任务创建一个索引
        final int index = i;
        try {
            // 让线程休眠一段时间，以便观察执行顺序
            Thread.sleep(index * 1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        // 添加一个Runnable任务到线程池
        executor.execute(new Runnable() {
            @Override
            public void run() {
                try {
                    System.out.println(index); // 输出任务编号
                    System.out.println("Task executed by " + Thread.currentThread().getName());
                    Thread.sleep(2000); // 模拟任务执行需要2秒的时间
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });
    }

    // 关闭线程池
    executor.shutdown();
}
```





#### 总结

##### ExecutorService和ThreadPoolExecutor创建线程的区别：

1. ExecutorService是一个接口，它定义了线程池的一些基本操作，如submit()、shutdown()等。ThreadPoolExecutor则是实现了ExecutorService接口的类，提供了创建和管理线程池的具体实现。
2. ThreadPoolExecutor允许你更具体地配置线程池，它有更多的参数和选项，比如corePoolSize、maximumPoolSize、keepAliveTime等。这使得ThreadPoolExecutor相对灵活且可定制。而通过ExecutorService的静态工厂方法，如newFixedThreadPool()、newCachedThreadPool()等创建线程池时，会有一些默认的配置，某些方面可能不如ThreadPoolExecutor灵活。

实际上，当调用ExecutorService的静态工厂方法（如newFixedThreadPool()）时，内部会创建一个ThreadPoolExecutor实例，并将其返回。因此，这两者之间的最大区别在于定制程度。如果你需要灵活定制线程池，使用ThreadPoolExecutor可能更适合。若需要默认配置的线程池，则使用ExecutorService的静止工厂方法。





---





## MySQL

### 常见的SQL优化方法

1. #### 索引优化

   通过建立合适的索引（主键索引、唯一索引、普通索引、全文索引等），可加快数据库查询速度。

   

   

2. #### 查询优化

   避免全表扫描，尽可能减小SQL语句返回的结果集大小，通过合理运用JOIN、WHERE等操作符减少查询结果集大小，首先应考虑在 where 及 order by 涉及的列上建立索引。

   ##### 在 where 子句中尽量避免下列几种情况，否则将导致引擎放弃使用索引而进行全表扫描：

   ###### 对字段进行 null 值判断：  

   ```sql
   SELECT id FROM t WHERE num IS NULL
   ```

   可以在num上设置默认值0，确保表中num列没有null值，然后这样查询：  

   ```sql
   SELECT id FROM t WHERE num = 0
   ```

   ###### 使用 != 或 <> (两个都是不等于)操作符：

   ```sql
   SELECT department_name, department_id
   FROM departments
   WHERE department_id <> 10;
   ----------------------------------------
   SELECT name, score
   FROM scores
   WHERE score != 60;
   ```

   ###### 使用 or 来连接条件：

   ```sql
   SELECT id FROM t WHERE num = 10 OR num = 20
   -- 可以这样查询：    
   SELECT id FROM t WHERE num = 10 
   UNION ALL    
   SELECT id FROM t WHERE num=20 
   ```

   ###### 对字段进行表达式操作：

   ```sql
   SELECT id FROM t WHERE num/2 = 100
   ```

   ###### 对字段进行函数操作：

   ```sql
   SELECT id FROM t WHERE substring(name,1,3) = 'abc'	-- name以abc开头的id
   -- 应改为:
   SELECT id FROM t WHERE name LIKE 'abc%'
   ```

   ###### 子句中的“=”左边进行函数、算术运算或其他表达式运算：

   ```sql
   WHERE 函数操作 = 值
   ```

   

   ##### 查询结果集过大时，避免使用IN

   ###### in 和 not in：

   ```sql
   SELECT id FROM t WHERE num IN(1,2,3)    
   -- 对于连续的数值，能用 BETWEEN 就不要用 in 了：  
   SELECT id FROM t WHERE num BETWEEN 1 AND 3 
   ```

   ###### 用 exists 代替 in ：

   ```sql
   SELECT num FROM a WHERE num IN(SELECT num FROM b)
   -- 用下面的语句替换：    
   SELECT num FROM a WHERE EXISTS(SELECT 1 FROM b WHERE num=a.num)
   ```

   

   ##### LIKE 进行模糊查询时，查询语句中使用了通配符 % 或者 _作为开头：

   ```sql
   -- 这样的查询方式需要扫描索引树的大部分或全部节点，以此来定位匹配的记录，
   -- 从而导致优化器放弃使用索引而选择全表扫描。
   SELECT id FROM t WHERE name LIKE '%abc'
   SELECT id FROM t WHERE name LIKE '_abc'
   ```

   

   

3. #### 分区表优化

   通过将大表分成多个小表，可以大幅度缩短查询时间，并优化索引效率。

   

   

4. #### 内存优化

   通过调整缓冲池大小(数据库在内存中预留的一部分空间)，可以减少磁盘I/O，从而提高查询速度。

   

   

5. #### SQL语句重构：

   不要使用 select * from xxx，多个简单的语句，可以提高查询效率。

   

   

7. #### 数据库分布式

   将数据分布到多个服务器上进行处理，可以承担更高的负载，提高整体性能。

   

   

8. #### 查询结果分页

   对于大量数据的查询，可以通过结果分页的方式来减少I/O操作和网络带宽的使用，提高查询效率。

   

   

   

### MySQL数据库innodb引擎索引底层实现的原理及查找过程

首先InnoDB会根据查询条件找到匹配的索引，如果找到多个索引，则选择其中一个来查询，如果没有任何索引匹配，则进行全表扫描。

查找过程从根节点开始，在索引节点和叶子节点中按照特定的顺序分别进行查找：

​	a. 如果当前节点是一个索引节点，则根据节点中存储的值进行查找，找到下一个要查找的子节点，然后继续下去，直到找到匹配的叶子节点。

​	b. 如果当前节点是一个叶子节点，则查找结束，返回对应的行数据。

在查找过程中，如果当前节点的数据已经不在内存中，则需要进行磁盘IO操作，从磁盘中读取对应的数据。

为了优化查询效率，InnoDB使用了多级索引缓存和数据缓存，可以将热点索引和数据缓存到内存中，减少磁盘IO的次数，提高查询性能。



##### 注意：

B+树不支持模糊查询和全文检索等操作，这些操作需要使用其他的索引结构来进行支持。此外，InnoDB还支持聚集索引，即通过主键来创建的索引，它可以直接将数据和索引存储在一起，提高查询效率。





 

### MySQL数据库innodb引擎与myisam引擎索引的区别

> MyISAM和InnoDB引擎是 MySQL 所采用的两种不同的存储引擎，之间的区别包括索引和锁机制等方面。

1. ##### 索引

   MyISAM 引擎和 InnoDB 引擎的索引实现方式是不同的。MyISAM 引擎使用 B+Tree 索引，对于全文本搜索，它还支持全文本索引；而 InnoDB 引擎则使用 B+Tree 索引，对于范围查找效果更佳，并且支持聚簇索引。

   

2. ##### 锁

   MyISAM 引擎和 InnoDB 引擎支持的锁机制不同。 MyISAM 引擎只支持表级锁，也就是说，在进行写操作时，整张表被锁定，其它查询和更新操作必须要等待；而 InnoDB 引擎支持行级锁和表级锁，可以根据需要选择行级锁或者表级锁，提高并发度和效率。

   

3. ##### 事务

   MyISAM 引擎和 InnoDB 引擎的支持事务处理的能力不同。MyISAM 引擎不支持事务处理，而 InnoDB 引擎支持事务处理，可以进行事务的提交和回滚操作，保证数据的一致性和完整性。

   

4. ##### 外键支持

   MyISAM 引擎和 InnoDB 引擎对外键支持的能力也不同。实际上，MyISAM 表不支持外键约束；而 InnoDB 引擎支持外键约束，能够维护表与表之间的关联性，并确保数据的完整性和一致性。



##### 总结：

MyISAM 引擎和 InnoDB 引擎在索引、锁、事务和外键支持等方面都存在着不同。

#### B树和B+树的区别如下：

##### 结点结构不同

B树每个结点都包含关键字和指向子节点的指针，而B+树的非叶子结点只包含关键字和指向子节点的指针，并不包含关键字对应的数据，数据(索引)只存储在叶子结点中。



##### 叶子结点不同

B树的叶子结点既包含关键字也包含数据，B+树的叶子结点只存储关键字和数据指针，数据存储在另外的磁盘块中，叶子结点都被连接成一个链表，在查询过程中可以顺序遍历叶子结点，可以提高搜索效率。

B+树的非叶子结点只起到索引作用，而不像B树既存储索引又存储数据，所以B+树所有非叶子结点的孩子个数相同，并且更浅，可以减少磁盘I/O次数，提高查询效率。

B+ 树的叶子结点只有链表中的最后一个叶子结点可能出现不满的情况，其他的叶子结点都是满的，这是因为B+树的叶子结点之间是有序的，可以直接进行范围搜索。 B树则不一样，各个叶子结点分布不均匀，需要进行不同程度的回溯，所以一般来说，B树的查询效率比B+树低。



##### 总结：

在B+树中，叶子节点只存储索引关键字，并不存储数据，而是额外维护了一个叶子节点的链表，数据存储在链表中。而在B树中，数据和索引都可以存储在叶子节点中。

B+树的优点是，由于数据只存储在链表中，极大地减少了访问磁盘的频率，适合于大数据量的场景。另外，所有叶子节点都连接成一颗有序的链表，方便区间查找和遍历。而B树适用于数据量比较小的场景，数据量小的时候，B树的查询效率相对B+树要高，因为在B树中，一个节点既存储索引又存储数据，可以更快地定位到需要的数据。



 



### MySQL索引在哪些情况下会失效（至少5条）

1. ##### 使用 OR 条件查询时

   OR 条件中的列没有被索引覆盖，则索引会失效，因为 MySQL 无法从索引中获取满足 OR 条件的所有行，只能进行全表扫描。

   

2. ##### 使用 NOT IN 或者 <> 操作符查询

   被查询的列上面的索引中包含 NULL 值，则索引会失效，因为 NULL 不等于任何值，这样会导致不满足查询条件的数据也会被放在结果集里面。

   

3. ##### 对于索引中的字符串类型的字段，使用了函数进行查询

   SELECT * FROM table WHERE LENGTH(name) > 10，则索引也会失效，因为在执行查询时需要对所有数据进行函数操作，无法利用索引提高查询效率。

   

4. ##### 表中数据量很小

   MySQL 查询优化器可能会忽略索引，直接进行全表扫描，因为此时使用索引的成本会比全表扫描更高，不利于优化查询性能。

   

5. ##### 使用了强制类型转换

   如：SELECT * FROM table WHERE id=’10’，将字符串类型的数据强制转换为整型，在进行比较操作时，MySQL 无法使用索引，因为数据类型已经发生了改变，与索引中的数据类型不匹配。

   

6. ##### 复合索引

   在查询条件中只使用了部分关键字进行匹配，则索引会失效。如：CREATE INDEX idx_name_age ON table (name, age)，但是在查询时只使用了 name 的条件，而没有使用 age 的条件，则索引会失效。

   

7. ##### 使用 LIKE 操作符进行模糊查询

   查询字符串以通配符 % 开头，则索引会失效，因为 MySQL 无法通过索引进入查询。

   

8. ##### 查询条件中使用了函数

   SELECT * FROM table WHERE YEAR(create_time)=2021，则索引会失效，因为在执行查询时需要对所有数据进行函数操作，无法利用索引提高查询效率。

   

9. ##### 通过 JOIN 等操作连接多个表进行查询

   MySQL 可能会忽略索引，使用全表扫描的方法来获取结果，因为此时使用索引的成本可能比全表扫描更高。

   

10. ##### 一个字段中包含了大量重复的数据（如性别字段等）

    则在对该字段进行查询时，索引可能会失效，因为索引无法提供足够的选择性，优化器可能会选择不使用索引来执行查询。







### 脏读、幻读、不可重复读、第一类丢失更新以及第二类丢失更新

##### 脏读：

指一个事务读取了另一个事务未提交的数据，此时如果另一个事务回滚，那么读取的数据就是不存在的。



##### 幻读：

指一个事务在读取一段范围的数据时，另一个事务又在这个范围内插入了新的数据，导致第一个事务在后续查询时多次读取到不同的数据行，这是因为第二个事务对数据的修改使得第一个事务读取的数据行的个数发生了变化。可重复读隔离级别只能避免插入和删除，而无法避免新插入的数据行影响查询结果，因此只能够在串行化隔离级别下得到解决。



##### 不可重复读：

指一个事务在两次读取同一数据之间，另一个事务修改了该数据，导致第一次读取和第二次读取结果不一致。



##### 第一类丢失更新：

指两个事务同时对同一数据进行更新操作，在其中一个事务提交之后，另一个事务对同一数据进行修改并提交，导致第一个事务的更新被覆盖掉，从而造成数据丢失。



##### 第二类丢失更新：

指两个事务同时对同一数据进行更新操作，其中一个事务先提交了更新，另一个事务在读取并修改该数据后提交，导致第一个事务的更新被覆盖掉，从而造成数据丢失。







### 事务隔离级别

> 数据库事务隔离级别指的是不同事务之间的隔离程度；
>
> 即在不同的事务之间，一个事务所做的改变在提交前是否能够被其他事务看到和操作。
>
> 不同的隔离级别在实现上的开销和并发控制强度不同，需要根据具体场景选择。

常见的事务隔离级别包括：

1. 读未提交（Read Uncommitted）：一个事务可以读取另一个事务尚未提交的数据。这种隔离级别最容易出现脏读、幻读、不可重复读。
2. 读已提交（Read Committed）：一个事务只能读取另一个事务已提交的数据。可以避免脏读，但可能出现幻读和不可重复读。
3. 可重复读（Repeatable Read）：保证同一事务中多次读取同一数据结果是一致的。避免了脏读和不可重复读，但仍可能出现幻读。
4. 序列化（Serializable）：最高的隔离级别，强制事务串行执行，避免了所有并发问题，但效率较低。

|           隔离级别           |                读数据一致性及允许的并发副作用                | 脏读 | 不可重复读 | 幻读 |
| :--------------------------: | :----------------------------------------------------------: | :--: | :--------: | :--: |
| 未提交读d(Read uncommitted)  | 最低级别，只能保证不读取物理上损坏的数据，事务可以看到其他事务没有被提交的数据(脏数据) |  是  |     是     |  是  |
|   已提交读(Read committed)   |          语句级，事务可以看到其他事务已经提交的数据          |  否  |     是     |  是  |
| 可重复读   (Repeatable read) |               事务级，事务中两次查询的结果相同               |  否  |     否     |  是  |
|   可序列化  (Serializable)   |                  最高级别，事务级。顺序执行                  |  否  |     否     |  否  |







### MySQL数据库表的连接方式

#### 内连接（Inner Join）：

只返回两个表之间满足连接条件的记录。这是默认连接方式





#### 外连接（Outer Join）：

分为左外连接(Left Join)、右外连接(Right Join)和全外连接(Full Outer Join)，返回一个表中匹配的所有记录以及另一个表中的记录





#### 自连接（Self Join）：

指把一张表看作两个存在的表(虚拟副本)，并在这两个表(自己跟自己)之间进行连接





#### 交叉连接（Cross Join）：

返回两个表中的所有记录的笛卡尔积。这种连接方式比较少用







### 第一，第二，第三范式

> 范式是用于设计关系数据库的规范和标准

范式的目的在于确保数据库的数据不重复，数据结构规范和一致性。这些范式是确保关系数据库能够有效管理和处理数据，避免数据冲突和不一致。通过遵循这些规范，可以提高数据库的可靠性、性能和可维护性。

##### 第一范式（1NF）：

确保每个列都是原子的，即不可分割。它消除了重复信息，属性中的每种类型都保持相同，并为每个表行获得唯一标识符。



##### 第二范式（2NF）：

确保表中的每个列都与表的主键相关联。它要求表中的非主属性要完全依赖于主属性，而不是部分依赖于主属性。



##### 第三范式（3NF）：

确保表中的每个列都与表中的键之外的列无关。它要求所有非主属性直接与主属性相关联，而不是与其他非主属性相关联。





---





## JVM

### Java运行时数据区域

> Java运行时数据区域指的是Java虚拟机运行时用于存储数据的区域

![image-20230607151915702](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230607151915702.png)

#### 程序计数器

是一块较小的内存空间，它用于保存当前线程所执行的字节码的行号指示器。当线程执行Java方法时，程序计数器记录的是正在执行的虚拟机字节码指令的地址，当线程执行的是Native方法时，程序计数器的值为空。





#### Java虚拟机栈

也称为Java栈，是一块线程私有的内存空间，用于存储Java方法执行时的局部变量表、操作数栈、动态链接、方法出口等信息。每个方法在执行时都会创建一个栈帧（Stack Frame）用于存储这些信息，当方法执行完毕时，栈帧将被弹出。





#### 本地方法栈

> Native Method就是一个Java调用非Java代码的接口：该方法的实现由非Java语言实现，比如C

与Java虚拟机栈类似，不同的是本地方法栈是为Native方法服务的，用于存储Native方法执行时的局部变量表、操作数栈等信息。





#### Java堆

是Java虚拟机中存储对象的内存区域。所有的对象实例和数组都在Java堆中分配空间，Java堆是垃圾回收的主要区域，也是Java虚拟机内存管理的重点。





#### 方法区

也称为永久代，用于存储已被虚拟机加载的类型信息、常量、静态变量、即时编译后的代码等数据。在Java 8之后，永久代被元空间所取代，但是元空间仍然属于方法区的一部分。





#### 运行时常量池

是方法区的一部分，用于存储编译器生成的各种字面量和符号引用。每个类或接口在加载时都会生成一个对应的运行时常量池，用于存储该类或接口的常量池信息。

保存的常量包括：

1. 字面量：如字符串、整数、浮点数等。
2. 符号引用：如类和接口的全限定名、字段名称和描述符、方法名称和描述符等。
3. 常量表达式：如常量表达式计算得出的值。
4. static final修饰的基本数据类型和String类型的变量值。

虽然static final修饰的基本数据类型和String类型的变量值在编译期间就已经确定了，但它们不一定会被直接放在运行时常量池中。如果在程序中引用这些常量，编译器会将它们存放在类的常量池中，并生成对应的getstatic指令或ldc指令来获取这些常量的值。只有当这些常量被真正使用时，才会被加载到运行时常量池中。

除了这些区域外，Java虚拟机还包括了一些其他的数据结构和服务，如直接内存、本地方法接口、线程等。







### Java中的引用类型

##### 强引用(Strong Reference)

指向对象的普通引用，只要存在强引用，垃圾回收器就不会清理该对象。

```java
// 创建强引用对象
Object obj = new Object();
```



##### 软引用(Soft Reference)

更加柔弱的引用，当内存空间不足时，垃圾回收器会回收被软引用关联的对象。可以用来实现内存敏感的缓存。

```java
// 创建软引用对象
Object obj = new Object();
SoftReference<Object> softRef = new SoftReference<>(obj);
```



##### 弱引用(Weak Reference)

比软引用更加柔弱，只能活到下次垃圾回收之前。可以用来实现对象的监控，当一个对象变得无用时，垃圾回收器会自动清理与之相关的弱引用对象。

```java
// 创建弱引用对象
Object obj = new Object();
WeakReference<Object> weakRef = new WeakReference<>(obj);
```



##### 虚引用(Phantom Reference)

是最弱的引用类型，不会对对象的生命周期产生影响。主要用来跟踪对象被GC回收的状态。使用虚引用的唯一目的就是在这个对象被回收时收到一个系统通知或者在finalize()方法中做一些调用前的清理工作。

```java
// 创建虚引用对象
Object obj = new Object();
PhantomReference<Object> phantomRef = new PhantomReference<>(obj, referenceQueue); 
```







### JVM怎么判断一个对象是否可用回收(垃圾回收算法)

#### 引用计数算法

该算法基于引用计数的思想，即为对象添加一个引用计数器，每当有一个地方引用它时，引用计数器就加1；当引用失效时，引用计数器就减1。当引用计数器为0时，即表示该对象不再被任何引用指向，可以被垃圾回收器回收。但是，引用计数算法无法解决对象之间相互引用的问题(A引用B，B引用A)，即循环引用问题。





#### 可达性分析算法

该算法基于可达性的思想，即从一组根对象开始，寻找所有能被根对象直接或间接引用的对象，把它们标记为“存活”状态，剩下的对象就可以被判定为“死亡”状态，可以被垃圾回收器回收。根对象包括虚拟机栈中引用的对象、静态变量引用的对象和常量引用的对象。可达性分析算法可以解决循环引用问题，因为只要对象不与根对象相连通，就可以被回收。







### JVM的垃圾回收算法

#### 标记-清除算法

这是最基本的垃圾回收算法。它通过标记所有不可达对象并清除它们来回收内存。但是，它会产生内存碎片，可能会导致分配失败。

两个不足：效率不高	空间会产生大量碎片





#### 复制算法

这个算法将堆分为两个区域，每次只使用其中一个区域。当一个区域被占满后，就将存活的对象复制到另一个区域中，然后清除之前使用的区域。这种算法可以避免内存碎片，但是需要额外的内存空间。





#### 标记-整理算法

这个算法是标记-清除算法的改进版。它会标记所有不可达对象并将所有存活的对象移动到内存的一端，然后清除另一端的所有对象。这种算法可以避免内存碎片，但是仍然需要移动对象，可能会影响性能。





#### 分代收集算法

这个算法基于一个假设，即大部分对象的生命周期很短。它将堆分为不同的代（Generation），每个代中的对象具有不同的生命周期。新创建的对象会被分配到新生代中，而长时间存活的对象会被移动到老年代中。因此，可以针对不同的代使用不同的垃圾回收算法，以提高效率。

##### 新生代

默认占堆空间的三分之一，每次垃圾回收都有大量对象死去，只有少量存活，选用复制算法比较合理。

在复制的期间会有频繁的Minor GC。

新生代分为2个区：Eden和Survivor区，其中Eden区默认占新生代十分之八的空间，对象优先进入Eden区。

当Eden区内存满了之后会进行一次Minor GC存活对象会进入Survivor区，默认占新生代十分之二空间， 其中它又均分为From区和To区，包括两个(S0和S1)，在Survivor区的对象每熬过一次从From区到TO区则年龄+1。



##### 老年代

默认占堆空间的三分之二，老年代的Minor GC开销非常大。

老年代中对象存活率较高、没有额外的空间分配对它进行担保。所以必须使用标记-清除或者标记-整理算法回收





#### 分区算法

这个算法将堆分为多个区域，每个区域都可以独立地进行垃圾回收。这种算法可以提高并行性和吞吐量，并且可以避免全局停顿。





#### 总结

Java虚拟机通常使用复制算法和标记-整理算法作为新生代和老年代的垃圾回收算法。同时，分代收集算法也被广泛地使用，因为它可以根据对象的生命周期来选择合适的垃圾回收算法，从而提高效率。







### JVM的内存分配策略和回收策略

#### 内存分配策略

JVM的内存分配策略主要针对堆内存。堆内存分为两个区域：新生代和老年代。

新生代又分为：

Eden区：新创建的对象会被分配到这个区域。

Survivor区：包括两个（S0和S1），用于存放从Eden区经过一次Minor GC后仍然存活的对象。





#### 回收策略

分代回收：根据对象的生命周期，将内存划分为新生代和老年代，针对不同区域采用不同回收策略。新生代中的对象多数是短期存活的，通常采用复制算法进行回收。老年代中的对象多数是长期存活的，通常采用标记-清除（Mark-Sweep）或标记-整理（Mark-Compact）算法进行回收。

##### Minor GC

回收新生代中的对象。当Eden区满时，触发Minor GC，将存活的对象复制到Survivor区。之后，清空Eden区和其中一个Survivor区，然后交换Survivor区的角色。



##### Full GC

回收整个堆内存，包括新生代和老年代。Full GC会导致应用程序暂停，因此会尽量避免发生。可能的触发条件包括：老年代空间不足、方法区空间不足、系统调用`System.gc()`等。



##### 垃圾收集器

JVM提供了多种垃圾收集器，如串行收集器（Serial GC）、并行收集器（Parallel GC）、并发标记-扫描收集器（Concurrent Mark-Sweep, CMS）、G1收集器等。它们有各自的优缺点和适用场景，可以根据应用程序的需求进行选择。







### 类生命周期的几个阶段

![image-20230608104901656](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230608104901656.png)

#### 加载（Loading）

在这个阶段，JVM会查找并加载类的二进制数据。类的二进制数据可以来自文件、网络、数据库等各种来源。加载完成后，JVM会在内存中生成一个表示该类的Class对象。





#### 链接（Linking）

在这个阶段，JVM会将类的二进制数据合并到JVM运行时环境中。链接分为三个子阶段：

**验证（Verification）**：JVM会检查类的二进制数据是否符合JVM规范，并且不会危害JVM的安全性。

**准备（Preparation）**：JVM会为类的静态变量分配内存，并设置默认的初始值。

**解析（Resolution）**：JVM会将符号引用解析为直接引用，例如将类名解析为类的实际内存地址。





#### 初始化（Initialization）

在这个阶段，JVM会执行类的初始化代码，包括静态变量的赋值和静态代码块的执行。初始化是类的生命周期中的最后一个阶段，也是类第一次被使用时执行的阶段。





#### 使用（Using）

在这个阶段，类被正式使用，例如创建对象、调用方法等。





#### 卸载（Unloading）

在JVM的内存中，不再需要使用的类会被卸载。

JVM会在内存中检查类的引用计数是否为零，如果为零则表示该类不再被使用，可以卸载。







## 其他

### JDK8新特性

#### Lambda表达式

支持函数式编程





#### 接口的默认方法和静态方法

使接口更加灵活和方便。





#### Stream API：

Stream流，支持流式处理数据。





#### Date/Time API：

提供了可变且线程安全的日期时间类，即java.time包，该包提供了多个可变且线程安全的日期时间类，包括：

|      类名      |                意义                |
| :------------: | :--------------------------------: |
|   LocalDate    | 表示一个日期（年月日），无时区信息 |
|   LocalTime    | 表示一个时间（时分秒），无时区信息 |
| LocalDateTime  |  表示日期和时间的组合，无时区信息  |
| ZonedDateTime  |    表示带有时区信息的日期和时间    |
| OffsetDateTime | 表示一个带有时区偏移量的日期和时间 |
|   OffsetTime   |    表示一个带有时区偏移量的时间    |

除了以上的日期时间类之外，java.time包提供了一些其他辅助类，如：

|       类名       |            意义            |
| :--------------: | :------------------------: |
|     Duration     |      表示一段时间间隔      |
|      Period      | 表示两个日期之间的时间间隔 |
| TemporalAdjuster |       表示日期调整器       |

这些类也同样是可变的且线程安全的，可以被多个线程同时访问而不会发生线程安全问题。这些类在设计时考虑到并发环境的需要，采用了不可变对象和不可变式的设计方式，防止了数据的并发修改和数据不一致问题。 

此外，Java 8的日期时间API不仅提供了更好的性能和精度，同时还提供了丰富的日期时间计算和查询方法，可以轻松地进行日期时间的加减、比较、格式化等操作。它的引入使得日期时间处理变得更加简单和方便，避免了以前使用Date和Calendar类时常见的错误和不便。





#### 函数式编程接口：

提供了函数式编程接口，如Function(函数接口)、Consumer(消费型接口)、Predicate(断言型接口)等。





#### Base64编解码器：

提供了Base64编解码器，方便编解码操作。





#### 方法引用：

可以使用方法名来代替Lambda表达式。





#### 类型注解：

可以为类型添加注解，提供更加严格的类型检查。





#### 并发新增API：

提供了新的并发API，如CompletableFuture。





#### Nashorn JavaScript引擎：

集成了高性能的Nashorn JavaScript引擎。



---

---



# JavaEE

## 设计模式

### 创建型模式：关注对象的创建过程

#### 单例模式

> 单例模式就是确保一个类只有一个实例存在，也就是类变量为static修饰的静态成员变量
>
> 确保单例模式只有一个实例，首先就要私有化构造方法
>
> 单例模式由三种设计：是否是懒汉加载，是否是线程安全，是否能被反射破坏。其中后两点不可兼得
>
> 单例模式分为两种：饿汉式、懒汉式

##### 饿汉式

> 类加载时就进行实例化，如果实例化过程比较繁琐和耗时，可以考虑使用静态代码块的方式进行初始化
>
> 如果单例类的实例在程序运行期间很少或者几乎不会被使用到，饿汉式单例就会导致系统资源的浪费，因为它在程序启动时就占用在线程池、CPU和内存等系统资源中。
>
> 如果程序启动时必须要使用该单例模式的实例，可以考虑采用饿汉式单例创建实例

```java
public class Student {

    // 私有静态成员变量，饿汉式在类加载时(程序启动时)就创建
    private static Student student = new Student();

    // 私有化构造方法
    private Student() {
    }

    // 获取单例对象实例的方法，必须是static，如果方法没有声明为静态方法，则它必须使用对象实例进行访问
    public static Student getStudent() {
        return student;
    }
}
```



##### 懒汉式

> 延迟加载，有需要时才进行实例化(调用时)，防止资源浪费
>
> 当单例实例不是很频繁使用的时候，可以考虑使用懒汉式单例，根据需要进行实例化

###### 基础懒汉式

```java
public class Teacher {

    // 创建静态成员变量，懒汉式在类加载时(程序启动时)不实例化
    private static Teacher teacher;

    // 私有化构造方法
    private Teacher() {
    }

    // 获取单例实例的方法，也是static修饰
    public Teacher getTeacher() {
        // 懒汉式先判断是否已经创建对象了，如果没创建，才创建静态成员变量
        if (teacher == null) {
            teacher = new Teacher();
        }
        return teacher;
    }
}
```

###### Class锁

> 基础懒汉式在多线程下存在一个问题：两个线程同时获取单例实例，在A线程创建实例时，B线程已经进入if判断，这时单例就会创建两次，违背了单例模式的初衷，多线程问题的解决方案——加锁

```java
// Class锁机制解决多线程问题，这样每次只允许一个线程调用getInstance方法
public static synchronized Teacher getTeacher2(){
    if (teacher == null) {
        teacher = new Teacher();
    }
    return teacher;
}
```

###### double-checked locking：双检锁

> Class锁的确可以防止错误的出现，但是它却很影响性能：每次调用getInstance方法的时候都必须获得Teacher的锁，而实际上，当单例实例被创建以后，其后的请求没有必要再使用互斥机制了

```java
/*
	首先，当一个线程发出请求后，会先检查instance是否为null，如果不是则直接返回其内容，
	这样避免了进入synchronized块所需要花费的资源。
	其次，即使第2节提到的情况发生了，两个线程同时进入了第一个if判断，那么他们也必须按照顺序执行
    synchronized块中的代码，第一个进入代码块的线程会创建一个新的Singleton实例，而后续的线程则因为无法
    通过if判断，而不会创建多余的实例。
*/
// double-checked locking，双检锁，优化性能
public static Teacher getTeacher3() {
    if (teacher == null) {
        synchronized (teacher) {
            if (teacher == null) {
                teacher = new Teacher();
            }
        }
    }
    return teacher;
}
```

###### 内部类实现

> 从JVM的角度讲，双检锁实现单例仍然可能发生错误：对于JVM而言，它执行的是一个个Java指令。在Java指令中创建对象和赋值操作是分开进行的，也就是说teacher= new Teacher();语句是分两步执行的。
>
> 但是JVM并不保证这两个操作的先后顺序，也就是说有可能JVM会为新的Teacher实例分配空间，然后直接赋值给teacher成员，然后再去初始化这个Teacher实例。
>
> 这样就使出错成为了可能，我们仍然以A、B两个线程为例：
>
> A、B线程同时进入了第一个if判断；
>
> A首先进入synchronized块，由于teacher为null，所以它执行teacher= new Teacher();
>
> 由于JVM内部的优化机制，JVM先划出了一些分配给Teacher实例的空白内存，并赋值给teacher成员（注意此时JVM没有开始初始化这个实例），然后A离开了synchronized块；
>
> B进入synchronized块，由于teacher此时不是null，因此它马上离开了synchronized块并将结果返回给调用该方法的程序；
>
> 此时B线程打算使用Teacher实例，却发现它没有被初始化，于是错误发生了。可以理解为：
>
> A线程执行完毕，Java分配了内存并赋值，还没有创建出对象去引用这块内存，仅仅是内存中存在这个对象；
>
> B进入内层if后，认为对象已经创建了，便直接执行return，但是这个对象是null，b线程在使用这个对象时就出现空指针(没有初始化)，最好并且最方便的解决办法就是基于内部类实现的单例模式

```java
/*
 * JVM内部的机制能够保证当一个类被加载的时候，这个类的加载过程是线程互斥的。
 * 这样当我们第一次调用getTeacher4的时候，JVM能够帮我们保证teacher只被创建一次;
 * 并且会保证把赋值给teacher的内存初始化完毕，这样我们就不用担心JVM中的问题。
 * 此外该方法也只会在第一次调用的时候使用互斥机制，这样就解决了双检锁中的低效问题。
 * 最后teacher是在第一次加载Teacher类时被创建的，而TeacherContainer类则在调用getTeacher4方法的时候	* 才会被加载，因此也实现了惰性加载。
 *
 * */	
// 内部类实现单例模式
private static class TeacherContainer {
    private static Teacher teacher = new Teacher();
}

public static Teacher getTeacher4() {
    return TeacherContainer.teacher;
}
```





#### 工厂模式

> 工厂模式是一种创建型设计模式，它提供了一个创建对象的通用接口，具体由子类去实现。

##### 简单工厂模式

```java
// 定义一个抽象类或者接口，用于定义要创建的对象的通用方法：
public interface Animal {
    void speak();
}

// 定义一个实现该接口的具体类，例如 Dog：
public class Dog implements Animal {
    @Override
    public void speak() {
        System.out.println("Dog is speaking");
    }
}

// 定义实现类Cat，同样实现Animal接口
public class Cat implements Animal {
    @Override
    public void speak() {
        System.out.println("Cat is speaking");
    }
}

// 定义一个工厂类，用于创建具体的对象：
// createAnimal()方法根据传入的参数type来创建具体的对象，如果传入的类型不是指定的类，就会抛出异常。
public class AnimalFactory {
    public Animal createAnimal(String type) {
        if ("Dog".equals(type)) {
            return new Dog();
        } else if ("Cat".equals(type)) {
            return new Cat();
        } else {
            throw new IllegalArgumentException("Invalid animal type: " + type);
        }
    }
}

// 可以使用工厂类来创建具体对象并调用方法：
AnimalFactory factory = new AnimalFactory();
Animal dog = factory.createAnimal("Dog");
dog.speak();
```



##### 方法工厂模式：

> 

```java

```



##### 抽象工厂模式：

> 它通过提供一个抽象工厂接口来创建一系列相关或相互依赖对象的家族，而无需指定具体的类。
>
> 抽象工厂模式可以方便地切换产品家族，且可以保证客户端代码不会发生改变，同时也符合开闭原则。

```java
// 抽象产品类：
public interface Car {
  void creat();
}

// 具体产品类：
public class Benz implements Car {
  @Override
  public void creat() {
    System.out.println("Driving Benz...");
  }
}
public class Audi implements Car {
  @Override
  public void creat() {
    System.out.println("Driving Audi...");
  }
}

// 抽象工厂接口：
public interface CarFactory {
  Car createCar();
}

// 具体工厂类：
public class BenzFactory implements CarFactory {
  @Override
  public Car createCar() {
    return new Benz();
  }
}
public class AudiFactory implements CarFactory {
  @Override
  public Car createCar() {
    return new Audi();
  }
}

// 客户端代码：
public class Client {
  public static void main(String[] args) {
    CarFactory factory = new BenzFactory();
    Car car = factory.createCar();
    car.drive();  // Driving Benz
    
    factory = new AudiFactory();
    car = factory.createCar();
    car.drive();  // Driving Audi
  }
}
```







#### 建造者模式：





#### 原型模式：





#### 结构型模式

> 关注对象的组合方式：有适配器模式、装饰模式、代理模式、组合模式、桥接模式、外观模式和享元模式。
>





#### 行为型模式

> 关注对象的交互和职责分配：有观察者模式、模板方法模式、命令模式、状态模式、职责链模式、访问者模式、策略模式、解释器模式和中介者模式。
>



#### 并发型模式

> 关注多线程并发编程：有信号量模式、锁模式、读写锁模式、生产者消费者模式、监视器锁模式、并行算法模式等。
>



#### 架构型模式

> 关注软件架构和系统设计：有MVC模式、MVP模式、MVVM模式、分层模式、微服务模式、事件驱动架构模式等。





---





## JavaWEB

### Get请求和Post请求的区别

> GET请求通常用于从服务器获取数据，而POST请求用于向服务器提交数据。

#### 数据位置：

GET请求是通过URL向服务器提交数据，POST请求是通过请求体向服务器提交数据。

所以GET请求的参数数据长度有限制，浏览器有URL长度限制，而POST请求则没有。

并且GET请求是可见且可书签的，POST请求不能被书签。





#### 编码方式：

GET请求的数据会被URL编码，POST请求则没有限制(可以是二进制数据)

支持类型：GET请求只支持ASCII字符传输，而POST请求支持多种字符集传输。

GET请求用于从服务器上读取资源，而POST请求用于向服务器提交数据，让服务器执行请求的相关操作。





#### 可缓存性：

GET请求可以被浏览器缓存，而POST请求则不会缓存。





#### 总结：

使用GET请求还是POST请求主要取决于具体的场景和目的。

GET请求适用于非敏感信息获取及简单数据提交。

POST请求数据则可以使用更多的数据类型，适用于大数据提交及敏感信息传递。

如果只是读取信息，可以使用GET请求，如果需要向服务器提交修改或新增数据，应使用POST请求。

如果需要进行密码或敏感数据的提交，则必须使用POST请求。







### 同步与异步的区别

> 同步和异步是两种不同的编程模型，它们之间的区别在于程序执行的方式和结果返回的时间
>
> 同步适用于需要按顺序执行的任务，而异步则适用于需要执行耗时操作或高响应能力的任务

#### 同步：

程序按照顺序一步一步地执行，每执行一条指令后需要等待结果返回后才能执行下一步。

当程序执行一个耗时的操作时，需要等待这个操作完成后才能继续执行后面的指令，这就会造成程序停顿的现象，直到耗时操作完成后才能继续向下执行。

同步适用于需要按顺序执行的任务，但是可能会降低程序的性能和响应能力。





#### 异步：

程序不会一直等待结果返回，而是可以继续执行下一条指令，以提高程序的性能和响应能力。

当需要执行一个耗时的操作时，程序可以将这个操作交给其他线程或进程去执行，同时继续执行后面的指令。当耗时操作完成后，程序可以通过回调函数或消息机制来获取结果。

异步适用于需要执行耗时操作或者需要高响应能力的任务，但是增加了程序复杂度。由于异步操作可能会打乱程序的执行顺序，因此需要进行异步操作的正确处理和调度，以确保程序的正确性和性能。







### HTTP协议如何保证请求安全

HTTP 协议并不能直接保证请求安全，因为 HTTP 是一个明文协议，发送的数据都以明文的形式传输，攻击者在网络中截获请求数据包时，可以直接读取数据包中的数据，从而获取其中的敏感信息。

所以，为了保证 HTTP 请求的安全性，需要通过其他的机制进行保护。以下是几种常见的保护机制：

1. ##### HTTPS：

   使用 HTTPS 协议可以在 HTTP 协议之上增加 SSL/TLS 加密，从而实现数据传输的安全。HTTPS 有着较高的安全性能，能够对传输的数据进行加密，并对传输的完整性进行校验。

   

2. ##### 认证授权机制：

   使用用户名密码、token 等方式对请求发起者进行身份认证，从而防止非法用户伪造请求。

   

3. ##### 防重放攻击：

   在请求中添加时间戳或 nonce 值等随机数，使得攻击者不可能在短时间内伪造另一个请求，从而防止请求被重复使用。

   

4. ##### 安全编码：

   遵循安全编码规范，对输入参数进行合法性校验和过滤，避免 SQL 注入、XSS 攻击等漏洞。





#### 总结：

HTTP 协议并不能直接保证请求的安全，需要通过其他方式进行数据的加密、认证、授权等防护措施，才能够确保 HTTP 请求的安全性。





---





## Spring

### JDK代理与CGLIB代理的区别

#### 原理

##### JDK：代理类和被代理类实现一个接口

通过Java的动态代理机制实现，基于接口实现，动态生成一个实现了目标接口的代理类的实例调用被代理的方法。

##### CGLIB：代理类继承被代理类

通过对目标对象进行继承来实现的，动态生成一个继承了目标对象的子类，代理调用目标对象的方法。





#### 实现方式

JDK：需要目标类实现一个接口，代理类是通过实现目标接口来实现的；

CGLIB：不需要目标类实现一个接口，代理类是通过继承目标对象来实现的。





#### 性能

由于JDK代理是基于接口实现的，因此在代理时需要频繁地动态生成代理类的实例，相比之下，在同样的场景下，CGLIB代理通常比JDK代理效率更高。但是，如果目标对象的接口比较多，则使用JDK代理可能更加合适。





#### 应用场景

##### JDK：

适用于对具有明确接口的类进行代理，应用更加广泛，应用场景主要包括对Spring中的Bean进行代理、对RPC框架中处理远程方法调用、JDBC连接池中的连接对象等。



##### CGLIB：

适用于对没有实现接口的类进行代理，主要应用于框架级别的代理实现，如Hibernate框架中的实体类懒加载、MyBatis框架中的Mapper接口代理。

 

 

 

### 对IOC/DI的理解

> IOC/DI是一种设计模式，用于减少计算机程序的耦合度，提高程序的可维护性和可扩展性

##### IOC

即控制反转，意味着将对象的创建和依赖关系的管理交给容器来处理，而不是由程序代码直接控制，这样可以减少代码的耦合度，提高代码的灵活性。实现IOC的方式有很多，比如依赖查找、依赖注入等，目的都是为了实现对象之间的解耦。



##### DI

即依赖注入，是IOC的一种具体实现方式。依赖注入的过程中，通过容器自动将依赖注入到目标对象中，从而消除了对象之间的耦合关系。所谓依赖注入，是指程序通过一个中间容器（如Spring容器）在运行过程中动态地将某些类需要的外部资源（如其他类的对象、配置文件等）注入到该类中，而不是在类内部创建这些资源。

通常，DI 是通过构造函数、setter方法，或者接口注入实现。当一个类需要依赖其他的类时，可以通过构造函数、setter方法等方式定义依赖注入点，容器在实例化该类时，就会通过依赖注入点将依赖的类实例注入到该类中。



##### 总结：

IOC和DI是现代软件开发中非常重要的设计模式之一，通过这种方式实现对象之间的解耦，提高程序的可维护性、可扩展性和代码的复用性。

 

 

 

### SpringBean的生命周期

1. ##### 实例化

   当 Spring 容器接收到创建 Bean 的请求时，会根据 Bean 的定义信息，通过反射机制实例化 Bean。此时 Bean 还未进行属性值的注入。

   

2. ##### 属性注入

   当 Bean 实例化完成后，Spring 容器会根据配置文件或注解信息，将 Bean 的属性值进行设置。包括构造器注入、setter注入和注解注入等方式。

   

3. ##### 初始化前回调方法：BeanPostProcessor 的 postProcessBeforeInitialization 方法

   在 Spring 容器将 Bean 的属性进行注入后，在 Bean 的初始化方法（如 init-method 指定的方法）执行之前，会调用 BeanPostProcessor 的 postProcessBeforeInitialization 方法进行处理。

   

4. ##### 初始化

   在 BeanPostProcessor 的 postProcessBeforeInitialization 方法执行完成后，容器会调用 Bean 的初始化方法（如配置文件中指定的 init-method），对 Bean 进行初始化的一些操作。比如：打开资源、建立数据库连接，以及对属性进行复杂的操作等。

   

5. ##### 初始化后回调方法：BeanPostProcessor 的 postProcessAfterInitialization 方法

   在 Bean 初始化方法执行完成后，会调用 BeanPostProcessor 的 postProcessAfterInitialization 方法进行处理。

   

6. ##### 使用

   Bean 初始化完成后，可以将其注入到别的对象中使用。

   

7. ##### 销毁前回调方法：

   在Bean被销毁之前，如：@PreDestroy 注解的修饰方法

   

8. ##### 销毁

   当 Bean 不再使用了，Spring 容器会调用 Bean 的 destroy-method 方法进行销毁。在容器销毁之前，也可以手动调用 Bean 的 destroy 方法进行销毁。

   

##### 总结：

Spring 容器对 Bean 进行管理的过程就是生命周期的过程，其中通过 BeanPostProcessor 的前后置处理器，可以在 Bean 的创建和初始化的过程中进行一些额外的处理







### spring mvc处理请求流程

![image-20230608141318445](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230608141318445.png)

#### 组件说明

##### DispatcherServlet：前端控制器

用户请求到达前端控制器，它就相当于mvc模式中的c，dispatcherServlet是整个流程控制的中心，由它调用其它组件处理用户的请求，dispatcherServlet的存在降低了组件之间的耦合性,系统扩展性提高。由框架实现。



##### HandlerMapping：处理器映射器

HandlerMapping负责根据用户请求的url找到Handler即处理器，springmvc提供了不同的映射器实现不同的映射方式，根据一定的规则去查找,例如：xml配置方式，实现接口方式，注解方式等。由框架实现。



##### Handler：处理器

Handler 是继DispatcherServlet前端控制器的后端控制器，在DispatcherServlet的控制下Handler对具体的用户请求进行处理。由于Handler涉及到具体的用户业务请求，所以一般情况需要程序员根据业务需求开发Handler。



##### HandlAdapter：处理器适配器

通过HandlerAdapter对处理器进行执行，这是适配器模式的应用，通过扩展适配器可以对更多类型的处理器进行执行。由框架实现。



##### ModelAndView：springmvc的封装对象，将model和view封装在一起



##### ViewResolver：视图解析器

ViewResolver负责将处理结果生成View视图，ViewResolver首先根据逻辑视图名解析成物理视图名即具体的页面地址，再生成View视图对象，最后对View进行渲染将处理结果通过页面展示给用户。



##### View：是springmvc的封装对象

是一个接口, springmvc框架提供了很多的View视图类型，包括：jspview、pdfview、jstlView、freemarkerView、pdfView等。一般情况下需要通过页面标签或页面模版技术将模型数据通过页面展示给用户，需要由程序员根据业务需求开发具体的页面。





#### 执行流程

用户发送请求至前端控制器DispatcherServlet

DispatcherServlet收到请求调用处理器映射器HandlerMapping

处理器映射器根据请求url找到具体的处理器，生成处理器执行链HandlerExecutionChain(包括处理器对象和处理器拦截器)一并返回给DispatcherServlet

DispatcherServlet根据处理器Handler获取处理器适配器HandlerAdapter执行HandlerAdapter处理一系列的操作，如：参数封装，数据格式转换，数据验证等操作

执行处理器Handler(Controller，也叫页面控制器)

Handler执行完成返回ModelAndView

HandlerAdapter将Handler执行结果ModelAndView返回到DispatcherServlet

DispatcherServlet将ModelAndView传给ViewReslover视图解析器

ViewReslover解析后返回具体View

DispatcherServlet对View进行渲染视图（即将模型数据model填充至视图中）

DispatcherServlet响应用户











### SpringBoot启动过程

> Spring Boot的启动过程是一个逐步递进的过程，通过读取配置文件、加载依赖项、启动IoC容器等

#### 解析扫描

1. ##### 加载和解析配置文件

   Spring Boot通过读取预定义的配置文件(如application.yml和application.properties)来加载应用程序的配置信息，并使用Spring Boot的核心类Environment来将这些配置文件转换为应用程序的PropertSource对象。

   

2. ##### 扫描和加载依赖项

   Spring Boot通过扫描类路径上的所有依赖项来加载应用程序的依赖项，包括Spring框架本身和其他第三方库。

   

3. ##### 启动Spring IoC容器

   Spring Boot使用Spring IoC容器作为应用程序的核心容器，通过注入所需的Bean来实现应用程序的组件集成。Spring Boot使用@SpringBootApplication注解自动配置并启动Spring IoC容器。

   

4. ##### 加载外部配置文件

   Spring Boot根据默认顺序加载外部配置文件，以覆盖内部的配置信息，Spring Boot支持多个配置文件，包括以命令行形式提供的配置文件。

   

5. ##### 执行CommandLineRunner

   Spring Boot执行实现了CommandLineRunner接口的Bean，这些Bean被用来在应用程序启动后执行一些特定的任务。

   

6. ##### 启动Web应用程序

   如果应用程序是Web应用程序，则Spring Boot会启动内嵌的Tomcat或Jetty服务器，并将应用程序部署到其中。

   

7. ##### 运行应用程序

   最后，Spring Boot启动应用程序，并监听来自用户的请求。







---





## MyBatis

### $与#的区别

- `$` 直接将参数拼接到 SQL 语句中，不进行预编译，存在 SQL 注入的风险；
- `#` 将参数作为预编译参数，会在 SQL 语句被解析和编译阶段进行占位符替换，能够避免 SQL 注入的风险

假设我们有一个如下 SQL 语句：

```mysql
SELECT * FROM user WHERE id = ${userId}
```

如果我们使用 `$` 来表示参数占位符，那么在拼装 SQL 时，MyBatis 会将 `${userId}` 直接替换为对应的参数值，例如 `userId=1`，则会变为：

```mysql
SELECT * FROM user WHERE id = 1
```

这样一来，如果攻击者在该参数中传入恶意 SQL 代码，例如：

```mysql
userId = 1 or 1 = 1;
```

那么最终合成的 SQL 语句就将变成：

```mysql
SELECT * FROM user WHERE id = 1 or 1 = 1;
```

这将导致查询返回所有的用户记录，造成严重的 SQL 注入攻击。

相反，如果我们使用 `#` 来表示参数占位符，那么在拼装 SQL 时，MyBatis 会将 `#` 后面的参数名称解析出来，并在编译 SQL 语句时使用 PreparedStatement 对参数进行绑定，同时对参数进行转义，防止 SQL 注入攻击。

例如：

```mysql
SELECT * FROM user WHERE id = #{userId}
```

这样一来，如果攻击者在该参数中传入恶意 SQL 代码，例如：

```mysql
userId = 1 or 1=1;
```

那么最终合成的 SQL 语句就会变成：

```mysql
SELECT * FROM user WHERE id = ?;
```

其中 `?` 就是占位符，`PreparedStatement` 对象在执行 SQL 语句时会使用占位符来绑定参数。由于参数在编译时进行了处理和转义，因此不管参数中是否存在恶意 SQL 代码，都不会对 SQL 查询造成影响。

除了 SQL 注入的问题之外，`$` 和 `#` 在功能上也略有不同。使用 `$` 可以将变量直接拼接到 SQL 语句中，适用于拼接字符型、日期型等基本类型的数据。而 `#` 则将变量作为预编译参数处理，适用于拼接数值型、布尔型等复杂类型的数据。

例如：

```xml
<!-- 拼接字符串类型的参数（使用 $）-->
<select id="getUserByName" parameterType="string" resultType="com.example.User">
  SELECT * FROM user WHERE name LIKE '%${value}%'
</select>

<!-- 拼接数字类型的参数（使用 #）-->
<select id="getUsersByAge" parameterType="int" resultType="com.example.User">
  SELECT * FROM user WHERE age > #{value}
</select>
```

总之，在编写 MyBatis 的 SQL 语句时，应该尽量使用 `#` 来表示参数占位符，这样可以避免 SQL 注入的风险，并保证 SQL 语句的可读性和可维护性。







### mybatis缓存机制

> MyBatis缓存机制主要分为一级缓存和二级缓存
>

#### 一级缓存

MyBatis的一级缓存是指在同一个SqlSession中，如果执行了同一个查询语句，那么第一次执行完毕后会将查询结果存储到缓存中，下次执行同一个查询语句时，直接从缓存中获取结果，不再去执行查询语句，从而提高查询效率。





#### 二级缓存

MyBatis的二级缓存是指将数据缓存到SQLSessionFactory对象中，不同的SqlSession可以共享同一个缓存。对于这种情况，只要Mapper映射文件中设置开启了二级缓存，然后在第二次查询相同数据时，MyBatis会从二级缓存中查找数据，而不是再次查询数据库，从而提高了整个应用的性能。





#### 一级缓存和二级缓存的区别

##### 一级缓存：

- 一级缓存的生命周期和SqlSession相同。
- 一级缓存默认开启，无法关闭。
- 一级缓存是SqlSession级别的缓存，不同的SqlSession之间的缓存并不共享。
- 如果两次查询之间间隔了更新操作，那么缓存将被清空，一级缓存失效。



##### 二级缓存：

- 二级缓存的生命周期是跨SqlSession的，存储在SQLSessionFactory中。
- 二级缓存可以通过配置文件中的<cache>元素来开启和关闭。
- 二级缓存是全局性的，可以被所有的SqlSession共享。
- 如果两次查询之间间隔了更新操作，那么缓存将被清空，二级缓存失效。

需要注意的是，由于MyBatis的缓存是基于实体对象的，而且对于不同的查询，缓存的Key是不一样的，所以在使用缓存的时候，需要保证查询使用的是同一个实体对象，否则缓存将失效。此外，在使用二级缓存时需要保证缓存的可靠性和准确性，避免因为缓存而出现数据不一致的情况。因此，在使用二级缓存时需要谨慎考虑，需要根据具体情况来决定是否使用二级缓存，并且需要根据具体应用场景进行合理的配置和使用。





---





## Redis

### 缓存穿透、缓存雪崩、缓存击穿的意思，怎么避免它们的发生

##### 缓存穿透：

访问一个不存在的key时，请求会直接穿透缓存到达数据库，导致数据库压力过大。

###### 避免方法：

可以采用布隆过滤器来缓存一定范围内的key，或者将不存在的key也缓存一个空值。



##### 缓存雪崩：

高并发下，缓存中大量的数据同时失效或者过期，导致请求直接打到数据库，系统压力过大而崩溃。

###### 避免方法：

可以采用多级缓存、缓存数据过期时间随机化、定时更新缓存等方法来避免同时失效。



##### 缓存击穿：

是指一个key非常热点，在不停的扛着高并发，有大量的请求过来，当这个key在失效的瞬间，持续的大并发请求直接打到数据库，导致数据库扛不住这样的压力而崩溃。

###### 避免方法：

可以采用互斥锁或者分布式锁来控制访问并发，或者使用ehcache等支持手动过期的缓存工具，当发现即将过期时主动刷新缓存。







### 假设redis只能存储10000条数据，怎么保证redis存储的数据都是热点数据

#### 第一种

##### 热点数据排序（点击次数）

既然热门数据，那么就需要有排序，使用redis中的zset数据类型是很自然的想法。数据中的某个唯一字段作为zset中的value，而点击次数作为score，记为click_zset。这样就可选出最热门的数据。而数据，则直接用HashMap存储。

 

##### 热点数据时间（近期访问）

既然只能存1w条数据且需要是热门数据，那么，点击次数是一方面，时效性也是一方面，如何保证？可以另起一个zset，数据的字段为value，而每次点击时更新当前时间戳为其score，记为time_zset这样，就可以记录时间。在后台跑一个任务，间隔一定时间段删除两个zset中长时间没有发生点击事件的键，并删除hash数据，为产生的新数据腾出数据空间。

 

##### 处理新热点数据

如果有空间，则保存到自己的hashmap，并将key存到两个zset中。

而没有空间时，就应该在click_zset中取出点击次数排在最前第1w位后面的键，删除对应的hash数据。然后看这1w个score的值，然后把key放入两个zset中即可。



#### 第二种

##### 设置合适的过期时间

对于已经不再使用的数据，及时删除，防止冷数据占用存储空间，导致热点数据无法存储。可以通过设置过期时间，使得Redis自动删除过期数据



##### 设置LRU算法

LRU是一种常见的缓存淘汰算法，可以在数据量达到阈值时，优先淘汰最近最少使用的数据，保留常用数据



##### 按照访问频率排序

可以通过记录每个键值的访问频率信息，将访问频率高的数据放在Redis中，访问频率低的数据则不存储，达到热点数据优先存储的效果



##### 使用数据分片

将数据分散到多个Redis实例中，每个实例存储一部分数据，可以增加存储空间，同时也使得热点数据更容易被存储在Redis中。







### redis常见的内存淘汰策略

#### 淘汰策略

1. ##### volatile-lru： 

   内存淘汰时只考虑设置了过期时间（即键值对中有ttl字段）的数据，且优先删除最近最少使用的数据，直到腾出足够的内存空间为止。

   

2. ##### volatile-ttl： 

   内存淘汰时只考虑设置了过期时间的数据，优先删除最近过期的数据，直到腾出足够的内存空间为止。

   

3. ##### volatile-random：

    内存淘汰时只考虑设置了过期时间的数据，随机删除一些数据，直到腾出足够的内存空间为止。

   

4. ##### allkeys-lru： 

   内存淘汰时考虑所有数据（不管是否设置了过期时间），优先删除最近最少使用的数据，直到腾出足够的内存空间为止。

   

5. ##### allkeys-random：

    内存淘汰时考虑所有数据，随机删除一些数据，直到腾出足够的内存空间为止。

   

6. ##### noeviction： 

   不做任何淘汰，当Redis的内存使用率超过了物理内存大小时，新键值的写入操作直接返回错误。



##### 注意：lru和ttl两个淘汰策略是选择最近最少使用的数据进行淘汰。redis 并不是保证取得所有数据集中最近最少使用的键值对，而只是随机挑选的几个键值对中的， 当内存达到限制的时候无法写入非过期时间的数据集。





#### 策略选择

##### allkeys-lru：

如果期望用户请求呈现幂律分布(power-law distribution)，也就是，期望一部分子集元素被访问得远比其他元素多时，可以使用allkeys-lru策略。在你不确定时这是一个好的选择。

 

##### allkeys-random：

如果期望是循环周期的访问，所有的键被连续扫描，或者期望请求符合平均分布(每个元素以相同的概率被访问)，可以使用allkeys-random策略。

 

##### volatile-ttl：

如果你期望能让 Redis 通过使用你创建缓存对象的时候设置的TTL值，确定哪些对象应该是较好的清除候选项，可以使用volatile-ttl策略。

> 另外，为键设置过期时间需要消耗内存，所以使用像allkeys-lru这样的策略会更高效，因为在内存压力下没有必要为键的回收设置过期时间。





---





## 分布式

### 服务熔断、服务降级，以及它们的区别

服务熔断和服务降级都是为了保障系统的可用性和稳定性而提出的应对措施。

服务熔断是指当一个服务出现故障或无法提供正常服务时，自动切换到备用服务，避免将故障传递到调用方。服务熔断通过监测系统状态和异常情况，并触发自动切换来保障系统的稳定性。

服务降级是指当系统出现高负载或服务故障时，通过保留关键服务而关闭非关键服务，来减少系统压力，避免系统整体崩溃。服务降级通过限制系统资源使用来保障系统的可用性。

它们的区别在于：

1. 对象不同：服务熔断是针对单个服务实例的故障情况，服务降级是针对系统整体或特定服务的高负载或故障情况。
2. 处理方式不同：服务熔断是自动切换到备用服务，服务降级是关闭非关键服务，减少对系统资源的消耗。
3. 目的不同：服务熔断是为了避免将故障传递到调用方，保障系统的稳定性，服务降级是为了减少系统压力，保障系统的可用性。







### 分布式事务常见的解决方案(05套)

TODO







### shiro认证流程(05套)

TODO









---

---



# 数据结构与算法

### 一致性哈希算法

> 一致性哈希算法是用来解决分布式系统中节点数据分配的问题

在分布式系统中，数据通常会被分散到多个节点上存储，而节点的数量也可能会随时变化。这时候，如何快速且均匀地将数据分配到不同的节点中，就成为了一个问题。

一致性哈希算法的核心思想是将数据和节点都映射到一个相同的环上，然后根据节点的位置来决定数据分配到哪个节点上。具体来说，一致性哈希算法将一个哈希函数的输出空间表示为一个环形空间，将节点和数据都映射到这个环上。在环上，每个节点都有一个位置，节点之间的距离也可以用角度度量。然后，在插入新节点或删除节点时，只需要根据节点位置对数据进行重新分配，而其他节点不受影响。这样，节点的数量变化时，只需要重新计算即可，不需要重新分配数据，从而保证了分布式系统的可伸缩性。

一致性哈希算法的优点是避免了节点变化时的数据迁移，保证了系统的可扩展性和负载均衡性。但是也存在一些问题，比如节点分布不均匀会导致数据倾斜，引入虚拟节点来解决；哈希函数的质量和哈希冲突的问题等等。因此，在使用一致性哈希算法时需要注意其实现细节和应用场景。







### 哈希槽

哈希槽，也称为槽位，是一种数据结构中用于存储哈希表中数据的元素。哈希表是一种基于哈希技术实现的数据结构，它通过哈希函数将元素映射为槽位，从而实现快速的查找和插入操作。

在哈希表中，一个槽位通常对应一个哈希值，因此可以将哈希值作为索引来访问这个槽位。每个槽位存储的数据类型可以是不同的，通常包括需要存储的键值对、指向其他数据结构的指针等。

哈希槽通常具有以下特点：

1. ##### 线性探测：

   哈希表中的槽位通常是一维数组，如果两个元素被哈希到了同一个槽位，这就会造成哈希冲突。为了减少冲突，通常会采用线性探测的方法，即从当前槽位向后依次查找空闲的槽位，直到找到为止。

2. ##### 容量：

   哈希表的容量是指可以存储的最大元素数量，通常是一个固定的值。当哈希表中存储的元素数量达到容量的一定比例时，就需要对哈希表进行扩容或缩减，以保证哈希表的效率。

3. ##### 负载因子：

   哈希表的负载因子是指存储的元素数量与容量之间的比值，通常是一个小数值。当负载因子较大时，哈希表中冲突的概率就会增加，因此需要采取相应的措施来调整哈希表的容量。

总之，哈希槽是哈希表中存储数据的基本单元，它通常包含一个键值对或指向其他数据的指针，并通过哈希函数将元素映射为索引。在哈希表中，槽位的设计和实现对哈希表的性能和效率具有重要的影响。







### 排序二叉树以及排序二叉树的遍历方式

排序二叉树（又称二叉搜索树）是一种具有二叉树特性并且满足以下条件的树结构：对于任意节点，其左子树中的所有节点都小于该节点，其右子树中的所有节点都大于该节点。这个性质保证了排序二叉树的中序遍历结果是有序的，因为中序遍历按照左子树-节点-右子树的顺序访问节点。

排序二叉树在插入和查找操作上具有优秀的时间复杂度性能，插入和查找操作的时间复杂度都是O(logN)，其中N为树中节点的数量。排序二叉树的删除操作比较复杂，需要考虑多种情况，但是时间复杂度也为O(logN)。

排序二叉树的遍历方式包括前序遍历、中序遍历和后序遍历。以前序遍历为例，其遍历顺序为：节点-左子树-右子树。中序遍历遍历顺序为：左子树-节点-右子树。后序遍历遍历顺序为：左子树-右子树-节点。递归实现前序遍历的方式如下所示：

```java
public void preOrder(TreeNode root) {
    if (root == null) {
        return;
    }
    System.out.print(root.val + " ");
    preOrder(root.left);
    preOrder(root.right);
}
```

递归实现中序遍历的方式如下所示：

```java
public void inOrder(TreeNode root) {
    if (root == null) {
        return;
    }
    inOrder(root.left);
    System.out.print(root.val + " ");
    inOrder(root.right);
}
```

递归实现后序遍历的方式如下所示：

```java
public void postOrder(TreeNode root) {
    if (root == null) {
        return;
    }
    postOrder(root.left);
    postOrder(root.right);
    System.out.print(root.val + " ");
}
```







### B树、B+树、红黑树的区别





---

---



# 计算机网络

### TCP与UDP的区别

##### 可靠性

TCP是一种可靠的协议，它保证了数据传输的可靠性，即使在网络传输过程中发生数据包丢失或出错的情况下，TCP也会重新发送数据包，直到接收方正确地收到数据为止。而UDP则是一种不可靠的协议，它不提供数据传输的可靠性，数据包丢失或出错时，UDP不会重新发送数据包，而是直接丢弃。



##### 连接性

TCP是一种面向连接的协议，它在数据传输之前必须先建立连接，进行三次握手，然后在连接上发送和接收数据。而UDP则是一种无连接的协议，不需要建立连接就可以直接发送和接收数据。



##### 速度

由于TCP提供了可靠的数据传输和连接管理，因此它的速度相对比较慢。而UDP则不提供这些功能，因此它的速度相对较快。



##### 流量控制

TCP具有流量控制的功能，可以根据网络的状况调整发送数据的速度，避免网络拥塞。而UDP没有流量控制的功能，如果网络拥塞，UDP数据包就会丢失。



##### 应用场景

由于TCP具有可靠性和连接管理的功能，因此适合用于需要可靠传输的应用程序，如传输文件、电子邮件和网页浏览等。而UDP适用于实时性要求高、数据量小的应用程序，如实时视频、音频和游戏等。







### 正向代理和反向代理

##### 正向代理

客户端无法直接访问目标服务器，需要通过代理服务器来进行访问。代理服务器代表客户端向目标服务器发出请求，将目标服务器的响应返回给客户端。正向代理常用于客户端无法直接访问的互联网的内部网络中，例如翻墙。正向代理，隐藏了客户端的真实信息。



##### 反向代理

客户端可以直接访问代理服务器，但代理服务器并非是目标服务器，而是代表目标服务器向客户端提供服务。客户端向代理服务器发出请求，代理服务器根据请求内容将请求转发给目标服务器，将目标服务器的响应返回给客户端。反向代理常用于负载均衡、安全过滤和隐藏真实服务器等用途。隐藏了服务器的真实信息。



![image-20230607145300721](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/image-20230607145300721.png)



##### 总结

正向代理是代理客户端，向目标服务器请求数据，而反向代理是代理服务器端，代表目标服务器向客户端提供服务。两者的主要区别在于代理的对象是谁。可以用Nginx来实现正向代理，但是目前Nginx有一个问题，那么就是不支持HTTPS。



---

---



# 其他

### 软件的生命周期

> 软件的生命周期是指从软件定义、开发、测试、部署到维护和升级的整个过程

1. 需求分析阶段：分析实际用户需求和系统需求，确定产品功能和性能要求，编写详细的需求文档。
2. 设计阶段：设计软件的系统架构、模块拆分、数据结构、算法等，编写详细的设计文档。
3. 编码阶段：根据需求定义和设计文档进行编码开发，并进行代码测试。
4. 测试阶段：对代码进行黑盒测试、白盒测试、性能测试、安全测试等。
5. 部署阶段：在测试通过后，通过自动化工具或手动部署将软件交付给用户，让用户开始使用。
6. 运维阶段：维护软件系统，包括监控系统运行状态、安全性、性能和故障排查等。
7. 升级阶段：根据用户需求的变化和新功能的加入，进行软件的迭代升级。





---

---





# Temporary

