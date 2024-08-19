## 数据类型与变量

在 C++ 中，数据类型和变量是构建程序的基础。理解 C++ 提供的各种数据类型及其特性，有助于编写高效且可靠的代码。本节将介绍 C++ 中的基本数据类型、变量声明及其初始化、常量以及枚举类型。

### 1. **基本数据类型**

C++ 提供了多种基本数据类型，用于表示不同类型的值。以下是常用的基本数据类型及其特点：

#### 1.1 **整型（Integer Types）**

- **`int`**：标准整型，通常用来表示整数值。大小依赖于编译器和平台，通常为 4 字节。
- **`short`**：短整型，通常为 2 字节。
- **`long`**：长整型，通常为 4 或 8 字节。
- **`long long`**：超长整型，至少为 8 字节。

```cpp
int age = 25;
short height = 180;
long population = 7000000000;
long long distance = 9876543210;
```

#### 1.2 **浮点型（Floating-Point Types）**

- **`float`**：单精度浮点型，通常占 4 字节，用于表示小数。
- **`double`**：双精度浮点型，通常占 8 字节，用于表示更精确的小数。
- **`long double`**：扩展精度浮点型，大小依赖于平台，提供更高的精度。

```cpp
float temperature = 36.6f;
double pi = 3.14159265358979;
long double e = 2.718281828459045;
```

#### 1.3 **字符型（Character Types）**

- **`char`**：字符型，通常为 1 字节，表示单个字符。
- **`wchar_t`**：宽字符型，用于表示 Unicode 字符，大小依赖于平台。

```cpp
char grade = 'A';
wchar_t symbol = L'Ω';
```

### 2. **变量声明与初始化**

在 C++ 中，变量用于存储数据。变量声明时需要指定数据类型，并可以在声明时进行初始化。

#### 2.1 **变量声明**

```cpp
int number;
float salary;
char initial;
```

#### 2.2 **变量初始化**

在声明的同时给变量赋初值。

```cpp
int number = 10;
float salary = 5000.50;
char initial = 'A';
```

#### 2.3 **自动推导**

使用 `auto` 关键字自动推导变量类型。

```cpp
auto age = 30; // 自动推导为 int
auto price = 19.99; // 自动推导为 double
```

### 3. **常量（Constants）**

常量用于定义在程序执行过程中不会改变的值。

#### 3.1 **`const` 常量**

使用 `const` 关键字定义常量，其值在初始化后不可更改。

```cpp
const int MAX_USERS = 100;
const double PI = 3.14159;
```

#### 3.2 **`constexpr` 常量**

`constexpr` 常量在编译时进行计算，用于更严格的编译期常量。

```cpp
constexpr int SQUARE(int x) { return x * x; }
constexpr int AREA = SQUARE(5);
```

### 4. **枚举类型（Enumerations）**

枚举类型用于定义一组命名的整型常量。

#### 4.1 **枚举声明**

```cpp
enum Color {
    RED,
    GREEN,
    BLUE
};
```

#### 4.2 **枚举类（Scoped Enumerations）**

C++11 引入了枚举类，它提供了更强的类型安全和作用域控制。

```cpp
enum class Direction {
    NORTH,
    EAST,
    SOUTH,
    WEST
};
```

### 5. **总结**

理解数据类型和变量的使用对于编写高效的 C++ 程序至关重要。C++ 提供了丰富的数据类型、变量声明和初始化方式，以及常量和枚举类型来满足不同编程需求。掌握这些基本概念可以帮助你更好地设计和实现程序功能。
