## 纯虚函数与抽象类

纯虚函数和抽象类是 C++ 面向对象编程中的重要概念，用于定义接口和实现多态性。通过使用纯虚函数，开发者可以在基类中声明接口，而让派生类提供具体的实现。这种设计方法使代码更加灵活和可扩展。

### 1. **纯虚函数**

纯虚函数是在基类中声明但不提供实现的虚函数。纯虚函数的声明方式是在函数声明后加上 `= 0`，表示该函数在基类中没有实现，需要在派生类中进行重写。

```cpp
class Base {
public:
    virtual void display() = 0;  // 纯虚函数
};
```

纯虚函数使得基类变得不完整，因此无法直接实例化基类。

### 2. **抽象类**

包含纯虚函数的类称为抽象类。抽象类无法实例化，只能用作基类，为派生类提供一个接口。抽象类的存在目的是为不同的派生类提供统一的接口定义。

```cpp
class Base {
public:
    virtual void display() = 0;  // 纯虚函数
};

class Derived : public Base {
public:
    void display() override {
        std::cout << "Derived class display function" << std::endl;
    }
};

int main() {
    // Base b;  // 错误：无法实例化抽象类
    Derived d;
    d.display();  // 调用派生类中的 display 函数
    return 0;
}
```

### 3. **实现纯虚函数**

派生类必须重写基类中的所有纯虚函数，否则派生类也将成为抽象类，无法实例化。

```cpp
class Base {
public:
    virtual void display() = 0;  // 纯虚函数
};

class Derived : public Base {
public:
    void display() override {
        std::cout << "Derived class display function" << std::endl;
    }
};

class AnotherDerived : public Base {
public:
    void display() override {
        std::cout << "AnotherDerived class display function" << std::endl;
    }
};
```

### 4. **抽象类的用途**

抽象类通常用来定义接口，以便不同的派生类实现不同的功能。这种设计方式可以使代码更加模块化，增加可维护性和可扩展性。

例如，可以定义一个图形基类和不同的图形派生类：

```cpp
class Shape {
public:
    virtual void draw() = 0;  // 纯虚函数
};

class Circle : public Shape {
public:
    void draw() override {
        std::cout << "Drawing Circle" << std::endl;
    }
};

class Square : public Shape {
public:
    void draw() override {
        std::cout << "Drawing Square" << std::endl;
    }
};

void renderShape(Shape& shape) {
    shape.draw();
}

int main() {
    Circle c;
    Square s;
    renderShape(c);  // 绘制圆形
    renderShape(s);  // 绘制方形
    return 0;
}
```

### 5. **接口与实现分离**

通过使用纯虚函数和抽象类，可以将接口与实现分离，促进代码的重用和模块化设计。开发者可以在不修改基类的情况下扩展新功能，符合开闭原则（对扩展开放，对修改关闭）。

### 6. **总结**

纯虚函数和抽象类是 C++ 面向对象编程中的重要机制，用于定义接口和实现多态。纯虚函数声明了必须由派生类实现的接口，而抽象类则提供了一个通用的框架，不能直接实例化。通过这种机制，可以实现接口与实现的分离，增加代码的灵活性和可扩展性。