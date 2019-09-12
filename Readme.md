---
typora-root-url: ./
---

[TOC]

------

### 基础

#### 类加载顺序,执行顺序

- 父类的静态字段——>父类静态代码块——>子类静态字段——>子类静态代码块——>

  父类成员变量（非静态字段）——>父类非静态代码块——>父类构造器——>子类成员变量——>子类非静态代码块——>子类构造器   

#### java 中 IO 流分为几种

- 2种，一种字节流，另外一种字符流，分别有四个抽象类表示InputStream,OutputStream,Reader,Writer

#### BIO、NIO、AIO 有什么区别

- BIO：同步并阻塞，服务器实现模式为一个连接一个线程，即客户端有连接请求时服务器端就需要启动一个线程进行处理，如果这个连接不做任何事情会造成不必要的线程开销，当然可以通过线程池机制改善
- NIO：同步非阻塞，服务器实现模式为一个请求一个线程，即客户端发送的连接请求都会注册到多路复用器上，多路复用器轮询到连接有I/O请求时才启动一个线程进行处理。
- AIO：异步非阻塞，服务器实现模式为一个有效请求一个线程，客户端的I/O请求都是由OS先完成了再通知服务器应用去启动线程进行处理。

#### Files的常用方法都有哪些？

- Files.exists() 检测文件路径是否存在
- Files.createFile()创建文件
  Files.createDirectory()创建文件夹
- Files.delete() 删除文件或者目录
- Files.copy() 复制文件
- Files.move() 移动文件
- Files.size（）查看文件个数
- Files.read() 读取文件

#### Java 浅拷贝和深拷贝的理解和实现方式

* ***浅拷贝（Shallow Copy）***：

  ![](/img/1218256-20171011182513121-1029542999.png)

  * 对于数据类型是基本数据类型的成员变量，浅拷贝会直接进行值传递，也就是将该属性值复制一份给新的对象。因为是两份不同的数据，所以对其中一个对象的该成员变量值进行修改，不会影响另一个对象拷贝得到的数据。

  * 对于数据类型是引用数据类型的成员变量，比如说成员变量是某个数组、某个类的对象等，那么浅拷贝会进行引用传递，也就是只是将该成员变量的引用值（内存地址）复制一份给新的对象。因为实际上两个对象的该成员变量都指向同一个实例。在这种情况下，在一个对象中修改该成员变量会影响到另一个对象的该成员变量值。

  **浅拷贝的实现方式主要有两种：**

  * 通过拷贝构造方法实现浅拷贝

  * 通过重写clone()方法进行浅拷贝

* ***深拷贝(Deep Copy)***：

  ![](/img/1218256-20171011190501371-68869476.png)

  * 深拷贝对引用数据类型的成员变量的对象所有的对象都开辟了内存空间；而浅拷贝只是传递地址指向，新的对象并没有对引用数据类型创建内存空间。

  **深拷贝的实现方式主要有两种**

  * 实现 Cloneable 接口，并重写 Object 类中的 `#clone()` 方法。可以实现**浅克隆**，也可以实现**深克隆**。
  * 实现 Serializable 接口，通过对象的序列化和反序列化实现克隆。可以实现真正的**深克隆**。

#### Java 对象创建的方式？

* 使用 `new` 关键字创建对象。
* 使用 Class 类的 newInstance 方法(反射机制)。
* 使用 Constructor 类的 newInstance 方法(反射机制)。
* 使用 clone 方法创建对象。
* 使用(反)序列化机制创建对象。



------

### 容器

#### comparator和comparable 区别

* Comparable 接口，在 `java.lang` 包下，用于当前对象和其它对象的比较，所以它有一个 `#compareTo(Object obj)` 方法用来排序，该方法只有一个参数。
* Comparator 接口，在 `java.util` 包下，用于传入的两个对象的比较，所以它有一个 `#compare(Object obj1, Object obj2)` 方法用来排序，该方法有两个参数。
* **如何对 Object 的 List 排序？**
  - 对 `Object[]` 数组进行排序时，我们可以用 `Arrays#sort(...)` 方法。
  - 对 `List<Object>` 数组进行排序时，我们可以用 `Collections#sort(...)` 方法。

#### 有顺序的Map实现类

* ThreeMap 和linkedHashMap是有序的（ThreeMap默认升序，LinkedHashMap则记录了插入顺序）

#### java 容器都有哪些？

* 数组,String,java.util下的集合容器

* List:存放有序,列表存储,元素可重复

* Set:无序,元素不可重复

* Map:无序,元素可重复

#### Collection 和 Collections 有什么区别？

* collection 是java集合框架中的基本接口，collections是java框架提供的针对集合的一个工具类，

#### List、Set、Map 之间的区别是什么？

* List :允许有重复的对象，可以插入null元素，是一个有序的容器，实现类：ArrayList,LinkedList.Vector
* Set:不允许有重复的对象，只允许一个null元素，是一个无序的容器，实现类：hashSet,LinkedHashSet,ThreeSet
* Map:map不是Collection的子接口或实现类，map是一个接口，map的存储是键值对形式，健唯一，map可以有随意个null值，但最多只有一个null健，TreeMap通过实现comparator和compareable维护排序顺序。实现类：hashMap,LinkedHashMap,hashTable,ThreeMap

