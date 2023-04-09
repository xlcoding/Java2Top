---
title: 《BAT高频面点》Java基础高频面试题八股文（必看🔥）
category: Java
tag:
  - Java基础
head:
  - - meta
    - name: keywords
      content: JVM,JDK,JRE,字节码详解,Java 基本数据类型,装箱和拆箱
    - name: description
      content: 全网质量最高的Java基础常见知识点和面试题总结，希望对你有帮助！
---
### 1、谈谈面向对象的理解

面向过程：一件事该怎么做，**注重实现过程**，以过程为中心

面向对象：实现对象是谁，只关心怎样使用，不关心具体实现（**只关心实现对象是谁，有封装、继承、多态三大特性**）

**封装：**可以不用关心内部实现，具体构造，只需知道怎么操作它就是，比如电视，手机，将内部封装起来，直接使用

**多态：**

同一个方法调用，由于对象不同可能会有不同的行为。比如都是休息，张三是睡觉，李四是爬山等；或则具体场景中，我不知道现在具体传进来的对象是student,还是teacher，那么可以用pepole去接收它。

**多态的存在要有3个必要条件：**继承，方法重写，父类引用指向子类对象。3. 父类引用指向子类对象后，用该父类引用调用子类重写的方法，此时多态就出现了

**继承：**使代码更容易扩展，比如有学生教师，他们都有一些公用方法与属性，可以将其抽取出来定义为父类，再去继承它，**复用代码，减少冗余，易于扩展**



面向对象是一种编程思想，早期的面向过程的思想就是一件事该怎么做，而面向对象就是一件事该由谁来做，它怎么做的我不管，我只需要调用就行。而这些是由面向对象的三大特性来实现的，三大特性就是封装、继承、多态。封装就是将一类属性和行为抽象成一个类，使其属性私有化，行为公开化，提高属性的安全性的同时，也可以使代码模块化，这样做使代码的复用性更高。继承就是将几个类共有的属性和行为抽象成一个父类，每个子类都有父类的属性和行为，也有自己的属性和行为，这样做，扩展了已存在的代码，进一步提高的代码的复用性，但是继承是耦合度很高的一种关系，父类代码修改，子类行为也会改变，如果过度使用继承会起到反效果。多态必须要有继承和重写，并且父类/接口引用指向子类/实现类对象，很多的设计模式都是基于面向对象中多态性设计的。

### 2、面向对象与面向过程区别

- **面向过程** ：**面向过程性能比面向对象高。** 因为类调用时需要实例化，开销比较大，比较消耗资源，所以当性能是最重要的考量因素的时候，比如单片机、嵌入式开发、Linux/Unix 等一般采用面向过程开发。但是，**面向过程没有面向对象易维护、易复用、易扩展。**
- **面向对象** ：**面向对象易维护、易复用、易扩展。** 因为面向对象有封装、继承、多态性的特性，所以可以设计出低耦合的系统，使系统更加灵活、更加易于维护。但是，**面向对象性能比面向过程低**。

### 3、JDK与JRE区别

