# 特殊成员函数

特殊成员函数是 C++ 中一些具有特殊用途的成员函数，它们在类的定义中自动生成，用于处理对象的生命周期和内存管理。以下是 C++ 中几种主要的特殊成员函数及其作用：

#### ** 默认构造函数**

- **定义**
  - 默认构造函数是没有参数的构造函数。
  - 如果用户没有定义构造函数，编译器会自动生成一个默认构造函数。
  - 用于初始化对象的成员变量。
  ```cpp
  class MyClass {
  public:
      MyClass() { } // 默认构造函数
  };
  ```

- **示例**
  ```cpp
  MyClass obj; // 调用默认构造函数
  ```

#### ** 拷贝构造函数**

- **定义**
  - 拷贝构造函数用于复制一个对象到另一个对象。
  - 函数的参数是对同一类对象的引用。
  - 如果类没有自定义拷贝构造函数，编译器会自动生成一个。
  ```cpp
  class MyClass {
  public:
      MyClass(const MyClass& other) { } // 拷贝构造函数
  };
  ```

- **示例**
  ```cpp
  MyClass obj1;
  MyClass obj2 = obj1; // 调用拷贝构造函数
  ```

#### ** 复制赋值操作符**

- **定义**
  - 复制赋值操作符用于将一个对象的值赋给另一个已存在的对象。
  - 函数的返回类型是 `MyClass&`，参数是对同一类对象的引用。
  ```cpp
  class MyClass {
  public:
      MyClass& operator=(const MyClass& other) { return *this; } // 复制赋值操作符
  };
  ```

- **示例**
  ```cpp
  MyClass obj1, obj2;
  obj2 = obj1; // 调用复制赋值操作符
  ```

#### ** 移动构造函数**

- **定义**
  - 移动构造函数用于通过“移动”资源而不是复制资源来初始化对象。
  - 函数的参数是对同一类对象的右值引用。
  ```cpp
  class MyClass {
  public:
      MyClass(MyClass&& other) noexcept { } // 移动构造函数
  };
  ```

- **示例**
  ```cpp
  MyClass obj1;
  MyClass obj2 = std::move(obj1); // 调用移动构造函数
  ```

#### ** 移动赋值操作符**

- **定义**
  - 移动赋值操作符用于将一个对象的资源转移到另一个已存在的对象。
  - 函数的返回类型是 `MyClass&`，参数是对同一类对象的右值引用。
  ```cpp
  class MyClass {
  public:
      MyClass& operator=(MyClass&& other) noexcept { return *this; } // 移动赋值操作符
  };
  ```

- **示例**
  ```cpp
  MyClass obj1, obj2;
  obj2 = std::move(obj1); // 调用移动赋值操作符
  ```

#### ** 析构函数**

- **定义**
  - 析构函数用于在对象生命周期结束时执行清理操作。
  - 析构函数没有参数且没有返回值。
  ```cpp
  class MyClass {
  public:
      ~MyClass() { } // 析构函数
  };
  ```

- **示例**
  ```cpp
  void function() {
      MyClass obj; // 析构函数在对象超出作用域时被调用
  }
  ```

#### ** 默认与删除**

- **定义**
  - 可以使用 `default` 关键字显式声明特殊成员函数的默认实现。
  - 可以使用 `delete` 关键字删除特殊成员函数，防止编译器生成默认实现。
  ```cpp
  class MyClass {
  public:
      MyClass() = default; // 默认构造函数
      MyClass(const MyClass&) = delete; // 删除拷贝构造函数
  };
  ```

- **示例**
  ```cpp
  MyClass obj1; // 调用默认构造函数
  // MyClass obj2 = obj1; // 编译错误: 拷贝构造函数被删除
  ```

#### ** 最佳实践**

- **合理定义特殊成员函数**
  - 如果类管理动态资源（如内存），则自定义拷贝构造函数、拷贝赋值操作符、移动构造函数和移动赋值操作符，确保正确管理资源。
  - 如果类不需要复制或移动功能，可以显式删除这些函数，防止不必要的复制或移动操作。

- **遵循规则**
  - **Rule of Three**: 如果需要自定义析构函数、拷贝构造函数或复制赋值操作符中的任何一个，通常需要自定义其他两个。
  - **Rule of Five**: 如果需要自定义上述三者中的任何一个，还需要自定义移动构造函数和移动赋值操作符。
  - **Rule of Zero**: 尽量避免自定义这些特殊成员函数，尽可能使用智能指针和其他资源管理工具来自动管理资源。

