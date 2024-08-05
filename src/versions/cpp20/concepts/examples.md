### C++20 概念（Concepts） 示例代码

以下是一些示例代码，展示了如何在 C++20 中定义和使用概念（Concepts）。

#### 1. **定义概念**

定义一个概念，要求类型必须支持加法操作，并且加法的结果能够转换为指定的类型。

```cpp
#include <iostream>
#include <concepts>

// 定义一个概念，要求类型 T 支持加法操作
template <typename T>
concept Addable = requires(T a, T b) {
    { a + b } -> std::convertible_to<T>;
};

// 测试概念
void testConcept() {
    std::cout << std::boolalpha;
    std::cout << "int: " << Addable<int> << std::endl;           // true
    std::cout << "double: " << Addable<double> << std::endl;     // true
    std::cout << "std::string: " << Addable<std::string> << std::endl;  // false
}

int main() {
    testConcept();
    return 0;
}
```

#### 2. **使用概念约束模板**

使用定义的概念约束模板，使模板只能接受符合概念要求的类型。

```cpp
#include <iostream>
#include <concepts>

// 定义一个概念，要求类型 T 支持加法操作
template <typename T>
concept Addable = requires(T a, T b) {
    { a + b } -> std::convertible_to<T>;
};

// 使用概念约束模板
template <Addable T>
T add(T a, T b) {
    return a + b;
}

int main() {
    std::cout << add(5, 3) << std::endl;  // 合法，int 满足 Addable 概念
    // std::cout << add("hello", "world") << std::endl; // 不合法，const char* 不满足 Addable 概念
    return 0;
}
```

#### 3. **概念的组合**

组合多个概念，以创建更复杂的类型要求。

```cpp
#include <iostream>
#include <concepts>

// 定义一个概念，要求类型 T 支持加法操作
template <typename T>
concept Addable = requires(T a, T b) {
    { a + b } -> std::convertible_to<T>;
};

// 定义一个概念，要求类型 T 支持减法操作
template <typename T>
concept Subtractable = requires(T a, T b) {
    { a - b } -> std::convertible_to<T>;
};

// 定义一个组合概念，要求类型 T 既支持加法又支持减法
template <typename T>
concept Arithmetic = Addable<T> && Subtractable<T>;

// 使用组合概念约束模板
template <Arithmetic T>
T compute(T a, T b) {
    return a + b - b; // 示例操作
}

int main() {
    std::cout << compute(10, 5) << std::endl;  // 合法，int 满足 Arithmetic 概念
    // std::cout << compute("hello", "world") << std::endl; // 不合法，const char* 不满足 Arithmetic 概念
    return 0;
}
```

#### 4. **概念与类模板**

将概念应用于类模板参数。

```cpp
#include <iostream>
#include <concepts>

// 定义一个概念，要求类型 T 支持加法操作
template <typename T>
concept Addable = requires(T a, T b) {
    { a + b } -> std::convertible_to<T>;
};

// 使用概念约束类模板
template <Addable T>
class Adder {
public:
    Adder(T x, T y) : a(x), b(y) {}

    T add() const {
        return a + b;
    }

private:
    T a, b;
};

int main() {
    Adder<int> intAdder(5, 3);
    std::cout << intAdder.add() << std::endl;  // 合法，int 满足 Addable 概念

    // Adder<std::string> strAdder("hello", "world"); // 不合法，std::string 不满足 Addable 概念
    return 0;
}
```

#### 5. **概念与函数重载**

通过概念实现函数重载。

```cpp
#include <iostream>
#include <concepts>

// 定义一个概念，要求类型 T 支持输出到流
template <typename T>
concept Printable = requires(T a, std::ostream& os) {
    { os << a } -> std::convertible_to<std::ostream&>;
};

// 定义两个重载函数，分别处理可打印和不可打印的类型
template <Printable T>
void print(const T& value) {
    std::cout << "Printable: " << value << std::endl;
}

template <typename T>
void print(const T&) {
    std::cout << "Non-printable" << std::endl;
}

int main() {
    print(42);              // 输出：Printable: 42
    print("hello");         // 输出：Printable: hello
    print(std::vector<int>()); // 输出：Non-printable
    return 0;
}
```

这些示例展示了如何在 C++20 中定义和使用概念（Concepts）。概念为模板编程引入了更加直观的类型约束机制，使得代码更具可读性和可维护性。