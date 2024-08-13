# 存储类型与生命周期

#### **存储类型**

存储类型指的是变量在程序中的存储位置和生命周期。C++中主要有以下几种存储类型：

- **静态存储类型（Static Storage Duration）**
  - 变量在程序启动时被分配内存，程序结束时释放。
  - 包括 `static` 和 `extern` 变量。
  - 例如，静态全局变量、静态局部变量、类的静态成员。
  ```cpp
  static int staticVar = 0; // 静态存储类型变量

  void function() {
      static int staticLocalVar = 0; // 函数内的静态存储类型变量
  }
  ```

- **自动存储类型（Automatic Storage Duration）**
  - 变量在其声明的块内被创建，块退出时销毁。
  - 默认情况下，局部变量为自动存储类型。
  ```cpp
  void function() {
      int autoVar = 10; // 自动存储类型变量
  }
  ```

- **线程存储类型（Thread Storage Duration）**
  - 变量在每个线程中都有独立的副本。
  - 使用 `thread_local` 关键字声明线程局部存储。
  ```cpp
  void function() {
      thread_local int threadLocalVar = 0; // 线程存储类型变量
  }
  ```

- **动态存储类型（Dynamic Storage Duration）**
  - 变量在运行时通过动态内存分配（`new`）创建，使用 `delete` 释放。
  - 适用于需要在程序运行时动态管理的对象。
  ```cpp
  void function() {
      int* dynamicVar = new int; // 动态存储类型变量
      delete dynamicVar; // 释放内存
  }
  ```

#### **生命周期**

生命周期指的是变量存在并可用的时间段。C++中变量的生命周期主要分为以下几种：

- **静态存储类型变量的生命周期**
  - 从程序启动到程序结束。
  - 不论是全局静态变量、类的静态成员，还是函数内的静态变量，均有相同的生命周期。
  ```cpp
  static int staticVar = 0; // 生命周期从程序开始到结束
  ```

- **自动存储类型变量的生命周期**
  - 从变量声明开始，到所在代码块（函数、循环等）结束。
  - 仅在声明的块内有效。
  ```cpp
  void function() {
      int autoVar = 10; // 生命周期仅在 function 内
  }
  ```

- **线程存储类型变量的生命周期**
  - 每个线程有独立的副本，从线程创建到线程结束。
  ```cpp
  void function() {
      thread_local int threadLocalVar = 0; // 每个线程中独立的生命周期
  }
  ```

- **动态存储类型变量的生命周期**
  - 从分配开始，到显式释放（`delete`）或程序结束时自动释放。
  ```cpp
  void function() {
      int* dynamicVar = new int; // 生命周期由用户管理
      delete dynamicVar; // 用户显式释放内存
  }
  ```

#### **3.3 示例**

- **静态存储类型示例**
  ```cpp
  static int staticVar = 5; // 静态存储类型，全局范围
  void function() {
      static int staticLocalVar = 10; // 静态存储类型，局部范围
      staticLocalVar++;
  }
  ```

- **自动存储类型示例**
  ```cpp
  void function() {
      int autoVar = 5; // 自动存储类型，生命周期仅在函数内部
  }
  ```

- **线程存储类型示例**
  ```cpp
  void threadFunction() {
      thread_local int threadLocalVar = 0; // 线程局部存储，每个线程有独立副本
      threadLocalVar++;
  }
  ```

- **动态存储类型示例**
  ```cpp
  void function() {
      int* dynamicVar = new int; // 动态存储类型，由用户显式管理
      *dynamicVar = 5;
      delete dynamicVar; // 释放内存
  }
  ```

#### **3.4 最佳实践**

- **选择合适的存储类型**
  - 根据变量的使用场景选择适当的存储类型（例如，静态存储类型用于需要跨函数调用保持状态的变量，自动存储类型用于临时计算）。

- **管理生命周期**
  - 对于动态存储类型变量，确保在不再使用时及时释放内存，防止内存泄漏。
  - 对于线程存储类型变量，理解线程的生命周期，并确保线程安全。

