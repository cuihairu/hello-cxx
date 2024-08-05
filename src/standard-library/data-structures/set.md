## `<set>` 数据结构

`<set>` 是 C++ 标准库中的一个关联容器，用于存储唯一的元素集合，并自动按照特定的排序准则进行排序。`std::set` 是一个基于红黑树（或其他平衡二叉搜索树）的集合类模板，确保集合中的元素是唯一的，并提供高效的元素查找、插入和删除操作。

### 1. **类介绍**

`std::set` 是一个关联容器，具有以下主要特性：
- **唯一性**：集合中的每个元素都是唯一的。
- **排序**：集合中的元素按照升序排列（或按照自定义的排序准则）。
- **自动平衡**：元素插入和删除操作保持集合的平衡，确保高效的查找操作。
- **高效操作**：插入、删除和查找操作的时间复杂度为 O(log n)。

### 2. **基本操作**

**创建和初始化：**

```cpp
#include <iostream>
#include <set>

int main() {
    // 创建一个空的 std::set
    std::set<int> s1;

    // 使用初始化列表创建 std::set
    std::set<int> s2 = {1, 2, 3, 4, 5};

    // 使用自定义排序准则创建 std::set
    std::set<int, std::greater<int>> s3 = {5, 4, 3, 2, 1};

    return 0;
}
```

**插入元素：**

```cpp
#include <iostream>
#include <set>

int main() {
    std::set<int> s = {1, 2, 3};

    // 插入单个元素
    s.insert(4);

    // 插入多个元素
    s.insert({5, 6, 7});

    // 尝试插入重复元素（不会插入）
    auto result = s.insert(4);
    if (!result.second) {
        std::cout << "Element 4 already exists" << std::endl;
    }

    // 输出集合中的元素
    for (const auto& elem : s) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

**查找元素：**

```cpp
#include <iostream>
#include <set>

int main() {
    std::set<int> s = {1, 2, 3, 4, 5};

    // 查找元素
    auto it = s.find(3);
    if (it != s.end()) {
        std::cout << "Element found: " << *it << std::endl;
    } else {
        std::cout << "Element not found" << std::endl;
    }

    // 使用 count() 检查元素是否存在
    if (s.count(5)) {
        std::cout << "Element 5 exists in the set" << std::endl;
    }

    return 0;
}
```

**删除元素：**

```cpp
#include <iostream>
#include <set>

int main() {
    std::set<int> s = {1, 2, 3, 4, 5};

    // 删除单个元素
    s.erase(3);

    // 删除范围内的元素
    s.erase(s.find(4), s.end());

    // 输出集合中的元素
    for (const auto& elem : s) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

**访问元素：**

```cpp
#include <iostream>
#include <set>

int main() {
    std::set<int> s = {1, 2, 3, 4, 5};

    // 使用范围-based for 循环访问元素
    for (const auto& elem : s) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    // 使用迭代器访问元素
    for (auto it = s.begin(); it != s.end(); ++it) {
        std::cout << *it << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

**大小和容量：**

```cpp
#include <iostream>
#include <set>

int main() {
    std::set<int> s = {1, 2, 3, 4, 5};

    // 获取集合大小
    std::cout << "Size of set: " << s.size() << std::endl;

    // 检查集合是否为空
    std::cout << "Is set empty? " << (s.empty() ? "Yes" : "No") << std::endl;

    return 0;
}
```

**排序和范围操作：**

```cpp
#include <iostream>
#include <set>

int main() {
    std::set<int> s = {1, 2, 3, 4, 5};

    // 输出集合中的元素（已排序）
    std::cout << "Set elements: ";
    for (const auto& elem : s) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    // 查找范围内的元素
    auto it1 = s.lower_bound(2);
    auto it2 = s.upper_bound(4);

    std::cout << "Elements in range [2, 4): ";
    for (auto it = it1; it != it2; ++it) {
        std::cout << *it << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

### 3. **总结**

`std::set` 提供了一种高效的方式来存储和管理唯一的元素集合，并自动按照特定的排序准则进行排序。它支持高效的查找、插入和删除操作，适用于需要确保元素唯一性和排序的场景。通过使用 `std::set`，可以实现集合操作的灵活性和高效性。