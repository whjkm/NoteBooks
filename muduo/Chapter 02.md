- [Chapter 02](#chapter-02)
  - [进程同步原则](#进程同步原则)
  - [互斥器（mutex）](#互斥器mutex)

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




  