#### HashMap 和 Hashtable 有什么区别？

* hashTable 继承Dictionary类，hashMap继承abstractMap

* hashMap允许有空的健值对，hashTable不允许

* hashTable 是同步，hashMap非同步，效率比hashTable 高

* hash值不同，hashTable直接使用对象的hashCode, hashMap重新计算hash值

* HashMap 的迭代器（Iterator）是 fail-fast 迭代器，HashTable的 enumerator 迭代器不是 fail-fast 的。

* hashTable默认容量为11，增长是
  $$
  old*2+1
  $$
  hashMap为16. 增长是 
  $$
  old*2
  $$
  

#### 如何决定使用 HashMap 还是 TreeMap？

* 对于在 Map 中插入、删除和定位元素这类操作，HashMap 是最好的选择。
* 然而，假如你需要对一个有序的 key 集合进行遍历， TreeMap 是更好的选择。

#### 说一下 HashMap 的实现原理？





**有哪些顺序的 HashMap 实现类？**

- LinkedHashMap ，是基于元素进入集合的顺序或者被访问的先后顺序排序。
- TreeMap ，是基于元素的固有顺序 (由 Comparator 或者 Comparable 确定)。

 **我们能否使用任何类作为 Map 的 key？**

我们可以使用任何类作为 Map 的 key ，然而在使用它们之前，需要考虑以下几点：

- 如果类重写了 equals 方法，它也应该重写 hashcode 方法。
- 类的所有实例需要遵循与 equals 和 hashcode 相关的规则。
- 如果一个类没有使用 equals ，你不应该在 hashcode 中使用它。
- 用户自定义 key 类的最佳实践是使之为不可变的，这样，hashcode 值可以被缓存起来，拥有更好的性能。不可变的类也可以确保hashcode 和 equals 在未来不会改变，这样就会解决与可变相关的问题了
- 那就是为何 String 和 Integer 被作为 HashMap 的 key 大量使用。

#### 说一下 HashaSet 的实现原理？

* HashSet底层由HashMap实现

* HashSet的值存放于HashMap的key上

* HashMap的value统一为PRESENT

  **HashSet 如何检查重复？**

  当你把对象加入 HashSet 时，HashSet会先计算对象的hashcode值来判断对象加入的位置，同时也会与其他加入的对象的hashcode值作比较。

  - 如果没有相符的 hashcode ，HashSet会假设对象没有重复出现。
  - 但是如果发现有相同 hashcode 值的对象，这时会调用 equals 方法来检查 hashcode 相等的对象是否真的相同。
    - 如果两者相同，HashSet 就不会让加入操作成功。
    - 如果两者不同，HashSet 就会让加入操作成功。

#### ArrayList 和 LinkedList 的区别是什么？

* ArrayList的实现是基于数组，LinkedList的实现是基于双向链表。 
*  对于随机访问，ArrayList优于LinkedList，ArrayList可以根据下标以O(1)时间复杂度对元素进行随机访问。而LinkedList的每一个元素都依靠地址指针和它后一个元素连接在一起，在这种情况下，查找某个元素的时间复杂度是O(n) 
*  对于插入和删除操作，LinkedList优于ArrayList，因为当元素被添加到LinkedList任意位置的时候，不需要像ArrayList那样重新计算大小或者是更新索引。 
* LinkedList比ArrayList更占内存，因为LinkedList的节点除了存储数据，还存储了两个引用，一个指向前一个元素，一个指向后一个元素。

#### 如何实现数组和 List 之间的转换？

* Arrays.asList,遍历

#### ArrayList 和 Vector 的区别是什么？

* Vector 是多线程安全的，线程安全就是说多线程访问同一代码，不会产生不确定的结果，而 ArrayList 不是。这个可以从源码中看出，Vector 类中的方法很多有 `synchronized` 进行修饰，这样就导致了 Vector 在效率上无法与 ArrayList 相比。

  > Vector 是一种老的动态数组，是线程同步的，效率很低，一般不赞成使用。

* 两个都是采用的线性连续空间存储元素，但是当空间不足的时候，两个类的增加方式是不同。

* Vector 可以设置增长因子，而 ArrayList 不可以。

#### Array 和 ArrayList 有何区别？

* Array 可以容纳基本类型和对象，而 ArrayList 只能容纳对象。

* Array 是指定大小的，而 ArrayList 大小是固定的，可自动扩容。

* Array 没有提供 ArrayList 那么多功能，比如 addAll、removeAll 和 iterator 等。

  **尽管 ArrayList 明显是更好的选择，但也有些时候 Array 比较好用，比如下面的三种情况**。

  - 如果列表的大小已经指定，大部分情况下是存储和遍历它们
  - 对于遍历基本数据类型，尽管 Collections 使用自动装箱来减轻编码任务，在指定大小的基本类型的列表上工作也会变得很慢。
  - 如果你要使用多维数组，使用 `[][]` 比 List 会方便。

  **ArrayList 是如何扩容的？**

   1、把原来的数组复制到另一个内存空间更大的数组中

   2、添加元素把新元素添加到扩容以后的数组中

  - 如果通过无参构造的话，初始数组容量为 0 ，当真正对数组进行添加时，才真正分配容量。每次按照 **1.5** 倍（位运算）的比率通过 copyOf 的方式扩容。
  - 在 JKD6 中实现是，如果通过无参构造的话，初始数组容量为10，每次通过 copeOf 的方式扩容后容量为原来的 **1.5** 倍。

  **ArrayList 集合加入 1 万条数据，应该怎么提高效率？**

  ArrayList 的默认初始容量为 10 ，要插入大量数据的时候需要不断扩容，而扩容是非常影响性能的。因此，现在明确了 10 万条数据了，我们可以直接在初始化的时候就设置 ArrayList 的容量！