JDK(java developer's kit): 

​		JDK=JRE+开发工具集(java javac javadoc jar....)

JRE(java runtime environment)---java运行环境：

​		JRE=JVM+核心类库

**只运行，JRE即可，要编译就要JDK**

### 4、值传递与引用传递

### 5、==与equals()区别

=比较的是地址。对于基本数据类型比较的值，对于引用数据类型比较的是内存地址

equals() 属于object类方法，没有重写之前使用效果和==一样。可以重写例如String类，使其比较内容值是否相等

### 6、为什么重写 equals 时必须重写 hashCode ⽅法

hashcode可以获取哈希码，确定该对象在哈希表中的索引位置

- **提高效率**：使用hashcode提前检验，定位，不用每一次都使用equlas方法比较，提高效率
- **保证没有重复对象出现，确保hashmap去重性**：假如只重写equas方法，不重写hashcode，相同的对象hashCode不同，从而映射到不同下标下，HashMap无法保证去重

equals相同，hashcode相同；hashcode不同，equals一定不同；hashcode相同，equals不一定相同(哈希冲突)

### 7、深拷贝与浅拷贝

### 8、Student s = new Student();在内存中做了哪些事情

- 载入Student.class文件进内存（方法区）
- 在栈内存为s开辟空间
- 在堆内存为学生对象开辟空间
- 对学生对象的成员变量进行默认初始化
- 对学生对象的成员变量进行显示初始化
- 通过构造方法对学生对象的成员变量赋值
- 学生对象初始化完成，把对象地址赋值给s变量

![img](https://cdn.nlark.com/yuque/0/2021/png/21967782/1626501601109-66887620-e544-477d-9374-4e022752c9b2.png?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_27%2Ctext_5b6u5L-h5YWs5LyX5Y-377ya5bCP6b6ZY29kaW5n%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10)

### 9、重载和重写（Override）的区别

方法的重载和重写都是实现多态的方式，区别在于前者实现的是编译时的多态性，而后者实现的是运行时的多态性。

重载：发生在同一个类中，方法名相同参数列表不同（参数类型不同、个数不同、顺序不同），与方法返回值和访问修饰符无关，即重载的方法不能根据返回类型进行区分

重写：发生在父子类中，方法名、参数列表必须相同，返回值小于等于父类，抛出的异常小于等于父类，访问修饰符大于等于父类（里氏代换原则）；如果父类方法访问修饰符为private则子类中就不是重写。

### 10、多态理解

父类或接口定义的引用变量可以指向子类或具体实现类的实例对象，然后你编译的时候不知道这个指针指向哪里，等到运行时才知道，从而去指向对应的子类或者接口具体实现的类所指向的方法

### 11、String为何不可变不可变好处

**String 类中使⽤ final 关键字修饰字符数组来保存字符串**，jdk9后，使用byte数组。StringBuilder 与 StringBuffer 都继承⾃ AbstractStringBuilder 类，在 AbstractStringBuilder 中也是使⽤字符数组保存字符串char[]value 但是没有⽤ final 关键字修饰，所以这两种对象都是可变的。

**不可变好处**：缓存hash值(使得hash值不变，只进行一次计算)、String pool需要、线程安全、参数安全性（网络连接，参数变了，以为连接主机变了）

### 12、String有几种编码格式？

### 13、String，StringBuffer和StringBuilder之间的区别是什么？

可变性：String是不可变对象，任何对String修改都会创建新的String对象，StringBuffer和StringBuilder可变类。

效率：频繁对字符进行操作时，使用String会生成一些临时对象，多一些附加操作，效率低些。

安全性：Stringbuffer方法由synchronized修饰，线程安全。

### 14、关于String的理解

![img](https://cdn.nlark.com/yuque/0/2021/png/21967782/1626509465265-dfb56d3b-8615-4b69-a6ee-2e4be8e764df.png?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_22%2Ctext_5b6u5L-h5YWs5LyX5Y-377ya5bCP6b6ZY29kaW5n%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10)

```java
String str1 = new String("123");//再常量池创一个“123”对象，遇到new在堆内存创建一个对象，并返回堆中的对象引用
String str2 = "123";//因为之前常量池中能找到“123”的对象，所以直接将引用返回，不创建新的
String str3 = str1.intern();//若常量池中包含了str1字符串“123”,则直接返回引用，否则就在池中先创建一个在返回池中的对象引用
System.out.println((str1 == str2) +","+ (str3 == str2))
//输出 false,true
String str4 = new String("234");
String str5 = new String("234");
String str6 = str4.intern();
String str7 = str5.intern();
System.out.println((str4 == str5) +","+ (str6 == str7));
//输出false ture
```

### 15、8种基本数据类型与占内存大小

**byte**(1字节 -2的7次方到2的7次方-1)、**short**(2字节 -2的15次方到2的15次方-1)、**int**(4字节)、**float**(4)、**double**(8)、**long**(8字节)，**char**(2)、booean(4-内存对齐)，

逻辑上boolean型只占1bit，但是虚拟机底层对boolean值进行操作实际使用的是int型，操作boolean数组则使用byte型；

### 16、float 与 double/short与int

 float f = 1.1；错    

 float f=1.1f；对



short s=1;           s+=1;
	s=s+1;错            s++; （隐式类型转换 相当于 s = (short) (s + 1);）

### 17、Java集合机制与使用场景

```java
1) Collection
一组"对立"的元素，通常这些元素都服从某种规则
 　　1.1) List必须保持元素特定的顺序 (有序、可重复、查找效率高、插入删除低、下标遍历)
   		1.1.1) ArrayList
        1.1.2) Vector
        1.1.3) LinkedList
 　　1.2) Set不能有重复元素(无序、不可重复、查询效率低)
   		1.2.1) HashSet(为快速查找设计，)
        	1.2.1.1) LinkedHashSet
        1.2.2) SortSet
        	1.2.2.1) TreeSet(使得有序)
 　　1.3) Queue保持一个队列(先进先出)的顺序
   		1.3.1) PriorityQueue(模拟堆，按照元素顺序排序)
    	1.3.2) Deque
2) Map
一组成对的"键值对"对象
	2.1) HashMap
    2.2) HashSet
    2.3) SortedMap
    	2.3.1) TreeMap(基于红黑树排序 O(logn))
    2.4) ....
```

### 18、set与list区别？

1、List,Set都是继承自Collection接口

2、List特点：元素有放入顺序，元素可重复 ，Set特点：元素无放入顺序，元素不可重复，重复元素会覆盖掉，（元素虽然无放入顺序，但是元素在set中的位置是有该元素的HashCode决定的，其位置其实是固定的，加入Set 的Object必须定义equals()方法 ，另外list支持for循环，也就是通过下标来遍历，也可以用迭代器，但是set只能用迭代，因为他无序，无法用下标来取得想要的值。） 

3.Set和List对比： 

Set：检索元素效率低下，删除和插入效率高，插入和删除不会引起元素位置改变。 

List：和数组类似，List可以动态增长，查找元素效率高，插入删除元素效率低，因为会引起其他元素位置改变。 

### 19、ArrayList扩容机制

- 添加元素时使用 ensureCapacityInternal() 方法来保证容量足够，如果不够时，需要使用 grow() 方法进行扩容
- 新容量的大小为 oldCapacity + (oldCapacity >> 1)，即 oldCapacity+oldCapacity/2。其中 oldCapacity >> 1 需要取整，所以新容量大约是旧容量的 1.5 倍左右。（oldCapacity 为偶数就是 1.5 倍，为奇数就是 1.5 倍-0.5）
- 扩容操作需要调用 Arrays.copyOf() 把原数组整个复制到新数组中，这个操作代价很高，因此最好在创建 ArrayList 对象时就指定大概的容量大小，减少扩容操作的次数。
- modCount记录结构修改次数

### 20、ArrayList 与 Vector 区别呢?为什么要⽤Arraylist取代Vector呢

**实现：**都实现List接口，底层采用Object[] elementData数组，

**线程安全**：Vector 使用了 Synchronized 来实现线程同步，是线程安全的，而 ArrayList 是非线程安全的。

**性能**：ArrayList 在性能方面要优于 Vector。

**扩容**：ArrayList 和 Vector 都会根据实际的需要动态的调整容量，只不过在 Vector 扩容每次变2倍，而 ArrayList 变1.5倍

**长度**：ArrayList默认初始长度10

### 21、ArrayList和LinkedList的区别

**ArrayList与LinkedList都实现List接口**：arrayList实现了 **RandomAccess**接口，代表支持随机访问

**线程安全问题**：ArrayList与LinkedList都是线程不同步的，也就是都不保证线程安全。

**底层数据结构**：ArrayLis底层使用数组，**默认初始大小为10**；插入元素超出则会动态扩容为原来1.5倍;LinkedList底层采用**双向链表数据结构**（注意：JDK1.6之前为循环链表，JDK1.7取消了循环）。

**插入删除**：ArrayList：若增加至末尾，O(1)；若在指定位置i插入O(n-i)。LinkedList：插入删除都是近似O(1),而数组为近似 O（n）

**查询**：数组支持随机快速访问，而链表需要依次遍历，更耗时。

**占用内存空间大小**：一般LinkedList占空间更大，双向列表每个结点要维护两个指针。但是若ArrayList刚到扩容阈值，扩容后会浪费很多空间。

**数组查找原理：**数组空间连续，查询通过偏移量找，LinkList底层链表，逻辑连续，空间不连续，指针访问

### 22、HashMap 和 Hashtable 的区别

- 线程安全：Hashtable方法sychonized修饰，线程安全
- 效率方面：由于Hashtable方法被sychonized修饰，效率比HashMap低
- 底层数据结构：HashMap jdk8当链表长度>=8并且数组长度>=64链表会转红黑树，Hashtable没有这样机制
- 初始容量与扩容：默认初始量：Hashtable为11，HashMap为16；若指定初始量：Hashtable用指定的值，HashMap会扩充为 2 的幂次⽅⼤⼩。扩容：Hashtable容量变为原来2n+1倍，HashMap变为2倍。
- 对Null key与Null value支持：HashMap支持一个Null key多个Null value，Hashtable不支持Null key，否则报错空指针异常

### 23、HashSet怎样检查重复

对HashMap封装了一层，很多方法还是直接用的map的

通过计算对象的hashcode定位，同时比较与其他对象hashcode是否相等，若没有相符的则假设没有重复对象；若有相同的则equlas判断

### 24、HashMap与HashSet区别

HashSet 底层就是基于 HashMap 实现的（除了个别方法自己实现，其他调用hashmap的）。HashMap使用键(Key)计算hashcode，HashSet使用成员对象来计算hashcode值。

### 25、HashMap jdk8与jdk7区别

- JDK8中新增了红黑树，JDK8是通过数组+链表+红黑树来实现的
- JDK7中链表的插入是用的头插法，而JDK8中则改为了尾插法

- - **因为JDK1.7是用单链表进行的纵向延伸，当采用头插法时会容易出现逆序且环形链表死循环问题。但是在JDK1.8之后是因为加入了红黑树使用尾插法，能够避免出现逆序且链表死循环的问题。**

- JDK8中的因为使用了红黑树保证了插入和查询了效率，所以实际上JDK8中 的Hash算法实现的复杂度降低了
- JDK7中是先扩容再添加新元素，JDK8中是先添加新元素然后再扩容 
- JDK8中数组扩容的条件也发了变化，只会判断是否当前元素个数是否超过了阈值，而不再判断当前put进来的元素对应的数组下标位置是否有值。 

### 26、HashMap 的⻓度为什么是2的幂次⽅

注意：&与 两个为1才为1   ^异或 相同则为0，不相同则为1

因为当容量为2的幂时，h&(length-1)运算才等价于length取模，也就是h%length，而&比%具有更高的效率，也就是计算机会计算的更快。

而且这样能尽量均匀分布减少哈希冲突：

2的n次方实际就是1后面n个0，2的n次方-1实际就是n个1。这样按位“与”时，每一位都能&1，真正参与了运算，分布更均匀。

### 27、为什么要把key的哈希码右移16位呢

因为h的int类型正好32位，为了使计算出的hash值更加的分散，所以选择先将h无符号右移16位，然后再与h异或时，就能达到h的高16位和低16位都能参与计算，尽最大努力减少哈希冲突

### 28、HashMap如何确定元素放在哪个位置呢

- 经过扰动函数计算得到hash值（先计算出key的hashcode，再计算h^(h>>>16））---减少hash碰撞
- 通过 **(n - 1) & hash** 判断当前元素存放的位置

### 29、hashmap的put方法流程

**HashMap** 通过**key** 的 **hashCode** 经过扰动函数处理过后得到 **hash** 值，然后通过 **(n - 1) & hash** 判断当前元素存放的位置（这⾥的 **n** 指的是数组的⻓度），如果当前位置存在元素的话，就判断该元素与要存⼊的元素的 **hash** 值以及 **key** 是否相同，如果相同的话，直接覆盖，不相同就通过拉链法解决冲突。

- 执行put方法会执行putval方法，执行putval前先计算hash值
- 经过扰动函数使其hash值更散列（调用key对象的hashcode方法计算出来hash值，将 Hash 值的高 16 位右移并与原 Hash 值取异或运算（^），混合高 16 位和低 16 位的值，得到一个更加散列的低 16 位的 Hash 值）
- 然后进入putval方法，会判断是否第一次调用put，若是第一次才初始化数组长度16，
- 然后会判断数组该位置是否为空，若空创建结点插入，不为空若插入元素与桶中元素key一样，后面会替换。若不为空且插入元素与桶中元素key不一样，则向后添加元素。

- - jdk7,头插法
  - jdk8尾插法，遍历链表，若有相同的node,替换。否则尾插，然后再判断是否树化（链表长度>=8 进入treeifyBin(tab, hash);进入该方法还需要判断当前数组长度>=64才能树化,如果<64则扩容）

- ++modCount
- size++

### 30、HashMap并发线程安全问题？

1、在JDK1.7中，当并发执行扩容操作会造成环形链，然后调用get方法会死循环

2、JDK1.8中，并发执行put操作时会发生**数据覆盖**的操作。

### 31、hashmap扩容流程？

**扩容时多线程操作可能会导致链表成环的出现，然后调⽤get⽅法会死循环**

触发时机：1、未初始化，第一次put时；2、大于扩容阈值。

流程：新建2倍大小的数组，根据新数组长度对其值重新hash，寻址。具体会将原来数组链表拆为高低位链表，低位链表存放扩容后数组下标没变的结点，高位链表存放变了的，然后将高低位链表插入新数组

### 32、TreeMap

TreeMap是基于**红黑树**的一种**提供顺序访问**的Map，操作的时间复杂度都是**O(logn)**;默认按键的升序排序，具体顺序可有指定的comparator决定。TreeMap键、值都不能为null；hashtable也不能为null

### 33、反射原理

- **什么是反射**：动态的获取类的各个属性以及调用它的方法
- **原理**：通过将类对应的字节码文件加载到jvm内存中得到一个Class对象，通过这个Class对象可以反向获取实例的各个属性以及调用它的方法。
- **获取Class对象的方式**：

- - Object ——> getClass();（**对象.getClass(**)）
  - 任何数据类型（包括基本数据类型）都有一个“静态”的class属性 (**类.class**)
  - Class.forName("");

- **使用场景**：

- - 1、通过反射运行配置文件内容

- - - 加载配置文件，并解析配置文件得到相应信息
    - 根据解析的字符串利用反射机制获取某个类的Class实例
    - 动态配置属性

- - 2、JDK动态代理
  - 3、jdbc通过Class.forName()加载数据的驱动程序
  - 4、Spring解析xml装配Bean

### 34、object的方法有哪些？notify和notifyAll的区别？

1、getClass--final方法，获得运行时类型。

2、toString——对象的字符串表示形式（对象所属类的名称+@+转换为十六进制的对象的哈希值组成的字符串 ）

3、equas方法——如果没有重写用的就是Object里的方法，和==一样都是比较两个引用地址是否相等，或则基本数据类型值是否相等

4、Clone方法——保护方法，实现对象的浅复制，只有实现了Cloneable接口才可以调用该方法，否则抛出CloneNotSupportedException异常。

5、notify方法——唤醒在该对象上等待的某个线程

6、notifyAll方法——唤醒在该对象上等待的所有线程

7、Wait方法——wait()的作用是让当前线程进入等待状态，同时，wait()也会让当前线程释放它所持有的锁，直到其他线程调用此对象的 notify() 方法或 notifyAll() 方法”，当前线程被唤醒(进入“就绪状态”)。还有一个wait(long timeout)超时时间-补充sleep不会释放锁

8、Finalize()方法——可以用于对象的自我拯救

9、Hashcode方法——该方法用于哈希查找，可以减少在查找中使用equals的次数，重写了equals方法一般都要重写hashCode方法。这个方法在一些具有哈希功能的Collection中用到。

一般必须满足obj1.equals(obj2)==true。可以推出obj1.hash- Code()==obj2.hashCode()，但是hashCode相等不一定就满足equals。不过为了提高效率，应该尽量使上面两个条件接近等价

### 35、Java中接口和抽象类的区别？

- 方法：接口只有定义，**不能有方法的实现**，java 1.8中可以定义default与static方法体，而抽象类可以有定义与实现，方法可在抽象类中实现。
- 成员变量：接口成员变量只能是public static final的，且必须初始化，抽象类可以和普通类一样任意类型。
- 继承实现：一个类只能继承一个抽象类(extends)，可以实现多个接口（implements)
- 都不能实例化
- 接口不能有构造函数，抽象类可以有

### 36、既然有了字节流,为什么还要有字符流

 Java 虚拟机转字节得到字符流，耗时；不知道编码类型还很容易出现乱码。所以干脆提供字符流。

### 37、throw与throws区别

throw 关键字用在**方法内部**，只能用于**抛出一种异常**；throws 关键字用在**方法声明**上，可以抛出多个异常，用来**标识该方法可能抛出的异常列表**

### 38、红黑树特性？时间复杂度？

二叉查找树（二叉排序，二叉搜索树），相当于二分查找，但是可能出现线性化，相当于o(n)，于是出现了红黑树，它是自平衡的二叉搜索树，有红黑两种结点，根节点红色，叶子节点是为空的黑色结点，红黑交替，从任意结点出发到达它可达的叶子结点路径所包含的黑色结点一样，增删查时间复杂度**O(logn)**.通过变色与旋转维持平衡。左旋：逆时针旋转，让父节点右孩子当父亲；右旋：顺时针旋转，让父节点左孩子当父亲。

### 39、JDK与cjlib动态代理

动态代理好处：

一个工程如果依赖另一个工程给的接口，但是另一个工程的接口不稳定，经常变更协议，就可以使用一个代理，接口变更时，只需要修改代理，不需要一一修改业务代码

**作用：**

- **功能增强**：再原有功能加新功能
- **控制访问**：代理类不让你访问目标

**JDK动态代理**：利用反射机制生成代理类，可以动态指定代理类的目标类，要求实现invovationHandler接口，重写invoke方法进行功能增强，还要求目标类必须实现接口。

Cjlib动态代理：利用ASM开源包，把**代理对象**的CLass文件加载进来，修改其字节码文件生成子类，子类重写目标类的方法，被final修饰不可以，然后在子类采用**方法拦截技术**拦截父类方法调用，织入逻辑（定义拦截器实现MethodInterceptor接口）

![img](https://cdn.nlark.com/yuque/0/2021/jpeg/21967782/1629119795356-ae8c3234-1f0c-439f-86e3-d2db4b629da3.jpeg?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_21%2Ctext_5b6u5L-h5YWs5LyX5Y-377ya5bCP6b6ZY29kaW5n%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10)

### 40、异常体系

Throwable的子类为**Error**和**Exception**

Exception的子类为RuntimeException异常和RuntimeException以外的异常（例如IOException）。

**主要分为Error，RuntimeException异常和RuntimeException以外的异常**。(错误、运行时异常和编译时异常)

Error就是一些程序处理不了的错误，**代表JVM出现了一些错误，应用程序无法处理**。例如当 JVM 不再有继续执行操作所需的内存资源时，将出现 OutOfMemoryError。

**常见异常**：NullPointerException、ClassNotFoundException、arrayindexoutofboundsexception、ClassCastException（类型强制转换）

![img](https://cdn.nlark.com/yuque/0/2021/png/21967782/1628730829528-3bf5ce61-c244-4844-8b10-d16a9a803faf.png?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_24%2Ctext_5b6u5L-h5YWs5LyX5Y-377ya5bCP6b6ZY29kaW5n%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10)

### 41、包装类型和基本类型的区别是什么

**最主要的区别是包装类型是对象**，拥有字段和方法，可以很方便地调用一些基本的方法，**初始值是null**，而且可以使用null代表空值，而基本数据类型只能使用**0来代表初始值**。

其次是**基本数据类型是直接存储在栈**中，而包装类型是一个对象，对象的引用变量是存储在栈中，存储了对象在堆中的地址，对象的数据是存在堆中。

### 42、BIO,NIO,AIO 有什么区别

**BIO (Blocking I/O):** 同步阻塞 I/O 模式，数据的读取写⼊必须阻塞在⼀个线程内等待其完成。

**NIO (Non-blocking/New I/O):** NIO 是⼀种同步⾮阻塞的 I/O 模型

**AIO (Asynchronous I/O):** AIO 也就是 NIO 2。在 Java 7 中引⼊了 NIO 的改进版 NIO 2,它是异步⾮阻塞的 IO 模型。异步 IO 是基于事件和回调机制实现的，也就是应⽤操作之后会直接返回，不会堵塞在那⾥

### 43、谈谈常量池的理解·

class文件常量池

方法区运行时常量池（Class 文件中的常量池（编译器生成的字面量和符号引用）会在类加载后被放入这个区域），除了在编译期生成的常量，还允许动态生成，例如 String 类的 intern()。）

字符串常量池（jdk6及以前，在方法区，jdk7及以后移到堆）

八种基本类型的包装类的对象池

### 44、动态链接与静态链接



#### 3、方法引用

#### 4、Stream API

Stream流

filter（过滤）、sort（排序）、map（对给个对象映射）、limit(获取指定数量的流)

```java
List<Integer> numbers = Arrays.asList(3, 2, 2, 3, 7, 3, 5);
numbers.stream().filter(t -> t % 2 == 0).map(t -> String.valueOf(t)+"*").collect(Collectors.toList()).forEach(System.out::println);
IntSummaryStatistics stats = numbers.stream().mapToInt((x) -> x).summaryStatistics();
```

#### 5、Date Time API 

j**dk7非线程安全**+设计很差(util.Date sql.Date，Date年1900开始，月0-11，)+时区处理麻烦

Java 8引入了新的日期和时间API，它们是不变类，默认按ISO 8601标准格式化和解析；

使用LocalDateTime可以非常方便地对日期和时间进行加减，或者调整日期和时间，它总是返回新对象；

使用isBefore()和isAfter()可以判断日期和时间的先后；

使用Duration和Period可以表示两个日期和时间的“区间间隔”。

从Java 8开始，java.time包提供了新的日期和时间API，主要涉及的类型有：

本地日期和时间：LocalDateTime，LocalDate，LocalTime；

带时区的日期和时间：ZonedDateTime；

时刻：Instant；

时区：ZoneId，ZoneOffset；

时间间隔：Duration。

以及一套新的用于取代SimpleDateFormat的格式化类型DateTimeFormatter。

和旧的API相比，新API严格区分了时刻、本地日期、本地时间和带时区的日期时间，并且，对日期和时间进行运算更加方便。

**此外，新API修正了旧API不合理的常量设计：**

#### 6、Optional 类

Java8新特性：

Optional



如果为非空，返回 Optional 描述的指定值，否则返回空的 Optional。

可以保存类型T的值，或者仅仅保存null，**很好的解决空指针异常**，减少空值判断代码，可读性降低

以前：

```java
public String getCity(User user)  throws Exception{
        if(user!=null){
            if(user.getAddress()!=null){
                Address address = user.getAddress();
                if(address.getCity()!=null){
                    return address.getCity();
                }
            }
        }
        throw new Excpetion("取值错误");  
    }
```

Java8：

```java
public String getCity(User user) throws Exception{
    return Optional.ofNullable(user)
                   .map(u-> u.getAddress())
                   .map(a->a.getCity())
                   .orElseThrow(()->new Exception("取指错误"));
}

//如上所示，如果user的name的长度是小于6的，则返回。如果是大于6的，则返回一个EMPTY对象。
Optional<User> user1 = Optional.ofNullable(user).filter(u -> u.getName().length()<6);
```