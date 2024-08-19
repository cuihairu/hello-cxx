## 函数式编程

函数式编程是一种编程范式，强调使用函数进行计算和数据处理。与面向对象编程和过程式编程不同，函数式编程注重函数的不可变性和纯度，避免使用状态和可变数据。C++ 虽然不是一种纯函数式编程语言，但它支持函数式编程的一些核心概念和特性。

### 1. **函数对象和Lambda表达式**

函数对象（Functors）和Lambda表达式是C++中实现函数式编程的重要工具。

#### 1.1 **函数对象**

函数对象是重载了 `operator()` 的类或结构体实例，可以像函数一样调用。

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

struct Multiply {
    int factor;
    Multiply(int f) : factor(f) {}
    int operator()(int x) const { return x * factor; }
};

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};
    std::transform(vec.begin(), vec.end(), vec.begin(), Multiply(2));
    for (int v : vec) {
        std::cout << v << " ";
    }
    return 0;
}
```

在这个示例中，`Multiply` 是一个函数对象，可以对向量中的每个元素进行乘法操作。

#### 1.2 **Lambda表达式**

Lambda表达式是一种内联定义匿名函数的方式，简洁且功能强大。

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};
    std::transform(vec.begin(), vec.end(), vec.begin(), [](int x) { return x * 2; });
    for (int v : vec) {
        std::cout << v << " ";
    }
    return 0;
}
```

在这个示例中，Lambda表达式 `[](int x) { return x * 2; }` 定义了一个匿名函数，直接在 `std::transform` 调用中使用。

### 2. **不可变性**

函数式编程提倡不可变性，避免使用可变状态和数据。C++ 提供了 `const` 关键字来定义不可变的变量和函数参数。

```cpp
#include <iostream>

int add(const int a, const int b) {
    return a + b;
}

int main() {
    const int x = 10;
    const int y = 20;
    std::cout << add(x, y) << std::endl;
    return 0;
}
```

在这个示例中，`add` 函数的参数和 `x`、`y` 变量都被声明为 `const`，表示它们在函数调用过程中不会改变。

### 3. **高阶函数**

高阶函数是指可以接受一个或多个函数作为参数，或返回一个函数的函数。C++ 支持高阶函数的实现。

```cpp
#include <iostream>
#include <functional>

std::function<int(int)> make_multiplier(int factor) {
    return [factor](int x) { return x * factor; };
}

int main() {
    auto times_two = make_multiplier(2);
    std::cout << times_two(5) << std::endl; // 输出 10
    return 0;
}
```

在这个示例中，`make_multiplier` 函数接受一个整数参数，并返回一个Lambda表达式，这个Lambda表达式是一个乘法器函数。

### 4. **递归**

递归是函数式编程中的一个重要概念，它允许一个函数调用自身来解决问题。

```cpp
#include <iostream>

int factorial(int n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);
}

int main() {
    std::cout << factorial(5) << std::endl; // 输出 120
    return 0;
}
```

在这个示例中，`factorial` 函数使用递归来计算阶乘。

### 5. **标准库中的函数式编程支持**

C++ 标准库提供了一些函数式编程的支持，包括函数对象、Lambda表达式、`std::function`、`std::bind`、以及 `<algorithm>` 库中的算法。

#### 5.1 **std::function**

`std::function` 是一个通用的多态函数包装器，用于存储、传递和调用可调用对象。

```cpp
#include <iostream>
#include <functional>

int add(int a, int b) {
    return a + b;
}

int main() {
    std::function<int(int, int)> func = add;
    std::cout << func(10, 20) << std::endl; // 输出 30
    return 0;
}
```

在这个示例中，`std::function` 包装了一个普通函数 `add`。

#### 5.2 **std::bind**

`std::bind` 用于创建绑定参数的函数对象，可以用于部分应用。

```cpp
#include <iostream>
#include <functional>

int add(int a, int b) {
    return a + b;
}

int main() {
    auto add10 = std::bind(add, std::placeholders::_1, 10);
    std::cout << add10(5) << std::endl; // 输出 15
    return 0;
}
```

在这个示例中，`std::bind` 将 `add` 函数的第二个参数绑定为 10，创建了一个新的函数对象 `add10`。

### 6. **总结**

函数式编程在 C++ 中提供了一种强大的编程范式，可以提高代码的可读性、可维护性和重用性。通过使用函数对象、Lambda表达式、不可变性、高阶函数和递归，以及 C++ 标准库中的函数式编程支持，可以在 C++ 中实现许多函数式编程的特性和优势。
