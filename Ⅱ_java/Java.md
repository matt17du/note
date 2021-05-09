



## 基础

### 进程线程



程序：具有指令和数据的文件，是一段静态的代码。

进程：程序的一次运行过程。

线程：和进程是类似的，是比进程更小的执行单位。同个类的多个线程会共享进程的堆和方法区，而每个进程会有自己程序计数器，虚拟机栈，本地方法栈。线程的切换消耗的资源会比进程更小。



### 面向过程、面向对象区别

面向过程性能更高，因为面向过程编译可以生成CPU直接执行的二进制代码，而面向对象不可以。

面向对象具有封装、继承、多态等特性，可以设计出具有易维护、易复用和易扩展的系统。

面向过程是一个一个函数，如何如何做，而面向对象将任务交给哪个对象去做



### JVM JRE JVM

jvm:用来运行java的字节码文件

jre:jvm和一些类库

jdk:jre + 工具（编译运行）



### 字符常量和字符串常量



字符常量是单引号的单个字符，字符串常量是双引号的多个字符。

字符常量相当于一个整型值，可以参与表达式运算，而字符串常量是一个内存地址

字符常量是2个字节，而字符串常量表示若干个字节。



### 自动装箱和拆箱



基本数据类型转换为对应引用类型

引用类型转换为对应的基本数据类型



### & &&

&&具有短路的功能。



### short +=



```java
short i = 1
short j = 1
short s = i + j  // 会报错，他们会转为int类型在计算 byte shorr char

i += 1 // 这种不会进行类型转换
```

### Integer 缓冲



```java
Integer a = 100
Integer b = 100 // a == b
```

使用上述方式创建Integer对象，-128 - 127jvm会进行缓存，而不会创建新的对象



## 面向对象



### 三个特性



封装：将对象的属性私有化，同时提供一些可以访问的这些属性的方法。

继承：在已有类的基础上创建新类的过程，已有的类是父类，新类为子类，子类可以增加新的属性和方法，同时拥有父类的属性和方法。

多态：一个引用变量到底指向哪个类的实例，在编程时不确定，在程序运行时才会确定。





### 接口和抽象类的区别



接口的方法默认是public abstract修饰，而抽象类的方法可以有抽象也可以有非抽象。

接口的变量是由public static final修饰，而抽象类没有此限制。

接口可以继承多个接口，实现多个接口，而抽象类继承一个类，实现多个接口。

接口是行为的规范，而抽象类是类的抽象。

java8接口提供了静态方法和默认方法



### 成员变量 和 局部变量



成员变量属于类和对象的，而局部变量属于方法或代码块。

成员变量可以被四种权限修饰符和static,final修饰，而局部变量只可以被final修饰。

在不被static和final修饰时，成员变量随着对象的创建而产生，随着对象的消失而消失，而局部变量随着方法调用而产生消失。

成员变量会自动赋值初值，而局部变量不会自动赋值初值，需要自己显示赋值。



### 重写和重载

重写：子类对父类允许访问的方法的实现过程进行重新编写。方法名相等，参数相等，权限修饰符大于等于父类，异常小于等于父类，返回值类型小于等于父类。



重载：在同一个类中，方法名相同，参数的个数、类型、顺序不同。返回值和权限修饰符没有做限制。



### 对象相等和引用相等



对象相等：对象的内容是否相等

引用相等：对象的内存地址是否相等。



## java值的传递



值的传递：方法接收一个变量的值

引用传递：方法接受变量的地址值，并可以修改该变量



无法修改基本类型的值

可以修改一个对象的状态

无法将对象引用参数指向另外一个对象。

## String



### String StringBuffer StringBuilder

不可变

String底层是由private final char[] value 字符数组存储，而StringBuffer和StringBuilder是继承AbstractBuilder,没有使用final修饰

线程安全

String每一次修改都会创建新的字符串对象，StringBuffer是由同步锁修饰，StringBuilder没有同步锁所以线程不安全。

性能

