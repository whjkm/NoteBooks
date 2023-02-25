- [Chapter 10](#chapter-10)
    - [为什么C语言需要预处理](#为什么c语言需要预处理)
  - [C++的编译模型](#c的编译模型)

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

## C++的编译模型

- 单遍编译
- 向前声明

[C++ 风格指南](https://zh-google-styleguide.readthedocs.io/en/latest/google-cpp-styleguide/contents/)

[LLVM编程规范](https://llvm.org/docs/CodingStandards.html)

[LLVM编程规范（译）](https://www.guyuemeng.com/post/pgl_cc++/coding_guide/llvm%E7%BC%96%E7%A0%81%E8%A7%84%E8%8C%83%E8%AF%91/)


[from 云风](https://www.sohu.com/a/535731844_115128)
> 为什么我会强调用简单的方法？Keep it Simple and Stupid，即KISS原则。在20年前，我不完全理解这个道理，比如，我在大学期间以及刚毕业的时候，比较喜欢做程序的优化，让自己写的代码比别人写的代码跑得快。很多年轻程序员和我一样，都喜欢炫技。但我现在看来，这些事不是解决问题的本质。这与把事情做简单有什么关系？以前我认为写出复杂的程序并且不出错是一种出色的能力，可随着时间的推移，我的代码需要被别人维护，可能还要和其他人合作，这时我们需要在这群人之间找到一个共同的基点，让代码更容易理解。所以我们需要让代码足够简单，让别人一看就明白。什么样的代码是好代码？并不是看上去好像没有问题的代码，而是看上去所有东西都清清楚楚，断定它肯定不会出问题的代码。
> 把复杂的问题简单化，对程序员而言是一项非常重要的能力。
> 另一项重要能力是评估事物的能力，知道一件事情大概是怎么回事，需要多长时间完成，需要什么条件完成，这是靠经验堆出来的。


[[6-看到一句话，心有戚戚#^cc345f]]

[[reactor-siemens#^8gtqau4hr4q]]
[[Reactor2-93.pdf]]

