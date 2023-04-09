---
title: 线程底层如何开启？ start0 底层源码分析
category: 
    - Java并发
    - 线程开启方式
    - 多线程
    - Java2Top
    - 源码分析
icon:
---

> Java2Top by 小龙coding
> 原创不易，请勿抄袭，转载注明出处，违者必究！


# 线程底层如何开启？ start0 底层源码分析

**面试官**：“听说你很熟悉并发原理相关知识？”

**小龙**：“e，还行吧~也就是练习时长两年半。”

**面试官**：“那么牛逼，你给我说说开启多线程有哪些方式？”

**小龙**：“e，就一种，一个词，start0.”

**面试官**：“卧槽！！！听不懂。。。。”

**小龙**：“一般人会说3种，4种，那是他还停留在 API层，让我 `脱下他的衣服给你看`”。

## 一、API 层线程开启的四种方式

如何开启 Java 线程？通过不同的 API 手段表面大体可以分为四种

### 1、继承Thread类

1. 定义 Thread类的子类，并重写该类的run()方法，作为线程执行体。
2. 创建 Thread 子类的实例，即创建线程对象；
3. **调用 start 方法，开启线程；**

```java
public class MyThread extends Thread {

    @Override
    public void run() {
        //doSomeThing();
    }

    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        t1.start();
    }
}
```

### 2、实现Runnable接口

 创建步骤如下：

1. 通过创建匿名内部类，并以此实例对象作为 Thread 的 target 来创建 Thread 类，这个新创建的 Thread 对象即作为真正的线程对象，开启新的线程；
2. **调用 start 方法，开启线程；**

```java
public class MyRunnable {

    public static void main(String[] args) {
        Thread t2 = new Thread(()->{
            //doSomething();
            System.out.println("22");
        },"t2");
        t2.start();
    }
}
```

### 3、实现Callable接口

创建步骤如下：

1. 定义实现 Callable 接口的实现类，实现 call 方法，这个方法是**线程执行体**；
2. 创建 Callable 实现类的实例，借助 FutureTask 得到线程执行的返回值；
3. 将 FutureTask 的实例，作为 Thread 的 target 来创建 Thread 类；
4. **调用 start 方法，开启线程；**

```java
public class MyCallable implements Callable<String> {

    @Override
    public String call() throws Exception {
        //doSomething()
        return "Java2Top";
    }

    public static void main(String[] args) throws Exception {
        MyCallable myCallable = new MyCallable();
        FutureTask<String> futureTask = new FutureTask<>(myCallable);
        Thread t3 = new Thread(futureTask, "t3");
        t3.start();
        System.out.println("线程返回结果："+futureTask.get());
    }
}
```

### 4、通过线程池

创建步骤如下：

- 创建线程池，以 Runnable 任务作为 线程执行体；
- 底层通过调用 thread.start 方法，开启线程。

```java
public class MyThreadPool {

    public static void main(String[] args) {
        ExecutorService pool = Executors.newFixedThreadPool(2);
        pool.execute(()->{
            //doSomething()
        });
    }
}
```

## 二、start0 底层源码分析

以上列举的 API 层面创建线程开启的方法便是大家 众所周知的，如果你仔细观察，相信一定发现不管何种方式创建线程启动，最终其实都是通过调用 Thread 对象 start() 方法启动线程。

那么start() 方法背后究竟发生了什么，下面我们走进源码一起探索。先看一下宏观流程分析：

![start0源码](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/concurrent202303201248215.png)

接下来看看 sart0 背后做了什么，源码分析图示：

### 1、start0

![1](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/concurrent202303191435129.png)

通过源码可以发现，线程的 start 方法背后底层最终调用的是 一个本地 native 方法  start0()，而 native 的方法是通过 JNI 对底层的 c++ 代码进行调用的。

如何查看本地方法 start0 底层是如何实现的呢？我们可以通过查看 OpenJDK 源码，在同名的 C 文件中找到注册方法。

![2](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/concurrent202303191559191.png)

### 2、JVM_StartThread

