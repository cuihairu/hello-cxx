## 内存管理 `<memory>`

`<memory>` 是 C++ 标准库中的一个重要头文件，专门用于内存管理。它提供了一些功能和工具来处理动态内存分配、智能指针以及自定义内存分配器。了解这些工具可以帮助程序员更高效和安全地管理内存资源。以下是 `<memory>` 头文件中的关键内容：

### 1. **智能指针**

智能指针是 C++ 中用于自动管理内存的工具，它们有助于减少内存泄漏和悬挂指针等问题。智能指针主要包括以下几种：

#### **`std::unique_ptr`**

`std::unique_ptr` 是一种独占智能指针，表示对动态分配对象的唯一所有权。它不允许复制，但可以转移所有权。`std::unique_ptr` 自动释放它管理的对象。

```cpp
#include <iostream>
#include <memory>

int main() {
    std::unique_ptr<int> ptr = std::make_unique<int>(10);  // 创建 unique_ptr
    std::cout << "Value: " << *ptr << std::endl;  // 使用 unique_ptr
    // 内存自动释放，无需手动 delete
    return 0;
}
```

#### **`std::shared_ptr`**

`std::shared_ptr` 是一种共享智能指针，允许多个 `std::shared_ptr` 实例共同拥有一个对象。引用计数机制确保对象在最后一个 `std::shared_ptr` 被销毁时释放。

```cpp
#include <iostream>
#include <memory>

int main() {
    std::shared_ptr<int> ptr1 = std::make_shared<int>(20);  // 创建 shared_ptr
    std::shared_ptr<int> ptr2 = ptr1;  // 共享所有权

    std::cout << "Value: " << *ptr1 << std::endl;
    std::cout << "Value: " << *ptr2 << std::endl;
    // 当最后一个 shared_ptr 被销毁时，内存自动释放
    return 0;
}
```

#### **`std::weak_ptr`**

`std::weak_ptr` 是一种弱引用智能指针，用于打破 `std::shared_ptr` 的循环引用问题。它不会改变引用计数，主要用于观察 `std::shared_ptr` 管理的对象。

```cpp
#include <iostream>
#include <memory>

int main() {
    std::shared_ptr<int> ptr1 = std::make_shared<int>(30);
    std::weak_ptr<int> weakPtr = ptr1;  // 创建 weak_ptr

    if (auto ptr2 = weakPtr.lock()) {  // 尝试获取 shared_ptr
        std::cout << "Value: " << *ptr2 << std::endl;
    } else {
        std::cout << "Object has been deleted" << std::endl;
    }

    return 0;
}
```

### 2. **自定义内存管理**

`<memory>` 还提供了对自定义内存分配的支持。`std::allocator` 类模板允许用户定义内存分配和释放的行为。

#### **`std::allocator`**

`std::allocator` 是一个标准内存分配器，用于动态分配内存和对象。

```cpp
#include <iostream>
#include <memory>

int main() {
    std::allocator<int> allocator;

    // 分配内存
    int* p = allocator.allocate(1);

    // 构造对象
    allocator.construct(p, 40);

    std::cout << "Value: " << *p << std::endl;

    // 销毁对象
    allocator.destroy(p);

    // 释放内存
    allocator.deallocate(p, 1);

    return 0;
}
```

### 3. **内存对齐**

`<memory>` 提供了对内存对齐的支持，特别是 `std::align` 函数可以调整内存的对齐方式，使其符合特定的对齐要求。

#### **`std::align`**

`std::align` 用于调整内存的对齐方式，可以确保内存块按照特定对齐要求对齐。

```cpp
#include <iostream>
#include <memory>

int main() {
    std::size_t alignment = alignof(double);
    std::size_t size = sizeof(double);
    char buffer[sizeof(double) + alignment - 1];

    void* ptr = buffer;
    void* alignedPtr = std::align(alignment, size, ptr, sizeof(buffer));

    if (alignedPtr) {
        std::cout << "Memory aligned at: " << alignedPtr << std::endl;
    } else {
        std::cout << "Memory alignment failed" << std::endl;
    }

    return 0;
}
```

### 4. **总结**

`<memory>` 提供了多种工具来管理动态内存和智能指针。智能指针（如 `std::unique_ptr`、`std::shared_ptr` 和 `std::weak_ptr`）帮助自动化内存管理，减少内存泄漏的风险。自定义内存管理功能（如 `std::allocator`）允许用户细粒度控制内存分配。内存对齐工具（如 `std::align`）确保内存块按照特定要求对齐。掌握这些工具可以提高 C++ 程序的安全性和效率。