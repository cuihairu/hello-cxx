## `<sstream>` 基础设施

`<sstream>` 是 C++ 标准库中的一个头文件，提供了用于字符串流操作的类。它主要包含 `std::stringstream`、`std::istringstream` 和 `std::ostringstream` 类，这些类允许在内存中对字符串进行输入和输出操作，提供了比传统的 `std::string` 更强大的数据流处理功能。

### 1. **类介绍**

#### 1.1 `std::stringstream`

`std::stringstream` 是一个综合了输入和输出流功能的类。它可以被用来从字符串中提取数据，或者将数据写入到字符串中。`std::stringstream` 结合了 `std::istringstream` 和 `std::ostringstream` 的功能，可以用于字符串的格式化、转换和解析等任务。

**常用操作：**

- **创建 `std::stringstream` 对象：**

  ```cpp
  std::stringstream ss;
  ```

- **写入数据到字符串流：**

  ```cpp
  ss << "Hello, " << 42 << " world!";
  ```

- **从字符串流中读取数据：**

  ```cpp
  std::string str;
  int num;
  ss >> str >> num;
  ```

- **获取字符串内容：**

  ```cpp
  std::string content = ss.str();
  ```

- **清空流：**

  ```cpp
  ss.str(""); // 清空字符串内容
  ss.clear(); // 重置状态标志
  ```

#### 1.2 `std::istringstream`

`std::istringstream` 用于从字符串中读取数据，类似于输入流。它提供了从字符串中解析数据的功能，通常用于将字符串数据转换为其他类型。

**常用操作：**

- **创建 `std::istringstream` 对象：**

  ```cpp
  std::istringstream iss("123 456 789");
  ```

- **从字符串流中读取数据：**

  ```cpp
  int a, b, c;
  iss >> a >> b >> c;
  ```

#### 1.3 `std::ostringstream`

`std::ostringstream` 用于将数据写入字符串中，类似于输出流。它可以将各种数据格式化为字符串，用于生成复杂的字符串输出。

**常用操作：**

- **创建 `std::ostringstream` 对象：**

  ```cpp
  std::ostringstream oss;
  ```

- **写入数据到字符串流：**

  ```cpp
  oss << "The value is " << 3.14;
  ```

- **获取字符串内容：**

  ```cpp
  std::string result = oss.str();
  ```

### 2. **示例**

以下是一个使用 `<sstream>` 的示例，演示了如何使用 `std::stringstream`、`std::istringstream` 和 `std::ostringstream`：

```cpp
#include <iostream>
#include <sstream>
#include <string>

int main() {
    // 使用 std::ostringstream 写入数据
    std::ostringstream oss;
    oss << "The number is " << 42;
    std::string result = oss.str();
    std::cout << result << std::endl; // 输出: The number is 42

    // 使用 std::istringstream 读取数据
    std::istringstream iss("123 456 789");
    int a, b, c;
    iss >> a >> b >> c;
    std::cout << a << " " << b << " " << c << std::endl; // 输出: 123 456 789

    // 使用 std::stringstream 综合操作
    std::stringstream ss;
    ss << "Hello, " << 2024;
    std::string str;
    int year;
    ss >> str >> year;
    std::cout << str << " " << year << std::endl; // 输出: Hello, 2024

    return 0;
}
```

### 3. **总结**

`<sstream>` 提供了一种灵活的方式来处理字符串流。`std::stringstream` 结合了输入和输出流的功能，`std::istringstream` 用于从字符串中读取数据，`std::ostringstream` 用于将数据写入字符串中。使用这些类可以方便地处理字符串格式化、转换和解析，提高程序的灵活性和可读性。