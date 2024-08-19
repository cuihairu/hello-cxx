## `<unordered_set>` 数据结构

`<unordered_set>` 是 C++ 标准库中的一个关联容器，用于存储唯一的元素集合，基于哈希表实现。`std::unordered_set` 提供了高效的插入、删除和查找操作，元素的顺序不被保证，主要通过哈希函数来快速定位元素。

### 1. **类介绍**

`std::unordered_set` 是一个哈希表容器，具有以下主要特性：
- **唯一键**：集合中的每个元素是唯一的。
- **无序**：元素的顺序不被保证，取决于哈希函数。
- **高效操作**：插入、删除和查找操作的平均时间复杂度为 O(1)，但在最坏情况下可能为 O(n)。

### 2. **基本操作**

**创建和初始化：**

```cpp
#include <iostream>
#include <unordered_set>

int main() {
    // 创建一个空的 std::unordered_set
    std::unordered_set<int> s1;

    // 使用初始化列表创建 std::unordered_set
    std::unordered_set<int> s2 = {1, 2, 3, 4, 5};

    // 使用自定义哈希函数和比较函数创建 std::unordered_set
    auto custom_hash = [](const int& x) { return std::hash<int>{}(x) ^ 0x12345678; };
    auto custom_equal = [](const int& a, const int& b) { return a == b; };
    std::unordered_set<int, decltype(custom_hash), decltype(custom_equal)> s3(custom_hash, custom_equal);

    return 0;
}
```

**插入元素：**

```cpp
#include <iostream>
#include <unordered_set>

int main() {
    std::unordered_set<int> s;

    // 插入单个元素
    s.insert(1);

    // 插入多个元素
    s.insert({2, 3, 4, 5});

    // 尝试插入重复元素（不会插入）
    auto result = s.insert(3);
    if (!result.second) {
        std::cout << "Element 3 already exists" << std::endl;
    }

    // 输出 unordered_set 中的元素
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
#include <unordered_set>

int main() {
    std::unordered_set<int> s = {1, 2, 3, 4, 5};

    // 查找元素
    auto it = s.find(3);
    if (it != s.end()) {
        std::cout << "Element 3 found" << std::endl;
    } else {
        std::cout << "Element 3 not found" << std::endl;
    }

    // 使用 count() 检查元素是否存在
    if (s.count(4)) {
        std::cout << "Element 4 exists in the unordered_set" << std::endl;
    }

    return 0;
}
```

**访问和修改元素：**

```cpp
#include <iostream>
#include <unordered_set>

int main() {
    std::unordered_set<int> s = {1, 2, 3, 4, 5};

    // 不支持直接修改元素值，但可以删除并重新插入
    s.erase(2);
    s.insert(20);

    // 输出 unordered_set 中的元素
    for (const auto& elem : s) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

**删除元素：**

```cpp
#include <iostream>
#include <unordered_set>

int main() {
    std::unordered_set<int> s = {1, 2, 3, 4, 5};

    // 删除单个元素
    s.erase(3);

    // 删除所有元素
    s.clear();

    // 输出 unordered_set 中的元素
    for (const auto& elem : s) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

**大小和容量：**

```cpp
#include <iostream>
#include <unordered_set>

int main() {
    std::unordered_set<int> s = {1, 2, 3, 4, 5};

    // 获取 unordered_set 的大小
    std::cout << "Size of unordered_set: " << s.size() << std::endl;

    // 检查 unordered_set 是否为空
    std::cout << "Is unordered_set empty? " << (s.empty() ? "Yes" : "No") << std::endl;

    // 获取桶的数量
    std::cout << "Number of buckets: " << s.bucket_count() << std::endl;

    return 0;
}
```

**哈希函数和负载因子：**

```cpp
#include <iostream>
#include <unordered_set>

int main() {
    std::unordered_set<int> s = {1, 2, 3, 4, 5};

    // 获取负载因子
    std::cout << "Load factor: " << s.load_factor() << std::endl;

    // 获取最大负载因子
    std::cout << "Max load factor: " << s.max_load_factor() << std::endl;

    // 获取指定桶中的元素数量
    std::cout << "Bucket 0 size: " << s.bucket_size(0) << std::endl;

    // 自定义哈希函数
    std::cout << "Hash function: " << typeid(s.hash_function()).name() << std::endl;

    return 0;
}
```

### 3. **总结**

`std::unordered_set` 是一个基于哈希表的容器，适合用于需要高效查找、插入和删除操作的场景。与 `std::set` 不同，`std::unordered_set` 不保证元素的顺序，而是通过哈希函数将元素映射到桶中，从而提供常数时间复杂度的操作。哈希表的性能依赖于哈希函数的质量和负载因子，因此选择合适的哈希函数和管理负载因子对于保持良好的性能至关重要。