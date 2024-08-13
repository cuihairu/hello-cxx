# 可见性与访问控制

#### ** 可见性**

可见性指的是程序中变量、函数或类成员的可访问性。C++提供了不同的机制来控制这些实体的可见性：

- **内部可见性**
  - 通过 `static` 关键字修饰的变量或函数具有内部可见性，仅在定义它的源文件中可见。
  - 内部可见性有助于隐藏实现细节，避免与其他文件中的符号冲突。
  ```cpp
  // file1.cpp
  static int internalVar = 0; // 仅在 file1.cpp 内可见
  
  static void internalFunction() { } // 仅在 file1.cpp 内可见
  ```

- **外部可见性**
  - 默认情况下，变量和函数具有外部可见性，可以在多个源文件之间共享。
  - 使用 `extern` 关键字声明外部变量或函数，指示它在其他源文件中定义。
  ```cpp
  // file1.cpp
  int externalVar = 1; // 外部可见
  
  // file2.cpp
  extern int externalVar; // 声明外部变量
  ```

#### ** 访问控制**

访问控制决定了对类成员的访问权限。C++ 提供了三种主要的访问控制修饰符：

- **`public`**
  - `public` 成员可以被任何函数访问，无论其定义在类内还是类外。
  - 常用于接口部分，提供类的公共 API。
  ```cpp
  class MyClass {
  public:
      int publicVar; // 公共成员
      void publicMethod(); // 公共方法
  };
  ```

- **`protected`**
  - `protected` 成员只能被类本身和其派生类访问，不能被其他代码直接访问。
  - 常用于需要在继承关系中共享数据，但不希望外部代码访问的情况。
  ```cpp
  class Base {
  protected:
      int protectedVar; // 受保护成员
  };
  
  class Derived : public Base {
      void method() {
          protectedVar = 10; // 派生类可以访问
      }
  };
  ```

- **`private`**
  - `private` 成员只能在类内部访问，外部代码和派生类无法直接访问。
  - 常用于封装，实现数据隐藏，保护类内部的状态。
  ```cpp
  class MyClass {
  private:
      int privateVar; // 私有成员
  public:
      void setPrivateVar(int value) { privateVar = value; } // 公共接口
  };
  ```

#### ** 示例**

- **`public` 成员示例**
  ```cpp
  class MyClass {
  public:
      int publicVar; // 公开成员，任何地方可以访问
  };
  
  void function() {
      MyClass obj;
      obj.publicVar = 5; // 直接访问公共成员
  }
  ```

- **`protected` 成员示例**
  ```cpp
  class Base {
  protected:
      int protectedVar; // 受保护成员
  };
  
  class Derived : public Base {
  public:
      void method() {
          protectedVar = 10; // 派生类可以访问
      }
  };
  ```

- **`private` 成员示例**
  ```cpp
  class MyClass {
  private:
      int privateVar; // 私有成员
  public:
      void setPrivateVar(int value) { privateVar = value; } // 公共接口
  };
  
  void function() {
      MyClass obj;
      // obj.privateVar = 5; // 编译错误: 不能访问私有成员
      obj.setPrivateVar(5); // 通过公共接口访问私有成员
  }
  ```

#### ** 最佳实践**

- **合理使用访问控制**
  - 使用 `public` 修饰符暴露类的接口部分。
  - 使用 `protected` 修饰符在继承关系中共享数据，但避免过度暴露。
  - 使用 `private` 修饰符隐藏实现细节，确保类的封装性。

- **封装**
  - 封装是面向对象编程的核心原则之一，隐藏类内部的实现细节，提供清晰的公共接口。