String每一次修改都会创建新的对象，所以性能比较低，StringBuffer加了锁的操作，所以性能相比StringBuiler也低



### intern

它首先会去常量池查找有没有相等的字符串对象，如果有则直接返回，否则会创建一个等值的对象。







## 关键字

### final



可以修饰属性、方法和类

在修饰属性的时候，如果这个属性是基本数据类型，初始化完成之后就不可以修改该值，如果这个属性是引用类型那么初始化完成之后就不可以将该变量指向其他对象。

在修饰类的时候，表明该类不可以被继承，同时将它所有的方法隐式被fianl修饰。

被final修饰的方法不可以被重写。



### static

1.修饰成员变量和成员方法时，表明该成员属于类的，而不是某个对象的，该类的所有实例共享。

2.修改内部类时，表明该内部类的创建不需要依赖外部类，不可以使用外部类的非静态的属性和方法。

3.**修饰代码块**

4.在静态导入可以使用，后续我们只需要直接使用静态变量或者静态方法，而不需要通过类来调用。



### this

表示当前对象或者当前正在创建的对象



### super

用来调用父类的属性和方法



### 四种权限修饰符

private 当前类

缺省：当前类、同一个包

protected:当前类、同一个包、不同包的子类

public:当前类、同一个包、不同包的子类、不同包













LinkedList源码分析

```java
 transient Node<E> first; // 头指针

    /**
     * Pointer to last node.
     * Invariant: (first == null && last == null) ||
     *            (last.next == null && last.item != null)
     */
 transient Node<E> last; // 尾指针
```

```java
public boolean add(E e) {
        linkLast(e);
        return true;
 }

/**
     * Links e as last element.
     */
    void linkLast(E e) {
        final Node<E> l = last;
        // 构造器：把当前节点的prev指针指向尾节点
        final Node<E> newNode = new Node<>(l, e, null);
        last = newNode;
        if (l == null)
            first = newNode;
        else
            l.next = newNode;
        size++;
        modCount++;
    }


```

构造添加的Node节点，当前节点的prev指针指向尾节点，判断尾指针是否为null,如果为null则把头指针指向新的节点，否则把尾节点指向next指针指向当前节点。

白话：构造添加的节点，添加在尾部即可。



```java
public void add(int index, E element) {
    	// 对索引进行判断，索引不能小于0，不能大于size
        checkPositionIndex(index);
    
		// 如果索引等于size，则添加在尾部即可
        if (index == size)
            linkLast(element);
        else
            linkBefore(element, node(index));
}
```

```java
 void linkBefore(E e, Node<E> succ) {
        // assert succ != null;
        final Node<E> pred = succ.prev;
     	// 
        final Node<E> newNode = new Node<>(pred, e, succ);
        succ.prev = newNode;
        if (pred == null)
            first = newNode;
        else
            pred.next = newNode;
        size++;
        modCount++;
    }
```

找到index位置的节点，创建插入的节点，插入节点next指针指向index位置的节点，prev指针指向index位置节点的前驱节点，该前驱节点指向next指针指向新添加的节点。

白话：索引的判断，不能小于0，不能大于size,索引是否等于size,等于就添加在尾部即可，否则找到index位置的节点，插入即可。



```java
public E get(int index) {
    checkElementIndex(index);
    return node(index).item;
}
```

```java
Node<E> node(int index) {
    // assert isElementIndex(index);
    if (index < (size >> 1)) {
        Node<E> x = first;
        for (int i = 0; i < index; i++)
            x = x.next;
        return x;
    } else {
        Node<E> x = last;
        for (int i = size - 1; i > index; i--)
            x = x.prev;
        return x;
    }
}
```

索引的检查，看索引如果在链表的左边，就在左边开始遍历，否则从右边开始遍历。





```java
public E remove(int index) {
        checkElementIndex(index);
        return unlink(node(index));
}
```

