# 游戏引擎架构笔记

## 3.2.2 声明 定义 和 链接

### 3.2.2.1 Translation Units Revisited

a C or C++ program is comprised of *translation units.* The compiler translates one .cpp file at a time, and for each one it generates an output file called an object file (.o or .obj).

The compiler only operates on one translation unit at a time, so whenever it encounters a reference to an external global variable or function, it must “go on faith” and assume that the entity in question really exists, as shown in Figure 3.7. 

链接器的主要工作是解析外部引用，在这种能力下它只能产生两种错误：

1. 可能找不到外部引用的目标，在这种情况下
   链接器生成“未解析的符号”错误。
2. 链接器可能会发现多个具有相同功能的变量或函数
   名称，在这种情况下，它会生成“多重定义符号”错误。

### 3.2.2.2 **Declaration versus Definition**

在 C 和 C++ 语言中，必须声明和定义变量和函数在使用之前完成。 理解 C 和 C++ 中声明和定义之间的区别很重要。

* 声明是对数据对象或函数的描述。它提供了带有实体名称及数据类型或函数签名的编译器（即，返回类型和参数类型）。
* 另一方面，定义描述了内存中的一个独特区域该程序。 这个内存可能包含一个变量，一个 struct 或 class，或函数的机器代码。

*定义和声明的多重性*

C/C++程序可以拥有多个相同的声明但每个只能有一个定义

*在头文件和内联中定义*

在头文件中放置定义通常是危险的。 这样做的原因应该很明显：如果包含定义的头文件是#included进入多个 .cpp 文件，这是产生“多重定义符号”链接器错误的可靠方法。

### 3.2.2.3 链接

C 和 C++ 中的每个定义都有一个称为链接的属性。 定义外部链接对翻译单元可见并可被翻译单元引用除了它出现的那个。具有内部链接的定义可以只能在它出现的翻译单元内“看到”，因此不能被其他翻译单位引用。

## 3.2.3 C/C++内存分布

### 3.2.3.1 可执行文件

构建 C/C++ 程序时，链接器会创建一个可执行文件。 大多数类似 UNIX 的操作系统，包括许多游戏机，都采用流行的可执行文件格式称为可执行文件和链接格式 (ELF)。 可执行因此，这些系统上的文件具有 .elf 扩展名。 Windows 可执行格式类似于 ELF 格式Windows 下的可执行文件有 exe 扩展名。 不管它的格式是什么，可执行文件总是包含一个程序的部分图像，因为它在运行时将存在于内存中。 我说一个“部分”映像，因为程序通常在运行时分配内存
除了在其可执行映像中布置的内存之外。

映像通常包含至少四部分

1. 文本段 代码段 包含程序定义的可执行机器代码
2. 数据段 包含所有初始化的全局和静态变量，所需内存会被精确布局 
3. BBS段 包含所有未初始化的全局和静态变量，未初始化的变量默认定义为0 运行时bbs保留请求的字节数和在程序入口调用前用零填充
4. 只读数据段 常量全局数据

### 3.2.3.2 栈堆

当可执行程序加载到内存并运行时，操作系统会为栈堆保留一块内存区域 每当一个函数被调用，栈堆内存的一块连续区域被压入栈堆被称为 堆栈帧