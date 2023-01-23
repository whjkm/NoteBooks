- [Chatpter 01](#chatpter-01)
  - [线程安全](#线程安全)
    - [对象构造线程安全](#对象构造线程安全)
  - [C++中可能出现的内存问题](#c中可能出现的内存问题)

# Chatpter 01

## 线程安全

- 多个线程同时访问时，其表现出正确的行为。
- 无论操作系统如何调度这些线程，无论这些线程的执行顺序如何交织(`interleaving`)。
- 调用端代码无须额外的同步或其他协调动作。
  
> C++ 标准库中的大多数`class`都不是线程安全的，包括std::string, std::vector, std::map等。

### 对象构造线程安全

- 不要在构造函数中注册任何回调。
- 也不要在构造函数中把this传给跨线程的对象，即便在构造函数的最后一行也不行。
  

## C++中可能出现的内存问题

- 缓冲区溢出(`buffer overrun`)：使用`std::vector<char>/std::string`或自己编写`Buffer class`来管理缓冲区。
- 空悬指针/野指针: 使用`shared_ptr/weak_ptr`。
- 重复释放(`double delete`)：使用`scoped_ptr`，只在对象析构的时候释放一次。
- 内存泄漏(`memory leak`)：使用`scoped_ptr`，对象析构的时候自动释放内存。
- 不配对的`new[]/delete`：把`new[]`统统替换为`std::vector/scoped_array`。
- 内存碎片(`memory fragmentation`)


[当析构函数遇到多线程](https://blog.csdn.net/Solstice/article/details/5238671?spm=1001.2014.3001.5501)

[快速掌握一个语言最常用的50%](https://blog.csdn.net/myan/article/details/3144661?spm=1001.2014.3001.5501)

[function/bind的救赎（上）](https://blog.csdn.net/myan/article/details/5928531?spm=1001.2014.3001.5501)

