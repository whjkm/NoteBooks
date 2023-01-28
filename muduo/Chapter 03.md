- [Chapter 03](#chapter-03)
  - [进程与线程](#进程与线程)
  - [单线程服务器的常用编程模型](#单线程服务器的常用编程模型)
  - [多线程服务的常用编程模型。](#多线程服务的常用编程模型)
    - [one loop per thread](#one-loop-per-thread)
    - [one loop per thread + thread pool](#one-loop-per-thread--thread-pool)
  - [多线程服务器的适用场合](#多线程服务器的适用场合)
    - [必须用单线程的场合](#必须用单线程的场合)
    - [适用多线程程序的场景](#适用多线程程序的场景)
      - [线程的分类：](#线程的分类)

# Chapter 03

## 进程与线程
- 进程：“内存中正在运行的程序”。 每个进程有自己独立的地址空间(`address space`)。
- 线程：共享地址空间，从而可以高效地共享数据。可以更好的发挥多核处理器(`multi-cores`)的效能。

## 单线程服务器的常用编程模型

- `non-blocking IO + IO multiplexing`: Reactor 模式。程序的基本结构是一个事件循环（`event loop`）,以事件驱动（`event-driven`）和事件回调的方式实现业务逻辑。缺点：要求事件回调函数必须是非阻塞的。
  - `lighttpd`, 单线程服务器。
  - `libevent`, `libev`。
  - `ACE`, `Poco C++ libraries`。
  - `Java NIO`, 包括`Apache Mina` 和 `Netty`。
  - `POE`(`Perl`)。
  - `Twisted`(`Python`)。
  
## 多线程服务的常用编程模型。

- 每个请求创建一个线程，使用阻塞式IO操作。
- 使用线程池，使用阻塞式IO操作。
- 使用`non-blocking IO + IO multiplexing`。即`Java NIO`的方式。
- `Leader/Follower`等高级模式。

### one loop per thread

程序里每个IO线程有一个`event loop`(`Reactor`)，用于处理读读写和定时事件（无论周期性的还是单次的）。

> One loop per thread is usually a good model. Doing this is almost never wrong, sometimes a better-performance model exists, but it is always a good start.

这种模式的好处：
- 线程数目基本固定，可以在程序启动的时候设置，不会频繁创建和销毁。
- 可以很方便地在线程间调配负载。
- IO事件发生的线程是固定的，同一个TCP连接不必考虑事件并发。


### one loop per thread + thread pool

- `event loop`用作`IO multiplexing`, 配合`non-blocking IO`和定时器。
- `thread pool`用来做计算，具体可以是任务队列或者生产者消费者队列。


## 多线程服务器的适用场合

- 运行一个单线程的进程。是不可伸缩的（scalable)，不能发挥多核机器的计算能力。
- 运行一个多线程的进程。
- 运行多个单线程的进程。（多进程）
   - 进程运行多份。
   - 主进程 + work进程。（nginx）
- 运行多个多线程的进程。

### 必须用单线程的场合
- 程序可能会`fork(2)`; 只有单线程程序能`fork(2)`，一个程序`fork(2)`之后一般有两种行为。
    - 立即执行`exec()`，变身为另一个程序。例如`shell`和`inetd`,计算节点上负责启动`job`的守护进程。
    - 不调用`exec()`，继续运行当前程序。
- 限制程序的CPU占用率。做成单线程能够避免过分抢夺系统的计算资源。


### 适用多线程程序的场景

提高响应速度，让IO和“计算”相互重叠，降低latency。虽然多线程不能提高绝对性能，但能提高平均响应性能。

一个程序要做成多线程的，大致要满足：

- 有多个cpu可用。单核机器上多线程没有性能优势。
- 线程间有共享数据，即内存中的全局状态。共享的数据是可以修改，而不是静态的常量表。
- 提供非均质的服务。事件的响应有优先级差异，可以用专门的线程来处理优先级高的事件，防止优先级反转。
- `latency`和`throughput`同样重要，不是逻辑简单的IO bound 或 CPU bound程序。
- 利用异步操作。
- 能`scale up`。一个好的多线程程序应该能够享受增加CPU数目带来的好处。
- 具有可预测的性能，线程数目一般不随负载变化。
- 多线程能有效地划分责任与功能，让每个线程的逻辑比较简单，任务单一，便于编码。

#### 线程的分类：

- IO线程：这类线程的主循环是`IO multiplexing`,阻塞地等在`select/poll/epoll_wait`系统调用上。
- 计算线程：这类线程的主循环是`blocking queue`,阻塞地等在`condition variable`上，这类线程一般位于`thread pool`中。
- 第三方库所用的线程：如`logging`。
  
