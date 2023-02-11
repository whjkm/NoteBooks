- [Chapter 10](#chapter-10)
    - [为什么C语言需要预处理](#为什么c语言需要预处理)

# Chapter 10

[一次定义原则](https://en.wikipedia.org/wiki/One_Definition_Rule)：
> The One Definition Rule (ODR) is an important rule of the C++ programming language that prescribes that classes/structs and non-inline functions cannot have more than one definition in the entire program and template and types cannot have more than one definition by translation unit. It is defined in the ISO C++ Standard (ISO/IEC 14882) 2003, at section 3.2.


C++语言的三大约束：
- 与C兼容：兼容C的语法，兼容C语言的编译模型与运行模型。
- 零开销（zero overhead）原则：
- 值语义


### 为什么C语言需要预处理
历史原因:
> 编译器没办法在内存里完整地表示单个源文件的抽象语法树，更不可能把整个程序（由多个源文件组成）放到内存里，以完成交叉引用（不同源文件的函数之间相互调用，使用外部变量等）。
由于内存限制，编译器必须要能够分别编译多个源文件，生成多个目标文件，再设法把这些目标文件组合（连接）为一个可执行文件。

`a.out`: "assembler output"的缩写，代表汇编程序输出。

[恐怖的C++语言](https://coolshell.cn/articles/1724.html)

  