```java
E unlink(Node<E> x) {
    // assert x != null;
    final E element = x.item;
    final Node<E> next = x.next;
    final Node<E> prev = x.prev;

    if (prev == null) {
        first = next;
    } else {
        prev.next = next;
        x.prev = null;
    }

    if (next == null) {
        last = prev;
    } else {
        next.prev = prev;
        x.next = null;
    }

    x.item = null;
    size--;
    modCount++;
    return element;
}
```

索引的检查，通过node方法找到需要删除的节点，删除即可。



### 锁

#### ReentrackLock

##### 1.1关键字段

state:锁状态标志位，0表示空闲，1表示有线程占用它

```java
/**
     * Head of the wait queue, lazily initialized.  Except for
     * initialization, it is modified only via method setHead.  Note:
     * If head exists, its waitStatus is guaranteed not to be
     * CANCELLED.
     */
    private transient volatile Node head;       //等待队列的头

    /**
     * Tail of the wait queue, lazily initialized.  Modified only via
     * method enq to add new wait node.
     */
    private transient volatile Node tail; //等待队列的尾

    /**
     * The synchronization state.
     */
    private volatile int state;             //原子性的锁状态位，ReentrantLock对该字段的调用是通过原子操作compareAndSetState进行的


   protected final boolean compareAndSetState(int expect, int update) {
        // See below for intrinsics setup to support this
        return unsafe.compareAndSwapInt(this, stateOffset, expect, update);
   }
```

##### 1.2关键代码

###### 1.21获取锁

```java
 public void lock() {
        sync.lock();
 }
```

NonfairSync、FairSync分别实现了lock方法

非公平锁

​	①尝试获取锁

通过CAS给锁状态设置为1，如果设置失败需要调用acquire(1)方法。

```java
package java.util.concurrent.locks.ReentrantLock;
final void lock() {
            if (compareAndSetState(0, 1))//表示如果当前state=0，那么设置state=1，并返回true；否则返回false。由于未等待，所以线程不需加入到等待队列
                setExclusiveOwnerThread(Thread.currentThread());
            else
                acquire(1);
}
 
 package java.util.concurrent.locks.AbstractOwnableSynchronizer  //AbstractOwnableSynchronizer是AQS的父类
 protected final void setExclusiveOwnerThread(Thread t) {
            exclusiveOwnerThread = t;
}
```

**acquire方法分析**



```java
package java.util.concurrent.locks.AbstractQueuedSynchronizer
public final void acquire(int arg) {
         if (!tryAcquire(arg) &&
              acquireQueued(addWaiter(Node.EXCLUSIVE), arg))
             selfInterrupt();
}

 
  protected final boolean tryAcquire(int acquires) {
            return nonfairTryAcquire(acquires);
 }
```

 (1)如果锁状态空闲(state=0)，且通过原子的比较并设置操作，那么当前线程获得锁，并把当前线程设置为锁拥有者；
 (2)如果锁状态空闲，且原子的比较并设置操作失败，那么返回false，说明尝试获得锁失败；
 (3)否则，检查当前线程与锁拥有者线程是否相等(表示一个线程已经获得该锁，再次要求该锁，这种情况叫可重入锁)，如果相等，维护锁状态，并返回true;
 (4)如果不是以上情况，说明锁已经被其他的线程持有，直接返回false;

```java
final boolean nonfairTryAcquire(int acquires) {  
            final Thread current = Thread.currentThread();
            int c = getState();
            if (c == 0) {
                if (compareAndSetState(0, acquires)) {
                    setExclusiveOwnerThread(current);
                    return true;
                }
            }
            else if (current == getExclusiveOwnerThread()) {  //表示一个线程已经获得该锁，再次要求该锁(重入锁的由来)，为状态位加acquires
                int nextc = c + acquires;
                if (nextc < 0) // overflow
                    throw new Error("Maximum lock count exceeded");
                setState(nextc);
                return true;
            }
            return false;
 }
```

