## `<fstream>` 基础设施

`<fstream>` 是 C++ 标准库中的一个头文件，提供了用于文件输入输出操作的类。它主要包含 `std::ifstream`、`std::ofstream` 和 `std::fstream` 类，用于从文件中读取数据、将数据写入到文件中，以及在同一文件中同时进行读写操作。

### 1. **类介绍**

#### 1.1 `std::ifstream`

`std::ifstream` 是用于从文件中读取数据的类。它继承自 `std::istream` 类，允许以输入流的方式访问文件内容。

**常用操作：**

- **打开文件：**

  ```cpp
  std::ifstream inputFile("example.txt");
  ```

- **检查文件是否成功打开：**

  ```cpp
  if (!inputFile.is_open()) {
      std::cerr << "Failed to open file!" << std::endl;
  }
  ```

- **读取数据：**

  ```cpp
  std::string line;
  while (std::getline(inputFile, line)) {
      std::cout << line << std::endl;
  }
  ```

- **关闭文件：**

  ```cpp
  inputFile.close();
  ```

#### 1.2 `std::ofstream`

`std::ofstream` 是用于将数据写入文件的类。它继承自 `std::ostream` 类，允许以输出流的方式将数据写入文件。

**常用操作：**

- **打开文件：**

  ```cpp
  std::ofstream outputFile("output.txt");
  ```

- **检查文件是否成功打开：**

  ```cpp
  if (!outputFile.is_open()) {
      std::cerr << "Failed to open file!" << std::endl;
  }
  ```

- **写入数据：**

  ```cpp
  outputFile << "Hello, world!" << std::endl;
  ```

- **关闭文件：**

  ```cpp
  outputFile.close();
  ```

#### 1.3 `std::fstream`

`std::fstream` 是一个多功能的文件流类，既可以用于读取文件也可以用于写入文件。它继承自 `std::iostream` 类，允许在同一文件流中进行读写操作。

**常用操作：**

- **打开文件：**

  ```cpp
  std::fstream file("data.txt", std::ios::in | std::ios::out | std::ios::trunc);
  ```

- **检查文件是否成功打开：**

  ```cpp
  if (!file.is_open()) {
      std::cerr << "Failed to open file!" << std::endl;
  }
  ```

- **读取数据：**

  ```cpp
  std::string line;
  while (std::getline(file, line)) {
      std::cout << line << std::endl;
  }
  ```

- **写入数据：**

  ```cpp
  file << "Writing data to file." << std::endl;
  ```

- **关闭文件：**

  ```cpp
  file.close();
  ```

### 2. **示例**

以下是一个使用 `<fstream>` 的示例，演示了如何使用 `std::ifstream`、`std::ofstream` 和 `std::fstream` 进行文件操作：

```cpp
#include <iostream>
#include <fstream>
#include <string>

int main() {
    // 使用 std::ofstream 写入数据
    std::ofstream outputFile("output.txt");
    if (!outputFile) {
        std::cerr << "Failed to open file for writing!" << std::endl;
        return 1;
    }
    outputFile << "Hello, world!" << std::endl;
    outputFile.close();

    // 使用 std::ifstream 读取数据
    std::ifstream inputFile("output.txt");
    if (!inputFile) {
        std::cerr << "Failed to open file for reading!" << std::endl;
        return 1;
    }
    std::string line;
    while (std::getline(inputFile, line)) {
        std::cout << line << std::endl;
    }
    inputFile.close();

    // 使用 std::fstream 进行读写操作
    std::fstream file("data.txt", std::ios::in | std::ios::out | std::ios::trunc);
    if (!file) {
        std::cerr << "Failed to open file for read/write!" << std::endl;
        return 1;
    }
    file << "Writing data to file." << std::endl;
    file.seekg(0); // 移动到文件开始位置
    while (std::getline(file, line)) {
        std::cout << line << std::endl;
    }
    file.close();

    return 0;
}
```

### 3. **总结**

`<fstream>` 提供了三种主要的文件流类：`std::ifstream`、`std::ofstream` 和 `std::fstream`，分别用于从文件中读取数据、将数据写入文件和在同一文件流中进行读写操作。这些类允许以流的方式访问文件，提供了高效且灵活的文件操作功能。通过适当使用这些类，可以实现文件的读取、写入、更新等操作，以满足不同的编程需求。