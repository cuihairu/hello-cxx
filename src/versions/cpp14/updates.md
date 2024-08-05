### C++14 更新内容

C++14 是对 C++11 的补充和修订版本，主要在语言特性、库功能和标准规范方面进行了一些改进。以下是 C++14 标准的主要更新内容：

#### 1. **语言特性**

1. **泛型 Lambda 表达式**
   C++14 扩展了 Lambda 表达式的能力，允许在 Lambda 表达式中使用自动类型推导（`auto`）作为参数类型。

   **示例**：
   ```cpp
   auto lambda = [](auto x, auto y) {
       return x + y;
   };
   std::cout << lambda(1, 2) << std::endl;       // 输出 3
   std::cout << lambda(1.5, 2.5) << std::endl;   // 输出 4.0
   ```

2. **`decltype(auto)`**
   `decltype(auto)` 关键字用于推导表达式的类型，可以保留表达式的返回值类型，包括引用类型。

   **示例**：
   ```cpp
   int x = 10;
   auto f() -> decltype(auto) { return x; } // 返回 x 的类型
   decltype(auto) result = f(); // result 的类型是 int
   ```

3. **返回类型推导**
   函数可以使用 `auto` 来推导返回类型，简化函数定义。

   **示例**：
   ```cpp
   auto add(int a, int b) {
       return a + b; // 自动推导返回类型为 int
   }
   ```

4. **`std::make_unique`**
   C++14 标准新增了 `std::make_unique` 函数，用于创建 `std::unique_ptr` 对象，简化了智能指针的创建。

   **示例**：
   ```cpp
   #include <memory>
   auto ptr = std::make_unique<int>(10); // 创建 unique_ptr<int> 指向 10
   ```

5. **用户自定义字面量（User-Defined Literals）改进**
   C++14 扩展了用户自定义字面量的功能，使得它们可以与现有字面量更好地结合使用。

   **示例**：
   ```cpp
   constexpr long double operator"" _km(long double x) {
       return x * 1000.0;
   }
   constexpr long double distance = 1.5_km; // distance 的值是 1500.0
   ```

6. **`constexpr` 函数的改进**
   C++14 放宽了 `constexpr` 函数的限制，允许在 `constexpr` 函数中使用更多的语言特性，例如局部变量的初始化。

   **示例**：
   ```cpp
   constexpr int square(int x) {
       return x * x;
   }
   constexpr int value = square(5); // value 的值是 25
   ```

7. **二进制字面量**
   C++14 允许使用二进制字面量（以 `0b` 开头）表示整数值。

   **示例**：
   ```cpp
   int binaryValue = 0b101010; // 二进制表示的 42
   ```

8. **`std::shared_timed_mutex`**
   引入了 `std::shared_timed_mutex`，允许多线程以读写锁的方式进行并发控制。

   **示例**：
   ```cpp
   #include <shared_mutex>

   std::shared_timed_mutex mtx;
   ```

9. **`std::integer_sequence` 和 `std::index_sequence`**
   提供了对整数序列的支持，常用于模板编程。

   **示例**：
   ```cpp
   template <std::size_t... Indices>
   void printIndices(std::index_sequence<Indices...>) {
       (std::cout << ... << Indices) << std::endl;
   }

   printIndices(std::make_index_sequence<4>{}); // 输出 0123
   ```

#### 2. **标准库更新**

1. **`std::chrono` 扩展**
   C++14 对时间库进行了改进，提供了对更高分辨率计时的支持。

   **示例**：
   ```cpp
   #include <chrono>
   auto now = std::chrono::high_resolution_clock::now();
   ```

2. **`std::get` 对元组的支持**
   增强了 `std::get` 对元组的支持，允许使用常量表达式作为索引。

   **示例**：
   ```cpp
   #include <tuple>

   std::tuple<int, double, std::string> myTuple(1, 2.3, "hello");
   auto value = std::get<1>(myTuple); // value 的值是 2.3
   ```

3. **`std::default_delete` 改进**
   `std::default_delete` 可以删除用户自定义的删除器类型，使得删除操作更加灵活。

   **示例**：
   ```cpp
   #include <memory>

   struct CustomDeleter {
       void operator()(int* ptr) const { delete ptr; }
   };

   std::unique_ptr<int, CustomDeleter> ptr(new int(10));
   ```

4. **`std::make_unique`**
   除了创建 `std::unique_ptr`，还支持传递多个参数给构造函数。

   **示例**：
   ```cpp
   #include <memory>
   auto ptr = std::make_unique<std::vector<int>>(10, 5); // 创建 unique_ptr<std::vector<int>>，初始化为 10 个值为 5 的元素
   ```

#### 3. **其他改进**

1. **`std::aligned_storage` 改进**
   改进了 `std::aligned_storage` 以支持更高对齐需求的类型。

2. **`std::enable_if` 改进**
   对 `std::enable_if` 进行了改进，使其使用更加简便。

C++14 的更新虽然不像 C++11 那样引入大量的新特性，但它提供了对现有功能的改进和增强，使得编程变得更加高效和便捷。