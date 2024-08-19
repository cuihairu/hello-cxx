## 类与对象的基本概念

类和对象是 C++ 面向对象编程（OOP）的核心概念。通过类和对象，程序员可以创建结构化和可重用的代码，模拟现实世界的实体，并实现抽象和封装。

### 1. **类的定义**

类是 C++ 中的一个用户定义的数据类型，它封装了数据（成员变量）和操作这些数据的函数（成员函数）。类提供了一种机制，用于将数据和操作封装在一起，从而实现数据的抽象和封装。

#### 1.1 **类的基本结构**

```cpp
class MyClass {
public:
    // 成员变量
    int data;

    // 成员函数
    void setData(int value) {
        data = value;
    }

    int getData() const {
        return data;
    }
};
```

在这个示例中，`MyClass` 是一个类，它包含一个数据成员 `data` 和两个成员函数 `setData` 和 `getData`。`public` 访问修饰符使这些成员对类的外部可见。

### 2. **对象的创建与使用**

对象是类的实例，通过类的构造函数创建。对象具有类定义的属性和行为。

#### 2.1 **创建对象**

```cpp
int main() {
    MyClass obj; // 创建一个 MyClass 的对象
    obj.setData(10); // 调用成员函数
    std::cout << obj.getData() << std::endl; // 输出: 10
}
```

在这个示例中，`obj` 是 `MyClass` 的一个对象。使用 `setData` 函数设置 `data` 的值，并使用 `getData` 函数获取该值。

### 3. **构造函数与析构函数**

#### 3.1 **构造函数**

构造函数是特殊的成员函数，在创建对象时自动调用，用于初始化对象。构造函数的名称与类名相同，并且没有返回值。

```cpp
class MyClass {
public:
    int data;

    // 构造函数
    MyClass(int value) : data(value) {
    }
};
```

在这个示例中，`MyClass` 包含一个接受 `int` 类型参数的构造函数，该构造函数初始化 `data` 成员变量。

#### 3.2 **析构函数**

析构函数是另一种特殊的成员函数，在对象生命周期结束时自动调用，用于清理资源。析构函数的名称是类名之前加上 `~` 符号。

```cpp
class MyClass {
public:
    MyClass() {
        // 构造函数
    }

    ~MyClass() {
        // 析构函数
    }
};
```

### 4. **访问控制**

类中的成员可以通过不同的访问修饰符（`public`、`protected` 和 `private`）控制其可见性。

#### 4.1 **`public`**

`public` 成员可以从类的外部访问。通常用于类的接口部分。

#### 4.2 **`protected`**

`protected` 成员只能在类内部和继承自该类的派生类中访问。用于提供类内部的访问权限。

#### 4.3 **`private`**

`private` 成员只能在类内部访问。用于隐藏数据，确保数据的封装性。

### 5. **数据封装**

数据封装是 OOP 的一个重要特性，通过隐藏内部实现细节，只暴露必要的接口来操作数据，从而保护数据的完整性和安全性。类的 `private` 和 `protected` 成员就是为了实现数据封装。

### 6. **成员函数**

成员函数是定义在类内部的函数，用于操作类的成员变量。成员函数可以访问类的私有数据，并可以是公有、保护或私有的。

#### 6.1 **普通成员函数**

```cpp
void printData() const {
    std::cout << data << std::endl;
}
```

#### 6.2 **常量成员函数**

常量成员函数不会修改类的成员变量，声明时在函数末尾加上 `const` 关键字。

### 7. **类的继承**

类可以从其他类继承，继承是实现代码重用和建立类之间关系的机制。派生类继承基类的成员，能够扩展或修改基类的行为。

#### 7.1 **继承示例**

```cpp
class Base {
public:
    void baseFunction() {
        std::cout << "Base function" << std::endl;
    }
};

class Derived : public Base {
public:
    void derivedFunction() {
        std::cout << "Derived function" << std::endl;
    }
};
```

在这个示例中，`Derived` 类继承自 `Base` 类，并可以访问 `Base` 类的公有成员 `baseFunction`。

### 8. **总结**

类和对象是 C++ 面向对象编程的核心概念，通过类的定义和对象的创建，我们可以实现数据的封装、继承和多态，进而编写更加结构化和模块化的代码。这些概念为 C++ 提供了强大的抽象能力和代码重用性，是编写高质量 C++ 程序的基础。
