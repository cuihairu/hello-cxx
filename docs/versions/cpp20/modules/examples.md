### C++20 协程（Coroutines） 示例代码

协程是 C++20 引入的一项重要特性，允许函数在执行过程中挂起并稍后恢复执行。下面是一些示例代码，展示了如何使用 C++20 协程进行基本的异步操作和生成器实现。

#### 1. **基本协程**

这是一个简单的协程示例，演示了如何使用 `co_await` 和 `co_return` 控制协程的执行流。

```cpp
#include <iostream>
#include <coroutine>
#include <chrono>
#include <thread>

// 定义一个等待器，用于模拟异步操作
struct Awaiter {
    bool await_ready() const noexcept { return false; }
    void await_suspend(std::coroutine_handle<>) const noexcept {
        std::this_thread::sleep_for(std::chrono::seconds(1));
    }
    void await_resume() const noexcept {}
};

// 定义一个协程函数
std::coroutine_handle<> simple_coroutine() {
    std::cout << "Coroutine started" << std::endl;
    co_await Awaiter{};  // 挂起协程1秒
    std::cout << "Coroutine resumed" << std::endl;
    co_return;           // 结束协程
}

int main() {
    auto handle = simple_coroutine();
    handle.resume(); // 恢复协程
    handle.destroy(); // 销毁协程句柄
    return 0;
}
```

#### 2. **使用 `co_await`**

这个示例展示了如何使用 `co_await` 和一个自定义的等待器来模拟异步操作。

```cpp
#include <iostream>
#include <coroutine>
#include <thread>
#include <chrono>

// 定义一个等待器
struct Timer {
    Timer(int milliseconds) : duration(milliseconds) {}
    bool await_ready() const noexcept { return false; }
    void await_suspend(std::coroutine_handle<>) const noexcept {
        std::this_thread::sleep_for(duration);
    }
    void await_resume() const noexcept {}

    std::chrono::milliseconds duration;
};

// 使用 `co_await` 的协程函数
std::coroutine_handle<> timed_coroutine() {
    std::cout << "Waiting for 2 seconds..." << std::endl;
    co_await Timer{2000}; // 暂停2秒
    std::cout << "2 seconds passed!" << std::endl;
    co_return;
}

int main() {
    auto handle = timed_coroutine();
    handle.resume(); // 恢复协程
    handle.destroy(); // 销毁协程句柄
    return 0;
}
```

#### 3. **生成器（使用 `co_yield`）**

这个示例展示了如何使用 `co_yield` 创建一个生成器，逐步生成整数序列。

```cpp
#include <iostream>
#include <coroutine>

// 定义生成器类型
struct Generator {
    struct promise_type;
    using handle_type = std::coroutine_handle<promise_type>;

    struct promise_type {
        int current_value;
        Generator get_return_object() {
            return Generator{handle_type::from_promise(*this)};
        }
        std::suspend_always initial_suspend() { return {}; }
        std::suspend_always final_suspend() noexcept { return {}; }
        void return_void() {}
        void unhandled_exception() {}

        std::suspend_always yield_value(int value) {
            current_value = value;
            return {};
        }
    };

    Generator(handle_type h) : handle(h) {}
    ~Generator() { if (handle) handle.destroy(); }

    handle_type handle;

    bool next() {
        handle.resume();
        return !handle.done();
    }

    int current() const {
        return handle.promise().current_value;
    }
};

// 使用 `co_yield` 的协程函数
Generator number_generator() {
    for (int i = 1; i <= 5; ++i) {
        co_yield i; // 生成整数1到5
    }
}

int main() {
    auto gen = number_generator();
    while (gen.next()) {
        std::cout << gen.current() << " "; // 输出生成的值
    }
    std::cout << std::endl;
    return 0;
}
```

#### 4. **协程的返回值**

这个示例展示了如何定义协程返回值并使用 `co_return` 返回一个结果。

```cpp
#include <iostream>
#include <coroutine>

// 定义协程类型
struct Task {
    struct promise_type;
    using handle_type = std::coroutine_handle<promise_type>;

    struct promise_type {
        int value;
        Task get_return_object() {
            return Task{handle_type::from_promise(*this)};
        }
        std::suspend_always initial_suspend() { return {}; }
        std::suspend_always final_suspend() noexcept { return {}; }
        void return_value(int v) {
            value = v;
        }
        void unhandled_exception() {}
    };

    Task(handle_type h) : handle(h) {}
    ~Task() { if (handle) handle.destroy(); }

    handle_type handle;

    int result() const {
        return handle.promise().value;
    }
};

// 使用 `co_return` 的协程函数
Task compute_value() {
    co_return 42; // 返回值42
}

int main() {
    auto task = compute_value();
    std::cout << "Value: " << task.result() << std::endl;
    return 0;
}
```

这些示例代码展示了 C++20 协程的基本用法，包括如何定义和使用协程函数、等待器、生成器以及如何处理协程的返回值。通过这些示例，你可以了解协程在 C++20 中的实际应用和操作方式。