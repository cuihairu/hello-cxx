### C++11 右值引用

C++11 引入了右值引用（**rvalue references**），这是一项重要的语言特性，它改变了对象的生命周期管理和资源的移动操作。这一特性主要用于实现移动语义和完美转发，从而提高程序的性能和效率。

#### 1. **右值引用的定义**

右值引用是通过使用 `&&` 符号定义的，和左值引用（`&`）相对。右值引用允许你引用一个右值（临时对象或不可修改的对象），而不是仅仅引用一个左值（具名对象）。

**基本语法**：
```cpp
T&& variableName;
```

#### 2. **移动语义**

移动语义允许将资源（如动态分配的内存）从一个对象转移到另一个对象，而不是复制。这可以显著提高程序的效率，尤其是在处理大量数据时。

**示例**：
```cpp
#include <iostream>
#include <utility>  // For std::move

class MyClass {
public:
    MyClass() : data(new int[100]) {}
    ~MyClass() { delete[] data; }
    
    // 移动构造函数
    MyClass(MyClass&& other) noexcept : data(other.data) {
        other.data = nullptr;
    }

    // 移动赋值运算符
    MyClass& operator=(MyClass&& other) noexcept {
        if (this != &other) {
            delete[] data;
            data = other.data;
            other.data = nullptr;
        }
        return *this;
    }

private:
    int* data;
};

int main() {
    MyClass obj1;
    MyClass obj2 = std::move(obj1); // 使用移动构造函数
    MyClass obj3;
    obj3 = std::move(obj2);         // 使用移动赋值运算符
}
```

在这个示例中，`std::move` 将 `obj1` 和 `obj2` 转换为右值引用，从而触发移动构造函数和移动赋值运算符，避免了不必要的复制。

#### 3. **完美转发**

完美转发（**perfect forwarding**）允许将函数参数转发到其他函数时保持其值类别（左值或右值）。这在实现泛型函数和库时非常有用。

**示例**：
```cpp
#include <iostream>
#include <utility>  // For std::forward

template <typename T>
void process(T&& arg) {
    // 完美转发 arg 到另一个函数
    anotherFunction(std::forward<T>(arg));
}

void anotherFunction(int& i) {
    std::cout << "Lvalue reference" << std::endl;
}

void anotherFunction(int&& i) {
    std::cout << "Rvalue reference" << std::endl;
}

int main() {
    int x = 10;
    process(x);                // 调用 lvalue 版本
    process(20);               // 调用 rvalue 版本
}
```

在这个示例中，`std::forward<T>(arg)` 确保了 `process` 函数能够根据传入参数的值类别（左值或右值）调用正确的重载版本。

#### 4. **使用 `std::move`**

`std::move` 是一个用于将左值转换为右值引用的标准库函数。它的作用是显式地表明一个对象的资源可以被转移，从而允许使用移动构造函数和移动赋值运算符。

**示例**：
```cpp
#include <iostream>
#include <utility>  // For std::move

class MyClass {
public:
    MyClass() : data(new int[100]) {}
    ~MyClass() { delete[] data; }

    MyClass(MyClass&& other) noexcept : data(other.data) {
        other.data = nullptr;
    }

    MyClass& operator=(MyClass&& other) noexcept {
        if (this != &other) {
            delete[] data;
            data = other.data;
            other.data = nullptr;
        }
        return *this;
    }

private:
    int* data;
};

int main() {
    MyClass obj1;
    MyClass obj2 = std::move(obj1); // 使用 std::move
}
```

在这个示例中，`std::move` 将 `obj1` 转换为右值引用，从而触发移动构造函数。

### 总结

C++11 中的右值引用为程序员提供了更高效的资源管理和对象转移能力。通过右值引用，可以实现移动语义和完美转发，从而提高程序的性能。理解右值引用和相关操作是现代 C++ 编程的重要组成部分。