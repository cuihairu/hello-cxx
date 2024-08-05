### C++17 文件系统库

C++17 引入了新的标准库组件——**文件系统库**（`<filesystem>`）。该库为 C++ 提供了强大的文件和目录操作功能，使得处理文件系统中的路径、文件和目录变得更加方便和一致。文件系统库是对 Boost.Filesystem 库的标准化，使得许多文件操作功能变得标准化且易于使用。

#### 1. **基本概念**

- **路径**：表示文件或目录在文件系统中的位置。使用 `std::filesystem::path` 类来处理。
- **文件系统操作**：包括文件和目录的创建、删除、复制、移动等操作。使用 `std::filesystem` 命名空间中的函数来执行。
- **迭代器**：可以用于遍历目录中的内容。

#### 2. **主要功能和类**

**`std::filesystem::path`**：表示文件系统路径。支持路径拼接、解析等操作。

**示例：路径操作**

```cpp
#include <filesystem>
#include <iostream>

int main() {
    std::filesystem::path p1 = "example";
    std::filesystem::path p2 = p1 / "file.txt";
    
    std::cout << "Path: " << p2 << std::endl;
    std::cout << "Parent Path: " << p2.parent_path() << std::endl;
    std::cout << "Filename: " << p2.filename() << std::endl;
    
    return 0;
}
```

**`std::filesystem::directory_entry`**：表示目录中的一个文件或子目录。可以用于访问文件的属性和信息。

**示例：访问文件属性**

```cpp
#include <filesystem>
#include <iostream>

int main() {
    std::filesystem::directory_entry entry("example.txt");
    
    std::cout << "Path: " << entry.path() << std::endl;
    std::cout << "Is Regular File: " << entry.is_regular_file() << std::endl;
    std::cout << "Size: " << entry.file_size() << std::endl;
    
    return 0;
}
```

**`std::filesystem::directory_iterator`**：用于遍历目录中的文件和子目录。

**示例：遍历目录**

```cpp
#include <filesystem>
#include <iostream>

int main() {
    std::filesystem::path p = ".";
    
    for (const auto& entry : std::filesystem::directory_iterator(p)) {
        std::cout << entry.path() << std::endl;
    }
    
    return 0;
}
```

#### 3. **常用函数**

**文件和目录操作**

- **创建和删除目录**：
  ```cpp
  std::filesystem::create_directory("new_directory");
  std::filesystem::remove("new_directory");
  ```

- **创建和删除文件**：
  ```cpp
  std::filesystem::path file = "new_file.txt";
  std::ofstream(file) << "Hello, World!"; // 创建并写入文件
  std::filesystem::remove(file); // 删除文件
  ```

- **复制和移动文件**：
  ```cpp
  std::filesystem::copy("source.txt", "destination.txt");
  std::filesystem::rename("old_name.txt", "new_name.txt");
  ```

- **获取文件状态**：
  ```cpp
  auto status = std::filesystem::status("file.txt");
  if (std::filesystem::exists(status)) {
      std::cout << "File exists" << std::endl;
  }
  ```

#### 4. **错误处理**

使用文件系统库时，许多函数可能会抛出 `std::filesystem::filesystem_error` 异常。建议使用 `try-catch` 块来捕获和处理这些异常。

**示例：错误处理**

```cpp
#include <filesystem>
#include <iostream>

int main() {
    try {
        std::filesystem::remove("non_existent_file.txt");
    } catch (const std::filesystem::filesystem_error& e) {
        std::cout << "Filesystem error: " << e.what() << std::endl;
    }
    
    return 0;
}
```

#### 5. **总结**

C++17 的文件系统库提供了丰富的功能来处理文件和目录，极大地简化了与文件系统交互的操作。它是一个强大的工具，帮助开发者更加高效地管理文件和目录操作，同时确保了跨平台的一致性和可靠性。