#### 在 Queue 中 poll()和 remove()有什么区别？

* offer()和add()的区别
  add()和offer()都是向队列中添加一个元素。但是如果想在一个满的队列中加入一个新元素，调用 add() 方法就会抛出一个 unchecked 异常，而调用 offer() 方法会返回 false。可以据此在程序中进行有效的判断！
* peek()和element()的区别
  peek()和element()都将在不移除的情况下返回队头，但是peek()方法在队列为空时返回null，调用element()方法会抛出NoSuchElementException异常。

* poll()和remove()的区别
  poll()和remove()都将移除并且返回对头，但是在poll()在队列为空时返回null，而remove()会抛出NoSuchElementException异常

#### 哪些集合类是线程安全的？

* hashTable,vector,statck(堆栈类，先进后出),enumeration(枚举，相当于迭代器)

#### 迭代器 Iterator 是什么？

* Iterator 接口，提供了很多对集合元素进行迭代的方法。每一个集合类都包含了可以返回迭代器实例的迭代方法。迭代器可以在迭代的过程中删除底层集合的元素，但是不可以直接调用集合的 `#remove(Object Obj)` 方法删除，可以通过迭代器的 `#remove()` 方法删除。

#### Iterator 怎么使用？有什么特点？

* Iterator来遍历集合元素，Iterator遍历集合元素有以下几个特点:

  * Iterator遍历集合元素的过程中不允许线程对集合元素进行修改，否则会抛出   

    ConcurrentModificationEception的异常。

  * Iterator遍历集合元素的过程中可以通过remove方法来移除集合中的元素。

  * Iterator必须依附某个Collection对象而存在，Iterator本身不具有装载数据对象的功能。

  * Iterator.remove方法删除的是上一次Iterator.next()方法返回的对象。

  * 强调以下next（）方法，该方法通过游标指向的形式返回Iterator下一个元素。

#### 怎么确保一个集合不能被修改？

* Collctions包也提供了对list和set集合的方法。
  Collections.unmodifiableList(List)
  Collections.unmodifiableSet(Set)

#### Iterator 和 ListIterator 有什么区别？

* Iterator 可用来遍历 Set 和 List 集合，但是 ListIterator 只能用来遍历 List。
* Iterator 对集合只能是前向遍历，ListIterator 既可以前向也可以后向。
* ListIterator 实现了 Iterator 接口，并包含其他的功能。比如：增加元素，替换元素，获取前一个和后一个元素的索引等等。

#### **快速失败（fail-fast）和安全失败（fail-safe）的区别是什么？**

- 快速失败：当你在迭代一个集合的时候，如果有另一个线程正在修改你正在访问的那个集合时，就会抛出一个 ConcurrentModification 异常。 在 `java.util` 包下的都是快速失败。
- 安全失败：你在迭代的时候会去底层集合做一个拷贝，所以你在修改上层集合的时候是不会受影响的，不会抛出 ConcurrentModification 异常。在 `java.util.concurrent` 包下的全是安全失败的。

#### 队列和栈是什么，列出它们的区别？

- Queue是一个接口，它的实现类在Java并发包中。
  - 队列允许先进先出（FIFO）检索元素，但并非总是这样。
  - Deque 接口允许从两端检索元素。
- 栈与队列很相似，但它允许对元素进行后进先出（LIFO）进行检索。
  - Stack 是一个扩展自 Vector 的类，而 Queue 是一个接口。

------



### 线程

#### 线程的生命周期

![](/img/thread.png)

- 新建(new)，就绪(Runable) ,运行(Runing)，阻塞(Bloked),死亡(Dead) 5种状态

#### 并行和并发有什么区别？

1. 解释一：并行是指两个或者多个事件在同一时刻发生；而并发是指两个或多个事件在同一时间间隔发生。
2. 解释二：并行是在不同实体上的多个事件，并发是在同一实体上的多个事件**。**
3. 解释三：在一台处理器上“同时”处理多个任务，在多台处理器上同时处理多个任务。如hadoop分布式集群

#### 创建线程的方式及实现？

- 方式一，继承 Thread 类创建线程类。

- 方式二，通过 Runnable 接口创建线程类。

- 方式三，通过 Callable 接口和 Future 创建线程。

  ***创建线程的三种方式的对比：***

  - 使用方式一

    - 优点：编写简单，如果需要访问当前线程，则无需使用 `Thread#currentThread()` 方法，直接使用 `this` 即可获得当前线程。
    - 缺点：线程类已经继承了 Thread 类，所以不能再继承其他父类。

  - ***使用方式二、或方式三***

    - 优点：

      - 线程类只是实现了 Runnable 接口或 Callable 接口，还可以继承其他类。

      - 在这种方式下，多个线程可以共享同一个 `target` 对象，所以非常适合多个相同线程来处理同一份资源的情况，从而可以将 CPU、代码和数据分开，形成清晰的模型，较好地体现了面向对象的思想。

        

        ```
        Runnable runner = new Runnable(){ ... };
        // 通过new Thread(target, name) 方法创建新线程
        new Thread(runna,"新线程1").start();
        new Thread(runna,"新线程2").start();
        ```

        

        - 当然，实际比较少这么用。

      - 【最重要】**可以使用线程池**。

    - 缺点：编程稍微复杂，如果要访问当前线程，则必须使用`Thread#currentThread()` 方法。

 **start 和 run 方法有什么区别？**

