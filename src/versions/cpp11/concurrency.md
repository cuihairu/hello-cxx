### C++11 并发支持

C++11 标准引入了对并发编程的原生支持，显著扩展了语言功能，使得多线程编程更加简便和安全。这些扩展包括线程库、互斥量、条件变量和原子操作等。以下是 C++11 在并发支持方面的主要改进：

#### 1. **线程库 (`<thread>`)**

C++11 引入了 `std::thread` 类，允许创建和管理线程。这使得并发编程变得更加直观和高效。

**示例**：
```cpp
#include <iostream>
#include <thread>

void printHello() {
    std::cout << "Hello from thread!" << std::endl;
}

int main() {
    std::thread t(printHello); // 创建一个新线程
    t.join(); // 等待线程结束
    return 0;
}
```

在这个示例中，`std::thread` 被用来创建一个新的线程，并调用 `printHello` 函数。`t.join()` 用于等待线程执行完成。

#### 2. **互斥量 (`<mutex>`)**

`std::mutex` 类提供了互斥量用于线程间的同步，防止多个线程同时访问共享资源。C++11 还引入了 `std::lock_guard` 和 `std::unique_lock`，以便更方便地管理互斥量的锁定和解锁。

**示例**：
```cpp
#include <iostream>
#include <thread>
#include <mutex>

std::mutex mtx;

void printNumbers(int id) {
    std::lock_guard<std::mutex> lock(mtx); // 自动锁定和解锁
    std::cout << "Thread " << id << " is printing" << std::endl;
}

int main() {
    std::thread t1(printNumbers, 1);
    std::thread t2(printNumbers, 2);
    t1.join();
    t2.join();
    return 0;
}
```

在这个示例中，`std::mutex` 用于保护 `std::cout` 的访问，以避免多个线程同时写入输出流。

#### 3. **条件变量 (`<condition_variable>`)**

`std::condition_variable` 类用于线程间的同步机制，允许一个线程等待某个条件发生，而另一个线程可以通知它条件已经满足。常与 `std::mutex` 配合使用。

**示例**：
```cpp
#include <iostream>
#include <thread>
#include <mutex>
#include <condition_variable>

std::mutex mtx;
std::condition_variable cv;
bool ready = false;

void waitForReady() {
    std::unique_lock<std::mutex> lock(mtx);
    cv.wait(lock, [] { return ready; }); // 等待条件满足
    std::cout << "Condition met, thread proceeding!" << std::endl;
}

void setReady() {
    {
        std::lock_guard<std::mutex> lock(mtx);
        ready = true;
    }
    cv.notify_one(); // 通知等待的线程条件已满足
}

int main() {
    std::thread t1(waitForReady);
    std::thread t2(setReady);
    t1.join();
    t2.join();
    return 0;
}
```

在这个示例中，`std::condition_variable` 用于在 `waitForReady` 线程中等待 `ready` 变量变为 `true`，而 `setReady` 线程负责设置这个条件并通知等待线程。

#### 4. **原子操作 (`<atomic>`)**

`std::atomic` 类提供了对原子操作的支持，使得在多线程环境下对基本数据类型的操作是线程安全的。它避免了使用互斥量的开销，并允许更细粒度的控制。

**示例**：
```cpp
#include <iostream>
#include <thread>
#include <atomic>

std::atomic<int> counter(0);

void increment() {
    for (int i = 0; i < 1000; ++i) {
        ++counter; // 原子操作
    }
}

int main() {
    std::thread t1(increment);
    std::thread t2(increment);
    t1.join();
    t2.join();
    std::cout << "Counter: " << counter.load() << std::endl; // 输出计数器的值
    return 0;
}
```

在这个示例中，`std::atomic` 用于确保 `counter` 的递增操作是原子的，从而避免了数据竞争和不一致性。

#### 5. **其他并发功能**

C++11 还引入了一些其他并发相关的功能：

- `std::async`：用于启动异步任务，并返回一个 `std::future` 对象来获取任务的结果。
- `std::future` 和 `std::promise`：用于在不同线程之间传递值或异常。
- `std::call_once`：用于确保某个操作只执行一次。

**示例（`std::async` 和 `std::future`）**：
```cpp
#include <iostream>
#include <future>

int calculateSquare(int x) {
    return x * x;
}

int main() {
    std::future<int> result = std::async(std::launch::async, calculateSquare, 10);
    std::cout << "Square: " << result.get() << std::endl; // 获取结果并输出
    return 0;
}
```

在这个示例中，`std::async` 用于启动异步任务来计算平方，并通过 `std::future` 获取结果。

### 总结

C++11 对并发编程的支持大大丰富了语言功能，使得编写多线程程序更加直接和高效。通过线程库、互斥量、条件变量、原子操作等工具，程序员可以更方便地实现并发控制和同步操作。这些功能使得 C++11 成为一个强大的并发编程语言工具。