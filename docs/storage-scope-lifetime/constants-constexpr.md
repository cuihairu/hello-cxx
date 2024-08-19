### 常量与 `constexpr`

#### ** 常量**

在 C++ 中，常量指的是其值在程序运行期间不能被修改的量。常量主要有以下几种类型：

- **`const` 常量**
  - 使用 `const` 关键字声明，表示变量的值在初始化后不能被改变。
  - 可以用于局部变量、全局变量和类的成员变量。
  ```cpp
  const int MAX_SIZE = 100; // `const` 常量
  void function() {
      const int LOCAL_CONST = 10; // 函数内的 `const` 常量
  }
  ```

- **`const` 成员变量**
  - 类中的 `const` 成员变量必须在构造函数的初始化列表中进行初始化。
  ```cpp
  class MyClass {
  public:
      const int value;
      MyClass(int v) : value(v) {}
  };
  ```

- **`constexpr` 常量**
  - `constexpr` 表示常量在编译时能够被求值，可以用于编译时常量表达式。
  - `constexpr` 可以用来声明常量变量和常量函数。
  ```cpp
  constexpr int MAX_SIZE = 100; // `constexpr` 常量
  ```

#### **`constexpr` 函数**

`constexpr` 函数在编译时能够求值，必须满足以下条件：

- 函数体内的代码必须是编译时常量表达式。
- 不能有副作用，函数体只能包含简单的操作，如基本的算术运算和条件判断。

- **`constexpr` 函数示例**
  ```cpp
  constexpr int square(int x) {
      return x * x; // 编译时求值
  }
  
  int main() {
      constexpr int result = square(5); // 编译时求值
      return 0;
  }
  ```

#### **4.3 `constexpr` 与 `const` 的区别**

- **`const`**
  - 在程序运行时保证变量不可变。
  - 可以用于运行时常量，值在编译时未知。
  - 主要用于需要在运行时计算的常量。

- **`constexpr`**
  - 在编译时进行求值，适用于需要在编译时确定值的常量。
  - 可以用于编译时常量和常量表达式。
  - 提供了更多的编译时优化。

#### **4.4 示例**

- **`const` 示例**
  ```cpp
  void example() {
      const int value = 10; // 运行时常量
      // value = 20; // 编译错误: `value` 是 `const` 变量，不能修改
  }
  ```

- **`constexpr` 示例**
  ```cpp
  constexpr int factorial(int n) {
      return (n <= 1) ? 1 : (n * factorial(n - 1));
  }
  
  int main() {
      constexpr int result = factorial(5); // 编译时求值
      return 0;
  }
  ```

#### **4.5 最佳实践**

- **使用 `const` 和 `constexpr`**
  - 使用 `const` 来定义那些在程序运行时不变的值。
  - 使用 `constexpr` 来定义编译时常量和能够在编译时计算的表达式，以优化程序性能。

- **`constexpr` 函数的设计**
  - 保持 `constexpr` 函数的简单性，避免复杂的控制流和副作用。
  - 确保 `constexpr` 函数能够在编译时求值。

