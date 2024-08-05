## 模板的基本概念

C++ 模板是一种强大的语言特性，允许在编写代码时指定类型或值，从而创建可以处理多种数据类型的通用代码。模板在 C++ 中主要用于泛型编程，使得程序员可以编写更灵活和可重用的代码。以下是模板的基本概念：

### 1. **模板的定义**

模板有两种主要类型：**函数模板** 和 **类模板**。它们允许代码在编译时根据提供的类型进行生成。

#### 1.1 **函数模板**

函数模板用于创建可以接受不同类型参数的函数。通过函数模板，您可以定义一个函数的通用版本，然后在调用时根据实际参数类型生成特定版本的函数。

**示例**：
```cpp
template <typename T>
T max(T a, T b) {
    return (a > b) ? a : b;
}
```

在上面的示例中，`max` 是一个函数模板，它接受两个相同类型的参数并返回较大的值。编译器会根据传递的参数类型实例化具体的函数版本，例如 `max<int>(3, 5)` 和 `max<double>(3.5, 2.1)`。

#### 1.2 **类模板**

类模板用于创建可以处理不同数据类型的类。类模板允许定义类的通用结构，然后根据实际类型生成特定的类实例。

**示例**：
```cpp
template <typename T>
class Stack {
private:
    std::vector<T> elements;
public:
    void push(const T& element) {
        elements.push_back(element);
    }
    
    T pop() {
        if (elements.empty()) {
            throw std::out_of_range("Stack<>::pop(): empty stack");
        }
        T elem = elements.back();
        elements.pop_back();
        return elem;
    }
};
```

在上面的示例中，`Stack` 是一个类模板，它使用 `T` 作为元素类型。可以创建 `Stack<int>`、`Stack<double>` 等具体类型的栈。

### 2. **模板的实例化**

当模板被实际使用时，编译器会实例化模板，即根据模板定义和提供的实际类型或值生成具体的代码。这一过程发生在编译时，编译器根据实际类型生成相应的代码。

### 3. **模板参数**

模板参数可以是类型参数或非类型参数。

#### 3.1 **类型参数**

类型参数用于指定模板中使用的数据类型。例如，在以下函数模板中，`T` 是一个类型参数：
```cpp
template <typename T>
void print(const T& value) {
    std::cout << value << std::endl;
}
```

#### 3.2 **非类型参数**

非类型参数可以是整数、枚举值等常量。这些参数用于指定模板中的具体值。例如：
```cpp
template <int size>
class Array {
private:
    int data[size];
public:
    int& operator[](int index) {
        return data[index];
    }
};
```

在上面的示例中，`size` 是一个非类型参数，用于定义数组的大小。

### 4. **模板特化**

模板特化允许为特定类型或值提供模板的特殊实现。特化分为完全特化和偏特化。

#### 4.1 **完全特化**

完全特化为模板的特定类型提供完整的实现。例如：
```cpp
template <>
class Stack<bool> {
private:
    std::vector<bool> elements;
public:
    void push(const bool& element) {
        elements.push_back(element);
    }
    
    bool pop() {
        if (elements.empty()) {
            throw std::out_of_range("Stack<>::pop(): empty stack");
        }
        bool elem = elements.back();
        elements.pop_back();
        return elem;
    }
};
```

#### 4.2 **偏特化**

偏特化为模板的特定类型组合提供部分特定实现。例如：
```cpp
template <typename T>
class Stack<T*> {
private:
    std::vector<T*> elements;
public:
    void push(T* element) {
        elements.push_back(element);
    }
    
    T* pop() {
        if (elements.empty()) {
            throw std::out_of_range("Stack<>::pop(): empty stack");
        }
        T* elem = elements.back();
        elements.pop_back();
        return elem;
    }
};
```

### 5. **模板的优势**

- **代码重用**：模板使得代码可以处理多种类型，从而减少了重复代码的编写。
- **类型安全**：模板提供了编译时类型检查，避免了运行时错误。
- **灵活性**：通过模板，可以在编译时根据实际类型生成代码，增强了程序的灵活性。

### 6. **总结**

C++ 模板是强大的泛型编程工具，使得程序员可以编写通用的、高效的代码。了解模板的基本概念、参数、实例化和特化是掌握 C++ 编程的重要部分。通过模板，程序员可以创建高性能、类型安全的代码，提高代码的复用性和灵活性。