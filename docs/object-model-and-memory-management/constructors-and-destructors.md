## 构造函数与析构函数

在 C++ 中，构造函数和析构函数是类的一部分，分别用于初始化和清理对象。它们在对象的生命周期管理中扮演着关键角色。

### 1. **构造函数**

构造函数（Constructor）是一个特殊的成员函数，在对象创建时自动调用，用于初始化对象。构造函数的名称与类名相同，并且没有返回类型。

#### 1.1 **默认构造函数**

默认构造函数没有参数，如果用户没有定义任何构造函数，编译器会自动生成一个默认构造函数。

```cpp
#include <iostream>

class Example {
public:
    Example() {
        std::cout << "Default Constructor called" << std::endl;
    }
};

int main() {
    Example obj;
    return 0;
}
```

#### 1.2 **参数化构造函数**

参数化构造函数接受参数，可以根据提供的值来初始化对象。

```cpp
#include <iostream>

class Example {
public:
    int value;
    Example(int v) : value(v) {
        std::cout << "Parameterized Constructor called with value: " << value << std::endl;
    }
};

int main() {
    Example obj(42);
    return 0;
}
```

#### 1.3 **拷贝构造函数**

拷贝构造函数用于创建一个新对象，该对象是现有对象的副本。它接受现有对象的引用作为参数。

```cpp
#include <iostream>

class Example {
public:
    int value;
    Example(int v) : value(v) {}
    Example(const Example& other) : value(other.value) {
        std::cout << "Copy Constructor called" << std::endl;
    }
};

int main() {
    Example obj1(42);
    Example obj2 = obj1;
    return 0;
}
```

#### 1.4 **移动构造函数**

移动构造函数用于实现资源的转移，从而避免不必要的拷贝操作。它接受一个右值引用作为参数。

```cpp
#include <iostream>
#include <utility>

class Example {
public:
    int* data;
    Example(int value) : data(new int(value)) {}
    Example(Example&& other) noexcept : data(other.data) {
        other.data = nullptr;
        std::cout << "Move Constructor called" << std::endl;
    }
    ~Example() {
        delete data;
    }
};

int main() {
    Example obj1(42);
    Example obj2 = std::move(obj1);
    return 0;
}
```

### 2. **析构函数**

析构函数（Destructor）是一个特殊的成员函数，在对象销毁时自动调用，用于释放资源。析构函数的名称与类名相同，前面加上 `~`，并且没有参数和返回类型。

```cpp
#include <iostream>

class Example {
public:
    Example() {
        std::cout << "Constructor called" << std::endl;
    }
    ~Example() {
        std::cout << "Destructor called" << std::endl;
    }
};

int main() {
    Example obj;
    return 0;
}
```

### 3. **构造函数与析构函数的调用顺序**

构造函数与析构函数的调用顺序遵循以下规则：

- 构造函数按照声明顺序初始化成员变量。
- 析构函数按照与构造函数相反的顺序销毁成员变量。
- 基类构造函数在派生类构造函数之前调用。
- 基类析构函数在派生类析构函数之后调用。

```cpp
#include <iostream>

class Base {
public:
    Base() {
        std::cout << "Base Constructor called" << std::endl;
    }
    ~Base() {
        std::cout << "Base Destructor called" << std::endl;
    }
};

class Derived : public Base {
public:
    Derived() {
        std::cout << "Derived Constructor called" << std::endl;
    }
    ~Derived() {
        std::cout << "Derived Destructor called" << std::endl;
    }
};

int main() {
    Derived obj;
    return 0;
}
```

### 4. **总结**

构造函数和析构函数是 C++ 类中用于管理对象生命周期的核心机制。通过理解和正确使用这些函数，程序员可以确保对象在创建和销毁过程中正确地初始化和清理资源，从而提高程序的稳定性和性能。
