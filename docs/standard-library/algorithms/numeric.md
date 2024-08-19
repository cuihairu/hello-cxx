## `<numeric>` 算法库

`<numeric>` 头文件提供了一组处理数值数据的算法。它们主要用于执行与数值计算相关的操作，如累积、计算最大公约数等。与 `<algorithm>` 头文件中的算法不同，`<numeric>` 更专注于数学运算，尤其是那些涉及数值处理的任务。

### 1. **常用算法**

#### 1.1 `std::accumulate`

**功能**：计算指定范围内所有元素的总和，或根据给定的二元操作计算累积结果。

**语法**：

```cpp
template< class InputIt, class T >
T accumulate( InputIt first, InputIt last, T init );
```

**示例**：

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

**示例（带二元操作）**：

```cpp
#include <numeric>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};
    int product = std::accumulate(vec.begin(), vec.end(), 1, std::multiplies<int>());

    std::cout << "Product: " << product << std::endl;

    return 0;
}
```

#### 1.2 `std::partial_sum`

**功能**：计算指定范围内的部分和，并将结果存储在另一个范围内。

**语法**：

```cpp
template< class InputIt, class OutputIt >
OutputIt partial_sum( InputIt first, InputIt last, OutputIt d_first );
```

**示例**：

```cpp
#include <numeric>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};
    std::vector<int> result(vec.size());

    std::partial_sum(vec.begin(), vec.end(), result.begin());

    for (const auto& num : result) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

#### 1.3 `std::adjacent_difference`

**功能**：计算指定范围内的相邻元素之间的差，并将结果存储在另一个范围内。

**语法**：

```cpp
template< class InputIt, class OutputIt >
OutputIt adjacent_difference( InputIt first, InputIt last, OutputIt d_first );
```

**示例**：

```cpp
#include <numeric>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> vec = {1, 3, 6, 10, 15};
    std::vector<int> result(vec.size());

    std::adjacent_difference(vec.begin(), vec.end(), result.begin());

    for (const auto& num : result) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

#### 1.4 `std::gcd` 和 `std::lcm`（C++17 起支持）

**功能**：计算两个数的最大公约数（GCD）和最小公倍数（LCM）。

**语法**：

```cpp
template< class T >
T gcd( T a, T b );

template< class T >
T lcm( T a, T b );
```

**示例**：

```cpp
#include <numeric>
#include <iostream>

int main() {
    int a = 60, b = 48;
    int gcd_val = std::gcd(a, b);
    int lcm_val = std::lcm(a, b);

    std::cout << "GCD: " << gcd_val << std::endl;
    std::cout << "LCM: " << lcm_val << std::endl;

    return 0;
}
```

### 2. **使用指南**

- **选择合适的算法**：根据需要选择适合的数值算法，如累积、部分和或相邻差等。
- **理解算法的时间复杂度**：了解算法的时间复杂度以优化程序性能。例如，`std::accumulate` 和 `std::partial_sum` 都是线性时间复杂度的算法。

### 3. **总结**

`<numeric>` 头文件中的算法为数值计算提供了强大的工具。通过利用这些算法，可以轻松完成各种数值处理任务，避免手动编写繁琐的循环和计算代码。这些算法能够显著提高代码的可读性和性能，特别是在处理大规模数据时。