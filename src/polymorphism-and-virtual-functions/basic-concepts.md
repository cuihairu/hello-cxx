## 多态的基本概念

多态（Polymorphism）是面向对象编程的一个核心概念，它允许相同的操作作用于不同的对象上，并在不同的对象上表现出不同的行为。C++ 中的多态性主要通过虚函数（virtual function）和继承（inheritance）来实现。

### 1. **多态的类型**

C++ 支持两种类型的多态：编译时多态和运行时多态。

#### 1.1 **编译时多态**

编译时多态主要通过函数重载（function overloading）和运算符重载（operator overloading）来实现。在编译时，编译器根据函数的签名或操作数的类型选择合适的函数或运算符。

```cpp
#include <iostream>

void print(int i) {
    std::cout << "Integer: " << i << std::endl;
}

void print(double d) {
    std::cout << "Double: " << d << std::endl;
}

int main() {
    print(5);      // 调用 print(int)
    print(3.14);   // 调用 print(double)
    return 0;
}
```

#### 1.2 **运行时多态**

运行时多态通过基类指针或引用调用派生类的重写函数来实现。运行时多态性是通过虚函数来实现的，虚函数使得派生类可以重写基类中的函数。

```cpp
#include <iostream>

class Base {
public:
    virtual void show() {
        std::cout << "Base class" << std::endl;
    }
};

class Derived : public Base {
public:
    void show() override {
        std::cout << "Derived class" << std::endl;
    }
};

void display(Base& obj) {
    obj.show();  // 调用的函数取决于传入对象的类型
}

int main() {
    Base b;
    Derived d;
    display(b);  // 调用 Base::show
    display(d);  // 调用 Derived::show
    return 0;
}
```

### 2. **虚函数**

虚函数是通过在基类中使用关键字 `virtual` 来声明的函数。派生类可以重写这个函数，从而实现不同的行为。通过基类指针或引用调用虚函数时，会根据对象的实际类型调用相应的重写函数，这就是多态的体现。

#### 2.1 **虚函数表**

当一个类包含虚函数时，编译器会为这个类生成一个虚函数表（vtable）。虚函数表中存储了类的虚函数指针。当通过基类指针或引用调用虚函数时，实际调用的是虚函数表中指向的函数。

### 3. **纯虚函数和抽象类**

纯虚函数是一种特殊的虚函数，它在基类中没有实现，需要在派生类中重写。包含纯虚函数的类称为抽象类，不能实例化，只能作为基类使用。

```cpp
#include <iostream>

class AbstractBase {
public:
    virtual void display() = 0;  // 纯虚函数
};

class ConcreteDerived : public AbstractBase {
public:
    void display() override {
        std::cout << "ConcreteDerived class" << std::endl;
    }
};

int main() {
    // AbstractBase a;  // 错误：不能实例化抽象类
    ConcreteDerived d;
    AbstractBase& ref = d;
    ref.display();  // 调用 ConcreteDerived::display
    return 0;
}
```

### 4. **多态的优点**

- **代码复用**：通过基类指针或引用，可以编写通用代码处理不同类型的对象。
- **灵活性**：可以在不修改现有代码的情况下，通过派生类扩展新功能。
- **可扩展性**：通过继承和重写，能够轻松添加新功能或修改现有行为。

### 5. **多态的应用场景**

- **接口设计**：通过抽象类和纯虚函数定义接口，派生类实现具体功能。
- **多态容器**：在容器中存储基类指针，可以处理不同类型的派生类对象。
- **回调函数**：使用虚函数实现回调机制，在运行时动态确定函数行为。

### 6. **总结**

多态是 C++ 面向对象编程的重要特性，通过虚函数和继承实现。它使得相同的操作可以作用于不同的对象，并在不同对象上表现出不同的行为，从而提高代码的灵活性和可扩展性。在实际编程中，合理使用多态可以编写出更简洁、可维护性更高的代码。