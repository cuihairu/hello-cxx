## `<deque>` 数据结构

`<deque>` 是 C++ 标准库中的双端队列类模板，提供了在队列的两端进行高效插入和删除操作的能力。`std::deque` 是一种序列容器，允许在容器的两端进行快速操作，适用于需要在两端进行高效操作的场景。

### 1. **类介绍**

`std::deque`（双端队列）是一种双端容器，它允许在队列的前端和尾端进行快速的插入和删除操作。它在内部实现为多个内存块的组合，这样可以在需要时动态地扩展容量。

#### 1.1 基本操作

**创建和初始化：**

```cpp
#include <iostream>
#include <deque>

int main() {
    // 创建一个空的 deque
    std::deque<int> deq1;

    // 创建一个指定大小并用默认值初始化的 deque
    std::deque<int> deq2(10); // 包含 10 个 int 元素，每个元素初始化为 0

    // 创建一个指定大小并用特定值初始化的 deque
    std::deque<int> deq3(5, 42); // 包含 5 个 int 元素，每个元素初始化为 42

    // 使用列表初始化
    std::deque<int> deq4 = {1, 2, 3, 4, 5}; // 使用列表初始化

    return 0;
}
```

**访问元素：**

```cpp
#include <iostream>
#include <deque>

int main() {
    std::deque<int> deq = {10, 20, 30, 40, 50};

    // 访问元素
    for (const auto& value : deq) {
        std::cout << value << " ";
    }
    std::cout << std::endl;

    // 使用 at() 函数访问元素
    std::cout << "Element at index 2: " << deq.at(2) << std::endl;

    return 0;
}
```

**添加和删除元素：**

```cpp
#include <iostream>
#include <deque>

int main() {
    std::deque<int> deq = {1, 2, 3};

    // 在前面插入元素
    deq.push_front(0);

    // 在末尾插入元素
    deq.push_back(4);

    // 插入元素到指定位置
    auto it = deq.begin();
    ++it; // 移动到第二个位置
    deq.insert(it, 10); // 在第二个位置插入 10

    // 删除指定位置的元素
    it = deq.begin();
    ++it; // 移动到第二个位置
    deq.erase(it); // 删除第二个位置的元素

    // 删除前面和末尾的元素
    deq.pop_front();
    deq.pop_back();

    // 清空所有元素
    deq.clear();

    return 0;
}
```

**合并和排序：**

```cpp
#include <iostream>
#include <deque>

int main() {
    std::deque<int> deq1 = {3, 1, 4, 1, 5};
    std::deque<int> deq2 = {9, 2, 6, 5};

    // 合并两个 deque
    deq1.insert(deq1.end(), deq2.begin(), deq2.end());

    // 排序 deque
    std::sort(deq1.begin(), deq1.end());

    // 输出合并和排序后的 deque
    for (const auto& value : deq1) {
        std::cout << value << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

### 2. **高级操作**

**迭代器：**

```cpp
#include <iostream>
#include <deque>

int main() {
    std::deque<int> deq = {1, 2, 3, 4, 5};

    // 使用迭代器遍历
    for (std::deque<int>::iterator it = deq.begin(); it != deq.end(); ++it) {
        std::cout << *it << " ";
    }
    std::cout << std::endl;

    // 使用范围-based for 循环
    for (const auto& value : deq) {
        std::cout << value << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

**反转和遍历：**

```cpp
#include <iostream>
#include <deque>

int main() {
    std::deque<int> deq = {1, 2, 3, 4, 5};

    // 反转 deque
    std::reverse(deq.begin(), deq.end());

    // 输出反转后的 deque
    for (const auto& value : deq) {
        std::cout << value << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

### 3. **总结**

`<deque>` 提供了一个双端队列的实现，支持在容器的两端进行高效的插入和删除操作。与 `std::vector` 不同，`std::deque` 在动态扩展时不会重新分配整个容器的内存，从而在两端操作中保持高效。通过掌握 `std::deque` 的基本操作和高级功能，可以有效地处理需要在容器两端进行频繁操作的场景。