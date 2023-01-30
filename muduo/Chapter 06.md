- [Chapter 06](#chapter-06)
  - [网络库要点](#网络库要点)

# Chapter 06

## 网络库要点

- 线程安全，原生支持多核多线程。
- 不考虑可移植性，不跨平台，只支持Linux，不支持Windows。
- 主要支持x86-64，兼顾IA32。
- 不支持UDP，只支持TCP。
- 不支持IPv6，只支持IPv4。（现在需要支持IPv6？？？）
- 不考虑广域网应用，只考虑局域网。
- 不考虑公网，只考虑内网。不为安全性做特别的增强。
- 只支持一种使用模式：非阻塞IO + one event loop per thread，不支持阻塞IO。
- API简单易用，只暴露具体类和标准库里的类。 API不使用`non-trivial templates`，也不使用虚函数。
- 只满足常用需求的90%，不面面俱到，必要时以app来适应lib。
- 只做library，不做成framework。
- 争取全部代码在5000行以内（不含测试）。
  
