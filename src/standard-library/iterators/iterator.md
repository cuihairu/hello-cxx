## `<iterator>` 迭代器

`<iterator>` 头文件定义了 C++ 标准库中使用的各种迭代器类型和相关工具。迭代器是一种用于遍历容器的抽象机制，它提供了统一的接口来访问容器中的元素，无论容器的实际类型如何。掌握迭代器的使用可以帮助编写更通用且可维护的代码。

### 1. **迭代器的基本概念**

迭代器是一个对象，提供了一组操作来访问和遍历容器中的元素。它们类似于指针，可以进行解引用、前进和比较操作。根据其功能和用途，迭代器通常分为以下几种类型：

- **输入迭代器（Input Iterator）**：支持只读操作，允许从容器中读取元素。
- **输出迭代器（Output Iterator）**：支持只写操作，允许向容器中写入元素。
- **前向迭代器（Forward Iterator）**：支持多次读取和写入操作，能够向前遍历容器。
- **双向迭代器（Bidirectional Iterator）**：支持双向遍历容器，即可以向前和向后移动。
- **随机访问迭代器（Random Access Iterator）**：支持直接访问容器中的任意位置，具有随机访问能力。

### 2. **迭代器类型**

#### 2.1 `std::iterator`

`std::iterator` 是一个基类模板，提供了迭代器的基本接口和类型定义。虽然现代 C++ 不再推荐直接使用 `std::iterator`，它仍然对理解迭代器的工作原理有帮助。

**语法**：

```cpp
template<
    typename Category,
    typename T,
    typename Distance = std::ptrdiff_t,
    typename Pointer = T*,
    typename Reference = T&
>
class iterator;
```

- **Category**：迭代器的类别（如 `std::input_iterator_tag`、`std::output_iterator_tag` 等）。
- **T**：迭代器指向的值的类型。
- **Distance**：迭代器之间的距离类型（通常为 `std::ptrdiff_t`）。
- **Pointer**：指向值的指针类型。
- **Reference**：对值的引用类型。

#### 2.2 `std::iterator_traits`

`std::iterator_traits` 是一个辅助模板，用于提取迭代器类型的信息，如迭代器的值类型、指针类型和引用类型。

**语法**：

```cpp
template<typename Iterator>
struct iterator_traits;
```

**示例**：

```cpp
#include <iterator>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};
    using Iter = std::vector<int>::iterator;

    std::cout << "Value type: " << typeid(std::iterator_traits<Iter>::value_type).name() << std::endl;
    std::cout << "Pointer type: " << typeid(std::iterator_traits<Iter>::pointer).name() << std::endl;
    std::cout << "Reference type: " << typeid(std::iterator_traits<Iter>::reference).name() << std::endl;

    return 0;
}
```

#### 2.3 `std::reverse_iterator`

`std::reverse_iterator` 是一个适配器，用于将正向迭代器转换为反向迭代器，从而实现反向遍历。

**语法**：

```cpp
template<typename Iterator>
class reverse_iterator;
```

**示例**：

```cpp
#include <vector>
#include <iostream>
#include <iterator>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};

    std::cout << "Reverse traversal: ";
    for (auto rit = vec.rbegin(); rit != vec.rend(); ++rit) {
        std::cout << *rit << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

### 3. **常用迭代器操作**

#### 3.1 解引用

通过迭代器访问容器中的元素。

```cpp
std::vector<int> vec = {1, 2, 3, 4, 5};
auto it = vec.begin();
std::cout << *it << std::endl; // 输出：1
```

#### 3.2 递增和递减

前进或后退到下一个或上一个元素。

```cpp
std::vector<int> vec = {1, 2, 3, 4, 5};
auto it = vec.begin();
++it; // 前进到第二个元素
std::cout << *it << std::endl; // 输出：2

--it; // 返回到第一个元素
std::cout << *it << std::endl; // 输出：1
```

#### 3.3 随机访问

对于支持随机访问的迭代器，可以直接进行加减操作。

```cpp
std::vector<int> vec = {1, 2, 3, 4, 5};
auto it = vec.begin() + 2;
std::cout << *it << std::endl; // 输出：3
```

### 4. **总结**

迭代器是 C++ 标准库中处理容器元素的核心工具。它们提供了一种一致的方式来访问和操作容器中的数据，使得容器之间的代码更具通用性和可移植性。了解和掌握迭代器的使用，可以显著提高 C++ 编程的效率和灵活性。