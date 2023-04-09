---
title: 《BAT高频面点》JDK集合框架高频面试题八股文（必看🔥）
category: 
   - Java
   - JDK集合
tag:
  - List
  - Map
  - Set
head:
  - - meta
    - name: keywords
      content: Collection,List,Set,Queue,Deque,PriorityQueue
    - name: description
      content: 图解《JDK集合-BAT高频面题》全网质量最高JDK集合高频面试题总结，希望对你有帮助
---

## 一、总览

## 1、Java集合机制与使用场景

集合相关类和接口都在 `java.util` 中，主要由两个根接口 **Collection** 和 **Map** 派生出来的，Collection 存储着对象的集合，而 Map 存储着键值对(两个对象)的映射表。

Collection派生出了三个子接口：List、Set、Queue（Java5新增的队列），因此Java集合大致也可分成List、Set、Queue、Map四种接口体系。

![集合](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/java/collection202304011958016.png)

**其各自特性与场景如下**：

```java
1) Collection 一组 "对立" 的元素，通常这些元素都服从某种规则

- 1.1) List 必须保持元素特定的顺序 (有序、可重复、查找效率高、插入删除低、下标遍历)
  - 1.1.1) ArrayList
  - 1.1.2) Vector
  - 1.1.3) LinkedList
- 1.2) Set 不能有重复元素 (无序、不可重复、查询效率低)
  - 1.2.1) HashSet(为快速查找设计，)
    - 1.2.1.1) LinkedHashSet
  - 1.2.2) SortSet
    - 1.2.2.1) TreeSet(使得有序)
- 1.3) Queue保持一个队列(先进先出)的顺序
  - 1.3.1) PriorityQueue(模拟堆，按照元素顺序排序)
  - 1.3.2) Deque

2) Map 一组成对的"键值对"对象

- 2.1) HashMap
- 2.2) HashSet
- 2.3) SortedMap
  - 2.3.1) TreeMap(基于红黑树排序 O(logn))
- 2.4) ....
```

## 二、Collection

### List

### 1、ArrayList 与 Vector 区别呢？为什么要⽤ArrayList取代Vector呢

**实现：**都实现List接口，底层采用Object[] elementData数组，

**线程安全**：Vector 使用了 Synchronized 来实现线程同步，是线程安全的，而 ArrayList 是非线程安全的。

**性能**：ArrayList 在性能方面要优于 Vector。

**扩容**：ArrayList 和 Vector 都会根据实际的需要动态的调整容量，只不过在 Vector 扩容每次变2倍，而 ArrayList 变1.5倍

**长度**：ArrayList默认初始长度10

### 2、ArrayList和LinkedList的区别

**ArrayList与LinkedList都实现List接口**：arrayList实现了 **RandomAccess**接口，代表支持随机访问

**线程安全问题**：ArrayList与LinkedList都是线程不同步的，也就是都不保证线程安全。

**底层数据结构**：ArrayLis底层使用数组，**默认初始大小为10**；插入元素超出则会动态扩容为原来1.5倍;LinkedList底层采用**双向链表数据结构**（注意：JDK1.6之前为循环链表，JDK1.7取消了循环）。

**插入删除**：ArrayList：若增加至末尾，O(1)；若在指定位置i插入O(n-i)。LinkedList：插入删除都是近似O(1),而数组为近似 O（n）

**查询**：数组支持随机快速访问，而链表需要依次遍历，更耗时。

**占用内存空间大小**：一般LinkedList占空间更大，双向列表每个结点要维护两个指针。但是若ArrayList刚到扩容阈值，扩容后会浪费很多空间。

**数组查找原理**：数组空间连续，查询通过偏移量找，LinkList底层链表，逻辑连续，空间不连续，指针访问

![arrayList](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/java/collection202304012054974.png)

### 3、ArrayList扩容机制

**一句话理解**：`ArrayList` 扩容的本质就是计算出新扩容数组的size后实例化，并将原有数组内容复制到新数组中去。**默认情况下，新的容量会是原容量的1.5倍**。

**具体剖析**🍬：

