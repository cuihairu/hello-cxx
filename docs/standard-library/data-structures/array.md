## `<array>` 数据结构

`<array>` 是 C++ 标准库中的固定大小数组类模板。它提供了对 C++ 原生数组的封装，并提供了更多功能，如大小检查和 STL 容器接口。`std::array` 的大小在编译时确定，一旦创建，它的大小不可更改。

### 1. **类介绍**

`std::array` 是一个封装原生 C++ 数组的类模板，支持与标准容器类似的操作，但其大小在编译时确定。它提供了对原生数组操作的一些额外功能，如元素访问、范围检查和迭代器支持。

#### 1.1 基本操作

**创建和初始化：**

```cpp
#include <iostream>
#include <array>

int main() {
    // 创建一个包含 5 个 int 元素的 std::array
    std::array<int, 5> arr1 = {1, 2, 3, 4, 5};

    // 使用默认构造函数创建
    std::array<int, 3> arr2;

    // 使用初始化列表创建
    std::array<int, 3> arr3 = {10, 20, 30};

    return 0;
}
```

**访问元素：**

```cpp
#include <iostream>
#include <array>

int main() {
    std::array<int, 3> arr = {1, 2, 3};

    // 使用 operator[] 访问元素
    std::cout << "First element: " << arr[0] << std::endl;

    // 使用 at() 访问元素并检查越界
    std::cout << "Second element: " << arr.at(1) << std::endl;

    // 使用 front() 和 back() 访问首尾元素
    std::cout << "First element using front(): " << arr.front() << std::endl;
    std::cout << "Last element using back(): " << arr.back() << std::endl;

    return 0;
}
```

**修改元素：**

```cpp
#include <iostream>
#include <array>

int main() {
    std::array<int, 3> arr = {1, 2, 3};

    // 修改元素
    arr[0] = 10;
    arr.at(1) = 20;

    // 输出修改后的数组
    for (const auto& elem : arr) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

**迭代和遍历：**

```cpp
#include <iostream>
#include <array>

int main() {
    std::array<int, 4> arr = {1, 2, 3, 4};

    // 使用范围-based for 循环遍历
    for (const auto& elem : arr) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    // 使用迭代器遍历
    for (auto it = arr.begin(); it != arr.end(); ++it) {
        std::cout << *it << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

**大小和容量：**

```cpp
#include <iostream>
#include <array>

int main() {
    std::array<int, 4> arr = {10, 20, 30, 40};

    // 获取大小
    std::cout << "Size of array: " << arr.size() << std::endl;

    // 获取容量（对于 std::array，size() == capacity()）
    std::cout << "Capacity of array: " << arr.size() << std::endl;

    // 检查是否为空
    std::cout << "Is array empty? " << (arr.empty() ? "Yes" : "No") << std::endl;

    return 0;
}
```

**填充和交换：**

```cpp
#include <iostream>
#include <array>

int main() {
    std::array<int, 3> arr1 = {1, 2, 3};
    std::array<int, 3> arr2 = {4, 5, 6};

    // 填充数组
    arr1.fill(10);

    // 交换两个数组
    arr1.swap(arr2);

    // 输出填充和交换后的数组
    std::cout << "Array 1 after fill and swap: ";
    for (const auto& elem : arr1) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    std::cout << "Array 2 after fill and swap: ";
    for (const auto& elem : arr2) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

### 2. **高级操作**

**排序和反转：**

```cpp
#include <iostream>
#include <array>
#include <algorithm>

int main() {
    std::array<int, 5> arr = {5, 4, 3, 2, 1};

    // 排序数组
    std::sort(arr.begin(), arr.end());

    // 反转数组
    std::reverse(arr.begin(), arr.end());

    // 输出排序和反转后的数组
    for (const auto& elem : arr) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

**多维数组：**

```cpp
#include <iostream>
#include <array>

int main() {
    // 创建一个 2x3 的二维数组
    std::array<std::array<int, 3>, 2> arr = {{{1, 2, 3}, {4, 5, 6}}};

    // 输出二维数组
    for (const auto& row : arr) {
        for (const auto& elem : row) {
            std::cout << elem << " ";
        }
        std::cout << std::endl;
    }

    return 0;
}
```

### 3. **总结**

`<array>` 提供了对固定大小数组的封装，增加了对数组操作的一些功能，如范围检查、迭代器支持和 STL 容器接口。它适用于需要固定大小和在编译时已知大小的场景。通过使用 `std::array`，可以获得更安全和更强大的数组操作功能。