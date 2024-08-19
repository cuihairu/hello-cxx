### C++20 其他新特性

C++20 带来了许多新的特性和改进，不仅包括协程和概念，还有其他显著的语言和库更新。以下是 C++20 的一些其他重要特性：

#### 1. **范围（Ranges）**

C++20 引入了范围库，提供了一种更简洁和表达力强的方式来操作集合。

- **`std::ranges::views`**：提供了一些用于创建视图的工具，支持链式调用和延迟计算。例如，`std::views::transform` 和 `std::views::filter`。
- **`std::ranges::range`**：引入了一个新的范围概念，简化了范围的定义和使用。

```cpp
#include <iostream>
#include <ranges>
#include <vector>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};

    auto even_numbers = vec | std::views::filter([](int n) { return n % 2 == 0; });

    for (int n : even_numbers) {
        std::cout << n << " "; // 输出: 2 4
    }

    return 0;
}
```

#### 2. **`constexpr` 扩展**

C++20 扩展了 `constexpr` 的功能，允许在编译期执行更多的代码。

- **动态内存分配**：`constexpr` 函数现在可以使用 `new` 和 `delete` 进行动态内存分配。
- **`constexpr` 变量**：允许 `constexpr` 变量的初始化更加灵活。

```cpp
#include <iostream>
#include <vector>

constexpr int factorial(int n) {
    return n <= 1 ? 1 : n * factorial(n - 1);
}

int main() {
    constexpr int result = factorial(5); // 编译期计算
    std::cout << result << std::endl; // 输出: 120
    return 0;
}
```

#### 3. **三路比较运算符（Spaceship Operator）**

C++20 引入了 `<=>` 运算符，也称为“太空船运算符”，用于简化自定义比较操作符的实现。

```cpp
#include <iostream>
#include <compare>

struct Person {
    std::string name;
    int age;

    auto operator<=>(const Person&) const = default; // 使用默认的三路比较
};

int main() {
    Person p1{"Alice", 30};
    Person p2{"Bob", 25};

    if (p1 < p2) {
        std::cout << "p1 is less than p2" << std::endl;
    } else if (p1 > p2) {
        std::cout << "p1 is greater than p2" << std::endl;
    } else {
        std::cout << "p1 is equal to p2" << std::endl;
    }

    return 0;
}
```

#### 4. **`[[likely]]` 和 `[[unlikely]]`**

这两个属性用于提示编译器某些分支的可能性，帮助优化代码性能。

- **`[[likely]]`**：表示某个分支在运行时可能被频繁执行。
- **`[[unlikely]]`**：表示某个分支在运行时可能不常被执行。

```cpp
#include <iostream>

void process(bool condition) {
    if (condition) [[likely]] {
        std::cout << "Condition is likely true" << std::endl;
    } else [[unlikely]] {
        std::cout << "Condition is unlikely true" << std::endl;
    }
}

int main() {
    process(true);  // 输出: Condition is likely true
    process(false); // 输出: Condition is unlikely true
    return 0;
}
```

#### 5. **`std::format`**

C++20 引入了 `std::format`，提供了一种类型安全、功能强大的格式化字符串的方法。

```cpp
#include <iostream>
#include <format>

int main() {
    std::string formatted = std::format("The answer is {} and {}", 42, 3.14);
    std::cout << formatted << std::endl; // 输出: The answer is 42 and 3.14
    return 0;
}
```

#### 6. **`std::ranges::to` 和 `std::ranges::to<std::vector>`**

用于将范围直接转换为容器，简化了范围操作后的数据存储。

```cpp
#include <iostream>
#include <ranges>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};

    auto result = vec | std::views::transform([](int n) { return n * 2; }) | std::ranges::to<std::vector>();

    for (int n : result) {
        std::cout << n << " "; // 输出: 2 4 6 8 10
    }

    return 0;
}
```

#### 7. **`std::span`**

`std::span` 是一个轻量级的、范围适配的视图，用于表示数组或其他连续的内存块的子集。

```cpp
#include <iostream>
#include <span>

void print_elements(std::span<int> sp) {
    for (int elem : sp) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    print_elements(arr); // 输出: 1 2 3 4 5
    return 0;
}
```

这些新特性和改进使得 C++20 更加现代化，提供了更强的语言功能、标准库组件和性能优化工具，提升了编程体验和效率。