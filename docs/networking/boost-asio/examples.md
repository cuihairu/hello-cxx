以下是一些 Boost.Asio 的示例代码，涵盖了常见的用例，如异步操作、定时器、Socket 编程等。通过这些示例，你可以更好地理解 Boost.Asio 的使用方法。

### 1. **异步操作示例**

#### 异步读取数据

```cpp
#include <boost/asio.hpp>
#include <iostream>

void read_handler(const boost::system::error_code& error, std::size_t bytes_transferred) {
    if (!error) {
        std::cout << "Read " << bytes_transferred << " bytes" << std::endl;
    } else {
        std::cerr << "Read error: " << error.message() << std::endl;
    }
}

int main() {
    boost::asio::io_context io_context;
    boost::asio::steady_timer timer(io_context, std::chrono::seconds(1));
    
    timer.async_wait([](const boost::system::error_code& error) {
        if (!error) {
            std::cout << "Timer expired!" << std::endl;
        }
    });

    io_context.run(); // 运行 I/O 服务
    return 0;
}
```

### 2. **定时器示例**

#### 设置定时器和回调函数

```cpp
#include <boost/asio.hpp>
#include <iostream>

void timer_handler(const boost::system::error_code& error) {
    if (!error) {
        std::cout << "Timer expired!" << std::endl;
    } else {
        std::cerr << "Timer error: " << error.message() << std::endl;
    }
}

int main() {
    boost::asio::io_context io_context;
    boost::asio::steady_timer timer(io_context, std::chrono::seconds(5)); // 5 秒后超时

    timer.async_wait(timer_handler);

    io_context.run(); // 运行 I/O 服务
    return 0;
}
```

### 3. **Socket 编程示例**

#### 异步 TCP 连接

```cpp
#include <boost/asio.hpp>
#include <iostream>

void connect_handler(const boost::system::error_code& error) {
    if (!error) {
        std::cout << "Connected to the server!" << std::endl;
    } else {
        std::cerr << "Connect error: " << error.message() << std::endl;
    }
}

int main() {
    boost::asio::io_context io_context;
    boost::asio::ip::tcp::resolver resolver(io_context);
    boost::asio::ip::tcp::resolver::results_type endpoints = resolver.resolve("example.com", "80");
    
    boost::asio::ip::tcp::socket socket(io_context);
    boost::asio::async_connect(socket, endpoints, connect_handler);

    io_context.run(); // 运行 I/O 服务
    return 0;
}
```

#### 异步读取数据

```cpp
#include <boost/asio.hpp>
#include <iostream>
#include <array>

void read_handler(const boost::system::error_code& error, std::size_t bytes_transferred) {
    if (!error) {
        std::cout << "Read " << bytes_transferred << " bytes" << std::endl;
    } else {
        std::cerr << "Read error: " << error.message() << std::endl;
    }
}

int main() {
    boost::asio::io_context io_context;
    boost::asio::ip::tcp::socket socket(io_context);
    
    // 假设 socket 已经连接到某个服务器
    std::array<char, 128> buffer;
    boost::asio::async_read(socket, boost::asio::buffer(buffer),
        boost::asio::transfer_at_least(1), read_handler);

    io_context.run(); // 运行 I/O 服务
    return 0;
}
```

### 4. **定时器与 I/O 操作结合示例**

#### 使用定时器设置超时

```cpp
#include <boost/asio.hpp>
#include <iostream>

void read_timeout_handler(const boost::system::error_code& error) {
    if (!error) {
        std::cerr << "Read operation timed out!" << std::endl;
    }
}

void read_handler(const boost::system::error_code& error, std::size_t bytes_transferred) {
    if (!error) {
        std::cout << "Read " << bytes_transferred << " bytes" << std::endl;
    } else {
        std::cerr << "Read error: " << error.message() << std::endl;
    }
}

int main() {
    boost::asio::io_context io_context;
    boost::asio::ip::tcp::socket socket(io_context);
    boost::asio::steady_timer timer(io_context);

    // 设置定时器超时为 5 秒
    timer.expires_after(std::chrono::seconds(5));
    timer.async_wait(read_timeout_handler);

    // 假设 socket 已经连接到某个服务器
    std::array<char, 128> buffer;
    boost::asio::async_read(socket, boost::asio::buffer(buffer),
        boost::asio::transfer_at_least(1), read_handler);

    io_context.run(); // 运行 I/O 服务
    return 0;
}
```

### 5. **异步写入数据示例**

```cpp
#include <boost/asio.hpp>
#include <iostream>

void write_handler(const boost::system::error_code& error, std::size_t bytes_transferred) {
    if (!error) {
        std::cout << "Wrote " << bytes_transferred << " bytes" << std::endl;
    } else {
        std::cerr << "Write error: " << error.message() << std::endl;
    }
}

int main() {
    boost::asio::io_context io_context;
    boost::asio::ip::tcp::socket socket(io_context);
    
    // 假设 socket 已经连接到某个服务器
    std::string message = "Hello, Boost.Asio!";
    boost::asio::async_write(socket, boost::asio::buffer(message),
        write_handler);

    io_context.run(); // 运行 I/O 服务
    return 0;
}
```

### 总结

这些示例代码展示了 Boost.Asio 的不同用例，包括异步操作、定时器、Socket 编程及其结合使用。每个示例中，`io_context.run()` 调用负责处理所有异步操作和事件。根据实际需要，你可以扩展和调整这些示例以适应特定的应用场景。