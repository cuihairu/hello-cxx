## `<mutex>` 互斥量库

`<mutex>` 头文件提供了多种互斥量（mutex）和锁机制，用于在多线程环境中保护共享资源，防止数据竞争和确保线程安全。互斥量是并发编程中最常用的同步原语之一，它们能够保证在任意时刻只有一个线程访问共享资源。

### 1. **基本概念**

#### 1.1 `std::mutex`

`std::mutex` 是一种基本的互斥量，提供了锁定和解锁的功能。它适用于那些需要在多个线程之间共享资源的情况。

```cpp
#include <iostream>
#include <thread>
#include <mutex>

std::mutex mtx;

void printNumbers() {
    std::lock_guard<std::mutex> lock(mtx);  // 锁定互斥量
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

#### 1.2 `std::recursive_mutex`

`std::recursive_mutex` 是一种递归互斥量，允许同一线程多次锁定它。递归互斥量适用于递归调用的场景。

```cpp
#include <iostream>
#include <thread>
#include <mutex>

std::recursive_mutex rmtx;

void recursivePrint(int count) {
    std::lock_guard<std::recursive_mutex> lock(rmtx);
    if (count > 0) {
        std::cout << count << std::endl;
        recursivePrint(count - 1);
    }
}

int main() {
    std::thread t(recursivePrint, 5);
    t.join();
    
    return 0;
}
```

#### 1.3 `std::timed_mutex` 和 `std::try_mutex`

`std::timed_mutex` 允许线程在指定的超时时间内尝试获取锁，而 `std::try_mutex` 提供了非阻塞的尝试锁定功能。

```cpp
#include <iostream>
#include <thread>
#include <mutex>
#include <chrono>

std::timed_mutex tm;

void timedLock() {
    if (tm.try_lock_for(std::chrono::seconds(1))) {
        std::cout << "Acquired lock" << std::endl;
        std::this_thread::sleep_for(std::chrono::seconds(2));
        tm.unlock();
    } else {
        std::cout << "Failed to acquire lock" << std::endl;
    }
}

int main() {
    std::thread t1(timedLock);
    std::thread t2(timedLock);
    
    t1.join();
    t2.join();
    
    return 0;
}
```

### 2. **锁管理**

#### 2.1 `std::lock_guard`

`std::lock_guard` 是一种 RAII 风格的锁管理工具，在其构造时自动锁定互斥量，在其析构时自动解锁，避免了显式的锁定和解锁操作。

```cpp
#include <iostream>
#include <thread>
#include <mutex>

std::mutex mtx;

void printNumbers() {
    std::lock_guard<std::mutex> lock(mtx);  // 自动锁定互斥量
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

#### 2.2 `std::unique_lock`

`std::unique_lock` 提供了更多的灵活性，例如可以延迟锁定、解锁互斥量、以及在作用域外释放锁。

```cpp
#include <iostream>
#include <thread>
#include <mutex>

std::mutex mtx;

void printNumbers() {
    std::unique_lock<std::mutex> lock(mtx);  // 锁定互斥量
    std::cout << "Thread started" << std::endl;
    lock.unlock();  // 手动解锁
    std::cout << "Thread finished" << std::endl;
}

int main() {
    std::thread t1(printNumbers);
    std::thread t2(printNumbers);
    
    t1.join();
    t2.join();
    
    return 0;
}
```

### 3. **锁的优化**

#### 3.1 死锁避免

死锁是一种常见的并发问题，发生在两个或多个线程因等待对方释放资源而相互阻塞。避免死锁的策略包括：

- **避免嵌套锁**：尽量减少多个锁的嵌套。
- **锁的顺序**：如果多个锁需要同时持有，确保所有线程按相同的顺序锁定它们。
- **使用 `std::lock`**：`std::lock` 可以同时锁定多个互斥量，避免死锁。

```cpp
#include <iostream>
#include <thread>
#include <mutex>

std::mutex mtx1, mtx2;

void deadlockAvoidance() {
    std::lock(mtx1, mtx2);  // 同时锁定两个互斥量
    std::lock_guard<std::mutex> lg1(mtx1, std::adopt_lock);
    std::lock_guard<std::mutex> lg2(mtx2, std::adopt_lock);
    
    std::cout << "No deadlock" << std::endl;
}

int main() {
    std::thread t1(deadlockAvoidance);
    std::thread t2(deadlockAvoidance);
    
    t1.join();
    t2.join();
    
    return 0;
}
```

#### 3.2 避免锁竞争

减少锁竞争可以提高程序性能。可以通过细化锁的粒度、减少锁的持有时间来避免锁竞争。

### 4. **总结**

C++ 的 `<mutex>` 库提供了多种互斥量和锁管理工具，用于在多线程环境中保护共享资源。通过正确使用这些工具，可以有效地控制并发访问、避免数据竞争，并确保线程安全。在并发编程中，理解和应用互斥量及其相关功能对于编写可靠的多线程程序至关重要。