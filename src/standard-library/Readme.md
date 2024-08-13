# 标准库

C++标准库是语言本身的强大补充，提供了大量的工具和组件来简化程序开发，提高代码的可读性、可维护性和性能。标准库涵盖了从输入输出操作到复杂的多线程编程的方方面面，为开发者提供了构建健壮应用程序所需的基础设施。本章将深入介绍C++标准库的各个模块，帮助您全面掌握其用法和最佳实践。

## 章节介绍

本章将通过几个主要类别来组织对C++标准库的介绍，每个类别下的模块都将在各自的子章节中详细讨论。通过这些内容，您将掌握如何使用标准库中的各种组件来编写高效、可维护的C++程序。

### 1. [基础设施](infrastructure/Readme.md)

此节将介绍C++标准库中的基础设施组件，如输入输出流、格式化操作、字符串流和文件流。这些组件构成了C++程序与外部环境交互的基础设施，您将学习如何通过这些工具进行数据输入输出、格式化和文件操作。

- [`<iostream>`](infrastructure/iostream.md): 输入输出流的基本使用。
- [`<iomanip>`](infrastructure/iomanip.md): 控制输出格式的工具。
- [`<sstream>`](infrastructure/sstream.md): 字符串流的使用方法。
- [`<fstream>`](infrastructure/fstream.md): 文件流操作的实现。

### 2. [数据结构](data-structures/Readme.md)

此节将探讨C++标准库中提供的各种数据结构，如向量、链表、集合和映射。您将学习这些容器的特点、适用场景，以及如何高效地使用它们进行数据存储和管理。

- [`<vector>`](data-structures/vector.md): 动态数组的实现和使用。
- [`<list>`](data-structures/list.md): 双向链表的特点和用法。
- [`<deque>`](data-structures/deque.md): 双端队列的灵活性。
- [`<array>`](data-structures/array.md): 固定大小数组的优势。
- [`<set>`](data-structures/set.md): 集合操作与无重复元素的管理。
- [`<map>`](data-structures/map.md): 键值对映射的实现与应用。
- [`<unordered_set>`](data-structures/unordered_set.md): 无序集合的高效查询。
- [`<unordered_map>`](data-structures/unordered_map.md): 无序映射的性能与使用。
- [`<stack>`](data-structures/stack.md): 栈数据结构的使用。
- [`<queue>`](data-structures/queue.md): 队列操作的实现。
- [`<priority_queue>`](data-structures/priority_queue.md): 优先队列的特点和应用。

### 3. [算法](algorithms/Readme.md)

此节将介绍C++标准库中的算法模块，涵盖排序、搜索、数值运算等。您将学习如何使用标准库中的算法来处理各种数据结构，提高代码的性能和效率。

- [`<algorithm>`](algorithms/algorithm.md): 常用算法的实现和应用。
- [`<numeric>`](algorithms/numeric.md): 数值运算的标准库支持。

### 4. [迭代器](iterators/Readme.md)

此节将介绍迭代器的概念及其在C++标准库中的重要性。迭代器使得算法和数据结构的分离成为可能，您将学习如何使用不同类型的迭代器在容器之间进行遍历和操作。

- [`<iterator>`](iterators/iterator.md): 迭代器的类型和应用。

### 5. [泛型编程](generic-programming/Readme.md)

此节将探讨C++标准库中支持泛型编程的组件，帮助您编写高效的、类型无关的代码。您将学习如何利用类型特征、元组和函数对象来创建灵活的代码。

- [`<type_traits>`](generic-programming/type_traits.md): 类型特征和元编程支持。
- [`<tuple>`](generic-programming/tuple.md): 元组的使用和应用场景。
- [`<functional>`](generic-programming/functional.md): 函数对象和函数适配器。

### 6. [并发](concurrency/Readme.md)

此节将介绍C++标准库中提供的并发编程工具，如线程、互斥量和条件变量。您将学习如何编写多线程程序，以及如何正确地管理线程间的同步和通信。

- [`<thread>`](concurrency/thread.md): 多线程编程的基本概念。
- [`<mutex>`](concurrency/mutex.md): 线程同步的工具。
- [`<future>`](concurrency/future.md): 异步编程的实现方法。
- [`<condition_variable>`](concurrency/condition_variable.md): 条件变量的使用。
- [`<atomic>`](concurrency/atomic.md): 原子操作的实现和应用。

### 7. [时间](time/Readme.md)

此节将探讨C++标准库中的时间处理工具，涵盖时间点、时间段和时钟的操作。您将学习如何使用这些工具进行时间的管理和计算。

- [`<chrono>`](time/chrono.md): 时间处理的工具和技术。

### 8. [数学](math/Readme.md)

此节将介绍C++标准库中的数学工具，包括基础数学运算、复数操作和数值数组处理。

- [`<cmath>`](math/cmath.md): 常用数学函数和运算。
- [`<complex>`](math/complex.md): 复数的表示和运算。
- [`<valarray>`](math/valarray.md): 数值数组的操作和应用。

### 9. [字符串](strings/Readme.md)

此节将探讨C++标准库中提供的字符串处理工具，涵盖字符串操作、字符数组处理等。

- [`<string>`](strings/string.md): 字符串类的使用。
- [`<cstring>`](strings/cstring.md): C风格字符串的操作。
- [`<cwchar>`](strings/cwchar.md): 宽字符处理的工具。

### 10. [内存管理](memory-management/Readme.md)

此节将介绍C++标准库中的内存管理工具，涵盖动态内存分配和管理。

- [`<memory>`](memory-management/memory.md): 智能指针和内存管理的工具。

### 11. [错误处理](error-handling/Readme.md)

此节将讨论C++标准库中的错误处理机制，帮助您编写健壮的、容错能力强的程序。

- [`<exception>`](error-handling/exception.md): 异常处理和错误管理的实现。

### 12. [文件系统](filesystem/Readme.md)

此节将介绍C++标准库中的文件系统操作工具，帮助您进行文件和目录的管理。

- [`<filesystem>`](filesystem/filesystem.md): 文件系统的操作和管理。

### 13. [正则表达式](regex/Readme.md)

此节将介绍正则表达式的使用，帮助您进行复杂的文本处理和匹配操作。

- [`<regex>`](regex/regex.md): 正则表达式的定义和应用。

### 14. [随机数](random/Readme.md)

此节将探讨C++标准库中的随机数生成工具，帮助您在程序中生成随机数。

- [`<random>`](standard-library/random/random.md): 随机数的生成和管理。

### 15. [工具](utilities/Readme.md)

此节将介绍C++标准库中的各种工具组件，如元组、对、交换和移动语义的实现等。

- [`<utility>`](utilities/utility.md): 实用工具的使用。

### 16. [国际化](misc/Readme.md)

此节将探讨C++标准库中的国际化支持，帮助您编写支持多语言、多区域的应用程序。

- [`<locale>`](misc/locale.md): 区域设置和国际化的工具。
