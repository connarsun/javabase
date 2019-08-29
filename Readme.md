[TOC]

------

### 基础

#### 类加载顺序,执行顺序

- 父类的静态字段——>父类静态代码块——>子类静态字段——>子类静态代码块——>
- 父类成员变量（非静态字段）——>父类非静态代码块——>父类构造器——>子类成员变量——>子类非静态代码块——>子类构造器   

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

------

### 数据结构

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

  - 如果通过无参构造的话，初始数组容量为 0 ，当真正对数组进行添加时，才真正分配容量。每次按照 **1.5** 倍（位运算）的比率通过 copeOf 的方式扩容。
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

- ![]()java.util.Queue是一个接口，它的实现类在Java并发包中。
  - 队列允许先进先出（FIFO）检索元素，但并非总是这样。
  - Deque 接口允许从两端检索元素。
- 栈与队列很相似，但它允许对元素进行后进先出（LIFO）进行检索。
  - Stack 是一个扩展自 Vector 的类，而 Queue 是一个接口。

------



### 线程

#### 线程的生命周期

- 新建(new)，就绪(Runable) ,运行(Runing)，阻塞(Bloked),死亡(Dead) 5种状态



 



