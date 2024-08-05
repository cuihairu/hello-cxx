## `<functional>` 函数对象与函数适配器

`<functional>` 是 C++ 标准库中的一个头文件，提供了与函数相关的功能，如函数对象（functors）、函数适配器（function adapters）和函数绑定（function binding）。这些工具可以帮助实现更灵活和可重用的代码，尤其在泛型编程中。

### 1. **函数对象（Functors）**

函数对象是重载了 `operator()` 的类对象。它们可以像普通函数一样被调用，但具有更高的灵活性。

#### 1.1 定义和使用函数对象

```cpp
#include <iostream>

class Add {
public:
    Add(int x) : x_(x) {}
    int operator()(int y) const {
        return x_ + y;
    }
private:
    int x_;
};

int main() {
    Add add5(5);
    std::cout << "5 + 3 = " << add5(3) << std::endl;  // 输出: 5 + 3 = 8
    return 0;
}
```

### 2. **`std::function`**

`std::function` 是一个通用的函数包装器，可以包装任何可调用对象，如普通函数、函数对象、Lambda 表达式、甚至是成员函数。

#### 2.1 使用 `std::function`

```cpp
#include <iostream>
#include <functional>

void print(int x) {
    std::cout << x << std::endl;
}

int main() {
    std::function<void(int)> func = print;
    func(42);  // 输出: 42
    
    return 0;
}
```

#### 2.2 使用 Lambda 表达式

```cpp
#include <iostream>
#include <functional>

int main() {
    std::function<void(int)> func = [](int x) {
        std::cout << x << std::endl;
    };
    func(42);  // 输出: 42
    
    return 0;
}
```

### 3. **函数适配器**

函数适配器是用于调整函数调用的方式或传递方式的工具。标准库提供了一些常用的函数适配器，如 `std::bind` 和 `std::not1` / `std::not2`。

#### 3.1 `std::bind`

`std::bind` 用于绑定函数参数。它创建一个新的可调用对象，可以将部分参数绑定到原始函数或函数对象上。

```cpp
#include <iostream>
#include <functional>

void print(int x, int y) {
    std::cout << x << ", " << y << std::endl;
}

int main() {
    auto boundPrint = std::bind(print, 42, std::placeholders::_1);
    boundPrint(24);  // 输出: 42, 24
    
    return 0;
}
```

#### 3.2 `std::not1` 和 `std::not2`

`std::not1` 和 `std::not2` 用于取反一个函数对象的结果。注意，这些工具在 C++11 中已经被弃用，被 `std::not_fn` 替代。

```cpp
#include <iostream>
#include <functional>

bool isEven(int x) {
    return x % 2 == 0;
}

int main() {
    auto isOdd = std::not_fn(isEven);
    std::cout << std::boolalpha << isOdd(5) << std::endl;  // 输出: true
    
    return 0;
}
```

### 4. **Lambda 表达式**

Lambda 表达式是一种内联的、无名的函数对象，可以用于定义简短的函数体。它们是 C++11 引入的一个强大功能，使得编写匿名函数变得简洁。

#### 4.1 基本用法

```cpp
#include <iostream>

int main() {
    auto lambda = [](int x) {
        return x * x;
    };
    std::cout << "Square of 5: " << lambda(5) << std::endl;  // 输出: Square of 5: 25
    
    return 0;
}
```

#### 4.2 捕获外部变量

Lambda 表达式可以捕获外部变量，这些变量可以通过值捕获或引用捕获。

```cpp
#include <iostream>

int main() {
    int factor = 10;
    auto lambda = [factor](int x) {
        return x * factor;
    };
    std::cout << "10 * 5: " << lambda(5) << std::endl;  // 输出: 10 * 5: 50
    
    return 0;
}
```

### 5. **总结**

`<functional>` 提供了多种工具，用于增强函数的灵活性和复用性。函数对象（functors）和 `std::function` 提供了对函数调用的高级封装，而函数适配器（如 `std::bind`）和 Lambda 表达式则为函数调用的创建和管理提供了更多的灵活性。这些功能在泛型编程中尤为重要，使得代码更具可重用性和可维护性。