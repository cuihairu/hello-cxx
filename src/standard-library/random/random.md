## 随机数 `<random>`

C++11 引入了 `<random>` 头文件，提供了强大的随机数生成器和分布函数，改进了之前的 `rand()` 函数，并提供了更多控制随机数生成的能力。以下是对 `<random>` 的主要组件和用法的介绍。

### 1. **随机数引擎**

随机数引擎负责生成原始的伪随机数序列。C++ 标准库提供了多种引擎，以满足不同的需求。

#### **常用随机数引擎**

- **`std::default_random_engine`**: 默认随机数引擎，通常基于标准库的实现。
- **`std::mt19937`**: Mersenne Twister 引擎，具有较长的周期和较好的均匀性。
- **`std::ranlux48`**: 基于 Lux 库的引擎，提供更高质量的随机数。
- **`std::minstd_rand`**: 线性同余引擎，提供较简单的随机数生成。

#### **示例: 使用随机数引擎**

```cpp
#include <iostream>
#include <random>

int main() {
    std::random_device rd; // 获取硬件随机数种子
    std::mt19937 gen(rd()); // 初始化 Mersenne Twister 引擎

    // 生成一个范围在 [0, 99] 的随机整数
    std::uniform_int_distribution<> dis(0, 99);

    std::cout << "Random number: " << dis(gen) << std::endl;
    return 0;
}
```

### 2. **随机数分布**

随机数分布将生成的原始随机数映射到所需的范围或概率分布。C++ 标准库提供了多种常用的分布。

#### **常用随机数分布**

- **`std::uniform_int_distribution`**: 均匀整数分布，用于生成指定范围内的整数。
- **`std::uniform_real_distribution`**: 均匀实数分布，用于生成指定范围内的浮点数。
- **`std::normal_distribution`**: 正态分布，用于生成符合正态分布的数值。
- **`std::bernoulli_distribution`**: 伯努利分布，用于生成布尔值（成功或失败）。
- **`std::exponential_distribution`**: 指数分布，用于生成符合指数分布的数值。
- **`std::gamma_distribution`**: Gamma 分布，用于生成符合 Gamma 分布的数值。

#### **示例: 使用随机数分布**

```cpp
#include <iostream>
#include <random>

int main() {
    std::random_device rd;
    std::mt19937 gen(rd());

    // 生成均匀分布的浮点数
    std::uniform_real_distribution<> dis(0.0, 1.0);
    std::cout << "Uniform real number: " << dis(gen) << std::endl;

    // 生成正态分布的浮点数
    std::normal_distribution<> normal_dis(0.0, 1.0); // 均值为0，标准差为1
    std::cout << "Normal distributed number: " << normal_dis(gen) << std::endl;

    return 0;
}
```

### 3. **随机数种子**

随机数种子用于初始化随机数引擎，以控制生成的随机数序列。使用相同的种子可以生成相同的随机数序列，这对于调试和测试非常有用。

#### **示例: 设置随机数种子**

```cpp
#include <iostream>
#include <random>

int main() {
    std::mt19937 gen(42); // 使用固定种子初始化随机数引擎

    std::uniform_int_distribution<> dis(1, 10);
    std::cout << "Random number with fixed seed: " << dis(gen) << std::endl;

    return 0;
}
```

### 4. **随机数引擎与分布的组合**

通常，随机数引擎和分布一起使用。引擎负责生成随机数序列，而分布决定生成的数值的分布特性。

#### **示例: 引擎与分布组合**

```cpp
#include <iostream>
#include <random>

int main() {
    std::random_device rd;
    std::mt19937 gen(rd());

    std::uniform_real_distribution<> uniform_dis(1.0, 10.0);
    std::normal_distribution<> normal_dis(5.0, 2.0);

    std::cout << "Uniform real number: " << uniform_dis(gen) << std::endl;
    std::cout << "Normal distributed number: " << normal_dis(gen) << std::endl;

    return 0;
}
```

### 5. **总结**

C++ 的 `<random>` 头文件提供了一个灵活和强大的随机数生成框架。通过使用不同的随机数引擎和分布，程序员可以生成各种类型的随机数，满足不同的应用需求。`<random>` 的引入改善了随机数生成的质量和控制，适用于需要高质量随机数的应用场景，如模拟、测试和游戏开发等。