## 文件系统 `<filesystem>`

C++17 引入了 `<filesystem>` 头文件，提供了对文件系统的标准化访问接口，使得文件和目录操作更加高效和易于使用。该库包括了对文件路径、文件操作和目录遍历等功能的支持。以下是 `<filesystem>` 的主要功能和用法介绍。

### 1. **文件系统库的基础**

`<filesystem>` 头文件定义了与文件和目录操作相关的类和函数。常用的类包括 `std::filesystem::path`、`std::filesystem::file_status`、`std::filesystem::directory_iterator` 等。

#### **`std::filesystem::path`**

`std::filesystem::path` 是一个用于表示文件路径的类。它支持路径操作、路径拼接和路径转换等功能。

```cpp
#include <iostream>
#include <filesystem>

int main() {
    std::filesystem::path p{"example.txt"};
    std::cout << "File name: " << p.filename() << std::endl;
    std::cout << "Parent path: " << p.parent_path() << std::endl;
    std::cout << "Extension: " << p.extension() << std::endl;
    return 0;
}
```

#### **`std::filesystem::file_status`**

`std::filesystem::file_status` 用于表示文件的状态信息，包括文件的类型（普通文件、目录、符号链接等）和权限。

```cpp
#include <iostream>
#include <filesystem>

int main() {
    std::filesystem::path p{"example.txt"};
    std::filesystem::file_status s = std::filesystem::status(p);

    if (std::filesystem::is_regular_file(s)) {
        std::cout << p << " is a regular file." << std::endl;
    } else if (std::filesystem::is_directory(s)) {
        std::cout << p << " is a directory." << std::endl;
    }
    return 0;
}
```

### 2. **文件和目录操作**

`<filesystem>` 提供了用于创建、删除和修改文件和目录的函数。

#### **创建文件和目录**

使用 `std::filesystem::create_directory` 可以创建目录，`std::filesystem::ofstream` 可以创建和写入文件。

```cpp
#include <iostream>
#include <filesystem>
#include <fstream>

int main() {
    std::filesystem::path dir{"test_directory"};
    if (!std::filesystem::exists(dir)) {
        std::filesystem::create_directory(dir);
        std::cout << "Directory created: " << dir << std::endl;
    }

    std::filesystem::path file{"test_directory/test_file.txt"};
    std::ofstream ofs(file);
    ofs << "Hello, filesystem!";
    ofs.close();
    std::cout << "File created: " << file << std::endl;

    return 0;
}
```

#### **删除文件和目录**

使用 `std::filesystem::remove` 可以删除文件和目录。请注意，删除目录时必须先删除目录中的所有内容。

```cpp
#include <iostream>
#include <filesystem>

int main() {
    std::filesystem::path file{"test_directory/test_file.txt"};
    if (std::filesystem::exists(file)) {
        std::filesystem::remove(file);
        std::cout << "File removed: " << file << std::endl;
    }

    std::filesystem::path dir{"test_directory"};
    if (std::filesystem::exists(dir)) {
        std::filesystem::remove_all(dir);
        std::cout << "Directory removed: " << dir << std::endl;
    }

    return 0;
}
```

### 3. **目录遍历**

使用 `std::filesystem::directory_iterator` 可以遍历目录中的文件和子目录。

```cpp
#include <iostream>
#include <filesystem>

int main() {
    std::filesystem::path dir{"test_directory"};
    for (const auto& entry : std::filesystem::directory_iterator(dir)) {
        std::cout << entry.path() << std::endl;
    }
    return 0;
}
```

### 4. **路径操作**

`std::filesystem::path` 提供了多种路径操作功能，包括拼接路径、获取绝对路径、规范化路径等。

#### **路径拼接**

```cpp
#include <iostream>
#include <filesystem>

int main() {
    std::filesystem::path base{"dir"};
    std::filesystem::path file = base / "file.txt";
    std::cout << "Full path: " << file << std::endl;
    return 0;
}
```

#### **获取绝对路径**

```cpp
#include <iostream>
#include <filesystem>

int main() {
    std::filesystem::path relative{"file.txt"};
    std::filesystem::path absolute = std::filesystem::absolute(relative);
    std::cout << "Absolute path: " << absolute << std::endl;
    return 0;
}
```

### 5. **错误处理**

`<filesystem>` 提供了函数来检查文件或目录是否存在，从而避免在操作时引发异常。使用 `std::filesystem::exists` 检查路径是否存在，使用 `std::filesystem::is_directory` 检查路径是否为目录等。

```cpp
#include <iostream>
#include <filesystem>

int main() {
    std::filesystem::path p{"example.txt"};
    if (std::filesystem::exists(p)) {
        if (std::filesystem::is_regular_file(p)) {
            std::cout << p << " is a file." << std::endl;
        } else if (std::filesystem::is_directory(p)) {
            std::cout << p << " is a directory." << std::endl;
        }
    } else {
        std::cout << p << " does not exist." << std::endl;
    }
    return 0;
}
```

### 6. **总结**

`<filesystem>` 头文件提供了强大而直观的文件系统操作功能。通过 `std::filesystem::path`、`std::filesystem::file_status` 和相关函数，程序员可以轻松地进行文件和目录的创建、删除、遍历以及路径操作。C++17 的文件系统库显著简化了文件系统操作，提供了更加安全和高效的接口。