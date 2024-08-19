### C++98 标准库

C++98 标准库提供了广泛的功能，以支持各种编程任务，包括容器、算法、输入/输出等。以下是 C++98 标准库的主要组成部分：

#### 1. **标准模板库（STL）**

- **容器**：
  - **序列容器**：`std::vector`, `std::list`, `std::deque`
  - **关联容器**：`std::set`, `std::multiset`, `std::map`, `std::multimap`
  - **无序容器**：C++98 不支持无序容器，`unordered_set` 和 `unordered_map` 是 C++11 引入的。
  - **适配器容器**：`std::stack`, `std::queue`, `std::priority_queue`

- **迭代器**：
  - **基本迭代器**：`std::iterator`
  - **迭代器类别**：输入迭代器、输出迭代器、前向迭代器、双向迭代器、随机访问迭代器

- **算法**：
  - **排序算法**：`std::sort`, `std::stable_sort`
  - **查找算法**：`std::find`, `std::binary_search`
  - **操作算法**：`std::copy`, `std::transform`, `std::accumulate`
  - **集合算法**：`std::set_union`, `std::set_intersection`

- **函数对象**：
  - **标准函数对象**：`std::plus`, `std::minus`, `std::multiplies`, `std::divides`, `std::negate`, `std::equal_to`, `std::not_equal_to`, `std::less`, `std::greater`

#### 2. **输入/输出库**

- **流类**：
  - **输入流**：`std::istream`, `std::ifstream`
  - **输出流**：`std::ostream`, `std::ofstream`
  - **文件流**：`std::fstream`
  - **字符串流**：`std::stringstream`, `std::istringstream`, `std::ostringstream`

- **流缓冲区**：
  - **流缓冲区**：`std::streambuf`
  - **流输入缓冲区**：`std::filebuf`, `std::stringbuf`
  - **流输出缓冲区**：`std::filebuf`, `std::stringbuf`

- **格式化**：
  - **格式化库**：`std::ios`, `std::iomanip`, `std::locale`
  - **格式化操作**：`std::setw`, `std::setprecision`, `std::fixed`, `std::scientific`

#### 3. **字符串类**

- **`std::string`**：支持动态大小的字符序列，包括字符串的基本操作，如拼接、查找、替换等。
- **`std::wstring`**：宽字符字符串，支持宽字符操作。

#### 4. **时间和日期**

- **`<ctime>`**：
  - **时间函数**：`std::time`, `std::localtime`, `std::gmtime`, `std::mktime`
  - **时间戳**：`std::clock`, `std::difftime`, `std::strftime`

#### 5. **数学库**

- **`<cmath>`**：
  - **数学函数**：`std::abs`, `std::sqrt`, `std::pow`, `std::sin`, `std::cos`, `std::tan`
  - **其他函数**：`std::log`, `std::exp`, `std::ceil`, `std::floor`

- **`<complex>`**：支持复数运算，包括基本复数操作，如加法、减法、乘法、除法等。

- **`<valarray>`**：提供了对数值数组的操作，包括基本的数组运算、数学函数和操作。

#### 6. **异常处理**

- **`<exception>`**：
  - **异常类**：`std::exception`, `std::logic_error`, `std::runtime_error`, `std::bad_alloc`, `std::bad_cast`
  - **异常处理机制**：`try`, `catch`, `throw`

#### 7. **工具库**

- **`<utility>`**：
  - **标准工具函数**：`std::swap`, `std::make_pair`, `std::pair`

- **`<functional>`**：
  - **函数对象**：`std::function`, `std::bind1st`, `std::bind2nd`

- **`<locale>`**：
  - **本地化支持**：`std::locale`, `std::ctype`, `std::num_get`, `std::num_put`

#### 8. **内存管理**

- **`<memory>`**：
  - **智能指针**：`std::auto_ptr`（在 C++11 中被 `std::unique_ptr` 替代）
  - **内存管理工具**：`std::allocator`

### 总结

C++98 标准库为 C++ 语言提供了广泛的功能支持，涵盖了容器、算法、输入/输出、字符串处理、数学运算等领域。它为 C++ 的开发提供了丰富的工具和资源，使得程序员可以编写高效、可维护的代码。