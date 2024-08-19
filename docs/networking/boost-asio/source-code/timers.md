### 定时器与过期操作

在 Boost.Asio 中，定时器（`steady_timer`、`deadline_timer` 等）和过期操作是处理时间相关任务的重要工具。定时器用于在指定的时间点或时间间隔后执行操作，广泛应用于超时处理、定时任务、周期性任务等场景。

#### 1. **定时器的基本概念**

定时器在 Boost.Asio 中主要用于执行延迟操作。以下是定时器的几个关键概念：

- **定时器类型**：
  - **`steady_timer`**：基于 `std::steady_clock`，用于测量经过的时间，不受系统时间变化的影响。适用于需要精确测量时间间隔的场景。
  - **`system_timer`**（或 `deadline_timer` 在早期版本）：基于系统时间，用于在指定的系统时间点执行操作。适用于需要在特定的绝对时间点执行任务的场景。

  ```cpp
  boost::asio::steady_timer timer(io_context);
  boost::asio::system_timer system_timer(io_context);
  ```

- **定时器的创建**：
  - 创建定时器时需要指定 `io_context` 对象，并可以设置初始超时时间。

  ```cpp
  boost::asio::steady_timer timer(io_context, std::chrono::seconds(5)); // 5 秒后触发
  ```

- **设置超时**：
  - 使用 `expires_after()` 或 `expires_at()` 方法设置定时器的超时时间。超时时间可以是相对时间（如 `std::chrono::seconds`）或绝对时间（如 `std::chrono::system_clock::now()`）。

  ```cpp
  timer.expires_after(std::chrono::seconds(5)); // 5 秒后超时
  ```

#### 2. **设置定时器操作**

在设置定时器后，需要指定操作函数，当定时器超时时该函数将被调用。使用 `async_wait()` 方法异步等待定时器超时：

- **异步等待**：
  - `async_wait()` 方法将定时器与回调函数关联，当定时器超时后，Boost.Asio 将异步调用该回调函数。

  ```cpp
  void handle_timeout(const boost::system::error_code& error) {
      if (!error) {
          std::cout << "Timer expired!" << std::endl;
      }
  }

  timer.async_wait(handle_timeout);
  ```

- **同步等待**：
  - `wait()` 方法可以用来同步等待定时器超时。这将阻塞当前线程，直到定时器超时。

  ```cpp
  timer.wait();
  ```

#### 3. **取消定时器**

有时需要取消定时器操作，这通常在任务被取消或不再需要时进行：

- **取消定时器**：
  - 使用 `cancel()` 方法取消定时器。如果定时器已经超时，该方法不会影响已执行的回调函数。

  ```cpp
  timer.cancel();
  ```

- **检查取消状态**：
  - 可以检查定时器是否被取消或已过期，使用 `expiry()` 方法查看当前超时状态。

  ```cpp
  if (timer.expiry() <= std::chrono::steady_clock::now()) {
      std::cout << "Timer expired or cancelled" << std::endl;
  }
  ```

#### 4. **定时器的实际应用**

- **超时处理**：
  - 定时器常用于设置操作的超时时间，比如网络连接的超时处理。

  ```cpp
  void handle_timeout(const boost::system::error_code& error) {
      if (error) {
          std::cerr << "Error: " << error.message() << std::endl;
      } else {
          std::cout << "Operation timed out!" << std::endl;
      }
  }

  boost::asio::steady_timer timer(io_context, std::chrono::seconds(10));
  timer.async_wait(handle_timeout);
  ```

- **定时任务**：
  - 定时器可以用来调度周期性任务，如定时执行某个操作。

  ```cpp
  void periodic_task(const boost::system::error_code& error) {
      if (!error) {
          std::cout << "Periodic task executed!" << std::endl;
          timer.expires_at(timer.expiry() + std::chrono::seconds(5)); // 5 秒后再次触发
          timer.async_wait(periodic_task);
      }
  }

  boost::asio::steady_timer timer(io_context, std::chrono::seconds(5));
  timer.async_wait(periodic_task);
  ```

- **定时器与 I/O 操作**：
  - 定时器可以与 I/O 操作结合使用，例如设置超时以防止长时间的网络等待。

  ```cpp
  void handle_read(const boost::system::error_code& error) {
      if (error) {
          std::cerr << "Read error: " << error.message() << std::endl;
      } else {
          std::cout << "Data received" << std::endl;
      }
  }

  void start_read() {
      boost::asio::async_read(socket, buffer(data),
          boost::asio::bind_executor(strand, handle_read));
  }

  boost::asio::steady_timer timer(io_context, std::chrono::seconds(10));
  timer.async_wait([&](const boost::system::error_code& error) {
      if (!error) {
          socket.cancel(); // 取消网络操作
      }
  });

  start_read();
  ```

### 总结

- **定时器**：用于在指定的时间点或时间间隔后执行操作。主要类型包括 `steady_timer` 和 `system_timer`。
- **设置超时**：使用 `expires_after()` 或 `expires_at()` 方法设置定时器的超时时间。
- **回调函数**：通过 `async_wait()` 方法异步设置回调函数，以在定时器超时后执行。
- **取消操作**：使用 `cancel()` 方法取消定时器操作。
- **实际应用**：包括超时处理、周期性任务、与 I/O 操作结合使用等场景。

定时器和过期操作在异步编程中发挥了重要作用，帮助实现时间控制和任务调度。