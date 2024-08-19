## 内存分配与释放

在 C++ 中，内存管理是一个重要的概念。程序员需要了解如何在堆上分配和释放内存，以确保程序的正确性和效率。本小节将介绍 C++ 中的内存分配与释放的基本知识。

### 1. **栈与堆**

C++ 中的内存分为栈（stack）和堆（heap）两种主要区域：

- **栈**：用于存储局部变量和函数调用信息。栈上的内存由编译器自动管理，超出变量作用域时自动释放。
- **堆**：用于动态分配内存，程序员需要手动管理。堆上的内存在显式释放之前会一直存在。

### 2. **栈内存分配**

栈内存分配用于局部变量，编译器自动管理其生命周期。

```cpp
#include <iostream>

void stackAllocation() {
    int x = 10; // 栈上分配内存
    std::cout << "Value of x: " << x << std::endl;
} // x 在函数结束时自动释放

int main() {
    stackAllocation();
    return 0;
}
```

### 3. **堆内存分配**

堆内存分配用于动态分配内存，程序员需要手动管理其生命周期。C++ 提供了 `new` 和 `delete` 运算符来管理堆内存。

#### 3.1 **使用 `new` 分配内存**

`new` 运算符用于在堆上分配内存，并返回指向分配内存的指针。

```cpp
#include <iostream>

int main() {
    int* p = new int(10); // 在堆上分配内存
    std::cout << "Value of *p: " << *p << std::endl;
    delete p; // 释放堆上的内存
    return 0;
}
```

#### 3.2 **使用 `delete` 释放内存**

`delete` 运算符用于释放由 `new` 分配的内存。如果忘记释放内存，会导致内存泄漏。

```cpp
#include <iostream>

int main() {
    int* p = new int(10);
    std::cout << "Value of *p: " << *p << std::endl;
    delete p; // 释放堆上的内存
    // p = nullptr; // 释放后将指针设为 nullptr 以避免悬空指针
    return 0;
}
```

#### 3.3 **数组的动态分配和释放**

使用 `new` 和 `delete` 可以动态分配和释放数组的内存。

```cpp
#include <iostream>

int main() {
    int* arr = new int[5]; // 动态分配数组内存
    for (int i = 0; i < 5; ++i) {
        arr[i] = i * 10;
        std::cout << "arr[" << i << "] = " << arr[i] << std::endl;
    }
    delete[] arr; // 释放数组内存
    return 0;
}
```

### 4. **智能指针**

C++11 引入了智能指针来简化内存管理，避免手动管理内存带来的错误。常用的智能指针有 `std::unique_ptr`、`std::shared_ptr` 和 `std::weak_ptr`。

#### 4.1 **`std::unique_ptr`**

`std::unique_ptr` 是一种独占所有权的智能指针，不能共享所有权。

```cpp
#include <iostream>
#include <memory>

int main() {
    std::unique_ptr<int> p = std::make_unique<int>(10); // 分配内存
    std::cout << "Value of *p: " << *p << std::endl;
    // 内存自动释放，不需要调用 delete
    return 0;
}
```

#### 4.2 **`std::shared_ptr`**

`std::shared_ptr` 允许多个指针共享同一块内存，使用引用计数来管理内存。

```cpp
#include <iostream>
#include <memory>

int main() {
    std::shared_ptr<int> p1 = std::make_shared<int>(10); // 分配内存
    std::shared_ptr<int> p2 = p1; // 共享所有权
    std::cout << "Value of *p1: " << *p1 << std::endl;
    std::cout << "Value of *p2: " << *p2 << std::endl;
    // 内存自动释放，当最后一个 shared_ptr 被销毁时
    return 0;
}
```

### 5. **内存泄漏与悬空指针**

- **内存泄漏**：动态分配的内存未被释放，导致内存无法重用。
- **悬空指针**：指向已释放内存的指针，使用悬空指针可能导致未定义行为。

防止内存泄漏和悬空指针的常用方法包括：

- 使用智能指针来自动管理内存。
- 在释放内存后将指针设为 `nullptr`。

### 6. **总结**

C++ 中的内存管理是一个复杂但非常重要的主题。通过理解栈和堆的区别，正确使用 `new` 和 `delete` 运算符，以及引入智能指针，可以有效地管理内存，避免内存泄漏和悬空指针，提高程序的稳定性和性能。
