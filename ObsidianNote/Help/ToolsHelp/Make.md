GNU Make 能让你在一个脚本里（即所谓的 `Makefile`）定义整个编译流程以及各个目标文件与源文件之间的依赖关系，并且只重新编译你的修改会影响到的部分，从而降低编译的时间。

这里有一篇写得深入浅出的[文档](https://seisman.github.io/how-to-write-makefile/overview.html)供大家参考。

GNU Make 掌握起来相对容易，但用好它需要不断的练习。将它融入到自己的日常开发中，勤于学习和模仿其他优秀开源项目里的 `Makefile` 的写法，总结出适合自己的 template，久而久之，你对 GNU Make 的使用会愈加纯熟。

CMake 是类似于 GNU make 的跨平台自动软件构建工具，使用 CMakeLists.txt 定义构建规则，相比于 make 它提供了更多的功能，在各种软件构建上广泛使用。**强烈建议学习使用 GNU Make 和熟悉 `Makefile` 后再学习 CMake**。

## 如何学习 CMake

`CMakeLists.txt` 比 `Makefile` 更为抽象，理解和使用难度也更大。现阶段很多 IDE (如 Visual Studio, CLion) 提供了自动生成 `CMakeLists.txt` 的功能，但掌握 `CMakeLists.txt` 的基本用法仍然很有必要。除了 [CMake 官方 Tutorial](https://cmake.org/cmake/help/latest/guide/tutorial/index.html) 外，上海交通大学 IPADS 组新人培训也提供了[大约一小时的视频教程](https://www.bilibili.com/video/BV14h41187FZ)。

[概述 — 跟我一起写Makefile 1.0 文档 (seisman.github.io)](https://seisman.github.io/how-to-write-makefile/overview.html)

# 概述

makefile关系到了整个工程的编译规则。一个工程中的源文件不计其数，并且按类型、功能、模块分别放在若干个目录中，makefile定义了一系列的规则来指定，哪些文件需要先编译，哪些文件需要后编译，哪些文件需要重新编译，甚至于进行更复杂的功能操作，因为makefile就像一个Shell脚本一样，其中也可以执行操作系统的命令。

makefile带来的好处就是——“自动化编译”，一旦写好，只需要一个make命令，整个工程完全自动编译，极大的提高了软件开发的效率。 make是一个命令工具，是一个解释makefile中指令的命令工具，一般来说，大多数的IDE都有这个命令，比如：Delphi的make，Visual C++的nmake，Linux下GNU的make。可见，makefile都成为了一种在工程方面的编译方法。

## 关于程序的编译和链接

一般来说，无论是C还是C++，首先要把源文件编译成中间代码文件，在Windows下也就是 `.obj` 文件，UNIX下是 `.o` 文件，即Object File，这个动作叫做编译（compile）。然后再把大量的Object File合成可执行文件，这个动作叫作链接（link）。

编译时，编译器需要的是语法的正确，函数与变量的声明的正确。对于后者，通常是你需要告诉编译器头文件的所在位置（头文件中应该只是声明，而定义应该放在C/C++文件中），只要所有的语法正确，编译器就可以编译出中间目标文件。一般来说，每个源文件都应该对应于一个中间目标文件（ `.o` 文件或 `.obj` 文件）。

链接时，主要是链接函数和全局变量。所以，我们可以使用这些中间目标文件（ `.o` 文件或 `.obj` 文件）来链接我们的应用程序。链接器并不管函数所在的源文件，只管函数的中间目标文件（Object File），在大多数时候，由于源文件太多，编译生成的中间目标文件太多，而在链接时需要明显地指出中间目标文件名，这对于编译很不方便。所以，我们要给中间目标文件打个包，在Windows下这种包叫“库文件”（Library File），也就是 `.lib` 文件，在UNIX下，是Archive File，也就是 `.a` 文件。

总结一下，源文件首先会生成中间目标文件，再由中间目标文件生成可执行文件。在编译时，编译器只检测程序语法和函数、变量是否被声明。如果函数未被声明，编译器会给出一个警告，但可以生成Object File。而在链接程序时，链接器会在所有的Object File中找寻函数的实现，如果找不到，那到就会报链接错误码（Linker Error），在VC下，这种错误一般是： `Link 2001错误` ，意思说是说，链接器未能找到函数的实现。你需要指定函数的Object File。