## `std::queue` 数据结构

`std::queue` 是 C++ 标准库中的一个容器适配器，用于实现队列（queue）数据结构。队列是一种遵循“先进先出”（FIFO，First In, First Out）原则的数据结构，即最早插入的元素最先被访问。`std::queue` 是基于其他容器（如 `std::deque` 或 `std::list`）实现的，默认使用 `std::deque` 作为底层容器。

### 1. **类介绍**

`std::queue` 的主要特点包括：
- **FIFO 结构**：队列的特性保证了元素的访问顺序。
- **封装底层容器**：队列适配器封装了底层容器，提供了一组用于队列操作的方法。
- **底层容器可定制**：可以使用不同的底层容器（如 `std::deque` 或 `std::list`）来实现 `std::queue`。

### 2. **基本操作**

**创建和初始化：**

```cpp
#include <iostream>
#include <queue>
#include <deque>
#include <list>

int main() {
    // 使用默认底层容器 std::deque
    std::queue<int> queue1;

    // 使用 std::list 作为底层容器
    std::queue<int, std::list<int>> queue2;

    return 0;
}
```

**队列操作：**

```cpp
#include <iostream>
#include <queue>

int main() {
    std::queue<int> queue;

    // 入队
    queue.push(10);
    queue.push(20);
    queue.push(30);

    // 输出队首元素
    std::cout << "Front element: " << queue.front() << std::endl;

    // 出队
    queue.pop();

    // 输出队首元素
    std::cout << "Front element after pop: " << queue.front() << std::endl;

    // 检查队列是否为空
    std::cout << "Is queue empty? " << (queue.empty() ? "Yes" : "No") << std::endl;

    // 获取队列的大小
    std::cout << "Queue size: " << queue.size() << std::endl;

    return 0;
}
```

### 3. **成员函数**

**`push(const value_type& value)`**  
将元素添加到队列的尾部。

**`pop()`**  
移除队列的头部元素。

**`front()`**  
返回队列的头部元素，但不移除它。

**`back()`**  
返回队列的尾部元素，但不移除它。

**`empty()`**  
检查队列是否为空。返回 `true` 如果队列为空，`false` 如果队列不为空。

**`size()`**  
返回队列中元素的数量。

### 4. **底层容器**

`std::queue` 可以使用不同的底层容器，最常见的是 `std::deque` 和 `std::list`。底层容器影响队列的性能和行为。以下是如何自定义底层容器的示例：

```cpp
#include <iostream>
#include <queue>
#include <deque>
#include <list>

int main() {
    // 使用 std::list 作为底层容器
    std::queue<int, std::list<int>> queue1;
    queue1.push(1);
    queue1.push(2);
    std::cout << "Queue with std::list as underlying container:" << std::endl;
    while (!queue1.empty()) {
        std::cout << queue1.front() << std::endl;
        queue1.pop();
    }

    // 使用 std::deque 作为底层容器
    std::queue<int, std::deque<int>> queue2;
    queue2.push(3);
    queue2.push(4);
    std::cout << "Queue with std::deque as underlying container:" << std::endl;
    while (!queue2.empty()) {
        std::cout << queue2.front() << std::endl;
        queue2.pop();
    }

    return 0;
}
```

### 5. **总结**

`std::queue` 是一个队列容器适配器，提供了简单的接口来处理队列数据结构。它的主要操作包括入队 (`push`)、出队 (`pop`)、访问队首元素 (`front`)、访问队尾元素 (`back`)、检查队列是否为空 (`empty`)、和获取队列的大小 (`size`)。`std::queue` 可以使用不同的底层容器，如 `std::deque` 和 `std::list`，每种底层容器具有不同的性能特征。选择适当的底层容器可以影响队列的效率和行为。