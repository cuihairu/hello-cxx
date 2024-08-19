## `<complex>`

`<complex>` 是 C++ 标准库中的一个头文件，用于处理复数的数学运算。它提供了一个复数类模板 `std::complex`，允许在程序中进行复数的创建、操作和数学计算。复数在很多科学和工程应用中非常重要，比如信号处理、控制系统和图像处理等领域。

### 1. **复数的基本概念**

复数由两个部分组成：实部和虚部。它们通常表示为 `a + bi`，其中 `a` 是实部，`b` 是虚部，`i` 是虚数单位（`i` 的平方等于 -1）。

### 2. **`std::complex` 类模板**

`std::complex` 是一个模板类，定义在 `<complex>` 头文件中，用于表示复数。它的基本语法如下：

```cpp
template<class T>
class complex {
public:
    // 构造函数
    complex();                       // 默认构造函数
    complex(T re, T im = T());       // 带实部和虚部的构造函数
    complex(const complex& other);   // 拷贝构造函数

    // 成员函数
    T real() const;                  // 返回实部
    T imag() const;                  // 返回虚部
    void real(T re);                 // 设置实部
    void imag(T im);                 // 设置虚部

    // 运算符重载
    complex& operator+=(const complex& rhs);
    complex& operator-=(const complex& rhs);
    complex& operator*=(const complex& rhs);
    complex& operator/=(const complex& rhs);
    // 其他运算符重载
};
```

### 3. **基本操作**

#### **创建和初始化**

```cpp
#include <iostream>
#include <complex>

int main() {
    std::complex<double> c1(1.0, 2.0); // 实部为 1.0，虚部为 2.0
    std::complex<double> c2(3.0, 4.0); // 实部为 3.0，虚部为 4.0

    std::cout << "c1: " << c1 << std::endl;
    std::cout << "c2: " << c2 << std::endl;

    return 0;
}
```

#### **基本运算**

`std::complex` 支持基本的算术运算，包括加法、减法、乘法和除法。以下是一些基本运算的示例：

```cpp
#include <iostream>
#include <complex>

int main() {
    std::complex<double> c1(1.0, 2.0);
    std::complex<double> c2(3.0, 4.0);

    auto sum = c1 + c2;      // 加法
    auto diff = c1 - c2;     // 减法
    auto prod = c1 * c2;     // 乘法
    auto quot = c1 / c2;     // 除法

    std::cout << "sum: " << sum << std::endl;
    std::cout << "diff: " << diff << std::endl;
    std::cout << "prod: " << prod << std::endl;
    std::cout << "quot: " << quot << std::endl;

    return 0;
}
```

### 4. **数学函数**

`<complex>` 还提供了一些数学函数用于复数的运算。以下是一些常见的函数：

- **`std::abs`**: 计算复数的模（绝对值）。
- **`std::arg`**: 计算复数的幅角（相位）。
- **`std::conj`**: 计算复数的共轭。
- **`std::norm`**: 计算复数的平方模。

#### **示例**

```cpp
#include <iostream>
#include <complex>
#include <cmath>

int main() {
    std::complex<double> c(3.0, 4.0);

    std::cout << "abs(c): " << std::abs(c) << std::endl;       // 模
    std::cout << "arg(c): " << std::arg(c) << std::endl;       // 幅角
    std::cout << "conj(c): " << std::conj(c) << std::endl;     // 共轭
    std::cout << "norm(c): " << std::norm(c) << std::endl;     // 平方模

    return 0;
}
```

### 5. **复数的 I/O 操作**

复数的输入输出操作需要使用流操作符 `<<` 和 `>>`。可以通过重载这些操作符来实现复数的格式化输入输出。

```cpp
#include <iostream>
#include <complex>

std::ostream& operator<<(std::ostream& os, const std::complex<double>& c) {
    return os << c.real() << " + " << c.imag() << "i";
}

std::istream& operator>>(std::istream& is, std::complex<double>& c) {
    double re, im;
    is >> re >> im;
    c = std::complex<double>(re, im);
    return is;
}

int main() {
    std::complex<double> c1;
    std::cout << "Enter a complex number (real and imaginary part): ";
    std::cin >> c1;

    std::cout << "You entered: " << c1 << std::endl;

    return 0;
}
```

### 6. **总结**

`<complex>` 头文件提供了对复数数学运算的支持，使得在 C++ 中处理复数变得非常方便。通过 `std::complex` 类模板，可以进行复数的基本操作和高级数学计算。掌握这些功能，可以在科学计算、信号处理等领域中发挥重要作用。