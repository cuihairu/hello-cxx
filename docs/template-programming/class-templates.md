## 类模板

类模板是 C++ 泛型编程的一个核心特性，它允许定义一个类的通用版本，使其能够处理不同的数据类型。类模板使得我们可以创建可重用的类，这些类在使用时可以根据实际的数据类型进行具体化，从而避免了重复编写类似的类。以下是类模板的详细介绍：

### 1. **类模板的定义**

类模板的定义语法如下：
```cpp
template <typename T>
class ClassName {
    T member;
public:
    ClassName(T val) : member(val) {}
    T getValue() const { return member; }
    void setValue(T val) { member = val; }
};
```
其中，`template <typename T>` 声明了一个模板，`T` 是一个类型参数。`ClassName` 是类模板的名称，`T` 用作类中的数据类型。

**示例**：
```cpp
template <typename T>
class Box {
    T value;
public:
    Box(T v) : value(v) {}
    T getValue() const { return value; }
    void setValue(T v) { value = v; }
};
```
在这个示例中，`Box` 是一个类模板，它使用模板参数 `T` 来定义一个可以存储任何类型值的容器。

### 2. **类模板的实例化**

类模板的实例化是指在编译时，根据实际提供的类型生成具体的类。每当使用模板类时，编译器都会生成相应类型的具体实现。

**示例**：
```cpp
int main() {
    Box<int> intBox(10);      // 实例化为 Box<int>
    Box<double> doubleBox(3.14); // 实例化为 Box<double>

    std::cout << intBox.getValue() << std::endl;    // 输出 10
    std::cout << doubleBox.getValue() << std::endl; // 输出 3.14

    return 0;
}
```
在这个示例中，`Box` 类模板分别被实例化为 `Box<int>` 和 `Box<double>` 两种类型。

### 3. **类模板的成员函数**

类模板可以有成员函数，并且这些成员函数也可以使用模板参数。成员函数可以定义在类内部或外部。

**内部定义示例**：
```cpp
template <typename T>
class Calculator {
public:
    T add(T a, T b) { return a + b; }
    T subtract(T a, T b) { return a - b; }
};
```

**外部定义示例**：
```cpp
template <typename T>
class Calculator {
public:
    T add(T a, T b);
    T subtract(T a, T b);
};

template <typename T>
T Calculator<T>::add(T a, T b) {
    return a + b;
}

template <typename T>
T Calculator<T>::subtract(T a, T b) {
    return a - b;
}
```
在这个示例中，`Calculator` 类模板有两个成员函数 `add` 和 `subtract`，它们被定义在类外部。

### 4. **模板参数的多个类型**

类模板可以接受多个类型参数，这使得我们能够定义更复杂的模板类。

**示例**：
```cpp
template <typename T1, typename T2>
class Pair {
    T1 first;
    T2 second;
public:
    Pair(T1 f, T2 s) : first(f), second(s) {}
    T1 getFirst() const { return first; }
    T2 getSecond() const { return second; }
};
```
在这个示例中，`Pair` 类模板接受两个类型参数 `T1` 和 `T2`，可以存储两个不同类型的值。

### 5. **类模板的特化**

类模板可以通过完全特化和偏特化来处理特定的类型组合或数据模式。

#### 5.1 **完全特化**

完全特化为模板的某个特定类型提供特殊的实现。

**示例**：
```cpp
template <>
class Pair<int, int> {
    int first;
    int second;
public:
    Pair(int f, int s) : first(f), second(s) {}
    int sum() const { return first + second; }
};
```
在这个示例中，`Pair<int, int>` 提供了一个特殊的实现，用于存储和计算两个整数的和。

#### 5.2 **偏特化**

偏特化为模板的某些类型组合提供特殊的实现。

**示例**：
```cpp
template <typename T>
class Wrapper {
    T value;
public:
    Wrapper(T v) : value(v) {}
    T getValue() const { return value; }
};

// 偏特化: 对于指针类型
template <typename T>
class Wrapper<T*> {
    T* value;
public:
    Wrapper(T* v) : value(v) {}
    T* getValue() const { return value; }
};
```
在这个示例中，`Wrapper` 类模板对指针类型进行了偏特化，提供了不同的实现。

### 6. **模板的优势**

- **代码复用**：类模板允许编写通用的类，避免了重复编写类似的类。
- **类型安全**：模板提供了编译时类型检查，避免了运行时类型错误。
- **灵活性**：类模板能够处理多种类型，提高了代码的灵活性和扩展性。

### 7. **总结**

类模板是 C++ 中强大的泛型编程工具，它允许定义通用的类，可以处理多种数据类型。理解类模板的定义、实例化、成员函数、特化等概念，对于编写高效、可重用的 C++ 代码至关重要。通过合理使用类模板，程序员可以显著提高代码的灵活性和可维护性。