- 添加元素时使用 ensureCapacityInternal() 方法来保证容量足够，如果不够时，需要使用 grow() 方法进行扩容
- 新容量的大小为 oldCapacity + (oldCapacity >> 1)，即 oldCapacity+oldCapacity/2。其中 oldCapacity >> 1 需要取整，所以新容量大约是旧容量的 1.5 倍左右。（oldCapacity 为偶数就是 1.5 倍，为奇数就是 1.5 倍-0.5）
- 扩容操作需要调用 Arrays.copyOf() 把原数组整个复制到新数组中，这个操作代价很高，因此最好在创建 ArrayList 对象时就指定大概的容量大小，减少扩容操作的次数。
- modCount记录结构修改次数

**浅析源码🍖：**

```jAVA
public boolean add(E e) {
    //判断是否可以容纳e，若能，则直接添加在末尾；若不能，则进行扩容，然后再把e添加在末尾
    ensureCapacityInternal(size + 1);  // Increments modCount!!
    //将e添加到数组末尾
    elementData[size++] = e;
    return true;
    }

// 每次在add()一个元素时，arraylist都需要对这个list的容量进行一个判断。通过ensureCapacityInternal()方法确保当前ArrayList维护的数组具有存储新元素的能力，经过处理之后将元素存储在数组elementData的尾部

private void ensureCapacityInternal(int minCapacity) {
      ensureExplicitCapacity(calculateCapacity(elementData, minCapacity));
}

private static int calculateCapacity(Object[] elementData, int minCapacity) {
        //如果传入的是个空数组则最小容量取默认容量与minCapacity之间的最大值
        if (elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA) {
            return Math.max(DEFAULT_CAPACITY, minCapacity);
        }
        return minCapacity;
    }
    
  private void ensureExplicitCapacity(int minCapacity) {
        modCount++;
        // 若ArrayList已有的存储能力满足最低存储要求，则返回add直接添加元素；如果最低要求的存储能力>ArrayList已有的存储能力，这就表示ArrayList的存储能力不足，因此需要调用 grow();方法进行扩容
        if (minCapacity - elementData.length > 0)
            grow(minCapacity);
    }


private void grow(int minCapacity) {
        // 获取elementData数组的内存空间长度
        int oldCapacity = elementData.length;
        // 扩容至原来的1.5倍
        int newCapacity = oldCapacity + (oldCapacity >> 1);
        //校验容量是否够
        if (newCapacity - minCapacity < 0)
            newCapacity = minCapacity;
        //若预设值大于默认的最大值，检查是否溢出
        if (newCapacity - MAX_ARRAY_SIZE > 0)
            newCapacity = hugeCapacity(minCapacity);
        // 调用Arrays.copyOf方法将elementData数组指向新的内存空间
         //并将elementData的数据复制到新的内存空间
        elementData = Arrays.copyOf(elementData, newCapacity);
    }
```

### 4、如何实现 ArrayList 线程安全？

ArrayList 是线程不安全的集合类，保证 ArrayList 的线程安全通常可以采用以下方案：

- 使用 **Vector** 代替 ArrayList。（不推荐，Vector是一个历史遗留类）；
- 使用 **Collections.synchronizedList** 包装 ArrayList，然后操作包装后的 list；
- 使用 **CopyOnWriteArrayLis**t 代替 ArrayList；
- 在使用 ArrayList 时，应用程序**通过同步机制去控制** ArrayList 的读写。

### 5、CopyOnWriteArrayList场景与原理

`CopyOnWriteArrayList` 相当于是线程安全版本的ArrayList。见名知意 `CopyOnWrite`——底层实现便是采用**读写分离**，**写时复制**的并发策略。

其实现了 List 接口，内部持有 ReentrantLock 对象，底层使用 volatile transient 声明得数组，读写分离。写时会先复制，先用 ReetrantLock 对象加锁，然后会复制一份原数组再进行写操作，写完了再将新数组值赋予原数组。**适合读多写少场景**。

### Set

::: tip 提示

记住 set 具有去重性即可，其他不是那么重要。重点在 List、Map~🍻

:::

### 1、HashSet怎样检查重复

对 HashMap 封装了一层，很多方法还是直接用的 map 的

通过计算对象的 hashcode 定位，同时比较与其他对象 hashcode 是否相等，若没有相符的则假设没有重复对象；若有相同的则equlas判断

### 2、HashMap与HashSet区别

HashSet 底层就是基于 HashMap 实现的（除了个别方法自己实现，其他调用 hashmap 的）。HashMap使用键(Key)计算hashcode，HashSet使用成员对象来计算hashcode值。

