[chu's blog - 从零开始的C++包管理器CONAN上手指南](http://chu-studio.com/posts/2019/%E4%BB%8E%E9%9B%B6%E5%BC%80%E5%A7%8B%E7%9A%84C++%E5%8C%85%E7%AE%A1%E7%90%86%E5%99%A8CONAN%E4%B8%8A%E6%89%8B%E6%8C%87%E5%8D%97)
[Tutorial — conan 2.0.1 documentation](https://docs.conan.io/2/tutorial.html)


`source`函数，用于源代码拉取和准备，比如对源码进行一些修改；`build`函数，调用 CMake 进行构建；`package`函数，用于执行打包操作；`package_info`则用于输出构建相关的信息，比如需要链接包中的哪些库文件。

在构建完成后，Conan 会以 Settings 和 Options 的取值 Hash 后为软件包指定一个 package_id，因而不同的构建选项会对应到不同的 Id 上。最终拉取预编译包时就会以这个 Id 作为基准。