通过查看 `Thread.c` 源码发现，本地方法 `start0` 又会交给 JVM 层面的 JVM_StartThread 方法执行，`(void *)&JVM_StartThread`方法是写在 `#include "jvm.h"` 这个库文件中的。接下来我们要查 `JVM` 虚拟机底层实现的代码，但是`JVM`也分很多种类，OpenJDK使用的是基于 `hotspot` 的虚拟机，我们可以在这里找到底层源码 [hotspot源码](https://hg.openjdk.java.net/jdk8u/jdk8u/hotspot/file) [jvm.h源码](https://hg.openjdk.java.net/jdk8u/jdk8u/hotspot/file/76a9c9cf14f1/src/share/vm/prims)

`jvm.h`文件只是声明了宏，具体实现在 [jvm.cpp ](https://hg.openjdk.java.net/jdk8u/jdk8u/hotspot/file/76a9c9cf14f1/src/share/vm/prims/jvm.cpp)去查看。在 jvm.cpp 文件中，找到对应的  ` JVM_StartThread` 。从 ` JVM_StartThread` 内部实现中发现，最后是调用 `Thread::start ` 方法进行创建，继续查看 `thread.cpp` 文件源码

![Jvm.cpp](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/concurrent202303191606447.png)

这块入口代码十分重要，我们将代码展开看看：

```
JVM_ENTRY(void, JVM_StartThread(JNIEnv* env, jobject jthread))
  JVMWrapper("JVM_StartThread");
  //创建引用
  JavaThread *native_thread = NULL;

  bool throw_illegal_thread_state = false;
  {
  //加线程锁
    MutexLocker mu(Threads_lock);

    if (java_lang_Thread::thread(JNIHandles::resolve_non_null(jthread)) != NULL) {
      throw_illegal_thread_state = true;
    } else {
      jlong size =
             java_lang_Thread::stackSize(JNIHandles::resolve_non_null(jthread));

      size_t sz = size > 0 ? (size_t) size : 0;
       //重点：虚拟机创建 JavaThread， 该类内部会创建操作系统线程，然后关联 Java 线程
      native_thread = new JavaThread(&thread_entry, sz);

      if (native_thread->osthread() != NULL) {
        native_thread->prepare(jthread);
      }
    }
  }

  if (throw_illegal_thread_state) {
    THROW(vmSymbols::java_lang_IllegalThreadStateException());
  }

  assert(native_thread != NULL, "Starting null thread?");

  if (native_thread->osthread() == NULL) {
    // No one should hold a reference to the 'native_thread'.
    delete native_thread;
    if (JvmtiExport::should_post_resource_exhausted()) {
      JvmtiExport::post_resource_exhausted(
        JVMTI_RESOURCE_EXHAUSTED_OOM_ERROR | JVMTI_RESOURCE_EXHAUSTED_THREADS,
        "unable to create new native thread");
    }
    THROW_MSG(vmSymbols::java_lang_OutOfMemoryError(),
              "unable to create new native thread");
  }
	// 设置线程状态为 Runnable
  Thread::start(native_thread);

JVM_END
```

### 3、 new JavaThread

这里面至关重要的一句代码就是 `native_thread = new JavaThread(&thread_entry, sz)` ，它会调用操作系统底层创建一个线程，然后关联 Java 线程：

![image-20230319202259283](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/concurrent202303192022402.png)

这里 通过 `new JavaThread(&thread_entry, sz)` 创建了一个 `JavaThread` 对象，并将对象赋给了 `native_thread` ，最后调用 `Thread::start(native_thread);` 启动线程。

这里 通过 `new JavaThread(&thread_entry, sz)` 便生成了一个 Java 线程。里面的第一个参数传进去的 `&thread_entry `是一个函数，告诉线程创建该做啥。

**我们需要分两步理解这句代码：**

1、 `new JavaThread(&thread_entry, sz)` 此构造函数内部具体干了什么？

![image-20230319203858678](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/concurrent202303192038800.png)

这里做了两个动作，**1、首先通过  set_entry_point 将要执行的方法 entry_point 保存了起来**，以便之后调用。**2、然后又调用了 `os::create_thread` 方法，通过调用OS底层创建Java线程对应的内核线程**。这里就是 Jvm跨平台的核心，**用来支持跨平台创建线程的**。所有和操作系统相关的方法，通过统一的接口调用，底层对应不同操作系统都有不同的代码实现。

![image-20230319164247797](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/concurrent202303191642864.png)

### 4、os::create_thread

 以 Linux 为例 （[hotspot/src/os/linux/vm/os_linux.cpp](https://link.juejin.cn/?target=)），核心步骤如下：

![image-20230319205114594](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/concurrent202303192051702.png)

`os::create_thread` 主要干了两件事：

> 分配OSThread对象，创建 OSThread 内核线程对象，设置完初始状态后 调用 Linux API 创建线程。

通过Linux相关文档了解到，当 `pthread_create` 函数执行创建完线程之后会调用第三个参数（Java_start 方法）传递过去的回调函数。

### 5、java_start

查看  `java_start` 函数，主要就是调用 Thread 的 run 方法：

![image-20230319210119685](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/concurrent202303192101802.png)

### 6、JavaThread::run

而该 `thread::run` 方法，其实就是调用 在 `thread.cpp` 中 的 `JavaThread::run` 方法，接着看此方法：

![image-20230319210454166](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/concurrent202303192104258.png)

### 7、thread_main_innder()

发现，run 方法里调用 `thread_main_innder()` 方法，在 `thread_main_inner` 方法内，再调用之前创建 `JavaThread` 对象的时候传递进来的 `entry_point` 方法（也就是之前提到的 **通过  set_entry_point 将要执行的方法 entry_point 保存起来** ）

![image-20230319210644569](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/concurrent202303192106660.png)

而这个此刻  **entry_point** 就是我们 执行  `native_thread = new JavaThread(&thread_entry, sz)` 创建线程时穿进的构造参数 `&thread_entry`，我们再回到最开始的这里，接着理解  `native_thread = new JavaThread(&thread_entry, sz)` 第二步，其入参 `&thread_entry` 方法内部干了什么：

![image-20230319202259283](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/concurrent202303192022402.png)

### 7、&thread_entry

**2、其入参 `&thread_entry` 方法内部干了什么？**

![image-20230319181704714](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/concurrent202303191817826.png)

注意看 `JavaCalls::call_virtual`，它表示调用了 `call_virtual` 这个方法，其中参数 `vmSymbols::run_method_name()`

我们继续查 **vmSymbols** 到底调用了什么，这个方法是在这个文件里面的:（我们可以在这里查到`vmSymbols.cpp`的源码：[vmSymbols.hpp源码](https://hg.openjdk.java.net/jdk8u/jdk8u/hotspot/file/76a9c9cf14f1/src/share/vm/classfile/vmSymbols.hpp)）

![image-20230319211932700](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/concurrent202303192119815.png)

可见`vmSymbols::run_method_name()`就是调用了`run`方法。

当然，执行前还会更改线程线程的状态，从  `initialization` —> `RUNNABLE`.

![image-20230319163742479](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/concurrent202303191637591.png)

至此，线程便是创建完成并启动啦。其他相关细节可以自行阅读 OpenJDK源码分析。

> 相关代码：`start0()`底层 c 代码地址：[start0()底层c代码](https://hg.openjdk.java.net/jdk8u/jdk8u/jdk/file/f0b93fbd8cf8/src/share/native/java/lang/Thread.c)、[hotspot源码](https://hg.openjdk.java.net/jdk8u/jdk8u/hotspot/file) [jvm.h源码](https://hg.openjdk.java.net/jdk8u/jdk8u/hotspot/file/76a9c9cf14f1/src/share/vm/prims)、[jvm.cpp](https://hg.openjdk.java.net/jdk8u/jdk8u/hotspot/file/76a9c9cf14f1/src/share/vm/prims/jvm.cpp)