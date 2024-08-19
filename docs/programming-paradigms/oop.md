## 面向对象编程

面向对象编程（OOP）是一种编程范式，强调将数据和操作数据的函数封装到一个统一的实体中——类。OOP 旨在提高代码的重用性、可维护性和可扩展性。C++ 是一种多范式语言，支持面向对象编程的关键特性包括封装、继承和多态。

### 1. **封装**

封装是将数据和操作这些数据的函数封装在一个类中。通过封装，可以隐藏实现细节，只暴露必要的接口给外部，从而保护数据的完整性并减少系统的复杂性。

#### 1.1 **数据隐藏**

数据隐藏通过 `private` 和 `protected` 访问修饰符实现，确保类的内部数据不被外部直接访问。只有类的成员函数可以访问这些数据。

```cpp
class MyClass {
private:
    int secretData;

public:
    void setSecretData(int value) {
        secretData = value;
    }

    int getSecretData() const {
        return secretData;
    }
};
```

在这个示例中，`secretData` 是一个私有成员，外部代码不能直接访问 `secretData`，只能通过公共成员函数 `setSecretData` 和 `getSecretData` 来访问和修改它。

### 2. **继承**

继承允许创建新类（派生类），从现有类（基类）继承成员。继承可以实现代码的重用，并建立类之间的层次结构。

#### 2.1 **继承的类型**

- **公有继承**：基类的 `public` 成员在派生类中保持 `public`，`protected` 成员保持 `protected`，`private` 成员不可访问。
- **保护继承**：基类的 `public` 和 `protected` 成员在派生类中都变成 `protected`，`private` 成员不可访问。
- **私有继承**：基类的 `public` 和 `protected` 成员在派生类中都变成 `private`，`private` 成员不可访问。

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

在这个示例中，`Derived` 类从 `Base` 类公有继承，因此可以访问 `Base` 类的公有成员 `baseFunction`。

### 3. **多态**

多态允许通过统一的接口访问不同类型的对象。C++ 的多态可以通过虚函数和继承实现。

#### 3.1 **虚函数**

虚函数是基类中的成员函数，允许派生类重新定义（覆盖）该函数。通过虚函数，可以在运行时决定调用哪个函数，从而实现多态。

```cpp
class Base {
public:
    virtual void show() {
        std::cout << "Base class show function" << std::endl;
    }
};

class Derived : public Base {
public:
    void show() override {
        std::cout << "Derived class show function" << std::endl;
    }
};
```

在这个示例中，`Base` 类的 `show` 函数是虚函数，`Derived` 类重写了该函数。通过基类指针或引用调用 `show` 函数时，实际调用的是 `Derived` 类的版本。

#### 3.2 **纯虚函数和抽象类**

纯虚函数是没有实现的虚函数，定义在基类中，派生类必须实现这些函数。包含纯虚函数的类称为抽象类，不能实例化，只能用作基类。

```cpp
class AbstractBase {
public:
    virtual void pureVirtualFunction() = 0; // 纯虚函数
};
```

在这个示例中，`AbstractBase` 类包含一个纯虚函数 `pureVirtualFunction`，`AbstractBase` 类是一个抽象类，不能直接创建对象。

### 4. **类的成员**

#### 4.1 **构造函数**

构造函数是特殊的成员函数，用于初始化对象。当创建对象时，构造函数自动调用。

```cpp
class MyClass {
public:
    MyClass(int value) : data(value) {
    }

private:
    int data;
};
```

在这个示例中，构造函数接受一个 `int` 类型的参数来初始化 `data` 成员变量。

#### 4.2 **析构函数**

析构函数是另一种特殊的成员函数，在对象销毁时自动调用，用于释放资源。

```cpp
class MyClass {
public:
    ~MyClass() {
        // 清理资源
    }
};
```

### 5. **操作符重载**

操作符重载允许自定义操作符的行为，使其可以用于自定义类型。例如，可以重载 `+` 操作符来实现两个对象的相加。

```cpp
class Vector {
public:
    Vector(int x, int y) : x(x), y(y) {}

    Vector operator+(const Vector& other) const {
        return Vector(x + other.x, y + other.y);
    }

private:
    int x, y;
};
```

### 6. **总结**

面向对象编程是 C++ 的重要编程范式，通过封装、继承和多态，可以构建结构化、模块化和可重用的代码。掌握 OOP 的基本概念和技术，对于编写高质量的 C++ 程序至关重要。