(1)如果tail节点不为null，说明队列不为空，则把新节点加入到tail的后面，返回当前节点，否则进入enq进行处理(2)；
 (2)如果tail节点为null，说明队列为空，需要建立一个虚拟的头节点，并把封装了当前线程的节点设置为尾节点；另外一种情况的发生，是由于在(1)中的compareAndSetTail可能会出现失败，这里采用for的无限循环，是要保证当前线程能够正确进入等待队列；



```java

package java.util.concurrent.locks.AbstractQueuedSynchronizer
   private Node addWaiter(Node mode) {
         Node node = new Node(Thread.currentThread(), mode);
         // Try the fast path of enq; backup to full enq on failure
         Node pred = tail;
         if (pred != null) {  //如果当前队列不是空队列，则把新节点加入到tail的后面，返回当前节点，否则进入enq进行处理。
              node.prev = pred;
              if (compareAndSetTail(pred, node)) {
                  pred.next = node;
                  return node;
              }
         }
         enq(node);
         return node;
     }

 package java.util.concurrent.locks.AbstractQueuedSynchronizer
 private Node enq(final Node node) {
        for (;;) {
            Node t = tail;
            if (t == null) { // tail节点为空，说明是空队列，初始化头节点，如果成功，返回头节点
                Node h = new Node(); // Dummy header
                h.next = node;
                node.prev = h;
                if (compareAndSetHead(h)) {
                    tail = node;
                    return h;
                }
            }
            else {   //
                node.prev = t;
                if (compareAndSetTail(t, node)) {
                    t.next = node;
                    return t;
                }
            }
        }

```

(1)如果当前节点是队列的头结点（如果第一个节点是虚拟节点，那么第二个节点实际上就是头结点了），就尝试在此获取锁tryAcquire(arg)。如果成功就将头结点设置为当前节点（不管第一个结点是否是虚拟节点），返回中断状态。否则进行(2)。 
(2)检测当前节点是否应该park()-"挂起的意思"，如果应该park()就挂起当前线程并且返回当前线程中断状态。进行操作(1)。



```java
 final boolean acquireQueued(final Node node, int arg) {
        try {
            boolean interrupted = false;
            for (;;) {
                final Node p = node.predecessor();
                if (p == head && tryAcquire(arg)) {
                    setHead(node);
                    p.next = null; // help GC
                    return interrupted;
                }
                if (shouldParkAfterFailedAcquire(p, node) &&
                    parkAndCheckInterrupt())
                    interrupted = true;
            }
        } catch (RuntimeException ex) {
            cancelAcquire(node);
            throw ex;
        }
     }
```

##### 总结

​		非公平锁：通过cas设置锁的状态1，成功则把锁对象的线程ID设置为当前线程ID，否则判断锁对象的线程ID是否为当前线程，如果是则直接获取，否则需要将当前线程封装为一个Node节点之后加入队列，对列为空则需要创建一个虚拟节点作为队头，之后把节点加入队尾。此时需要判断是否挂起该节点，判断该节点的前驱节点的状态是否<0,小于0则挂起，如果>0则删除该前驱节点，通过循环删除所有前驱节点的状态小于0，最后不可以挂起该节点。如果前驱节点状态=0，则把该前驱节点设置为signal，也是不可以挂起。

​		公平锁：在获取锁时判断该线程是否满足，对列为空或者该线程是否时队首，满足条件则可以通过CAS设置锁的状态，设置失败则需要判断锁对象线程ID是否为该线程，如果时则获取锁，否则不可以获取。





### 多线程

#### synchronized和lock区别

synchronized是关键字，lock是一个接口
synchronized在发生异常时，会自动释放锁，而lock需要手动释放锁。
synchronized无法判断锁的状态，lock可以判断
synchronized和lock都是可重入锁，synchronized是非公平锁，lock可以做公平锁也可以做非公平锁。





## 异常



异常可分为异常和错误，它们都继承java.lang.Throwable类，错误是程序无法处理的，而异常是程序可以处理的

### 处理

try:用于捕获异常

catch：用于处理异常

finally：一定会被执行



throw:将异常抛出，由方法的调用者去处理



