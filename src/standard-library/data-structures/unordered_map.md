## `<unordered_map>` 数据结构

`<unordered_map>` 是 C++ 标准库中的一个关联容器，用于存储键值对。它基于哈希表实现，提供了高效的键值对存取操作。`std::unordered_map` 不保证元素的顺序，而是通过哈希函数来快速定位键值对。

### 1. **类介绍**

`std::unordered_map` 是一个哈希表容器，具有以下主要特性：
- **键值对存储**：每个元素是一个键值对 (`std::pair<Key, Value>`)，其中 `Key` 是唯一的。
- **无序**：元素的顺序不被保证，取决于哈希函数。
- **高效操作**：插入、删除和查找操作的平均时间复杂度为 O(1)，但在最坏情况下可能为 O(n)。

### 2. **基本操作**

**创建和初始化：**

```cpp
#include <iostream>
#include <unordered_map>

int main() {
    // 创建一个空的 std::unordered_map
    std::unordered_map<int, std::string> um1;

    // 使用初始化列表创建 std::unordered_map
    std::unordered_map<int, std::string> um2 = {
        {1, "one"}, {2, "two"}, {3, "three"}
    };

    // 使用自定义哈希函数和比较函数创建 std::unordered_map
    auto custom_hash = [](const int& key) { return std::hash<int>{}(key) ^ 0x12345678; };
    auto custom_equal = [](const int& a, const int& b) { return a == b; };
    std::unordered_map<int, std::string, decltype(custom_hash), decltype(custom_equal)> um3(custom_hash, custom_equal);

    return 0;
}
```

**插入元素：**

```cpp
#include <iostream>
#include <unordered_map>

int main() {
    std::unordered_map<int, std::string> um;

    // 插入单个元素
    um[1] = "one";

    // 插入多个元素
    um.insert({{2, "two"}, {3, "three"}});

    // 插入或更新元素
    um[4] = "four";  // 插入新元素
    um[4] = "four updated";  // 更新已有元素

    // 输出 unordered_map 中的元素
    for (const auto& pair : um) {
        std::cout << pair.first << ": " << pair.second << std::endl;
    }

    return 0;
}
```

**查找元素：**

```cpp
#include <iostream>
#include <unordered_map>

int main() {
    std::unordered_map<int, std::string> um = {
        {1, "one"}, {2, "two"}, {3, "three"}
    };

    // 查找元素
    auto it = um.find(2);
    if (it != um.end()) {
        std::cout << "Key 2 found with value: " << it->second << std::endl;
    } else {
        std::cout << "Key 2 not found" << std::endl;
    }

    // 使用 at() 访问元素
    try {
        std::cout << "Value for key 3: " << um.at(3) << std::endl;
    } catch (const std::out_of_range& e) {
        std::cout << "Key 3 not found" << std::endl;
    }

    return 0;
}
```

**访问和修改元素：**

```cpp
#include <iostream>
#include <unordered_map>

int main() {
    std::unordered_map<int, std::string> um = {
        {1, "one"}, {2, "two"}, {3, "three"}
    };

    // 修改元素
    um[2] = "two updated";

    // 访问元素
    for (const auto& pair : um) {
        std::cout << pair.first << ": " << pair.second << std::endl;
    }

    return 0;
}
```

**删除元素：**

```cpp
#include <iostream>
#include <unordered_map>

int main() {
    std::unordered_map<int, std::string> um = {
        {1, "one"}, {2, "two"}, {3, "three"}
    };

    // 删除单个元素
    um.erase(2);

    // 删除所有元素
    um.clear();

    // 输出 unordered_map 中的元素
    for (const auto& pair : um) {
        std::cout << pair.first << ": " << pair.second << std::endl;
    }

    return 0;
}
```

**大小和容量：**

```cpp
#include <iostream>
#include <unordered_map>

int main() {
    std::unordered_map<int, std::string> um = {
        {1, "one"}, {2, "two"}, {3, "three"}
    };

    // 获取 unordered_map 的大小
    std::cout << "Size of unordered_map: " << um.size() << std::endl;

    // 检查 unordered_map 是否为空
    std::cout << "Is unordered_map empty? " << (um.empty() ? "Yes" : "No") << std::endl;

    // 获取桶的数量
    std::cout << "Number of buckets: " << um.bucket_count() << std::endl;

    return 0;
}
```

**哈希函数和负载因子：**

```cpp
#include <iostream>
#include <unordered_map>

int main() {
    std::unordered_map<int, std::string> um = {
        {1, "one"}, {2, "two"}, {3, "three"}
    };

    // 获取负载因子
    std::cout << "Load factor: " << um.load_factor() << std::endl;

    // 获取最大负载因子
    std::cout << "Max load factor: " << um.max_load_factor() << std::endl;

    // 获取指定桶中的元素数量
    std::cout << "Bucket 0 size: " << um.bucket_size(0) << std::endl;

    // 自定义哈希函数
    std::cout << "Hash function: " << typeid(um.hash_function()).name() << std::endl;

    return 0;
}
```

### 3. **总结**

`std::unordered_map` 是一个基于哈希表的关联容器，适合用于需要高效查找、插入和删除操作的场景。它通过哈希函数将键值对映射到桶中，从而提供常数时间复杂度的操作。与 `std::map` 不同，`std::unordered_map` 不保证元素的顺序，而是通过哈希表实现高效的键值对存取。选择合适的哈希函数和管理负载因子对于保持容器的性能至关重要。