## 三、Map

### 1、HashMap的底层数据结构？

JDK1.7的数据结构是`数组`+`链表`

JDK1.8的数据结构是`数组`+`链表`+`红黑树`。

数据结构示意图如下：

![jdk1.8 hashmap数据结构示意图](https://cdn.tobebetterjavaer.com/tobebetterjavaer/images/sidebar/sanfene/collection-8.png)

其中，桶数组是用来存储数据元素，链表是用来解决冲突，红黑树是为了提高查询的效率。

- 数据元素通过映射关系，也就是散列函数，映射到桶数组对应索引的位置
- 如果发生冲突，从冲突的位置拉一个链表，插入冲突的元素
- 如果链表长度>8&数组大小>=64，链表转为红黑树
- 如果红黑树节点个数<6 ，转为链表

### 2、HashMap在jdk8中做了哪些优化？

jdk1.8 的HashMap主要有五点优化：

1. **数据结构**：数组 + 链表改成了数组 + 链表或红黑树

   `原因`：发生 hash 冲突，元素会存入链表，链表过长转为红黑树，将时间复杂度由`O(n)`降为`O(logn)`

2. **链表插入方式**：链表的插入方式从头插法改成了尾插法

   简单说就是插入时，如果数组位置上已经有元素，1.7 将新元素放到数组中，原始节点作为新节点的后继节点，1.8 遍历链表，将元素放置到链表的最后。

   `原因`：因为 1.7 头插法扩容时，头插法会使链表发生反转，多线程环境下会产生环。

3. **扩容rehash**：扩容的时候 1.7 需要对原数组中的元素进行重新 hash 定位在新数组的位置，1.8 采用更简单的判断逻辑，不需要重新通过哈希函数计算位置，新的位置不变或索引 + 新增容量大小。

   `原因：`提高扩容的效率，更快地扩容。

4. **扩容时机**：在插入时，1.7 先判断是否需要扩容，再插入，1.8 先进行插入，插入完成再判断是否需要扩容；

5. **散列函数**：1.7 做了四次移位和四次异或，jdk1.8只做一次。

   `原因`：做 4 次的话，边际效用也不大，改为一次，提升效率。

### 3、解决Hash冲突的办法有哪些？HashMap用的什么？

解决Hash冲突方法有:开放定址法、再哈希法、链地址法（拉链法）、建立公共溢出区。HashMap中采用的是 链地址法 。

- **开放定址法**：也称为`再散列法`，基本思想就是，如果`p=H(key)`出现冲突时，则以`p`为基础，再次hash，`p1=H(p)`,如果p1再次出现冲突，则以p1为基础，以此类推，直到找到一个不冲突的哈希地址`pi`。 因此开放定址法所需要的hash表的长度要大于等于所需要存放的元素，而且因为存在再次hash，所以`只能在删除的节点上做标记，而不能真正删除节点。`
- **再哈希法**(双重散列，多重散列)：提供多个不同的hash函数，当`R1=H1(key1)`发生冲突时，再计算`R2=H2(key1)`，直到没有冲突为止。 这样做虽然不易产生堆集，但增加了计算的时间。
- **链地址法**(拉链法)：将哈希值相同的元素构成一个同义词的单链表,并将单链表的头指针存放在哈希表的第i个单元中，查找、插入和删除主要在同义词链表中进行。链表法适用于经常进行插入和删除的情况。
- **建立公共溢出区**：将哈希表分为公共表和溢出表，当溢出发生时，将所有溢出数据统一放到溢出区。

![image-20230402123528260](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/java/collection202304021235384.png)

### 4、Hash冲突时，为什么使用红黑树？

### 5、HashMap的put流程

**HashMap** 通过**key** 的 **hashCode** 经过扰动函数处理过后得到 **hash** 值，然后通过 **(n - 1) & hash** 判断当前元素存放的位置（这⾥的 **n** 指的是数组的⻓度），如果当前位置存在元素的话，就判断该元素与要存⼊的元素的 **hash** 值以及 **key** 是否相同，如果相同的话，直接覆盖，不相同就通过拉链法解决冲突。

- 执行put方法会执行putval方法，执行putval前先计算hash值
- 经过扰动函数使其hash值更散列（调用key对象的hashcode方法计算出来hash值，将 Hash 值的高 16 位右移并与原 Hash 值取异或运算（^），混合高 16 位和低 16 位的值，得到一个更加散列的低 16 位的 Hash 值）
- 然后进入putval方法，会判断是否第一次调用put，若是第一次才初始化数组长度16，
- 然后会判断数组该位置是否为空，若空创建结点插入，不为空若插入元素与桶中元素key一样，后面会替换。若不为空且插入元素与桶中元素key不一样，则向后添加元素。

- - jdk7,头插法
  - jdk8尾插法，遍历链表，若有相同的node,替换。否则尾插，然后再判断是否树化（链表长度>=8 进入treeifyBin(tab, hash);进入该方法还需要判断当前数组长度>=64才能树化,如果<64则扩容）

- ++modCount
- size++

![HashMap](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/java/collection202304021105163.png)

### 一般用什么作为HashMap的key？

一般用Integer、String 这种不可变类当 HashMap 当 key，而且 String 最为常用。

- 因为字符串是不可变的，所以在它创建的时候 hashcode 就被缓存了，不需要重新计算。这就是 HashMap 中的键往往都使用字符串的原因。
- 因为获取对象的时候要用到 equals() 和 hashCode() 方法，那么键对象正确的重写这两个方法是非常重要的,这些类已经很规范的重写了 hashCode() 以及 equals() 方法。

### 6、HashMap 的⻓度为什么是2的幂次⽅

注意：&与 两个为1才为1   ^异或 相同则为0，不相同则为1

因为当容量为2的幂时，h&(length-1)运算才等价于length取模，也就是h%length，而&比%具有更高的效率，也就是计算机会计算的更快。

而且这样能尽量均匀分布减少哈希冲突：

2的n次方实际就是1后面n个0，2的n次方-1实际就是n个1。这样按位“与”时，每一位都能&1，真正参与了运算，分布更均匀。

### 7、为什么要把key的哈希码右移16位呢

因为h的int类型正好32位，为了使计算出的hash值更加的分散，所以选择先将h无符号右移16位，然后再与h异或时，就能达到h的高16位和低16位都能参与计算，尽最大努力减少哈希冲突

### 8、HashMap如何确定元素放在哪个位置呢

- 经过扰动函数计算得到hash值（先计算出key的hashcode，再计算h^(h>>>16））---减少hash碰撞
- 通过 **(n - 1) & hash** 判断当前元素存放的位置

### 9、hashmap扩容流程？

**扩容时多线程操作可能会导致链表成环的出现，然后调⽤get⽅法会死循环**

**触发时机**：1、未初始化，第一次put时；2、大于扩容阈值。

**流程**：新建2倍大小的数组，根据新数组长度对其值重新hash，寻址。具体会将原来数组链表拆为高低位链表，低位链表存放扩容后数组下标没变的结点，高位链表存放变了的，然后将高低位链表插入新数组。

**优化点**：而扩容中有一个非常重要的点，就是jdk1.8中的优化操作，可以不需要再重新计算每一个元素的哈希值。

因为HashMap的初始容量是2的次幂，扩容之后的长度是原来的二倍，新的容量也是2的次幂，所以，元素，要么在原位置，要么在原位置再移动2的次幂。

### 10、讲一讲快速失败(fail-fast)和安全失败(fail-safe)

**快速失败（fail—fast）**

- 在用迭代器遍历一个集合对象时，如果遍历过程中对集合对象的内容进行了修改（增加、删除、修改），则会抛出Concurrent Modification Exception。
- 原理：迭代器在遍历时直接访问集合中的内容，并且在遍历过程中使用一个 modCount 变量。集合在被遍历期间如果内容发生变化，就会改变modCount的值。每当迭代器使用hashNext()/next()遍历下一个元素之前，都会检测modCount变量是否为expectedmodCount值，是的话就返回遍历；否则抛出异常，终止遍历。
- 注意：这里异常的抛出条件是检测到 modCount！=expectedmodCount 这个条件。如果集合发生变化时修改modCount值刚好又设置为了expectedmodCount值，则异常不会抛出。因此，不能依赖于这个异常是否抛出而进行并发操作的编程，这个异常只建议用于检测并发修改的bug。
- 场景：java.util包下的集合类都是快速失败的，不能在多线程下发生并发修改（迭代过程中被修改），比如HashMap、ArrayList 这些集合类。

**安全失败（fail—safe）**

- 采用安全失败机制的集合容器，在遍历时不是直接在集合内容上访问的，而是先复制原有集合内容，在拷贝的集合上进行遍历。
- 原理：由于迭代时是对原集合的拷贝进行遍历，所以在遍历过程中对原集合所作的修改并不能被迭代器检测到，所以不会触发Concurrent Modification Exception。
- 缺点：基于拷贝内容的优点是避免了Concurrent Modification Exception，但同样地，迭代器并不能访问到修改后的内容，即：迭代器遍历的是开始遍历那一刻拿到的集合拷贝，在遍历期间原集合发生的修改迭代器是不知道的。
- 场景：java.util.concurrent包下的容器都是安全失败，可以在多线程下并发使用，并发修改，比如：ConcurrentHashMap。

### 11、HashMap并发线程安全问题？

**简记**：

1、在JDK1.7中，当并发执行扩容操作会造成环形链，然后调用get方法会死循环

2、在JDK1.8 & JDK1.7中，并发执行put操作时会发生**数据覆盖**的操作。

**详细**：

- 多线程下扩容死循环。JDK1.7 中的 HashMap 使用头插法插入元素，在多线程的环境下，扩容的时候有可能导致环形链表的出现，形成死循环。因此，JDK1.8 使用尾插法插入元素，在扩容时会保持链表元素原本的顺序，不会出现环形链表的问题。
- 多线程的 put 可能导致元素的丢失。多线程同时执行 put 操作，如果计算出来的索引位置是相同的，那会造成前一个 key 被后一个 key 覆盖，从而导致元素的丢失。此问题在 JDK 1.7 和 JDK 1.8 中都存在。
- put 和 get 并发时，可能导致 get 为 null。线程 1 执行 put 时，因为元素个数超出 threshold 而导致 rehash，线程 2 此时执行 get，有可能导致这个问题。这个问题在 JDK 1.7 和 JDK 1.8 中都存在

![image-20230402131749910](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/java/collection202304021317992.png)

### 如何解决HashMap线程不安全的问题？

Java 中有 `HashTable`、`Collections.synchronizedMap`、以及 `ConcurrentHashMap` 可以实现线程安全的 Map。

- `HashTable` 是直接在操作方法上加 synchronized 关键字，锁住整个table数组，粒度比较大；
- `Collections.synchronizedMap` 是使用 Collections 集合工具的内部类，通过传入 Map 封装出一个 SynchronizedMap 对象，内部定义了一个对象锁，方法内通过对象锁实现；
- `ConcurrentHashMap` 在jdk1.7中使用分段锁，在jdk1.8中使用CAS+synchronized

### 12、ConcurrentHashMap 的实现原理是什么？

ConcurrentHashMap 在 JDK1.7 和 JDK1.8 的实现方式是不同的。

最大区别在于，ConcurrentHashmap线程安全在jdk1.7版本是基于`分段锁`实现，在jdk1.8是基于`CAS+synchronized`实现。细看：

**先来看下JDK1.7**

数据结构：Segment数组+HashEntry数组+链表

```
一个Segment中包含一个HashEntry数组，每个HashEntry又是一个链表结构

static final class Segment<K,V> extens ReentrantLock implements Serializable{

transient volatile HashEntry<K,V>[] tables;
//.....
}
static final class HashEntry<K,V>
{
  final int hash;
  final K key;
  volatile V value;
  volatile HashEntry<K,V> next;
}
```

- 锁机制：Segmen继承了ReentrantLock，分段锁，每次只锁定操作的segment，segment数组默认16（并发度16）
- get：二次hash，第一次Hash定位到Segment，第二次Hash定位到元素所在的链表的头部，get方法无需加锁，volatile保证
- put

- - 会二次hash定位到插入位置
  - 第一次根据key的hash值定位到segment位置，若segment数组还未初始化，cas将其赋值
  - 第二次hash定位到HashEntry位置
  - 然后插入元素时，会尝试获取锁，成功插入链表尾端，失败自旋再次获取锁，超过指定次数就挂起等待唤醒

- 链表遍历时间复杂度O(n)

**再来看下JDK1.8**

**数据结构**：Node数组+链表+红黑树

**锁机制**

- 抛弃Segment分段锁，采用CAS+synchronized，锁粒度更细
- 只锁住链表头节点（红黑树根结点），不影响其他哈希桶数组元素的读写，提高并发度

**put**

- 1、根据key计算出hash值
- 2、判断是否需要初始化
- 3、定位到对应槽位，拿到首结点f，判断首结点f

- - 3.1、若f==null,则通过CAS的方式尝试添加
  - 3.2、若f.hash=MOVED=-1，说明其他线程在扩容，参与一起扩容
  - 3.3、若都不满足，synchronized锁住f结点，判断是链表还是红黑树插入结点

- 4、当链表长度>=8，进行数组扩容或则链表树化

红黑树遍历O(logN)

#### 为何不支持null value？

vaule为null，有两种情况，可能是存的值为null或则没有映射到值返回null，hashmap用于单线程下可以通过containskey()区分这两种情况，但是ConcurrentHashMap用于多线程场景，本来是没有映射containskey返回fasle，但是可能在你调用containskey检查时新线程插入null值，返回ture，存在二义性

#### ConcurrentHashMap迭代器弱一致性

迭代器创建后，遍历每个元素，若遍历过程钟内部元素变化，变化发生在遍历过的部分迭代器不会反映出来，没遍历过的部分反映出来

#### 多线程先安全操作Map？

Collection.synchronizedMap（对方法加同步锁，本质也是全表锁）

### 13. JDK1.7与JDK1.8 中ConcurrentHashMap 的区别？

- **数据结构**：取消了`Segment分段锁` 的数据结构，取而代之的是 `数组+链表+红黑树` 的结构。
- **保证线程安全机制**：JDK1.7采用Segment的分段锁机制实现线程安全，其中segment继承自ReentrantLock。JDK1.8 采用CAS+Synchronized保证线程安全。
- **锁的粒度**：原来是对需要进行数据操作的Segment加锁，现调整为对每个数组元素加锁（Node）。
- **链表转化为红黑树**：定位结点的hash算法简化会带来弊端,Hash冲突加剧,因此在链表节点数量大于8时，会将链表转化为红黑树进行存储。
- **查询时间复杂度**：从原来的遍历链表O(n)，变成遍历红黑树O(logN)。

### 14. ConcurrentHashMap 的 put 方法执行逻辑是什么？

**先来看JDK1.7**

首先，会尝试获取锁，如果获取失败，利用自旋获取锁；如果自旋重试的次数超过 64 次，则改为阻塞获取锁。

获取到锁后：

1. 将当前 Segment 中的 table 通过 key 的 hashcode 定位到 HashEntry。
2. 遍历该 HashEntry，如果不为空则判断传入的 key 和当前遍历的 key 是否相等，相等则覆盖旧的 value。
3. 不为空则需要新建一个 HashEntry 并加入到 Segment 中，同时会先判断是否需要扩容。
4. 释放 Segment 的锁。

**再来看JDK1.8**

大致可以分为以下步骤：

1. 根据 key 计算出 hash值。
2. 判断是否需要进行初始化。
3. 定位到 Node，拿到首节点 f，判断首节点 f：
   - 如果为 null ，则通过cas的方式尝试添加。
   - 如果为 `f.hash = MOVED = -1` ，说明其他线程在扩容，参与一起扩容。
   - 如果都不满足 ，synchronized 锁住 f 节点，判断是链表还是红黑树，遍历插入。
4. 当在链表长度达到8的时候，数组扩容或者将链表转换为红黑树。

### 15. ConcurrentHashMap 和Hashtable的效率哪个更高？为什么？

ConcurrentHashMap 的效率要高于Hashtable，因为Hashtable给整个哈希表加了一把大锁从而实现线程安全。而ConcurrentHashMap 的锁粒度更低，在JDK1.7中采用分段锁实现线程安全，在JDK1.8 中采用`CAS+Synchronized`实现线程安全。

### 16、TreeMap

TreeMap 是基于**红黑树**的一种**提供顺序访问**的 Map，操作的时间复杂度都是 **O(logn)** ;默认按键的升序排序，具体顺序可有指定的comparator 决定。TreeMap 键、值都不能为 null；hashtable 也不能为 null