finally一定会停止执行的四种情况：

①finally第一行出现了异常

②finally之前使用了Sytem.exit(0)退出了程序

③当前程序所在的线程挂掉

④CPU关闭

### 五种常见的运行时异常



NullPointerException

ArrayIndexOutofBoundsException

ClassCastException

ClassNotFoundException

IllegalArgumentException:参数异常



## IO

从键盘输入

```java
Scanner input = new Scanner(Sytem.in);
```

```java
BufferReader input = new BufferReader(new InputStreamReader(System.in);
input.readLine();                                      
```



### 流分为

输入流和输出流

字节流和字符流

节点流和处理流



### 为啥有字符流

字符和字节转换比较耗时，其次转换的过程会产生乱码。所有在处理视频和图片的时候使用字节流即可，而涉及字符的操作时使用字符流即可。



## 反射

### 反射

在程序运行的过程中，对于任何一个类的属性和方法都可以获取，对于任何一个对象都可以调用它的属性和方法



### 优缺点

优点：动态的加载类，提高了代码的灵活度

缺点：是一种解释操作，告诉jvm如何做，性能不是很高。



### 使用

数据库连接的时候使用class.forname()动态加载某个数据库的驱动

Spring在加载bean的时候也使用了反射



## 深拷贝和浅拷贝



浅拷贝：对基本数据类型的变量进行值的拷贝，引用数据类型不会重新创建一个新的对象而是将内存地址进行拷贝

深拷贝：对基本数据类型的变量进行值的拷贝，对引用数据类型会创建新的对象，并赋值其内容，需要我们重写clone方法。



## 集合

### ArrayList和Vector区别

1.vector是线程安全的，而arrayList不是线程安全的

2.vector每次扩容是原来的2倍，而arrayList是1.5倍



### 比较器

重写compare方法的实现并不一定都是互减可能会越界，可以使用compareTo方法

```java
Arrays.sort(arr, (o1, o2) -> {
    return Integer.valueOf(o1[1]).compareTo(o2[1]);
});
```





## 泛型

泛型工作原理

编译之前会进行类型检查，编译之后会进行泛型察除，变成原始类型。









**传值的方式传引用**。 或者说**传值的方式传地址**。
你这个问题其实很简单。要搞清楚这个问题，要明白：堆 和 栈。引用是保存在栈上，对象是保存在堆中。引用指向堆上的对象，也就是说引用的值为对象在栈上的内存地址。那么你修改引用时改的是引用的值，也就是让引用指向其它对象。那么应该怎么修改堆上的对象呢？首先你得访问到堆上的对象吧？如何访问到它呢？在C/C++中是通过指针运算符 *p 来访问到指针p指向的堆上的对象的，然后再修改它。那么Java中没有指针运算符，那么怎么办呢？Java中是通过点操作符，也就是 list.add中的那个点，表示先访问到list这个引用指向的对象，然后让该对象调用 add 方法，从而修改了list指向的堆上的对象。所以当你单独修改 list = xxx;时你修改的是引用，让list引用指向其它对象，而没有修改 list 引用指向的对象，因为你根本就没有访问到堆上的对象，你怎么修改它呢？
所以：要修改堆上的对象，你要先访问到它，不然你就不能修改它。访问堆上的对象的方法就是 . 点操作符。
没有访问到如何修改呢



作者：Andy Young
链接：https://www.zhihu.com/question/31203609/answer/51320855
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。











```java
 @Override
    public <T extends Product> T createProduct(Class<T> c) throws ClassNotFoundException, IllegalAccessException, InstantiationException {
        T t = (T)Class.forName(c.getName()).newInstance();
        return t;
    }
```

extends 不是extend





抽象类；类的抽象

接口：行为的规范





jvm：常量池

final, finally, finalize 的区别

nio bio aio

线程进程

内存泄漏







常见的包

```
java.lang.* //核心包
java.util.* // 工具包
java.io.*
java.text.*; // 格式化
java.net.*
java.sql.*

```

