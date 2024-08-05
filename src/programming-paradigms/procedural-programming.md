## 过程式编程

过程式编程（Procedural Programming）是一种编程范式，强调通过一系列顺序执行的过程、函数或子程序来实现程序的功能。C++ 支持过程式编程，继承了其前身 C 语言的许多特点。过程式编程关注函数的调用、参数传递、变量作用域和控制流，是编写清晰和结构化代码的重要方法。

### 1. **基本概念**

过程式编程的核心是函数。函数是代码的基本组织单元，用于执行特定任务。通过函数的调用和返回，程序可以实现复杂的功能。

```cpp
#include <iostream>

void greet() {
    std::cout << "Hello, World!" << std::endl;
}

int main() {
    greet();
    return 0;
}
```

在这个示例中，`greet` 函数被定义为打印一条消息，并在 `main` 函数中被调用。

### 2. **函数定义与调用**

函数的定义包括函数名、参数列表和函数体。函数可以有返回值，也可以是 `void` 类型不返回任何值。

```cpp
#include <iostream>

int add(int a, int b) {
    return a + b;
}

int main() {
    int result = add(5, 3);
    std::cout << "Result: " << result << std::endl;
    return 0;
}
```

在这个示例中，`add` 函数接收两个整数参数，并返回它们的和。

### 3. **参数传递**

C++ 支持按值传递（pass by value）、按引用传递（pass by reference）和按指针传递（pass by pointer）三种参数传递方式。

#### 3.1 **按值传递**

按值传递会将参数的副本传递给函数，函数内部对参数的修改不会影响原始变量。

```cpp
void increment(int x) {
    x++;
}

int main() {
    int value = 5;
    increment(value);
    std::cout << "Value: " << value << std::endl; // 输出 5
    return 0;
}
```

#### 3.2 **按引用传递**

按引用传递会将参数的引用传递给函数，函数内部对参数的修改会影响原始变量。

```cpp
void increment(int& x) {
    x++;
}

int main() {
    int value = 5;
    increment(value);
    std::cout << "Value: " << value << std::endl; // 输出 6
    return 0;
}
```

#### 3.3 **按指针传递**

按指针传递会将参数的指针传递给函数，函数内部通过指针对参数进行修改。

```cpp
void increment(int* x) {
    (*x)++;
}

int main() {
    int value = 5;
    increment(&value);
    std::cout << "Value: " << value << std::endl; // 输出 6
    return 0;
}
```

### 4. **变量作用域**

变量的作用域定义了变量在程序中可见和可访问的范围。C++ 支持局部变量、全局变量和静态变量。

#### 4.1 **局部变量**

局部变量在函数或代码块内声明和定义，只在其作用域内有效。

```cpp
#include <iostream>

void printLocal() {
    int localVar = 10;
    std::cout << "Local variable: " << localVar << std::endl;
}

int main() {
    printLocal();
    // std::cout << localVar << std::endl; // 错误：localVar 在此作用域内不可见
    return 0;
}
```

#### 4.2 **全局变量**

全局变量在所有函数外部声明和定义，可以在整个程序中访问。

```cpp
#include <iostream>

int globalVar = 20;

void printGlobal() {
    std::cout << "Global variable: " << globalVar << std::endl;
}

int main() {
    printGlobal();
    globalVar++;
    printGlobal();
    return 0;
}
```

#### 4.3 **静态变量**

静态变量在函数内声明，并在程序的生命周期内保持其值。

```cpp
#include <iostream>

void printStatic() {
    static int staticVar = 0;
    staticVar++;
    std::cout << "Static variable: " << staticVar << std::endl;
}

int main() {
    printStatic(); // 输出 1
    printStatic(); // 输出 2
    return 0;
}
```

### 5. **控制流**

控制流语句用于控制程序的执行顺序，包括条件语句和循环语句。

#### 5.1 **条件语句**

条件语句用于根据条件执行不同的代码块。

```cpp
#include <iostream>

int main() {
    int number = 10;
    if (number > 0) {
        std::cout << "Positive number" << std::endl;
    } else {
        std::cout << "Non-positive number" << std::endl;
    }
    return 0;
}
```

#### 5.2 **循环语句**

循环语句用于重复执行代码块。

```cpp
#include <iostream>

int main() {
    for (int i = 0; i < 5; i++) {
        std::cout << "Iteration: " << i << std::endl;
    }
    return 0;
}
```

### 6. **总结**

过程式编程是 C++ 中一种基础且重要的编程范式，通过函数的定义与调用、参数传递、变量作用域和控制流语句，可以实现程序的结构化和模块化。掌握过程式编程有助于编写清晰、可维护和高效的代码。
