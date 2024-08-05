## 泛型编程

泛型编程是一种编程范式，旨在编写与类型无关的代码，允许在不同的数据类型上进行操作。C++ 的泛型编程通过模板（template）机制实现，模板提供了一种创建类型安全的代码的方式，同时允许在编译时进行类型检查。泛型编程的主要目标是实现代码的重用和抽象，减少重复代码。

### 1. **模板基础**

模板允许定义与类型无关的函数和类，编译器会根据实际使用的类型生成相应的代码。

#### 1.1 **函数模板**

函数模板允许编写可以接受不同类型参数的函数。例如，下面是一个泛型的 `max` 函数模板，可以比较不同类型的两个值。

```cpp
template <typename T>
T max(T a, T b) {
    return (a > b) ? a : b;
}
```

在这个示例中，`T` 是一个模板参数，函数 `max` 可以接受任意类型的参数，并返回最大值。

#### 1.2 **类模板**

类模板允许定义可以处理不同数据类型的类。例如，下面是一个泛型的 `Box` 类模板，它可以存储任意类型的值。

```cpp
template <typename T>
class Box {
public:
    void setValue(T value) {
        this->value = value;
    }

    T getValue() const {
        return value;
    }

private:
    T value;
};
```

在这个示例中，`Box` 类模板可以存储任意类型 `T` 的值，并提供设置和获取值的方法。

### 2. **模板特化**

模板特化允许为特定类型提供自定义实现。特化可以是完全特化（针对特定类型）或部分特化（针对类型的某些属性）。

#### 2.1 **完全特化**

完全特化为模板参数的特定类型提供特定的实现。

```cpp
template <>
class Box<bool> {
public:
    void setValue(bool value) {
        this->value = value;
    }

    bool getValue() const {
        return value;
    }

private:
    bool value;
};
```

在这个示例中，为 `bool` 类型提供了 `Box` 类的特定实现。

#### 2.2 **部分特化**

部分特化允许为模板参数的某些属性提供特定实现。例如，可以为具有特定类型属性的类提供部分特化。

```cpp
template <typename T, typename U>
class Pair {
public:
    Pair(T first, U second) : first(first), second(second) {}

private:
    T first;
    U second;
};

template <typename T>
class Pair<T, T> {
public:
    Pair(T value) : value(value) {}

private:
    T value;
};
```

在这个示例中，`Pair` 类模板的部分特化处理两个相同类型的参数。

### 3. **模板元编程**

模板元编程（TMP）利用模板在编译时进行计算和逻辑推理。这允许在编译时生成高效的代码并进行类型检查。

#### 3.1 **类型特征**

类型特征是模板元编程中的一种技术，用于在编译时查询类型属性。例如，`std::is_same` 可以用于检查两个类型是否相同。

```cpp
#include <type_traits>
#include <iostream>

template <typename T>
void checkType() {
    if (std::is_same<T, int>::value) {
        std::cout << "Type is int" << std::endl;
    } else {
        std::cout << "Type is not int" << std::endl;
    }
}

int main() {
    checkType<int>();   // 显式指定模板参数为 int
    checkType<double>(); // 显式指定模板参数为 double
    return 0;
}
```

在这个示例中，`checkType` 函数模板使用 `std::is_same` 来检查模板参数 `T` 是否是 `int` 类型，并在 `main` 函数中显式指定模板参数进行调用。

#### 3.2 **编译时计算**

模板元编程可以进行编译时计算，例如计算常量值或生成特定的编译时代码。

```cpp
template <int N>
struct Factorial {
    static const int value = N * Factorial<N - 1>::value;
};

template <>
struct Factorial<0> {
    static const int value = 1;
};
```

在这个示例中，`Factorial` 结构体模板计算阶乘值，并在编译时生成结果。

### 4. **模板与 STL**

标准模板库（STL）是 C++ 的一部分，广泛使用模板技术。STL 包括各种容器（如 `vector` 和 `map`）、算法（如 `sort` 和 `find`）和迭代器（如 `begin` 和 `end`），所有这些都利用了模板来实现类型无关的代码。

```cpp
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> v = {1, 2, 3, 4, 5};
    std::sort(v.begin(), v.end());
    return 0;
}
```

在这个示例中，`std::vector` 和 `std::sort` 都是模板类和模板函数，支持多种数据类型。

### 5. **总结**

泛型编程在 C++ 中通过模板机制提供了强大的功能，允许编写与类型无关的代码，增强了代码的重用性和可维护性。掌握模板基础、特化、元编程及其在 STL 中的应用，对于高效编写 C++ 代码至关重要。
