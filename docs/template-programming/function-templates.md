## 函数模板

函数模板是 C++ 的一个重要特性，允许定义一个函数的通用版本，这个函数可以处理多种数据类型。函数模板使得我们能够编写泛型代码，从而在编写函数时避免重复代码，并且可以在编译时根据传递的参数类型生成具体的函数实例。以下是函数模板的详细介绍：

### 1. **函数模板的定义**

函数模板的定义语法如下：
```cpp
template <typename T>
T functionName(T parameter) {
    // Function body
}
```
其中，`template <typename T>` 声明了一个模板，`T` 是一个类型参数。函数 `functionName` 接受一个类型为 `T` 的参数并返回 `T` 类型的值。编译器在使用该函数时，会根据实际提供的参数类型生成对应的函数实现。

**示例**：
```cpp
template <typename T>
T max(T a, T b) {
    return (a > b) ? a : b;
}
```
在这个示例中，`max` 函数模板接受两个相同类型的参数，并返回较大的值。编译器会根据传递的参数类型自动生成具体的函数版本，例如 `max<int>(3, 5)` 和 `max<double>(3.5, 2.1)`。

### 2. **函数模板的实例化**

函数模板的实例化指的是在编译时，编译器根据模板定义和实际参数类型生成具体的函数版本。模板的实例化是自动的，无需程序员显式地创建不同类型的函数。

**示例**：
```cpp
int main() {
    int a = 5, b = 10;
    double x = 5.5, y = 10.5;

    // 自动实例化
    std::cout << max(a, b) << std::endl; // 输出 10
    std::cout << max(x, y) << std::endl; // 输出 10.5

    return 0;
}
```
在这个示例中，`max` 函数模板会自动实例化成 `max<int>` 和 `max<double>` 两个版本。

### 3. **模板参数的类型**

函数模板可以接受多种类型参数，包括基本类型、用户定义的类型以及指针类型等。

**示例**：
```cpp
template <typename T>
void printArray(T arr[], int size) {
    for (int i = 0; i < size; ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;
}
```
在这个示例中，`printArray` 函数模板可以打印任意类型的数组。

### 4. **函数模板的重载**

函数模板可以与普通函数或其他模板函数一起重载。编译器会根据参数的类型和数量来选择具体的函数版本。

**示例**：
```cpp
template <typename T>
void display(T value) {
    std::cout << value << std::endl;
}

void display(int value) {
    std::cout << "Integer: " << value << std::endl;
}

int main() {
    display(10);         // 调用普通函数
    display(3.14);       // 调用模板函数
    return 0;
}
```
在这个示例中，`display` 有两个版本，一个是普通函数，一个是模板函数。编译器会根据传递的参数类型选择合适的版本。

### 5. **模板特化**

函数模板可以通过完全特化或偏特化来处理特定的类型组合。特化允许为特定类型提供特殊的实现。

#### 5.1 **完全特化**

完全特化为模板的某个特定类型提供特殊的实现。

**示例**：
```cpp
template <>
void printArray<bool>(bool arr[], int size) {
    for (int i = 0; i < size; ++i) {
        std::cout << (arr[i] ? "true" : "false") << " ";
    }
    std::cout << std::endl;
}
```
在这个示例中，`printArray` 对 `bool` 类型进行了完全特化，以提供特殊的打印方式。

#### 5.2 **偏特化**

偏特化为模板的某些类型组合提供特殊的实现。

**示例**：
```cpp
template <typename T, typename U>
class Pair {
    T first;
    U second;
public:
    Pair(T f, U s) : first(f), second(s) {}
    T getFirst() { return first; }
    U getSecond() { return second; }
};

template <typename T>
class Pair<T, T> {
    T first;
    T second;
public:
    Pair(T f, T s) : first(f), second(s) {}
    T getFirst() { return first; }
    T getSecond() { return second; }
};
```
在这个示例中，`Pair` 类模板对 `T` 和 `U` 类型的不同组合进行了偏特化。当两个类型相同时，`Pair<T, T>` 提供了特殊的实现。

### 6. **模板的优势**

- **代码复用**：函数模板允许编写可以处理多种数据类型的通用函数，减少了代码重复。
- **类型安全**：模板提供了编译时类型检查，避免了运行时类型错误。
- **灵活性**：通过模板，函数可以适应不同的类型，增强了代码的灵活性和扩展性。

### 7. **总结**

函数模板是 C++ 中强大的泛型编程工具，允许编写通用的、类型安全的代码。理解函数模板的定义、实例化、重载、特化及其优势，对于编写高效、灵活的 C++ 代码至关重要。通过合理使用函数模板，程序员可以显著提升代码的复用性和可维护性。