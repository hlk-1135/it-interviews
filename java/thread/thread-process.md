# 线程与进程

## 关系

* **进程**是资源分配的基本单位，**线程**是cpu调度，或者说是程序执行的最小单位

* 线程是进程的一个实体,是CPU调度和分派的基本单位,它是比进程更小的能独立运行的基本单位

* 线程自己基本上**不拥有系统资源**,只拥有一点在运行中必不可少的资源(如程序计数器,一组寄存器和栈),但是它可与同属一个进程的其他的线程共享进程所拥有的全部资源

* 一个线程可以创建和撤销另一个线程;同一个进程中的多个线程之间可以并发执行


## 进程的状态

基本状态有3种,即ready(就绪),running(运行),wait(等待)


## 多进程之间的通信

- **管道( pipe )**：管道是一种半双工的通信方式，数据只能单向流动，而且只能在具有亲缘关系的进程间使用。进程的亲缘关系通常是指父子进程关系

- **有名管道 (named pipe)** ： 有名管道也是半双工的通信方式，但是它允许无亲缘关系进程间的通信

- **信号量( semaphore )** ： 信号量是一个计数器，可以用来控制多个进程对共享资源的访问。它常作为一种锁机制，防止某进程正在访问共享资源时，其他进程也访问该资源。因此，主要作为进程间以及同一进程内不同线程之间的同步手段

- **消息队列( message queue )** ： 消息队列是由消息的链表，存放在内核中并由消息队列标识符标识。消息队列克服了信号传递信息少、管道只能承载无格式字节流以及缓冲区大小受限等缺点

- **信号 ( sinal )** ： 信号是一种比较复杂的通信方式，用于通知接收进程某个事件已经发生

- **共享内存( shared memory )** ：共享内存就是映射一段能被其他进程所访问的内存，这段共享内存由一个进程创建，但多个进程都可以访问。共享内存是最快的 IPC 方式，它是针对其他进程间通信方式运行效率低而专门设计的。它往往与其他通信机制，如信号两，配合使用，来实现进程间的同步和通信

- **套接字( socket )** ： 套接字也是一种进程间通信机制，与其他通信机制不同的是，它可用于不同及其间的进程通信


## 多线程之间的通信

- 方法1：通过访问共享变量的方式(注:需要处理同步问题)

- 方法2：通过管道流

###两个线程间共享数据

* 通过共享对象(用wait和notify方法)

* 使用像阻塞队列这样并发的数据结构

###`notify` 和 `notifyAll`的区别

* notify()方法不能唤醒某个具体的线程，所以只有一个线程在等待的时候它才有用武之地

* notifyAll()唤醒所有线程并允许他们争夺锁确保了至少有一个线程能继续运行

####为什么wait, notify 和 notifyAll这些方法不在thread类里面？

* 由于wait，notify和notifyAll都是锁级别的操作，所以把他们定义在Object类中因为锁属于对象

* JAVA提供的锁是对象级的而不是线程级的


