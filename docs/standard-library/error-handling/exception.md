## 错误处理 `<exception>`

C++ 提供了一个全面的错误处理机制，主要通过异常处理机制来实现。异常处理允许程序在遇到错误条件时，将控制权转移到处理错误的代码部分，而不是简单地终止程序。`<exception>` 头文件定义了异常处理机制的核心类和函数。以下是 `<exception>` 头文件中的主要内容及其用法：

### 1. **异常类**

C++ 的异常处理机制基于类的继承体系。`<exception>` 头文件定义了几个重要的异常类，它们可以作为用户定义异常的基类。

#### **`std::exception`**

`std::exception` 是所有标准异常类的基类。它提供了一个虚拟的 `what()` 方法，用于获取异常的描述信息。

```cpp
#include <iostream>
#include <exception>

class MyException : public std::exception {
public:
    const char* what() const noexcept override {
        return "MyException occurred";
    }
};

int main() {
    try {
        throw MyException();
    } catch (const std::exception& e) {
        std::cout << "Exception: " << e.what() << std::endl;
    }
    return 0;
}
```

#### **`std::runtime_error`**

`std::runtime_error` 继承自 `std::exception`，用于表示运行时错误。它的构造函数接受一个描述错误的字符串。

```cpp
#include <iostream>
#include <stdexcept>

int main() {
    try {
        throw std::runtime_error("Runtime error occurred");
    } catch (const std::runtime_error& e) {
        std::cout << "Runtime error: " << e.what() << std::endl;
    }
    return 0;
}
```

#### **`std::logic_error`**

`std::logic_error` 继承自 `std::exception`，用于表示逻辑错误，例如函数参数不合法等情况。

```cpp
#include <iostream>
#include <stdexcept>

int main() {
    try {
        throw std::logic_error("Logic error occurred");
    } catch (const std::logic_error& e) {
        std::cout << "Logic error: " << e.what() << std::endl;
    }
    return 0;
}
```

### 2. **异常处理机制**

C++ 的异常处理机制由 `try`、`catch` 和 `throw` 关键字组成。

#### **`throw`**

`throw` 关键字用于抛出异常。异常对象可以是任何类型，但通常是从 `std::exception` 继承的类。

```cpp
void mayThrow(bool shouldThrow) {
    if (shouldThrow) {
        throw std::runtime_error("An error occurred");
    }
}
```

#### **`try` 和 `catch`**

`try` 块用于包含可能会抛出异常的代码，`catch` 块用于处理这些异常。`catch` 块可以捕捉不同类型的异常。

```cpp
try {
    mayThrow(true);
} catch (const std::runtime_error& e) {
    std::cout << "Caught runtime error: " << e.what() << std::endl;
} catch (const std::exception& e) {
    std::cout << "Caught exception: " << e.what() << std::endl;
}
```

### 3. **异常的传播**

当异常被抛出时，它会沿调用栈向上传播，直到找到合适的 `catch` 块。如果没有找到合适的 `catch` 块，程序会终止。

```cpp
void funcB() {
    throw std::runtime_error("Error in funcB");
}

void funcA() {
    funcB();
}

int main() {
    try {
        funcA();
    } catch (const std::runtime_error& e) {
        std::cout << "Caught: " << e.what() << std::endl;
    }
    return 0;
}
```

### 4. **异常安全**

编写异常安全的代码可以确保在异常发生时，程序能够正常恢复。异常安全的代码通常使用 RAII（Resource Acquisition Is Initialization）技术来管理资源。

#### **RAII**

RAII 是一种编程技术，它确保资源（如内存、文件句柄）在对象的生命周期内自动分配和释放。智能指针和其他资源管理类通常采用 RAII 技术来提供异常安全保障。

```cpp
#include <iostream>
#include <memory>

void mayThrow(bool shouldThrow) {
    if (shouldThrow) {
        throw std::runtime_error("Error occurred");
    }
}

int main() {
    try {
        std::unique_ptr<int> ptr = std::make_unique<int>(10);
        mayThrow(true);  // 会抛出异常
    } catch (const std::runtime_error& e) {
        std::cout << "Caught: " << e.what() << std::endl;
    }
    // std::unique_ptr 会自动释放内存
    return 0;
}
```

### 5. **自定义异常**

用户可以创建自己的异常类，继承自标准异常类（如 `std::exception`）或其他异常类。这样可以提供更具体的错误信息。

```cpp
#include <iostream>
#include <exception>

class CustomException : public std::exception {
public:
    const char* what() const noexcept override {
        return "Custom exception occurred";
    }
};

int main() {
    try {
        throw CustomException();
    } catch (const CustomException& e) {
        std::cout << "Caught custom exception: " << e.what() << std::endl;
    }
    return 0;
}
```

### 6. **总结**

`<exception>` 头文件提供了 C++ 异常处理机制的核心功能，包括标准异常类（如 `std::exception`、`std::runtime_error` 和 `std::logic_error`）和异常处理语法（`try`、`catch` 和 `throw`）。使用异常处理可以提高程序的鲁棒性和可维护性，但编写异常安全的代码同样重要。通过 RAII 和自定义异常类，程序员可以更好地管理资源和处理特定错误情况。