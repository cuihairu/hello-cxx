## `<cmath>`

`<cmath>` 是 C++ 标准库中提供的一组数学函数的头文件，它为各种数学计算提供了基本的功能。该头文件包括了多种数学函数和常量，可以用于浮点数的数学运算。`<cmath>` 是 C++ 中 `<math.h>` 的标准化版本，并提供了对 C 标准库 `<math.h>` 函数的兼容性。

### 1. **常量**

- **`M_PI`**: 圆周率常量，表示圆周率π的值。
- **`M_E`**: 自然对数的底数常量，表示 e 的值。
- **`M_LOG2E`**: 2 为底的对数 e 的值。
- **`M_LOG10E`**: 10 为底的对数 e 的值。
- **`M_LN2`**: 自然对数 2 的值。
- **`M_LN10`**: 自然对数 10 的值。

**注意**: 这些常量的定义可能会依赖于实现和编译器，实际使用中应查阅具体的标准库文档。

### 2. **基本数学函数**

#### **1. 三角函数**

- **`std::sin(double x)`**: 计算角度 x 的正弦值。
- **`std::cos(double x)`**: 计算角度 x 的余弦值。
- **`std::tan(double x)`**: 计算角度 x 的正切值。
- **`std::asin(double x)`**: 计算 x 的反正弦值，结果范围在 [-π/2, π/2]。
- **`std::acos(double x)`**: 计算 x 的反余弦值，结果范围在 [0, π]。
- **`std::atan(double x)`**: 计算 x 的反正切值，结果范围在 [-π/2, π/2]。
- **`std::atan2(double y, double x)`**: 计算 (x, y) 坐标点的反正切值，结果范围在 [-π, π]。

#### **2. 指数和对数函数**

- **`std::exp(double x)`**: 计算 e 的 x 次方。
- **`std::log(double x)`**: 计算 x 的自然对数（以 e 为底）。
- **`std::log10(double x)`**: 计算 x 的以 10 为底的对数。
- **`std::pow(double base, double exponent)`**: 计算 base 的 exponent 次方。
- **`std::sqrt(double x)`**: 计算 x 的平方根。

#### **3. 绝对值和舍入函数**

- **`std::abs(int x)`**: 计算整数 x 的绝对值。
- **`std::fabs(double x)`**: 计算浮点数 x 的绝对值。
- **`std::ceil(double x)`**: 计算不小于 x 的最小整数（向上取整）。
- **`std::floor(double x)`**: 计算不大于 x 的最大整数（向下取整）。
- **`std::round(double x)`**: 计算最接近 x 的整数（四舍五入）。
- **`std::trunc(double x)`**: 计算去掉小数部分后的整数部分。

#### **4. 其他数学函数**

- **`std::fmod(double x, double y)`**: 计算 x 除以 y 的余数。
- **`std::hypot(double x, double y)`**: 计算直角三角形的斜边长度，等于 `sqrt(x*x + y*y)`。
- **`std::modf(double x, double* intpart)`**: 将 x 分解为整数部分和小数部分。

### 3. **使用示例**

以下是使用 `<cmath>` 中一些常见函数的示例：

```cpp
#include <iostream>
#include <cmath>

int main() {
    double angle = 0.5; // 弧度

    std::cout << "sin(" << angle << ") = " << std::sin(angle) << std::endl;
    std::cout << "cos(" << angle << ") = " << std::cos(angle) << std::endl;
    std::cout << "tan(" << angle << ") = " << std::tan(angle) << std::endl;

    double x = 2.0;
    double y = 3.0;
    std::cout << "pow(" << x << ", " << y << ") = " << std::pow(x, y) << std::endl;
    std::cout << "sqrt(" << x << ") = " << std::sqrt(x) << std::endl;

    double value = -3.5;
    std::cout << "fabs(" << value << ") = " << std::fabs(value) << std::endl;
    std::cout << "ceil(" << value << ") = " << std::ceil(value) << std::endl;
    std::cout << "floor(" << value << ") = " << std::floor(value) << std::endl;
    std::cout << "round(" << value << ") = " << std::round(value) << std::endl;

    return 0;
}
```

### 4. **总结**

`<cmath>` 头文件提供了广泛的数学函数和常量，允许在 C++ 程序中进行各种数学计算。通过使用这些函数，你可以进行基本的数学运算、三角函数计算、指数和对数运算等。这些函数的设计旨在提供高效且可靠的数学运算能力，同时保证与 C 语言库的兼容性。