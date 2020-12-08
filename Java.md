





## 面向对象

三个特性



### 关键字

#### final

final 的意思是不变的，一般来说用于以下三种场景：

1. 被 final 修饰的类，表明该类是无法继承的；
2. 被 final 修饰的方法，表明该方法是无法覆写的；
3. 被 final 修饰的变量，说明该变量在声明的时候，就必须初始化完成，而且以后也不能修改其内存地址。

第三点注意下，我们说的是无法修改其内存地址，并没有说无法修改其值。因为对于 List、Map 这些集合类来说，被 final 修饰后，是可以修改其内部值的，但却无法修改其初始化时的内存地址。





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





