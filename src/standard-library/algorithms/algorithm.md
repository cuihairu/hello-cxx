## `<algorithm>` 算法库

C++ 标准库中的 `<algorithm>` 头文件提供了一组强大且通用的算法，能够对容器中的数据进行操作。这些算法包括排序、搜索、变换等操作，广泛用于各种数据处理任务。`<algorithm>` 中的算法设计遵循泛型编程思想，与容器解耦，允许在各种容器类型上使用这些算法。

### 1. **常用算法**

#### 1.1 排序算法

**`std::sort`**  
对指定范围内的元素进行排序，默认为升序。

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> vec = {5, 2, 9, 1, 5, 6};
    std::sort(vec.begin(), vec.end());

    for (const auto& num : vec) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

**`std::stable_sort`**  
对指定范围内的元素进行排序，保持相等元素的相对顺序。

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<std::pair<int, std::string>> vec = {{1, "one"}, {2, "two"}, {1, "uno"}};
    std::stable_sort(vec.begin(), vec.end(), [](const auto& a, const auto& b) {
        return a.first < b.first;
    });

    for (const auto& pair : vec) {
        std::cout << pair.first << ": " << pair.second << std::endl;
    }

    return 0;
}
```

#### 1.2 搜索算法

**`std::find`**  
在指定范围内查找第一个匹配的元素。

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};
    auto it = std::find(vec.begin(), vec.end(), 3);

    if (it != vec.end()) {
        std::cout << "Found: " << *it << std::endl;
    } else {
        std::cout << "Not found" << std::endl;
    }

    return 0;
}
```

**`std::binary_search`**  
检查指定值是否存在于已排序的范围内。

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};
    bool found = std::binary_search(vec.begin(), vec.end(), 3);

    std::cout << (found ? "Found" : "Not found") << std::endl;

    return 0;
}
```

#### 1.3 变换算法

**`std::transform`**  
对指定范围内的每个元素应用指定的函数，并将结果存储在另一个范围内。

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};
    std::vector<int> result(vec.size());

    std::transform(vec.begin(), vec.end(), result.begin(), [](int x) {
        return x * x;
    });

    for (const auto& num : result) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

**`std::for_each`**  
对指定范围内的每个元素应用指定的函数。

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};

    std::for_each(vec.begin(), vec.end(), [](int x) {
        std::cout << x << " ";
    });
    std::cout << std::endl;

    return 0;
}
```

#### 1.4 其他算法

**`std::accumulate`**  
计算范围内所有元素的总和（或应用指定的二元操作）。

```cpp
#include <numeric>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};
    int sum = std::accumulate(vec.begin(), vec.end(), 0);

    std::cout << "Sum: " << sum << std::endl;

    return 0;
}
```

**`std::count`**  
计算指定值在范围内出现的次数。

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 2, 2, 5};
    int count = std::count(vec.begin(), vec.end(), 2);

    std::cout << "Count of 2: " << count << std::endl;

    return 0;
}
```

### 2. **使用指南**

- **选择合适的算法**：根据数据处理的需求选择合适的算法，如排序、查找或变换。
- **避免重复计算**：利用 STL 算法避免手动编写复杂的循环和条件判断，提高代码的可读性和性能。
- **理解算法的时间复杂度**：选择适当的算法时，了解其时间复杂度，以优化程序性能。

### 3. **总结**

`<algorithm>` 头文件中的算法提供了对容器元素的高效操作。通过泛型编程，这些算法能够与多种容器类型配合使用，从而实现强大的数据处理能力。熟练掌握这些算法对于编写高效、可维护的 C++ 代码至关重要。