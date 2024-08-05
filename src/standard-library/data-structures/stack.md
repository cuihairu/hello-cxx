## `std::stack` 数据结构

`std::stack` 是 C++ 标准库中的一个容器适配器，用于实现栈（stack）数据结构。栈是一种遵循“后进先出”（LIFO，Last In, First Out）原则的数据结构，即最后插入的元素最先被访问。`std::stack` 是基于其他容器（如 `std::deque` 或 `std::vector`）实现的，默认使用 `std::deque` 作为底层容器。

### 1. **类介绍**

`std::stack` 的主要特点包括：
- **LIFO 结构**：栈的特性保证了元素的访问顺序。
- **封装底层容器**：栈适配器封装了底层容器，提供了一组用于栈操作的方法。
- **底层容器可定制**：可以使用不同的底层容器（如 `std::deque`、`std::vector`）来实现 `std::stack`。

### 2. **基本操作**

**创建和初始化：**

```cpp
#include <iostream>
#include <stack>
#include <deque>
#include <vector>

int main() {
    // 使用默认底层容器 std::deque
    std::stack<int> stack1;

    // 使用 std::vector 作为底层容器
    std::stack<int, std::vector<int>> stack2;

    // 使用 std::deque 作为底层容器
    std::stack<int, std::deque<int>> stack3;

    return 0;
}
```

**栈操作：**

```cpp
#include <iostream>
#include <stack>

int main() {
    std::stack<int> stack;

    // 入栈
    stack.push(10);
    stack.push(20);
    stack.push(30);

    // 输出栈顶元素
    std::cout << "Top element: " << stack.top() << std::endl;

    // 出栈
    stack.pop();

    // 输出栈顶元素
    std::cout << "Top element after pop: " << stack.top() << std::endl;

    // 检查栈是否为空
    std::cout << "Is stack empty? " << (stack.empty() ? "Yes" : "No") << std::endl;

    // 获取栈的大小
    std::cout << "Stack size: " << stack.size() << std::endl;

    return 0;
}
```

### 3. **成员函数**

**`push(const value_type& value)`**  
将元素添加到栈的顶部。

**`pop()`**  
移除栈顶的元素。

**`top()`**  
返回栈顶的元素，但不移除它。

**`empty()`**  
检查栈是否为空。返回 `true` 如果栈为空，`false` 如果栈不为空。

**`size()`**  
返回栈中元素的数量。

### 4. **底层容器**

`std::stack` 可以使用不同的底层容器，最常见的是 `std::deque` 和 `std::vector`。底层容器影响栈的性能和行为。以下是如何自定义底层容器的示例：

```cpp
#include <iostream>
#include <stack>
#include <vector>
#include <deque>

int main() {
    // 使用 std::vector 作为底层容器
    std::stack<int, std::vector<int>> stack1;
    stack1.push(1);
    stack1.push(2);
    std::cout << "Stack with std::vector as underlying container:" << std::endl;
    while (!stack1.empty()) {
        std::cout << stack1.top() << std::endl;
        stack1.pop();
    }

    // 使用 std::deque 作为底层容器
    std::stack<int, std::deque<int>> stack2;
    stack2.push(3);
    stack2.push(4);
    std::cout << "Stack with std::deque as underlying container:" << std::endl;
    while (!stack2.empty()) {
        std::cout << stack2.top() << std::endl;
        stack2.pop();
    }

    return 0;
}
```

### 5. **总结**

`std::stack` 是一个栈容器适配器，提供了简单的接口来处理栈数据结构。它的主要操作包括入栈 (`push`)、出栈 (`pop`)、访问栈顶元素 (`top`)、检查栈是否为空 (`empty`)、和获取栈的大小 (`size`)。`std::stack` 可以使用不同的底层容器，如 `std::deque` 和 `std::vector`，每种底层容器具有不同的性能特征。选择适当的底层容器可以影响栈的效率和行为。