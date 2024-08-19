## `<iomanip>` 基础设施

`<iomanip>` 是 C++ 标准库中的一个头文件，用于定义输入输出流的格式化操作。它提供了一系列操控器，用于控制输出数据的显示格式，例如数字的精度、宽度、对齐方式、填充字符等。使用 `<iomanip>` 可以使输出更符合需求，增强程序的可读性和美观性。

### 1. **流操控器（Stream Manipulators）**

流操控器是 `<iomanip>` 中定义的特殊对象或函数，用于修改流的格式设置。常用的流操控器包括：

- **`std::setw(int n)`**: 设置字段宽度为 `n`。如果数据的宽度小于 `n`，则会在数据前面填充空格。

  ```cpp
  #include <iostream>
  #include <iomanip>

  int main() {
      std::cout << std::setw(10) << 42 << std::endl; // 输出: "         42"
      return 0;
  }
  ```

- **`std::setfill(char c)`**: 设置字段填充字符为 `c`。默认填充字符是空格，可以用它改变填充字符。

  ```cpp
  #include <iostream>
  #include <iomanip>

  int main() {
      std::cout << std::setw(10) << std::setfill('*') << 42 << std::endl; // 输出: "********42"
      return 0;
  }
  ```

- **`std::setprecision(int n)`**: 设置浮点数的显示精度为 `n` 位小数。影响浮点数的输出格式。

  ```cpp
  #include <iostream>
  #include <iomanip>

  int main() {
      double pi = 3.141592653589793;
      std::cout << std::setprecision(4) << pi << std::endl; // 输出: "3.142"
      return 0;
  }
  ```

- **`std::fixed`**: 使用定点表示法输出浮点数，保持固定的精度。

  ```cpp
  #include <iostream>
  #include <iomanip>

  int main() {
      double pi = 3.141592653589793;
      std::cout << std::fixed << std::setprecision(2) << pi << std::endl; // 输出: "3.14"
      return 0;
  }
  ```

- **`std::scientific`**: 使用科学计数法输出浮点数。

  ```cpp
  #include <iostream>
  #include <iomanip>

  int main() {
      double pi = 3.141592653589793;
      std::cout << std::scientific << std::setprecision(2) << pi << std::endl; // 输出: "3.14e+00"
      return 0;
  }
  ```

- **`std::hex`**, **`std::dec`**, **`std::oct`**: 设置整数的输出进制格式为十六进制、十进制和八进制。

  ```cpp
  #include <iostream>
  #include <iomanip>

  int main() {
      int num = 255;
      std::cout << std::hex << num << std::endl; // 输出: "ff"
      std::cout << std::dec << num << std::endl; // 输出: "255"
      std::cout << std::oct << num << std::endl; // 输出: "377"
      return 0;
  }
  ```

- **`std::showbase`**: 显示整数输出的进制前缀（如 `0x`、`0`、`0b`）。

  ```cpp
  #include <iostream>
  #include <iomanip>

  int main() {
      int num = 255;
      std::cout << std::hex << std::showbase << num << std::endl; // 输出: "0xff"
      return 0;
  }
  ```

- **`std::noshowbase`**: 关闭进制前缀显示。

  ```cpp
  #include <iostream>
  #include <iomanip>

  int main() {
      int num = 255;
      std::cout << std::hex << std::showbase << num << std::endl; // 输出: "0xff"
      std::cout << std::noshowbase << num << std::endl; // 输出: "ff"
      return 0;
  }
  ```

- **`std::left`**, **`std::right`**, **`std::internal`**: 设置对齐方式。`std::left` 左对齐，`std::right` 右对齐，`std::internal` 将填充字符放在数值的内部。

  ```cpp
  #include <iostream>
  #include <iomanip>

  int main() {
      std::cout << std::setw(10) << std::left << 42 << std::endl; // 输出: "42        "
      std::cout << std::setw(10) << std::right << 42 << std::endl; // 输出: "        42"
      return 0;
  }
  ```

### 2. **使用示例**

以下是一个使用 `<iomanip>` 的示例，演示了如何使用各种流操控器来格式化输出：

```cpp
#include <iostream>
#include <iomanip>

int main() {
    // 输出宽度和填充字符
    std::cout << std::setw(10) << std::setfill('*') << 123 << std::endl;

    // 输出精度和格式
    double pi = 3.141592653589793;
    std::cout << std::fixed << std::setprecision(4) << pi << std::endl;

    // 进制格式
    int num = 255;
    std::cout << std::hex << std::showbase << num << std::endl;
    std::cout << std::oct << num << std::endl;
    std::cout << std::dec << num << std::endl;

    return 0;
}
```

### 3. **总结**

`<iomanip>` 提供了丰富的格式化选项来控制数据的输出格式。通过使用流操控器，可以方便地设置字段宽度、填充字符、数值精度、进制表示等。掌握这些操控器的使用可以帮助你实现更复杂的输出需求，提高程序的可读性和用户体验。