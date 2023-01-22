- [Chapter 04](#chapter-04)
  - [多线程与IO](#多线程与io)
  - [用RAII包装文件描述符](#用raii包装文件描述符)
    - [多线程与fork()](#多线程与fork)
    - [多线程与Signal](#多线程与signal)

# Chapter 04

## 多线程与IO

“显然是正确”方式：一个文件只能由一个进程中的一个线程来读写。

多线程应该遵循的原则：
- 每个文件描述符只由一个线程操作，从而轻松解决消息收发的顺序性问题，也避免关闭文件描述符的各种`race condition`。
- 一个线程可以操作多个文件描述符，但一个线程不能操作别的线程拥有的文件描述符。

**Exception**:

- 对于磁盘文件，在必要的时候多个线程可以同时调用`pread(2)/pwrite(2)`来读写同一个文件；
- 对于`UDP`, 由于协议本身保证消息的原子性，在适当的条件下（比如消息之间彼此独立）可以多个线程同时读写同一个`UDP`文件描述符。


## 用RAII包装文件描述符


### 多线程与fork()

`fork()` 一般不能在多线程程序中调用。

[准则3：多线程程序里不准使用fork](http://www.cppblog.com/lymons/archive/2008/06/01/51836.html)

**Solution**:

- 做`fork()`的时候，在它之前让其他的线程完全终止。
- `fork()`之后，在子进程中马上调用`exec()`,彻底隔断子进程和父进程的联系。
- 其他线程中，不做`fork-unsafe`的处理。

### 多线程与Signal

在多线程程序中，使用`signal`的第一原则是**不要使用`signal`**。

Reference:

[UNIX上的C++程序设计守则(1)](http://www.cppblog.com/lymons/archive/2008/06/01/51838.html)

[UNIX上C++程序设计守则 (2)](http://www.cppblog.com/lymons/archive/2008/06/01/51837.html)




