## `std::future` 和 `std::promise`

在 C++11 中，`<future>` 头文件提供了 `std::future` 和 `std::promise` 类，用于实现异步计算和线程间的结果传递。它们允许你在将来某个时刻获取异步操作的结果，并且支持异步任务的组合和同步。

### 1. **基本概念**

#### 1.1 `std::future`

`std::future` 是一种机制，用于从异步操作中获取结果。你可以用它来等待一个异步任务完成，并获取其返回值或异常。

- **获取值**: 使用 `get()` 方法从 `std::future` 对象中获取结果。此方法会阻塞当前线程，直到异步操作完成。

```cpp
#include <iostream>
#include <future>
#include <thread>

int asyncTask() {
    std::this_thread::sleep_for(std::chrono::seconds(2));
    return 42;
}

int main() {
    std::future<int> fut = std::async(std::launch::async, asyncTask);
    std::cout << "Waiting for result..." << std::endl;
    int result = fut.get();  // 阻塞直到异步任务完成
    std::cout << "Result: " << result << std::endl;
    
    return 0;
}
```

- **异常处理**: 如果异步任务抛出了异常，`get()` 方法会重新抛出该异常。

```cpp
#include <iostream>
#include <future>
#include <thread>

void errorTask() {
    throw std::runtime_error("Something went wrong");
}

int main() {
    std::future<void> fut = std::async(std::launch::async, errorTask);
    try {
        fut.get();  // 阻塞直到任务完成，可能会抛出异常
    } catch (const std::exception& e) {
        std::cout << "Caught exception: " << e.what() << std::endl;
    }
    
    return 0;
}
```

#### 1.2 `std::promise`

`std::promise` 用于将一个值或异常传递到 `std::future` 对象。它提供了 `set_value()` 和 `set_exception()` 方法，用于设置异步任务的结果或异常。

```cpp
#include <iostream>
#include <future>
#include <thread>

void produceValue(std::promise<int> prom) {
    try {
        prom.set_value(42);  // 设置值
    } catch (...) {
        prom.set_exception(std::current_exception());  // 设置异常
    }
}

int main() {
    std::promise<int> prom;
    std::future<int> fut = prom.get_future();
    std::thread t(produceValue, std::move(prom));
    
    std::cout << "Waiting for result..." << std::endl;
    int result = fut.get();  // 阻塞直到值被设置
    std::cout << "Result: " << result << std::endl;
    
    t.join();
    return 0;
}
```

### 2. **`std::async`**

`std::async` 是一个便捷函数，用于启动一个异步任务，并返回一个 `std::future` 对象。它支持不同的启动策略（如 `std::launch::async` 和 `std::launch::deferred`）。

```cpp
#include <iostream>
#include <future>
#include <thread>

int asyncTask(int x) {
    return x * 2;
}

int main() {
    std::future<int> fut = std::async(std::launch::async, asyncTask, 10);
    int result = fut.get();
    std::cout << "Result: " << result << std::endl;
    
    return 0;
}
```

- **`std::launch::async`**: 立即在新线程中执行任务。
- **`std::launch::deferred`**: 任务会在 `get()` 或 `wait()` 调用时延迟执行，通常会在调用线程中执行。

### 3. **组合和同步**

`std::future` 支持组合多个异步任务和同步其结果。

#### 3.1 `std::when_all` 和 `std::when_any`

- **`std::when_all`**: 等待所有 `std::future` 对象完成。

```cpp
#include <iostream>
#include <future>
#include <vector>

int compute(int x) {
    return x * x;
}

int main() {
    std::vector<std::future<int>> futures;
    for (int i = 0; i < 5; ++i) {
        futures.push_back(std::async(std::launch::async, compute, i));
    }
    
    std::vector<int> results;
    for (auto& fut : futures) {
        results.push_back(fut.get());
    }
    
    for (int result : results) {
        std::cout << result << std::endl;
    }
    
    return 0;
}
```

- **`std::when_any`**: 等待任意一个 `std::future` 对象完成。

### 4. **总结**

`std::future` 和 `std::promise` 提供了在 C++ 中进行异步计算和线程间结果传递的强大工具。通过合理使用这些工具，可以简化并发编程中的复杂性，实现更加清晰和可维护的代码。异步任务的组合和同步能力进一步增强了其在多线程环境中的应用灵活性。