- 当你调用 start 方法时，你将创建新的线程，并且执行在 run 方法里的代码。
- 但是如果你直接调用 run 方法，它不会创建新的线程也不会执行调用线程的代码，只会把 run 方法当作普通方法去执行。

#### sleep() 和 wait() 有什么区别？

* sleep：Thread类中定义的方法，表示线程休眠，会自动唤醒；

* wait：Object中定义的方法，需要手工调用notify()或者notifyAll()方法。  
* sleep是线程类（Thread）的方法，导致此线程暂停执行指定时间，给执行机会给其他线程，但是监控状态依然保持，到时后会自动恢复。调用sleep不会释放对象锁。 
* wait是Object类的方法，对此对象调用wait方法导致本线程放弃对象锁，进入等待此对象的等待锁定池，只有针对此对象发出notify方法（或notifyAll）后本线程才进入对象锁定池准备获得对象锁进入运行状态。

#### notify()和 notifyAll()有什么区别？







### 反射 ###

#### 什么是反射？

* Java反射就是在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意方法和属性；并且能改变它的属性。而这也是Java被视为动态语言的一个关键性质。

* **得到 Class 的三种方式**

  * 通过对象调用 getClass() 方法来获取

     通常应用在：比如你传过来一个 Object 类型的对象，而我不知道你具体是什么类，用这种方法
    　　Person p1 = new Person();
    　　Class c1 = p1.getClass();

  * 直接通过 类名.class 的方式得到,该方法最为安全可靠，程序性能更高
      这说明任何一个类都有一个隐含的静态成员变量 class
    　　Class c2 = Person.class;

  * 通过 Class 对象的 forName() 静态方法来获取，用的最多，
     但可能抛出 ClassNotFoundException 异常
    　　Class c3 = Class.forName("com.ys.reflex.Person");

* 通过 Class 类获取成员变量、成员方法、接口、超类、构造方法等

   查阅 API 可以看到 Class 有很多方法：

  * getName()：获得类的完整名字。
  * getFields()：获得类的public类型的属性。
  * getDeclaredFields()：获得类的所有属性。包括private 声明的和继承类
  * getMethods()：获得类的public类型的方法。
  * getDeclaredMethods()：获得类的所有方法。包括private 声明的和继承类
  * getMethod(String name, Class[] parameterTypes)：获得类的特定方法，name参数指定方法的名字，parameterTypes 参数指定方法的参数类型。
  * getConstructors()：获得类的public类型的构造方法。
  * getConstructor(Class[] parameterTypes)：获得类的特定构造方法，parameterTypes 参数指定构造方法的参数类型。
  * newInstance()：通过类的不带参数的构造方法创建这个类的一个对象。

#### 什么是 java 序列化？什么情况下需要序列化？

* 序列化：将 Java 对象转换成字节流的过程。

* 反序列化：将字节流转换成 Java 对象的过程

* 当 Java 对象需要在网络上传输 或者 持久化存储到文件中时，就需要对 Java 对象进行序列化处理。

  序列化的实现：类实现 Serializable 接口，这个接口没有需要实现的方法。实现 Serializable 接口是为了告诉 jvm 这个类的对象可以被序列化。

  注意事项：

  * 某个类可以被序列化，则其子类也可以被序列化
  * 声明为 static 和 transient 的成员变量，不能被序列化。static 成员变量是描述类级别的属性，transient 表示临时数据
  * 反序列化读取序列化对象的顺序要保持一致

#### 动态代理是什么？有哪些应用？

动态代理：在运行时，创建目标类，可以调用和扩展目标类的方法。

应用场景如：

- 统计每个 api 的请求耗时
- 统一的日志输出
- 校验被调用的 api 是否已经登录和权限鉴定
- Spring的 AOP 功能模块就是采用动态代理的机制来实现切面编程

#### 怎么实现动态代理？

