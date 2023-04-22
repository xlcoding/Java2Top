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

**封装**：可以不用关心内部实现，具体构造，只需知道怎么操作它就是，比如电视，手机，将内部封装起来，直接使用

**多态**：同一个方法调用，由于对象不同可能会有不同的行为。

> 比如都是休息，张三是睡觉，李四是爬山等；或则具体场景中，我不知道现在具体传进来的对象是 `Student`,还是 `Teacher`，那么可以用 `Pepole` 去接收它。

**多态的存在要有3个必要条件**：继承，方法重写，父类引用指向子类对象。3. 父类引用指向子类对象后，用该父类引用调用子类重写的方法，此时多态就出现了

**继承**：使代码更容易扩展，比如有学生教师，他们都有一些公用方法与属性，可以将其抽取出来定义为父类，再去继承它，**复用代码，减少冗余，易于扩展**

### 2、面向对象与面向过程区别

- **面向过程** ：**面向过程性能比面向对象高。** 因为类调用时需要实例化，开销比较大，比较消耗资源，所以当性能是最重要的考量因素的时候，比如单片机、嵌入式开发、Linux/Unix 等一般采用面向过程开发。但是，**面向过程没有面向对象易维护、易复用、易扩展。**
- **面向对象** ：**面向对象易维护、易复用、易扩展。** 因为面向对象有封装、继承、多态性的特性，所以可以设计出低耦合的系统，使系统更加灵活、更加易于维护。但是，**面向对象性能比面向过程低**。

### 3、JDK 与 JRE 区别

`简单总结`：

**JDK（Java Developer's Kit）**

JDK = JRE + 开发工具集（java javac javadoc jar....）

**JRE（Java Runtime Environment)** java运行环境

JRE = JVM + 核心类库

**只运行，JRE即可，要编译就要JDK**

![image-20230419230213841](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/java/k202304192302967.png)

### 4、值传递与引用传递

Java 语言是**值传递**。Java 语言的方法调用只支持参数的值传递。当一个对象实例作为一个参数被传递到方法中时，参数的值就是对该对象的引用。对象的属性可以在被调用过程中被改变，但对对象引用的改变是不会影响到调用者的。

JVM 的内存分为堆和栈，其中栈中存储了基本数据类型和引用数据类型实例的地址，也就是对象地址。

而对象所占的空间是在堆中开辟的，所以传递的时候可以理解为把变量存储的对象地址给传递过去，因此引用类型也是值传递。

### 5、==与equals()区别

= 比较的是地址。对于基本数据类型比较的值，对于引用数据类型比较的是内存地址

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

![image-20230419230633023](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/java/k202304192306154.png)

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

short s=1；s+=1;

s=s+1；错

s++; （隐式类型转换 相当于 s = (short) (s + 1);）

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

![Java反射相关类](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/java/k202304192304283.png)

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

