## 正则表达式 `<regex>`

C++11 引入了 `<regex>` 头文件，提供了对正则表达式的标准支持，使得文本匹配和搜索变得更加高效和灵活。该库包括了对正则表达式的定义、匹配、替换和搜索等功能的支持。以下是 `<regex>` 的主要功能和用法介绍。

### 1. **正则表达式基础**

`<regex>` 头文件定义了处理正则表达式的类和函数。常用的类包括 `std::regex`、`std::smatch`、`std::sregex_iterator` 等。

#### **`std::regex`**

`std::regex` 是用来表示正则表达式的类。它支持多种正则表达式语法规则，包括 ECMAScript、Perl、POSIX 等。

```cpp
#include <iostream>
#include <regex>

int main() {
    std::regex e(R"(hello)"); // 创建一个正则表达式对象，匹配 "hello"
    std::string text = "hello world";
    std::smatch match;

    if (std::regex_search(text, match, e)) {
        std::cout << "Match found: " << match[0] << std::endl;
    } else {
        std::cout << "No match found" << std::endl;
    }

    return 0;
}
```

### 2. **正则表达式匹配**

`<regex>` 提供了多种匹配正则表达式的函数，包括 `std::regex_match`、`std::regex_search` 和 `std::regex_replace`。

#### **`std::regex_match`**

`std::regex_match` 用于测试整个字符串是否与正则表达式匹配。

```cpp
#include <iostream>
#include <regex>

int main() {
    std::regex e(R"(\d{3}-\d{2}-\d{4})"); // 匹配社会安全号码格式
    std::string text = "123-45-6789";

    if (std::regex_match(text, e)) {
        std::cout << "Match found: " << text << std::endl;
    } else {
        std::cout << "No match found" << std::endl;
    }

    return 0;
}
```

#### **`std::regex_search`**

`std::regex_search` 用于在字符串中搜索与正则表达式匹配的子串。

```cpp
#include <iostream>
#include <regex>

int main() {
    std::regex e(R"(\d{3})"); // 匹配任意三位数字
    std::string text = "There are 123 apples";

    std::smatch match;
    if (std::regex_search(text, match, e)) {
        std::cout << "Match found: " << match[0] << std::endl;
    } else {
        std::cout << "No match found" << std::endl;
    }

    return 0;
}
```

#### **`std::regex_replace`**

`std::regex_replace` 用于用正则表达式替换字符串中的匹配项。

```cpp
#include <iostream>
#include <regex>

int main() {
    std::regex e(R"(\d{3})"); // 匹配任意三位数字
    std::string text = "My number is 123456789";
    std::string replaced = std::regex_replace(text, e, "XXX");

    std::cout << "Replaced text: " << replaced << std::endl;
    return 0;
}
```

### 3. **正则表达式模式**

正则表达式支持多种模式，用于定义要匹配的文本格式。常用的正则表达式模式包括：

- **字符类**: `[abc]` 匹配 'a'、'b' 或 'c'。
- **数量词**: `a{2,4}` 匹配 'a' 至少两次，最多四次。
- **边界匹配**: `^` 匹配行的开始，`$` 匹配行的结束。
- **分组与捕获**: `(abc)` 匹配并捕获 'abc'。
- **非捕获分组**: `(?:abc)` 匹配 'abc' 但不捕获。

#### **示例: 捕获组**

```cpp
#include <iostream>
#include <regex>

int main() {
    std::regex e(R"( (\d{3})-(\d{2})-(\d{4}) )"); // 捕获三部分
    std::string text = "123-45-6789";
    std::smatch match;

    if (std::regex_match(text, match, e)) {
        std::cout << "Match found:" << std::endl;
        std::cout << "Full match: " << match[0] << std::endl;
        std::cout << "Area code: " << match[1] << std::endl;
        std::cout << "Group code: " << match[2] << std::endl;
        std::cout << "Serial number: " << match[3] << std::endl;
    } else {
        std::cout << "No match found" << std::endl;
    }

    return 0;
}
```

### 4. **正则表达式迭代**

使用 `std::sregex_iterator` 可以遍历字符串中所有匹配的子串。

```cpp
#include <iostream>
#include <regex>

int main() {
    std::regex e(R"(\d{3})"); // 匹配三位数字
    std::string text = "123 456 789";

    auto begin = std::sregex_iterator(text.begin(), text.end(), e);
    auto end = std::sregex_iterator();

    for (std::sregex_iterator i = begin; i != end; ++i) {
        std::smatch match = *i;
        std::cout << "Match found: " << match[0] << std::endl;
    }

    return 0;
}
```

### 5. **正则表达式 flags**

正则表达式的行为可以通过标志进行控制，如不区分大小写、对多行进行匹配等。

```cpp
#include <iostream>
#include <regex>

int main() {
    std::regex e(R"(hello)", std::regex_constants::icase); // 不区分大小写
    std::string text = "Hello World";

    if (std::regex_search(text, e)) {
        std::cout << "Match found (case insensitive)" << std::endl;
    } else {
        std::cout << "No match found" << std::endl;
    }

    return 0;
}
```

### 6. **总结**

`<regex>` 头文件提供了强大的正则表达式功能，使得处理文本匹配和搜索变得更加简便和高效。通过 `std::regex`、`std::smatch` 和相关函数，程序员可以轻松地进行正则表达式的定义、匹配、搜索和替换操作。正则表达式的灵活性和功能性使其在文本处理、数据验证和复杂匹配场景中得到了广泛应用。