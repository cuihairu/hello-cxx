## `std::priority_queue` 数据结构

`std::priority_queue` 是 C++ 标准库中的一个容器适配器，用于实现优先队列（priority queue）。优先队列是一种数据结构，其中的元素按照优先级排序，具有最高优先级的元素会被最先访问。`std::priority_queue` 默认使用最大堆（max-heap）作为底层容器，确保最大元素位于队列的顶部。

### 1. **类介绍**

`std::priority_queue` 的主要特点包括：
- **优先级排序**：元素按照优先级排序，默认情况下，具有最大值的元素优先级最高。
- **底层容器**：通常使用 `std::vector` 作为底层容器，但可以指定其他底层容器。
- **提供高效的访问**：允许在对数时间内插入和删除元素。

### 2. **基本操作**

**创建和初始化：**

```cpp
#include <iostream>
#include <queue>
#include <vector>

int main() {
    // 默认底层容器是 std::vector
    std::priority_queue<int> pq;

    // 使用自定义比较函数
    auto cmp = [](int left, int right) { return left > right; }; // 最小堆
    std::priority_queue<int, std::vector<int>, decltype(cmp)> pq_custom(cmp);

    return 0;
}
```

**优先队列操作：**

```cpp
#include <iostream>
#include <queue>

int main() {
    std::priority_queue<int> pq;

    // 插入元素
    pq.push(10);
    pq.push(20);
    pq.push(30);

    // 输出优先队列的最大元素
    std::cout << "Top element: " << pq.top() << std::endl;

    // 删除最大元素
    pq.pop();

    // 输出新的最大元素
    std::cout << "Top element after pop: " << pq.top() << std::endl;

    // 检查优先队列是否为空
    std::cout << "Is priority queue empty? " << (pq.empty() ? "Yes" : "No") << std::endl;

    // 获取优先队列的大小
    std::cout << "Priority queue size: " << pq.size() << std::endl;

    return 0;
}
```

### 3. **成员函数**

**`push(const value_type& value)`**  
将元素添加到优先队列中，保持优先队列的优先级顺序。

**`pop()`**  
移除优先队列中优先级最高的元素。

**`top()`**  
返回优先队列中优先级最高的元素，但不移除它。

**`empty()`**  
检查优先队列是否为空。返回 `true` 如果队列为空，`false` 如果队列不为空。

**`size()`**  
返回优先队列中元素的数量。

### 4. **自定义比较函数**

`std::priority_queue` 默认使用最大堆（max-heap），即最大元素在顶部。如果需要自定义优先级（如最小堆），可以提供一个比较函数：

```cpp
#include <iostream>
#include <queue>
#include <vector>

int main() {
    // 自定义比较函数（最小堆）
    auto cmp = [](int left, int right) { return left > right; };
    std::priority_queue<int, std::vector<int>, decltype(cmp)> pq_custom(cmp);

    // 插入元素
    pq_custom.push(10);
    pq_custom.push(20);
    pq_custom.push(30);

    // 输出优先队列的最小元素
    std::cout << "Top element (min-heap): " << pq_custom.top() << std::endl;

    return 0;
}
```

### 5. **底层容器**

`std::priority_queue` 默认使用 `std::vector` 作为底层容器，底层容器负责存储元素并提供支持堆操作的接口。可以使用其他容器，如 `std::deque`，但通常 `std::vector` 是最常用的选择，因为它提供了较好的内存布局和访问性能。

### 6. **总结**

`std::priority_queue` 是一个提供优先级排序的容器适配器，确保具有最高优先级的元素在顶部。它支持基本的优先级队列操作，如插入、删除和访问顶部元素。通过自定义比较函数，可以实现不同的优先级策略，如最小堆。`std::priority_queue` 默认使用 `std::vector` 作为底层容器，但可以根据需要选择其他容器。