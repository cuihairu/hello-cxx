## 控制流语句

控制流语句是程序中用来决定执行路径的关键部分。通过控制流语句，程序可以根据不同的条件执行不同的代码块，从而实现复杂的逻辑处理。C++ 提供了多种控制流语句来满足不同的编程需求。

### 1. **条件语句**

条件语句用于根据条件的真假来选择不同的执行路径。

#### 1.1 **if 语句**

`if` 语句用于根据条件的真假执行代码块。

```cpp
int a = 10;
if (a > 0) {
    std::cout << "a 是正数" << std::endl;
}
```

#### 1.2 **if-else 语句**

`if-else` 语句在条件为假时执行另一个代码块。

```cpp
int a = -5;
if (a > 0) {
    std::cout << "a 是正数" << std::endl;
} else {
    std::cout << "a 不是正数" << std::endl;
}
```

#### 1.3 **if-else if-else 语句**

`if-else if-else` 语句用于处理多个条件。

```cpp
int a = 0;
if (a > 0) {
    std::cout << "a 是正数" << std::endl;
} else if (a < 0) {
    std::cout << "a 是负数" << std::endl;
} else {
    std::cout << "a 是零" << std::endl;
}
```

#### 1.4 **switch 语句**

`switch` 语句用于基于变量的值执行不同的代码块，适用于多重选择。

```cpp
int day = 3;
switch (day) {
    case 1:
        std::cout << "星期一" << std::endl;
        break;
    case 2:
        std::cout << "星期二" << std::endl;
        break;
    case 3:
        std::cout << "星期三" << std::endl;
        break;
    default:
        std::cout << "无效的输入" << std::endl;
        break;
}
```

### 2. **循环语句**

循环语句用于重复执行一段代码，直到满足特定条件。

#### 2.1 **for 循环**

`for` 循环用于在已知迭代次数的情况下执行循环。

```cpp
for (int i = 0; i < 5; ++i) {
    std::cout << "i = " << i << std::endl;
}
```

#### 2.2 **while 循环**

`while` 循环用于在条件为真的情况下执行循环，适用于不知道具体迭代次数的情况。

```cpp
int i = 0;
while (i < 5) {
    std::cout << "i = " << i << std::endl;
    ++i;
}
```

#### 2.3 **do-while 循环**

`do-while` 循环与 `while` 循环类似，但无论条件是否成立，循环体至少执行一次。

```cpp
int i = 0;
do {
    std::cout << "i = " << i << std::endl;
    ++i;
} while (i < 5);
```

### 3. **跳转语句**

跳转语句用于改变程序的执行顺序。

#### 3.1 **break 语句**

`break` 语句用于退出当前的循环或 `switch` 语句。

```cpp
for (int i = 0; i < 10; ++i) {
    if (i == 5) {
        break;  // 退出循环
    }
    std::cout << "i = " << i << std::endl;
}
```

#### 3.2 **continue 语句**

`continue` 语句用于跳过当前迭代的剩余部分，直接进入下一次迭代。

```cpp
for (int i = 0; i < 10; ++i) {
    if (i % 2 == 0) {
        continue;  // 跳过当前循环
    }
    std::cout << "i = " << i << std::endl;
}
```

#### 3.3 **return 语句**

`return` 语句用于退出当前函数并返回值。

```cpp
int sum(int a, int b) {
    return a + b;  // 返回两个数的和
}

int main() {
    int result = sum(5, 3);
    std::cout << "结果: " << result << std::endl;
    return 0;
}
```

### 4. **总结**

控制流语句在 C++ 编程中扮演了至关重要的角色。通过合理使用条件语句、循环语句和跳转语句，可以实现复杂的逻辑控制和数据处理。这些语句帮助程序员有效地管理代码执行的路径和流程，从而实现预期的功能。
