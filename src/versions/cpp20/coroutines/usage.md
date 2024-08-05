### C++20 协程（Coroutines） 协程的使用

协程（Coroutines）是 C++20 引入的一项特性，它极大地简化了异步编程和生成器的实现。协程允许在函数中暂停执行并随后恢复，使得编写异步操作和生成器变得更加直观和易于维护。

#### 1. **协程的基本用法**

协程函数的基本语法与普通函数类似，但它们可以使用 `co_await`、`co_yield` 和 `co_return` 来控制执行流。协程函数的返回类型通常为 `std::coroutine_handle` 或自定义的协程句柄类型。

下面是一个使用 `std::coroutine_handle` 的简单示例：

```cpp
#include <iostream>
#include <coroutine>

struct Awaiter {
    bool await_ready() const noexcept { return false; }
    void await_suspend(std::coroutine_handle<>) const noexcept {}
    void await_resume() const noexcept {}
};

std::coroutine_handle<> my_coroutine() {
    std::cout << "Coroutine starts" << std::endl;
    co_await Awaiter{}; // 暂停协程
    std::cout << "Coroutine resumes" << std::endl;
    co_return; // 结束协程
}

int main() {
    auto handle = my_coroutine();
    handle.resume(); // 恢复协程执行
    handle.destroy(); // 销毁协程句柄
    return 0;
}
```

#### 2. **使用 `co_await`**

`co_await` 用于等待一个异步操作完成并暂停协程的执行。要使用 `co_await`，必须定义一个等待器（awaiter）类型，该类型需实现以下接口：

- `bool await_ready()`：检查异步操作是否已完成，如果是，返回 `true`，否则返回 `false`。
- `void await_suspend(std::coroutine_handle<>)`：在异步操作未完成时，挂起协程并保存状态。
- `void await_resume()`：在异步操作完成后，恢复协程执行并返回结果。

以下是一个使用 `co_await` 的例子，其中使用了一个模拟的异步操作：

```cpp
#include <iostream>
#include <coroutine>
#include <chrono>
#include <thread>

struct Timer {
    Timer(int milliseconds) : duration(milliseconds) {}
    bool await_ready() const noexcept { return false; }
    void await_suspend(std::coroutine_handle<>) const noexcept {
        std::this_thread::sleep_for(duration);
    }
    void await_resume() const noexcept {}

    std::chrono::milliseconds duration;
};

std::coroutine_handle<> timed_coroutine() {
    std::cout << "Waiting for 2 seconds..." << std::endl;
    co_await Timer{2000}; // 暂停协程2秒
    std::cout << "2 seconds passed!" << std::endl;
    co_return;
}

int main() {
    auto handle = timed_coroutine();
    handle.resume(); // 恢复协程执行
    handle.destroy(); // 销毁协程句柄
    return 0;
}
```

#### 3. **使用 `co_yield`**

`co_yield` 用于生成一个值并暂停协程。调用协程的代码可以在下次恢复时接收这个值。下面是一个简单的生成器示例，生成一系列整数：

```cpp
#include <iostream>
#include <coroutine>

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
    return 0;
}
```

#### 4. **使用 `co_return`**

`co_return` 用于结束协程并返回结果。协程的返回类型决定了 `co_return` 的用法。如果协程返回 `void`，`co_return` 不需要指定返回值；如果返回一个具体类型，需要提供一个返回值。

以下是一个带返回值的协程示例：

```cpp
#include <iostream>
#include <coroutine>

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

Task compute_value() {
    co_return 42; // 返回值42
}

int main() {
    auto task = compute_value();
    std::cout << "Value: " << task.result() << std::endl;
    return 0;
}
```

#### 5. **自定义协程类型的使用**

自定义协程类型的使用与标准协程类似。你需要实现 `promise_type` 和协程函数，定义如何处理挂起、恢复和返回值。

通过协程，C++20 为异步编程和生成器提供了一个更清晰的语法，使得这些操作更加自然和易于理解。