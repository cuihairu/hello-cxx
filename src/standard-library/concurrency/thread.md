## `<thread>` 线程库

C++11 引入了对多线程编程的标准支持，主要通过 `<thread>` 头文件提供。这个头文件定义了 `std::thread` 类和相关的线程管理功能，使得在 C++ 中编写并发程序变得更加简便。

### 1. **创建和管理线程**

`std::thread` 类用于创建和管理线程。你可以通过将函数或可调用对象传递给 `std::thread` 的构造函数来启动线程。

#### 1.1 创建线程

```cpp
#include <iostream>
#include <thread>

void printHello() {
    std::cout << "Hello from thread!" << std::endl;
}

int main() {
    std::thread t(printHello);  // 创建并启动线程
    t.join();  // 等待线程完成
    return 0;
}
```

#### 1.2 传递参数

你可以将参数传递给线程函数：

```cpp
#include <iostream>
#include <thread>

void printNumber(int x) {
    std::cout << "Number: " << x << std::endl;
}

int main() {
    std::thread t(printNumber, 5);  // 传递参数给线程函数
    t.join();  // 等待线程完成
    return 0;
}
```

### 2. **线程同步**

在多线程程序中，确保线程之间的安全访问共享资源是至关重要的。`<thread>` 头文件提供了一些基本的同步工具，例如 `std::mutex` 和 `std::lock_guard`。

#### 2.1 使用 `std::mutex`

`std::mutex` 是一种互斥锁，能够保护共享资源，防止多个线程同时访问它。

```cpp
#include <iostream>
#include <thread>
#include <mutex>

std::mutex mtx;

void printNumbers() {
    std::lock_guard<std::mutex> lock(mtx);
    for (int i = 0; i < 5; ++i) {
        std::cout << i << std::endl;
    }
}

int main() {
    std::thread t1(printNumbers);
    std::thread t2(printNumbers);
    
    t1.join();
    t2.join();
    
    return 0;
}
```

#### 2.2 使用 `std::lock_guard`

`std::lock_guard` 是一个 RAII 类型的锁管理工具，它会在构造时锁定互斥量，在析构时自动释放互斥量。

```cpp
#include <iostream>
#include <thread>
#include <mutex>

std::mutex mtx;

void safePrint(int x) {
    std::lock_guard<std::mutex> lock(mtx);
    std::cout << "Thread: " << x << std::endl;
}

int main() {
    std::thread t1(safePrint, 1);
    std::thread t2(safePrint, 2);
    
    t1.join();
    t2.join();
    
    return 0;
}
```

### 3. **线程条件变量**

`std::condition_variable` 是一个线程同步工具，它允许线程等待某个条件发生。与 `std::mutex` 配合使用，能够实现复杂的线程协调机制。

#### 3.1 使用 `std::condition_variable`

```cpp
#include <iostream>
#include <thread>
#include <mutex>
#include <condition_variable>

std::mutex mtx;
std::condition_variable cv;
bool ready = false;

void waitForSignal() {
    std::unique_lock<std::mutex> lock(mtx);
    cv.wait(lock, []{ return ready; });
    std::cout << "Thread received signal" << std::endl;
}

void sendSignal() {
    std::this_thread::sleep_for(std::chrono::seconds(1));
    {
        std::lock_guard<std::mutex> lock(mtx);
        ready = true;
    }
    cv.notify_one();
}

int main() {
    std::thread waiter(waitForSignal);
    std::thread signaler(sendSignal);
    
    waiter.join();
    signaler.join();
    
    return 0;
}
```

### 4. **线程的其他功能**

#### 4.1 获取线程 ID

你可以使用 `std::this_thread::get_id()` 获取当前线程的 ID，并使用 `std::thread::get_id()` 获取线程对象的 ID。

```cpp
#include <iostream>
#include <thread>

void printThreadId() {
    std::cout << "Thread ID: " << std::this_thread::get_id() << std::endl;
}

int main() {
    std::thread t(printThreadId);
    t.join();
    return 0;
}
```

#### 4.2 线程的 `detach` 和 `join` 方法

`std::thread::detach()` 方法将线程与主线程分离，使其在后台运行，不再需要等待其完成。`std::thread::join()` 方法则用于等待线程完成。

```cpp
#include <iostream>
#include <thread>

void backgroundTask() {
    std::cout << "Background task running" << std::endl;
}

int main() {
    std::thread t(backgroundTask);
    t.detach();  // 分离线程，使其在后台运行
    // 主线程可以继续执行其他任务
    
    std::this_thread::sleep_for(std::chrono::seconds(1));  // 等待一段时间以确保后台线程有时间执行
    return 0;
}
```

### 5. **总结**

C++ 的 `<thread>` 库为多线程编程提供了基本工具，包括创建和管理线程、线程同步、线程条件变量等。通过正确使用这些工具，可以有效地编写并发程序并确保线程安全。