Java 中实现动态的方式：[JDK 中的动态代理](https://blog.csdn.net/meism5/article/details/90744045) 和 [Java类库 CGLib](https://blog.csdn.net/meism5/article/details/90781518)。

**JDK代理必须要提供接口，而CGLIB则不需要，可以直接代理类**

### jsp 和 servlet 有什么区别？

* jsp更擅长表现于页面显示,servlet更擅长于[逻辑控制](https://www.baidu.com/s?wd=逻辑控制&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao).
* Servlet中没有内置对象，Jsp中的内置对象都是必须通过HttpServletRequest对象，HttpServletResponse对象以及HttpServlet对象得到.
* Jsp是Servlet的一种简化，使用Jsp只需要完成程序员需要输出到客户端的内容，Jsp中的Java脚本如何镶嵌到一个类中，由Jsp容器完成。

### jsp 有哪些内置对象？作用分别是什么？

* **request**：表示HttpServletRequest对象，用户端请求。它包含了有关浏览器请求的信息，并且提供了几个用于获取cookie, header, 和session数据的有用的方法。

* **response**：表示HttpServletResponse对象，并提供了几个用于设置送回 浏览器的响应的方法（如cookies,头信息等），网页传回用户端的回应

* **out**：对象是javax.jsp.JspWriter的一个实例，并提供了几个方法使你能用于向浏览器回送输出结果。

* **pageContext：**表示一个javax.servlet.jsp.PageContext对象。该对象提供了对JSP页面内所有的对象及名字空间（就是四大作用域空间，如page空间、request空间、session空间、application空间）的访问，也就是说他可以访问到当前请求对应session中保存的信息，也可以取当前应用所在的application的某一属性值，它相当于页面中所有功能的集大成者，包装了通用的servlet相关功能的方法。**

* **session：**表示一个请求的javax.servlet.http.HttpSession对象。Session可以存贮用户的状态信息

* **applicaton：**表示一个javax.servle.ServletContext对象。类似于系统的全局变量，用于实现Web应用中的资源共享。

* **config：**表示一个javax.servlet.ServletConfig对象。用于存放JSP编译后的初始数据。

* **page：**表示从该页面产生的一个servlet实例，JSP网页本身

* **exception：**针对错误网页，未捕捉的例外。表示JSP页面运行时产生的异常和错误信息，该对象只有在错误页面（page指令中设定isErrorPage为true的页面）中才能够使用。

* 常用内置对象:

  1. 输出输入对象:request对象、response对象、out对象

  2. 通信控制对象:pageContext对象、session对象、application对象

  3. Servlet对象:page对象、config对象

  4. 错误处理对象:exception对象

### 说一下 jsp 的 4 种作用域？

pageContext, request, session、application四个作用域中

* 如果把变量放到pageContext里，就说明它的作用域是page，它的有效范围只在当前jsp页面里。 从把变量放到pageContext开始，到jsp页面结束，你都可以使用这个变量。

* 如果把变量放到request里，就说明它的作用域是request，它的有效范围是当前请求周期。所谓请求周期，就是指从http请求发起，到服务器处理结束，返回响应的整个过程。在这个过程中可能使用forward的方式跳转了多个jsp页面，在这些页面里你都可以使用这个变量。

* 如果把变量放到session里，就说明它的作用域是session，它的有效范围是当前会话。所谓当前会话，就是指从用户打开浏览器开始，到用户关闭浏览器这中间的过程。这个过程可能包含多个请求响应。也就是说，只要用户不关浏览器，服务器就有办法知道这些请求是一个人发起的，整个过程被称为一个会话（session），而放到会话中的变量，

* 如果把变量放到application里，就说明它的作用域是application，它的有效范围是整个应用。整个应用是指从应用启动，到应用结束。我们没有说“从服务器启动，到服务器关闭”是因为一个服务器可能部署多个应用，当然你关闭了服务器，就会把上面所有的应用都关闭了。application作用域里的变量，它们的存活时间是最长的，如果不进行手工删除，它们就一直可以使用。与上述三个不同的是，application里的变量可以被所有用户共用。如果用户甲的操作修改了application中的变量，用户乙访问时得到的是修改后的值。这在其他scope中都是不会发生的，page, request, session都是完全隔离的，无论如何修改都不会影响其他

### session 和 cookie 有什么区别？

* session存储在服务器端，cookie是存储在客户端，

* session 可以存储任意对象，cookie只能存储string类型
* Session过多时会消耗服务器资源，大型网站会有专门Session服务器，Cookie存在客户端对服务器没影响
* Session在整个网页都有效，Cookie通过设置指定作用域只能在指定作用域有效
* 关闭网页Session就结束了。Cookie可以通过 setMaxAge设置有效时间，即使浏览器关闭了仍然存在

### 说一下 session 的工作原理？

### 如果客户端禁止 cookie 能实现 session 还能用吗？

### spring mvc 和 struts 的区别是什么？

### 如何避免 sql 注入？

* **采用预编译语句集**，它内置了处理SQL注入的能力，只要使用它的setString方法传值即可
  * String sql= "select * from users where username=? and password=?";
    PreparedStatement preState = conn.prepareStatement(sql);
    preState.setString(1, userName);
    preState.setString(2, password);
    ResultSet rs = preState.executeQuery();

* **采用正则表达式**将包含有 单引号(')，分号(;) 和 注释符号(--)的语句给替换掉来防止SQL注入

  public static String TransactSQLInjection(String str)

  {

  ```
    return str.replaceAll(".*([';]+|(--)+).*", " ");
  ```

  }

  userName=TransactSQLInjection(userName);

  password=TransactSQLInjection(password);

  String sql="select * from users where username='"+userName+"' and password='"+password+"' "

  Statement sta = conn.createStatement();

  ResultSet rs = sta.executeQuery(sql);

* 使用Hibernate框架的SQL注入防范 Hibernate是目前使用最多的ORM框架，在Java Web开发中，很多时候不直接使用JDBC，而使用Hibernate来提高开发效率。

### 什么是 XSS 攻击，如何避免？

XSS（Cross Site Scripting），即跨站脚本攻击，是一种常见于web应用程序中的计算机安全漏洞.XSS通过在用户端注入恶意的可运行脚本，若服务器端对用户输入不进行处理，直接将用户输入输出到浏览器，然后浏览器将会执行用户注入的脚本

#### XSS 分类

根据攻击的来源，XSS 攻击可分为存储型、反射型和 DOM 型三种。

| 类型       | 存储区*                 | 插入点*         |
| :--------- | :---------------------- | :-------------- |
| 存储型 XSS | 后端数据库              | HTML            |
| 反射型 XSS | URL                     | HTML            |
| DOM 型 XSS | 后端数据库/前端存储/URL | 前端 JavaScript |

  举例：

有一个input输入框，需要用户输入名字，用户却输入一个恶意脚本，<script>alert(document.cookie)</script>，

或者用户输入一个HTML，在标签中嵌入恶意脚本，如src，href，css style等。如：<IMG SRC="javascript:alert('XSS');">;
                                                                                                             <BODY BACKGROUND="javascript:alert('XSS')">

防御：

* XSS防御的总体思路是：**对输入(和URL参数)进行过滤，对输出进行编码**。

* 对输入和URL参数进行过滤(白名单和黑名单)

### 什么是 CSRF 攻击，如何避免？

 CSRF（Cross-site request forgery）跨站请求伪造：攻击者诱导受害者进入第三方网站，在第三方网站中，向被攻击网站发送跨站请求。利用受害者在被攻击网站已经获取的注册凭证，绕过后台的用户验证，达到冒充用户对被攻击的网站执行某项操作的目的。

一个典型的CSRF攻击有着如下的流程：

- 受害者登录a.com，并保留了登录凭证（Cookie）。
- 攻击者引诱受害者访问了b.com。
- b.com 向 a.com 发送了一个请求：a.com/act=xx。浏览器会默认携带a.com的Cookie。
- a.com接收到请求后，对请求进行验证，并确认是受害者的凭证，误以为是受害者自己发送的请求。
- a.com以受害者的名义执行了act=xx。
- 攻击完成，攻击者在受害者不知情的情况下，冒充受害者，让a.com执行了自己定义的操作。

#### 几种常见的攻击类型：

- GET类型的CSRF：

  GET类型的CSRF利用非常简单，只需要一个HTTP请求，一般会这样利用：

  ```
   <img src="http://bank.example/withdraw?amount=10000&for=hacker" >
  ```

  在受害者访问含有这个img的页面后，浏览器会自动向`http://bank.example/withdraw?account=xiaoming&amount=10000&for=hacker`发出一次HTTP请求。bank.example就会收到包含受害者登录信息的一次跨域请求。

- POST类型的CSRF：

  这种类型的CSRF利用起来通常使用的是一个自动提交的表单，如：

  ```
   <form action="http://bank.example/withdraw" method=POST>
      <input type="hidden" name="account" value="xiaoming" />
      <input type="hidden" name="amount" value="10000" />
      <input type="hidden" name="for" value="hacker" />
  </form>
  <script> document.forms[0].submit(); </script>
  ```

  访问该页面后，表单会自动提交，相当于模拟用户完成了一次POST操作。

  POST类型的攻击通常比GET要求更加严格一点，但仍并不复杂。任何个人网站、博客，被黑客上传页面的网站都有可能是发起攻击的来源，后端接口不能将安全寄托在仅允许POST上面。

- 链接类型的CSRF

  链接类型的CSRF并不常见，比起其他两种用户打开页面就中招的情况，这种需要用户点击链接才会触发。这种类型通常是在论坛中发布的图片中嵌入恶意链接，或者以广告的形式诱导用户中招，攻击者通常会以比较夸张的词语诱骗用户点击，例如：

  ```
    <a href="http://test.com/csrf/withdraw.php?amount=1000&for=hacker" taget="_blank">
    重磅消息！！
    <a/>
  ```

   防御策略：

  - 阻止不明外域的访问
    - 同源检测
    - Samesite Cookie
  - 提交时要求附加本域才能获取的信息
    - CSRF Token
    - 双重Cookie验证

### 异常

#### throw 和 throws 的区别？

* throws出现在方法函数头；而throw出现在函数体。

* throws表示出现异常的一种可能性，并不一定会发生这些异常；throw则是抛出了异常，执行

  throw则一定抛出了某种异常对象。

* 两者都是消极处理异常的方式（这里的消极并不是说这种方式不好），只是抛出或者可能抛出异常，但是不会由函数去处理异常，真正的处理异常由函数的上层调用处理。
  

#### final、finally、finalize 有什么区别？

* final表示一个修饰符
  	修饰一个类，该类不能被继承。
  	修饰一个方法，该方法不能被重写。
  	修饰一个变量，该变量一旦赋值后不能修改。

* finally用于异常处理
  	它用于修饰一个代码块，即使前面的代码处理异常，该代码块中的代码也会执行。通常用于释放资源

* finalize表示Object类中的定义的一个方法，它可以重写，用于回收资源。

#### try-catch-finally 中哪个部分可以省略？



#### try-catch-finally 中，如果 catch 中 return 了，finally 还会执行吗？

* 不管有无异常，只要存在finally，那么finally均会执行，且finally中有return时，会返回finally中return的值，且finally是在return之后执行的，只是会把finally之前的return的值保存起来，等运行结束后再进行返回

#### 常见的异常类有哪些？

* Error异常以及Exception异常，Excption又分为一般异常和常见异常，Exception一般为代码逻辑异常，通常使用try-catch-finally来对其进行捕获，而Error异常一般是JVM异常，通常情况下是不可捕获处理，难以恢复的异常。 
  一般常见异常为：
  * NullPointerException 空指针异常
  * ClassNotFoundException 指定类不存在
  * NumberFormatException 字符串转换为数字异常
  * IndexOutOfBoundsException 数组下标越界异常
  * ClassCastException 数据类型转换异常
  * FileNotFoundException 文件未找到异常
  * NoSuchMethodException 方法不存在异常
  * IOException IO 异常
  * SocketException Socket 异常

### MyBatis

####  MyBatis 编程步骤

* 创建 SqlSessionFactory 对象。

* 通过 SqlSessionFactory 获取 SqlSession 对象。
* 通过 SqlSession 获得 Mapper 代理对象。
* 通过 Mapper 代理对象，执行数据库操作。
* 执行成功，则使用 SqlSession 提交事务。
* 执行失败，则使用 SqlSession 回滚事务。
* 最终，关闭会话。

####  `{}` 和 `${}` 的区别是什么？

`${}` 是 Properties 文件中的变量占位符，它可以用于 XML 标签属性值和 SQL 内部，属于**字符串替换**。例如将 `${driver}` 会被静态替换为 `com.mysql.jdbc.Driver` ：

```
<dataSource type="UNPOOLED">   
<property name="driver" value="${driver}"/> 
<property name="url" value="${url}"/>
<property name="username" value="${username}"/>
</dataSource>
```

`${}` 也可以对传递进来的参数**原样拼接**在 SQL 中。代码如下：

```
<select id="getSubject3" parameterType="Integer" resultType="Subject"> 
SELECT * FROM subject    WHERE id = ${id}
</select>
```

- 实际场景下，不推荐这么做。因为，可能有 SQL 注入的风险。

------

`#{}` 是 SQL 的参数占位符，Mybatis 会将 SQL 中的 `#{}` 替换为 `?` 号，在 SQL 执行前会使用 PreparedStatement 的参数设置方法，按序给 SQL 的 `?` 号占位符设置参数值，比如 `ps.setInt(0, parameterValue)` 。 所以，`#{}` 是**预编译处理**，可以有效防止 SQL 注入，提高系统安全性。

------

另外，`#{}` 和 `${}` 的取值方式非常方便。例如：`#{item.name}` 的取值方式，为使用反射从参数对象中，获取 `item` 对象的 `name` 属性值，相当于 `param.getItem().getName()` 。

#### Mybatis 动态 SQL 是做什么的？都有哪些动态 SQL ？能简述一下动态 SQL 的执行原理吗？

- Mybatis 动态 SQL ，可以让我们在 XML 映射文件内，以 XML 标签的形式编写动态 SQL ，完成逻辑判断和动态拼接 SQL 的功能。
- Mybatis 提供了 9 种动态 SQL 标签：
  * `<if />`
  * `<choose />`
  * `<when />`
  * `<otherwise />`
  * `<trim />`
  * `<where />`
  * `<set />`
  * <foreach />`
  * `<bind />` 
- 其执行原理为，使用 **OGNL** 的表达式，从 SQL 参数对象中计算表达式的值，根据表达式的值动态拼接 SQL ，以此来完成动态 SQL 的功能。

#### Mapper 接口，对应的关系如下：

- 接口的全限名，就是映射文件中的 `"namespace"` 的值。

- 接口的方法名，就是映射文件中 MappedStatement 的 `"id"` 值。

- 接口方法内的参数，就是传递给 SQL 的参数。

  Mapper 接口是没有实现类的，当调用接口方法时，接口全限名 + 方法名拼接字符串作为 key 值，可唯一定位一个对应的 MappedStatement 。举例：`com.mybatis3.mappers.StudentDao.findStudentById` ，可以唯一找到 `"namespace"` 为 `com.mybatis3.mappers.StudentDao` 下面 `"id"` 为 `findStudentById` 的 MappedStatement 。

#### Mapper 接口绑定有几种实现方式,分别是怎么实现的?

接口绑定有三种实现方式：

第一种，通过 **XML Mapper** 里面写 SQL 来绑定。在这种情况下，要指定 XML 映射文件里面的 `"namespace"` 必须为接口的全路径名。

第二种，通过**注解**绑定，就是在接口的方法上面加上 `@Select`、`@Update`、`@Insert`、`@Delete` 注解，里面包含 SQL 语句来绑定。

第三种，是第二种的特例，也是通过**注解**绑定，在接口的方法上面加上 `@SelectProvider`、`@UpdateProvider`、`@InsertProvider`、`@DeleteProvider` 注解，通过 Java 代码，生成对应的动态 SQL 

#### Mybatis 是否支持延迟加载？如果支持，它的实现原理是什么？

Mybatis 仅支持 association 关联对象和 collection 关联集合对象的延迟加载。其中，association 指的就是**一对一**，collection 指的就是**一对多查询**。

在 Mybatis 配置文件中，可以配置 `<setting name="lazyLoadingEnabled" value="true" />` 来启用延迟加载的功能。默认情况下，延迟加载的功能是**关闭**的。

#### Mybatis 有哪些执行器（Executor）？

* **SimpleExecutor**：**每执行一次update或select，就开启一个Statement对象，用完立刻关闭Statement对象。

* **ReuseExecutor**：**执行update或select，以sql作为key查找Statement对象，存在就使用，不存在就创建，用完后，不关闭Statement对象，而是放置于Map内，供下一次使用。简言之，就是重复使用Statement对象。

* **BatchExecutor**：**执行update（没有select，JDBC批处理不支持select），将所有sql都添加到批处理中（addBatch()），等待统一执行（executeBatch()），它缓存了多个Statement对象，每个Statement对象都是addBatch()完毕后，等待逐一执行executeBatch()批处理。与JDBC批处理相同。

作用范围：Executor的这些特点，都严格限制在SqlSession生命周期范围内。

* Mybatis中如何指定使用哪一种Executor执行器？

  在Mybatis配置文件中，可以指定默认的ExecutorType执行器类型，也可以手动给DefaultSqlSessionFactory的创建SqlSession的方法传递ExecutorType类型参数。

### Jvm

####  `Roots`对象有哪些？
* 引用栈帧中的本地变量表的所有对象；
* 引用方法区中静态属性的所有对象；
* 引用方法区中常量的所有对象；
* 引用Native方法的所有对象。

#### 方法区如何判断是否需要回收

- 堆中不存在该类的任何实例
- 加载该类的classloader已经被回收
- 该类的java.lang.Class对象没有在任何地方被引用，也就是说无法通过反射再带访问该类的信息

四类引用的区别就在于GC时是否回收该对象

- - 强引用(Strong) 就是我们平时使用的方式 A a = new A();强引用的对象是不会被回收的
  - 软引用(Soft) 在jvm要内存溢出(OOM)时，会回收软引用的对象，释放更多内存
  - 弱引用(Weak) 在下次GC时，弱引用的对象是一定会被回收的
  - 虚引用(Phantom) 对对象的存在时间没有任何影响，也无法引用对象实力，唯一的作用就是在该对象被回收时收到一个系统通知

####  什么是类加载器

Java类加载器是Java运行时环境的一部分，负责动态加载Java类到Java虚拟机的内存空间中。类通常是按需加载，即第一次使用该类时才加载。由于有了类加载器，Java运行时系统不需要知道文件与文件系统。

* 类加载机制

 JVM把描述类数据的字节码.Class文件加载到内存，并对数据进行校验、转换解析和初始化，最终形成可以被虚拟机直接使用的java类型，这就是虚拟机的类加载机制。

#### 双亲委派模型

类加载器 Java 类如同其它的 Java 类一样，也是要由类加载器来加载的；除了启动类加载器，每个类都有其父类加载器（父子关系由组合（不是继承）来实现）；

所谓双亲委派是指每次收到类加载请求时，先将请求委派给父类加载器完成（所有加载请求最终会委派到顶层的Bootstrap ClassLoader加载器中），如果父类加载器无法完成这个加载（该加载器的搜索范围中没有找到对应的类），子类尝试自己加载。



![s](/img/879896-20160415085506488-408997874.png)





#### 类加载过程详解

​      类从被加载到虚拟机内存中开始，到卸载出内存为止，它的生命周期包括了：加载(Loading)、验证(Verification)、准备(Preparation)、解析(Resolution)、初始化(Initialization)、使用(Using)、卸载(Unloading)七个阶段，其中验证、准备、解析三个部分统称链接。

![](/img/20150905224439218.png)

1、**加载**：这个很简单，程序运行之前jvm会把编译完成的.class二进制文件加载到内存，供程序使用，用到的就是类加载器classLoader ，这里也可以看出java程序的运行并不是直接依   靠底层的操作系统，而是基于jvm虚拟机。如果没有类加载器，java文件就只是磁盘中的一个普通文件。

2、**连接**：连接是很重要的一步，过程比较复杂，分为三步  验证  》准备  》解析  　　

　　**验证**：确保类加载的正确性。一般情况由javac编译的class文件是不会有问题的，但是可能有人的class文件是自己通过其他方式编译出来的，这就很有可能不符合jvm的编译规则，这一步就是要过滤掉这部分不合法文件　

　　**准备**：为类的静态变量分配内存，将其初始化为默认值 。我们都知道静态变量是可以不用我们手动赋值的，它自然会有一个初始值 比如int 类型的初始值就是0 ；boolean类型初始值为false，引用类型的初始值为null 。 这里注意，只是为静态变量分配内存，此时是没有对象实例的　

　　**解析**：把类中的符号引用转化为直接引用。解释一下符号引用和直接引用。比如在方法A中使用方法B，A（）{B（）；}，这里的B（）就是符号引用，初学java时我们都是知道这是java的引用，以为B指向B方法的内存地址，但是这是不完整的，这里的B只是一个符号引用，它对于方法的调用没有太多的实际意义，可以这么认为，他就是给程序员看的一个标志，让程序员知道，这个方法可以这么调用，但是B方法实际调用时是通过一个指针指向B方法的内存地址，这个指针才是真正负责方法调用，他就是直接引用。

3、**初始化**：为类的静态变量赋予正确的初始值，上述的准备阶段为静态变量赋予的是虚拟机默认的初始值，此处赋予的才是程序编写者为变量分配的真正的初始值

现在java程序的执行就可以分为