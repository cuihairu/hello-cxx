## `<vector>` 数据结构

`<vector>` 是 C++ 标准库中的一个动态数组类模板，提供了一个可以自动扩展大小的数组实现。`std::vector` 是 C++ 标准库中最常用的数据结构之一，广泛应用于需要动态调整大小的场景。

### 1. **类介绍**

`std::vector` 是一个封装了动态数组的类模板，提供了对元素的快速访问、动态扩展以及一系列便利的操作接口。它是一个序列容器，支持随机访问和快速的元素插入和删除操作。

#### 1.1 基本操作

**创建和初始化：**

```cpp
#include <vector>

int main() {
    // 创建一个空的 vector
    std::vector<int> vec1;

    // 创建一个指定大小并用默认值初始化的 vector
    std::vector<int> vec2(10); // 包含 10 个 int 元素，每个元素初始化为 0

    // 创建一个指定大小并用特定值初始化的 vector
    std::vector<int> vec3(5, 42); // 包含 5 个 int 元素，每个元素初始化为 42

    // 使用列表初始化
    std::vector<int> vec4 = {1, 2, 3, 4, 5}; // 使用列表初始化

    return 0;
}
```

**访问元素：**

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> vec = {10, 20, 30, 40, 50};

    // 使用下标访问
    std::cout << vec[2] << std::endl; // 输出 30

    // 使用 at() 方法访问（带边界检查）
    std::cout << vec.at(3) << std::endl; // 输出 40

    // 使用 front() 和 back() 方法访问
    std::cout << vec.front() << std::endl; // 输出 10
    std::cout << vec.back() << std::endl;  // 输出 50

    return 0;
}
```

**添加和删除元素：**

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> vec = {1, 2, 3};

    // 添加元素到末尾
    vec.push_back(4);
    vec.push_back(5);

    // 插入元素到指定位置
    vec.insert(vec.begin() + 2, 10); // 在索引 2 处插入 10

    // 删除指定位置的元素
    vec.erase(vec.begin() + 1); // 删除索引 1 处的元素

    // 删除末尾的元素
    vec.pop_back();

    // 清空所有元素
    vec.clear();

    return 0;
}
```

**容量和大小：**

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};

    // 获取当前大小和容量
    std::cout << "Size: " << vec.size() << std::endl;   // 输出 5
    std::cout << "Capacity: " << vec.capacity() << std::endl; // 输出当前容量

    // 重新分配容量
    vec.reserve(20); // 设置容量为 20
    std::cout << "New Capacity: " << vec.capacity() << std::endl; // 输出 20

    // 减少容量
    vec.shrink_to_fit(); // 收缩到当前元素数量

    return 0;
}
```

### 2. **高级操作**

**迭代器：**

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};

    // 使用迭代器遍历
    for (std::vector<int>::iterator it = vec.begin(); it != vec.end(); ++it) {
        std::cout << *it << " ";
    }
    std::cout << std::endl;

    // 使用范围-based for 循环
    for (const auto& value : vec) {
        std::cout << value << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

**排序和查找：**

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> vec = {5, 3, 8, 1, 2};

    // 排序
    std::sort(vec.begin(), vec.end());

    // 查找元素
    auto it = std::find(vec.begin(), vec.end(), 3);
    if (it != vec.end()) {
        std::cout << "Found: " << *it << std::endl;
    }

    return 0;
}
```

### 3. **总结**

`<vector>` 提供了一个动态大小的数组实现，具有自动扩展和快速访问的优点。它支持多种操作，包括元素的添加、删除、访问、排序和查找。通过掌握 `std::vector` 的基本操作和高级功能，可以有效地管理动态数据，满足各种编程需求。