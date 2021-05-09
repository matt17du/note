### 内存区域

线程共享：堆和方法区

非线程共享：程序计数机器、虚拟机栈、本地方法栈

#### 如何看待OOM

没有继续执行操作所需要的内存时就会产生内存溢出。内存溢出有以下几种：

- `java.lang.OutOfMemoryError:Java heap space`:堆内存溢出 ， 对象过大
- `java.lang.OutOfMemoryError:GC overhead limit exceeded`:GC回收时间过长
- `java.lang.OutOfMemoryError:Direct buffer memory`执行内存挂了，比如：NIO
- `java.lang.OutOfMemoryError:unable to create new native thread`
  - 应用创建了太多线程，一个应用进程创建了多个线程，超过系统承载极限
  - 你的服务器并不允许你的应用程序创建这么多线程，linux系统默认允许单个进程可以创建的线程数是1024，超过这个数量，就会报错
  - 解决办法：降低应用程序创建线程的数量，分析应用给是否针对需要这么多线程，如果不是，减到最低修改linux服务器配置
- `java.lang.OutOfMemoryError:Metaspace`:元空间主要存放了虚拟机加载的类的信息、常量池、静态变量、即时编译后的代码

&emsp;&emsp;hello word



### 垃圾回收

#### 垃圾回收器

##### cms

优点：并发收集、停动时间比较少

缺点：CPU资源比较敏感、无法处理浮动垃圾、会产生空间碎片//因为使用了标记清除算法









young gc:

old gc

full gc : 整个堆和方法区的垃圾收集

oom