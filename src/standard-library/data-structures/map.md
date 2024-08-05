## `<map>` 数据结构

`<map>` 是 C++ 标准库中的一个关联容器，用于存储键值对（key-value pairs）。`std::map` 是一个基于红黑树（或其他平衡二叉搜索树）的容器，确保每个键是唯一的，并自动按照键的顺序进行排序。`std::map` 提供了高效的元素查找、插入和删除操作，键值对中的键是唯一的，值则可以重复。

### 1. **类介绍**

`std::map` 是一个关联容器，具有以下主要特性：
- **唯一键**：每个键在集合中是唯一的。
- **排序**：键按照升序（或按照自定义的排序准则）排列。
- **自动平衡**：插入和删除操作会保持集合的平衡，确保高效的查找操作。
- **高效操作**：插入、删除和查找操作的时间复杂度为 O(log n)。

### 2. **基本操作**

**创建和初始化：**

```cpp
#include <iostream>
#include <map>

int main() {
    // 创建一个空的 std::map
    std::map<int, std::string> m1;

    // 使用初始化列表创建 std::map
    std::map<int, std::string> m2 = {{1, "one"}, {2, "two"}, {3, "three"}};

    // 使用自定义排序准则创建 std::map
    std::map<int, std::string, std::greater<int>> m3 = {{1, "one"}, {2, "two"}, {3, "three"}};

    return 0;
}
```

**插入元素：**

```cpp
#include <iostream>
#include <map>

int main() {
    std::map<int, std::string> m;

    // 插入单个键值对
    m.insert({1, "one"});

    // 插入多个键值对
    m.insert({2, "two"});
    m.insert({3, "three"});

    // 尝试插入重复键（不会插入）
    auto result = m.insert({1, "uno"});
    if (!result.second) {
        std::cout << "Key 1 already exists" << std::endl;
    }

    // 输出 map 中的元素
    for (const auto& [key, value] : m) {
        std::cout << key << ": " << value << std::endl;
    }

    return 0;
}
```

**查找元素：**

```cpp
#include <iostream>
#include <map>

int main() {
    std::map<int, std::string> m = {{1, "one"}, {2, "two"}, {3, "three"}};

    // 查找元素
    auto it = m.find(2);
    if (it != m.end()) {
        std::cout << "Key 2 maps to value: " << it->second << std::endl;
    } else {
        std::cout << "Key 2 not found" << std::endl;
    }

    // 使用 count() 检查键是否存在
    if (m.count(3)) {
        std::cout << "Key 3 exists in the map" << std::endl;
    }

    return 0;
}
```

**访问和修改元素：**

```cpp
#include <iostream>
#include <map>

int main() {
    std::map<int, std::string> m = {{1, "one"}, {2, "two"}, {3, "three"}};

    // 访问元素
    std::cout << "Value associated with key 2: " << m[2] << std::endl;

    // 修改元素
    m[2] = "deux";
    std::cout << "Updated value associated with key 2: " << m[2] << std::endl;

    return 0;
}
```

**删除元素：**

```cpp
#include <iostream>
#include <map>

int main() {
    std::map<int, std::string> m = {{1, "one"}, {2, "two"}, {3, "three"}};

    // 删除单个元素
    m.erase(2);

    // 删除范围内的元素
    m.erase(m.find(1), m.end());

    // 输出 map 中的元素
    for (const auto& [key, value] : m) {
        std::cout << key << ": " << value << std::endl;
    }

    return 0;
}
```

**大小和容量：**

```cpp
#include <iostream>
#include <map>

int main() {
    std::map<int, std::string> m = {{1, "one"}, {2, "two"}, {3, "three"}};

    // 获取 map 的大小
    std::cout << "Size of map: " << m.size() << std::endl;

    // 检查 map 是否为空
    std::cout << "Is map empty? " << (m.empty() ? "Yes" : "No") << std::endl;

    return 0;
}
```

**排序和范围操作：**

```cpp
#include <iostream>
#include <map>

int main() {
    std::map<int, std::string> m = {{1, "one"}, {2, "two"}, {3, "three"}};

    // 输出 map 中的元素（按键排序）
    std::cout << "Map elements: ";
    for (const auto& [key, value] : m) {
        std::cout << key << ": " << value << " ";
    }
    std::cout << std::endl;

    // 查找范围内的元素
    auto it1 = m.lower_bound(1);
    auto it2 = m.upper_bound(2);

    std::cout << "Elements in range [1, 2]: ";
    for (auto it = it1; it != it2; ++it) {
        std::cout << it->first << ": " << it->second << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

### 3. **总结**

`std::map` 提供了一种高效的方式来存储和管理键值对，并确保键的唯一性及排序。它支持高效的查找、插入和删除操作，非常适合需要按键值对进行快速查找和有序存储的场景。`std::map` 的实现基于平衡二叉搜索树，因此其操作的时间复杂度为 O(log n)，使其在许多应用场景中具有优良的性能。