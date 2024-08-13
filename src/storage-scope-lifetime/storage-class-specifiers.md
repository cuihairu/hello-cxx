# C++存储类说明符

#### **1.1 存储类简介**
- **定义与目的**
  - 存储类说明符用于指定变量的存储类型、生命周期以及作用域。
  - 主要包括 `auto`、`static`、`thread_local` 和 `extern` 等。

#### **1.2 自动存储持续时间（`auto`）**
- **定义**
  - `auto` 存储类说明符用于声明一个局部变量，变量的生命周期在其所在的块内。
  - 默认情况下，局部变量即为自动存储类型，无需显式使用 `auto`，C++11 起 `auto` 主要用于类型推导。
- **用法**
  ```cpp
  void function() {
      auto x = 5; // 自动推导为 int
      // x 的生命周期仅在 function 内
  }
  ```
- **示例**
  ```cpp
  void example() {
      auto x = 10; // x 是自动存储类型，局部变量
  }
  ```

#### **1.3 静态存储持续时间（`static`）**
- **定义**
  - `static` 存储类说明符用于声明变量或函数，使其具有静态存储持续时间。
  - 变量在程序运行期间一直存在，但其作用域依赖于声明位置。
- **函数内部的 `static` 变量**
  - 仅在声明所在的函数内可见，但其生命周期贯穿整个程序运行。
  ```cpp
  void function() {
      static int counter = 0; // 只初始化一次
      counter++;
      // counter 的值会在多次调用中保留
  }
  ```
- **类中的 `static` 成员**
  - 类的静态成员变量在所有类的实例之间共享。
  ```cpp
  class MyClass {
  public:
      static int count; // 类的静态成员
  };
  
  int MyClass::count = 0; // 静态成员的定义
  ```

#### **1.4 线程存储持续时间（`thread_local`）**
- **定义**
  - `thread_local` 存储类说明符用于声明线程局部存储变量，每个线程都有独立的副本。
- **用法**
  ```cpp
  void function() {
      thread_local int counter = 0; // 每个线程有独立的 counter
      counter++;
  }
  ```
- **示例**
  ```cpp
  void example() {
      thread_local int value = 0;
      // value 在每个线程中独立存在
  }
  ```

#### **1.5 动态存储持续时间（`new`/`delete`）**
- **定义**
  - 动态存储持续时间是通过动态内存分配（`new`）和释放（`delete`）来管理的。
- **用法**
  ```cpp
  void function() {
      int* p = new int; // 分配动态内存
      *p = 5;
      delete p; // 释放内存
  }
  ```
- **示例**
  ```cpp
  void example() {
      int* p = new int(10); // 动态分配
      // 使用 p
      delete p; // 释放内存
  }
  ```

#### **1.6 存储类比较**
- **总结**
  - `auto` 用于局部变量，默认存储类型。
  - `static` 使变量在整个程序运行期间存在，但作用域有限。
  - `thread_local` 提供线程局部存储，适用于多线程环境。
  - 动态存储持续时间通过 `new`/`delete` 实现，适合动态管理内存。

#### **附录**
- **存储类说明符的历史与演变**
  - `auto` 从 C++11 起引入类型推导功能。
  - `thread_local` 从 C++11 起标准化。

