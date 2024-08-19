### C++11 Lambda 表达式

C++11 引入了 Lambda 表达式，这是一种在函数体内部定义匿名函数的方式。Lambda 表达式使得在代码中定义和使用函数变得更加简洁和灵活，特别是在需要使用短小函数对象的地方，比如 STL 算法和回调函数。

#### 1. **基本语法**

Lambda 表达式的基本语法如下：
```cpp
[capture](parameters) -> return_type {
    // function body
}
```

- `capture`：捕获列表，用于指定如何捕获外部变量。
- `parameters`：函数参数列表，类似于普通函数的参数。
- `return_type`：返回类型，默认为 `auto`。
- `function body`：函数体。

**示例**：
```cpp
#include <iostream>

int main() {
    // 定义一个 Lambda 表达式
    auto add = [](int a, int b) -> int {
        return a + b;
    };

    std::cout << "Sum: " << add(3, 4) << std::endl; // 输出 Sum: 7
    return 0;
}
```

在这个示例中，`add` 是一个 Lambda 表达式，用于计算两个整数的和。

#### 2. **捕获列表**

捕获列表指定 Lambda 表达式如何捕获外部变量。可以捕获变量的值、引用，或两者结合。

**示例**：
```cpp
#include <iostream>

int main() {
    int x = 10;
    int y = 20;

    // 捕获 x 和 y 的值
    auto captureByValue = [x, y]() {
        return x + y;
    };

    // 捕获 x 和 y 的引用
    auto captureByReference = [&x, &y]() {
        x += 10;
        y += 10;
        return x + y;
    };

    std::cout << "Capture by value: " << captureByValue() << std::endl; // 输出 Capture by value: 30
    std::cout << "Capture by reference: " << captureByReference() << std::endl; // 输出 Capture by reference: 50
    std::cout << "x after capture by reference: " << x << std::endl; // 输出 x after capture by reference: 20
    std::cout << "y after capture by reference: " << y << std::endl; // 输出 y after capture by reference: 30

    return 0;
}
```

在这个示例中，`captureByValue` 捕获 `x` 和 `y` 的值，而 `captureByReference` 捕获它们的引用，这使得对 `x` 和 `y` 的修改能够反映到外部变量中。

#### 3. **可变 Lambda**

默认情况下，Lambda 表达式中的捕获变量是不可修改的。如果需要在 Lambda 表达式中修改捕获的变量，可以使用 `mutable` 关键字。

**示例**：
```cpp
#include <iostream>

int main() {
    int x = 10;

    // 可变 Lambda 表达式
    auto mutableLambda = [x]() mutable {
        x += 5;
        return x;
    };

    std::cout << "Result of mutable lambda: " << mutableLambda() << std::endl; // 输出 Result of mutable lambda: 15
    std::cout << "Value of x after mutable lambda: " << x << std::endl; // 输出 Value of x after mutable lambda: 10

    return 0;
}
```

在这个示例中，`mutable` 关键字允许 Lambda 表达式修改捕获的变量 `x`，但不会影响外部变量 `x` 的值。

#### 4. **返回类型**

Lambda 表达式的返回类型可以显式指定，也可以由编译器自动推导。如果返回类型很复杂，可以使用 `auto` 进行自动推导。

**示例**：
```cpp
#include <iostream>

int main() {
    auto lambdaWithReturnType = [](int a, int b) -> double {
        return static_cast<double>(a) / b;
    };

    std::cout << "Result: " << lambdaWithReturnType(5, 2) << std::endl; // 输出 Result: 2.5
    return 0;
}
```

在这个示例中，Lambda 表达式显式地指定了返回类型为 `double`。

#### 5. **Lambda 表达式的应用**

Lambda 表达式广泛用于 STL 算法、异步编程和回调函数等场景。

**示例（用于 STL 算法）**：
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> numbers = {1, 2, 3, 4, 5};

    // 使用 Lambda 表达式进行排序
    std::sort(numbers.begin(), numbers.end(), [](int a, int b) {
        return a > b;
    });

    for (int number : numbers) {
        std::cout << number << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

在这个示例中，Lambda 表达式用于指定 `std::sort` 算法的排序规则，使得 `numbers` 向量按降序排列。

### 总结

C++11 的 Lambda 表达式极大地增强了语言的表达能力，简化了函数对象的创建和使用。通过 Lambda 表达式，代码变得更加简洁、可读，并且能够更灵活地处理各种编程任务。理解和掌握 Lambda 表达式是现代 C++ 编程的关键技能。