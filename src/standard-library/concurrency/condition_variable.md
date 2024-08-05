## `std::condition_variable`

在 C++11 中，`<condition_variable>` 头文件提供了 `std::condition_variable` 和 `std::condition_variable_any` 类，用于实现线程间的通知机制，帮助线程在某些条件满足时进行同步。它们通常与 `std::mutex` 一起使用，以协调线程之间的执行。

### 1. **基本概念**

`std::condition_variable` 允许线程等待某个条件变量的信号，以便在条件满足时继续执行。线程通过调用 `wait` 方法进入等待状态，并在条件满足时被唤醒。条件变量通常与互斥锁 (`std::mutex`) 一起使用，以确保条件检查和修改的原子性。

#### 1.1 `std::condition_variable`

- **`wait` 方法**: 使线程在条件变量上等待。线程在等待时会释放与之关联的互斥锁，并在条件满足时重新获取锁。

```cpp
#include <iostream>
#include <thread>
#include <mutex>
#include <condition_variable>
#include <chrono>

std::mutex mtx;
std::condition_variable cv;
bool ready = false;

void waitingThread() {
    std::unique_lock<std::mutex> lock(mtx);
    cv.wait(lock, [] { return ready; });  // 等待条件满足
    std::cout << "Condition satisfied!" << std::endl;
}

void signalingThread() {
    std::this_thread::sleep_for(std::chrono::seconds(1));  // 模拟工作
    {
        std::lock_guard<std::mutex> lock(mtx);
        ready = true;
    }
    cv.notify_all();  // 唤醒所有等待线程
}

int main() {
    std::thread t1(waitingThread);
    std::thread t2(signalingThread);
    
    t1.join();
    t2.join();
    
    return 0;
}
```

- **`notify_one` 和 `notify_all` 方法**: 用于唤醒一个或所有等待的线程。

```cpp
#include <iostream>
#include <thread>
#include <mutex>
#include <condition_variable>

std::mutex mtx;
std::condition_variable cv;
bool ready = false;

void waitingThread() {
    std::unique_lock<std::mutex> lock(mtx);
    cv.wait(lock, [] { return ready; });  // 等待条件满足
    std::cout << "Thread woke up!" << std::endl;
}

void signalingThread() {
    {
        std::lock_guard<std::mutex> lock(mtx);
        ready = true;
    }
    cv.notify_one();  // 唤醒一个等待线程
}

int main() {
    std::thread t1(waitingThread);
    std::thread t2(signalingThread);
    
    t1.join();
    t2.join();
    
    return 0;
}
```

#### 1.2 `std::condition_variable_any`

`std::condition_variable_any` 可以与任何类型的锁（如 `std::mutex`、`std::recursive_mutex` 等）一起使用。它提供了类似于 `std::condition_variable` 的功能，但不需要特定类型的锁。

```cpp
#include <iostream>
#include <thread>
#include <mutex>
#include <condition_variable>
#include <chrono>

std::mutex mtx;
std::condition_variable_any cv;
bool ready = false;

void waitingThread() {
    std::unique_lock<std::mutex> lock(mtx);
    cv.wait(lock, [] { return ready; });  // 等待条件满足
    std::cout << "Condition satisfied!" << std::endl;
}

void signalingThread() {
    std::this_thread::sleep_for(std::chrono::seconds(1));  // 模拟工作
    {
        std::lock_guard<std::mutex> lock(mtx);
        ready = true;
    }
    cv.notify_all();  // 唤醒所有等待线程
}

int main() {
    std::thread t1(waitingThread);
    std::thread t2(signalingThread);
    
    t1.join();
    t2.join();
    
    return 0;
}
```

### 2. **使用场景**

- **线程同步**: 当多个线程需要在特定条件下执行任务时，使用 `std::condition_variable` 可以协调它们的执行。
- **生产者-消费者模式**: 在生产者-消费者模式中，消费者线程在没有数据可用时等待条件变量，生产者线程在生产数据后通知消费者线程。

### 3. **最佳实践**

- **避免虚假唤醒**: 条件变量可能会因虚假唤醒而导致线程被唤醒但条件不满足。总是使用 `wait` 的重载版本，并提供一个谓词函数来检查条件是否满足。
  
  ```cpp
  cv.wait(lock, [] { return conditionIsMet(); });
  ```

- **锁的持有**: 确保在调用 `wait` 方法时持有互斥锁，并在 `notify` 调用后尽快释放锁。

- **性能考虑**: 在多线程应用中，频繁的 `notify_all` 可能会导致性能问题。使用 `notify_one` 时，能避免不必要的线程唤醒，减少上下文切换的开销。

### 4. **总结**

`std::condition_variable` 和 `std::condition_variable_any` 是 C++11 提供的重要同步工具，用于在线程间传递信号和条件。通过正确使用条件变量，可以实现高效的线程同步，确保线程在特定条件下进行协调和通信。了解和掌握这些工具的使用方法，对于编写健壮的多线程程序至关重要。