## 工具 `<utility>`

C++ 的 `<utility>` 头文件包含了许多有用的工具和功能，这些工具通常用于简化常见的编程任务，如类型操作、资源管理和模板编程。以下是对 `<utility>` 头文件中主要组件的介绍。

### 1. **`std::pair`**

`std::pair` 是一个简单的容器，用于存储一对值。它常用于函数返回多个值、容器中的键值对等场景。

#### **基本用法**

```cpp
#include <iostream>
#include <utility> // 包含 std::pair

int main() {
    std::pair<int, std::string> p(1, "example");

    std::cout << "First: " << p.first << std::endl;
    std::cout << "Second: " << p.second << std::endl;

    return 0;
}
```

### 2. **`std::make_pair`**

`std::make_pair` 是一个辅助函数，用于创建 `std::pair` 对象。它可以根据提供的值自动推导类型。

#### **示例**

```cpp
#include <iostream>
#include <utility> // 包含 std::make_pair

int main() {
    auto p = std::make_pair(1, "example");

    std::cout << "First: " << p.first << std::endl;
    std::cout << "Second: " << p.second << std::endl;

    return 0;
}
```

### 3. **`std::swap`**

`std::swap` 用于交换两个值。它是一个常用的工具函数，通常用于实现算法和数据结构的操作。

#### **示例**

```cpp
#include <iostream>
#include <utility> // 包含 std::swap

int main() {
    int a = 5, b = 10;

    std::cout << "Before swap: a = " << a << ", b = " << b << std::endl;

    std::swap(a, b);

    std::cout << "After swap: a = " << a << ", b = " << b << std::endl;

    return 0;
}
```

### 4. **`std::move`**

`std::move` 是一个类型转换工具，用于将对象的资源从一个对象转移到另一个对象。它通常用于启用移动语义和完美转发。

#### **示例**

```cpp
#include <iostream>
#include <utility> // 包含 std::move

void process(int&& value) {
    std::cout << "Processing value: " << value << std::endl;
}

int main() {
    int a = 10;
    process(std::move(a)); // 将 a 的资源移动到 process 函数中

    std::cout << "Value of a after move: " << a << std::endl; // a 的值未定义

    return 0;
}
```

### 5. **`std::forward`**

`std::forward` 用于在模板中完美转发参数，保持参数的值类别（左值或右值）。它通常用于转发函数参数。

#### **示例**

```cpp
#include <iostream>
#include <utility> // 包含 std::forward

template <typename T>
void process(T&& value) {
    // 使用 std::forward 转发参数
    process_impl(std::forward<T>(value));
}

void process_impl(int& value) {
    std::cout << "Processing lvalue: " << value << std::endl;
}

void process_impl(int&& value) {
    std::cout << "Processing rvalue: " << value << std::endl;
}

int main() {
    int a = 10;
    process(a); // 调用 lvalue 版本
    process(20); // 调用 rvalue 版本

    return 0;
}
```

### 6. **`std::tuple`**

`std::tuple` 是一个通用的固定大小的容器，可以存储不同类型的值。它常用于需要存储多个不同类型值的场景。

#### **基本用法**

```cpp
#include <iostream>
#include <tuple> // 包含 std::tuple

int main() {
    std::tuple<int, std::string, double> t(1, "example", 3.14);

    std::cout << "First: " << std::get<0>(t) << std::endl;
    std::cout << "Second: " << std::get<1>(t) << std::endl;
    std::cout << "Third: " << std::get<2>(t) << std::endl;

    return 0;
}
```

### 7. **`std::get`**

`std::get` 用于从 `std::tuple` 中获取指定索引位置的值。它可以与 `std::tuple` 结合使用，以访问存储在元组中的值。

#### **示例**

```cpp
#include <iostream>
#include <tuple> // 包含 std::get

int main() {
    std::tuple<int, std::string, double> t(1, "example", 3.14);

    std::cout << "Second element: " << std::get<1>(t) << std::endl;

    return 0;
}
```

### 8. **总结**

C++ 的 `<utility>` 头文件提供了多种实用的工具和功能，包括 `std::pair`、`std::make_pair`、`std::swap`、`std::move`、`std::forward` 和 `std::tuple` 等。这些工具极大地简化了编程任务，使得代码更加简洁和易于维护。掌握这些工具有助于编写高效、清晰的 C++ 代码。