- [Chapter 02](#chapter-02)
  - [进程同步原则](#进程同步原则)
  - [互斥器（mutex）](#互斥器mutex)
  - [条件变量（condition variable）](#条件变量condition-variable)
  - [读写锁（Readers-Writer lock, rwlock）](#读写锁readers-writer-lock-rwlock)

# Chapter 02

## 进程同步原则

- 尽量最低限度地共享对象，减少使用同步的场合。
- 使用高级的并发编程构件， 如`TaskQueue`, `Producer-Consumer Queue`。
- 不得已必须使用底层同步原语(`primitives`)时，只使用非递归的互斥器和条件变量，慎用读写锁，不要用信号量。
- 除了使用`atomic`整数外，不自己编写`lock-free`代码，也不要使用“内核级”同步原语。

[Please Don’t Rely on Memory Barriers for Synchronization!](https://www.thinkingparallel.com/2007/02/19/please-dont-rely-on-memory-barriers-for-synchronization/)


## 互斥器（mutex）

- 用`RAII`方式封装`mutex`的创建，销毁，加锁，解锁操作。
- 只使用非递归的`mut`ex(即不可重入的`mutex`)。
- 不手工调用`lock()`和`unlock()`函数，一切交给栈上的`Guard`对象的构造和析构函数负责。
- 每次构造`Guard`对象时，需要考虑栈上的已持有的锁，防止加锁顺序不同而导致死锁。
- 不使用跨进程的`mutex`, 进程间通信只用`TCP sockets`。
- 加锁，解锁在同一个线程。

## 条件变量（condition variable）

from [condition variable wiki](https://en.wikipedia.org/wiki/Monitor_(synchronization)#Condition_variables)
> Conceptually a condition variable is a queue of threads, associated with a mutex, on which a thread may wait for some condition to become true. Thus each condition variable c is associated with an assertion Pc. While a thread is waiting on a condition variable, that thread is not considered to occupy the monitor, and so other threads may enter the monitor to change the monitor's state. In most types of monitors, these other threads may signal the condition variable c to indicate that assertion Pc is true in the current state. 


对于`wait`端：

- 必须与`mutex`一起使用，读写需受到此`mutex`的保护。
- 在`mutex`已上锁的时候才能调用`wait()`。
- 把判断布尔条件和`wait()`放到`while`循环中。

对于`signal/broadcast`端：

- 不一定要在`mutex`已经上锁的情况下调用`signal`(理论上)。
- 在`signal`之前一般要修改布尔表达式。
- 修改布尔表达式通常要用`mutex`保护（至少用做`full memory barrier`）。
- 注意区分`signal` 和 `broadcast`：“`broadcast`通常用于表明状态变化，`signal`通常用于表示资源可用。

[spurious wakeup](https://www.jianshu.com/p/0eff666a4875):

> On a multi-processor, it may be impossible for an implementation of `pthread_cond_signal()` to avoid the unblocking of more than one thread blocked on a condition variable.
The effect is that more than one thread can return from its call to `pthread_cond_wait()` or `pthread_cond_timedwait()` as a result of one call to `pthread_cond_signal()`. This effect is called “spurious wakeup”. Note that the situation is self-correcting in that the number of threads that are so awakened is finite; for example, the next thread to call `pthread_cond_wait()` after the sequence of events above blocks.
While this problem could be resolved, the loss of efficiency for a fringe condition that occurs only rarely is unacceptable, especially given that one has to check the predicate associated with a condition variable anyway. Correcting this problem would unnecessarily reduce the degree of concurrency in this basic building block for all higher-level synchronization operations.

## 读写锁（Readers-Writer lock, rwlock）

- 首选`mutex`,一般不用`rwlock`。
  

[read-copy-update(RCU)](https://en.wikipedia.org/wiki/Read-copy-update)
> In computer science, read-copy-update (RCU) is a synchronization mechanism that avoids the use of lock primitives while multiple threads concurrently read and update elements that are linked through pointers and that belong to shared data structures (e.g., linked lists, trees, hash tables).[1]

[memory barrier](https://en.wikipedia.org/wiki/Memory_barrier)

> In computing, a memory barrier, also known as a membar, memory fence or fence instruction, is a type of barrier instruction that causes a central processing unit (CPU) or compiler to enforce an ordering constraint on memory operations issued before and after the barrier instruction. This typically means that operations issued prior to the barrier are guaranteed to be performed before operations issued after the barrier.

[volatile](https://www.runoob.com/w3cnote/c-volatile-keyword.html)
> A volatile specifier is a hint to a compiler that an object may change its value in ways not specified by the language so that aggressive optimizations must be avoided.



