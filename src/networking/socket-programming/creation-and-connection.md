# Socket 的创建与连接

Socket 编程的基本操作包括创建和连接 Socket，这些操作是网络通信的基础。以下是有关 Socket 创建与连接的详细说明，包括在不同编程语言中的示例。

#### 1. **Socket 的创建**

**创建 Socket** 是指在应用程序中创建一个用于网络通信的端点。创建 Socket 的步骤如下：

- **选择 Socket 类型**：确定使用的套接字类型，如流式 Socket（SOCK_STREAM）用于 TCP 通信，数据报 Socket（SOCK_DGRAM）用于 UDP 通信。
- **调用系统函数**：使用系统提供的函数创建 Socket 实例。

##### **Python 示例**

```python
import socket

# 创建一个 TCP 套接字
sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
```

##### **C++ 示例**

```cpp
#include <sys/socket.h>
#include <netinet/in.h>
#include <unistd.h>

int main() {
    // 创建一个 TCP 套接字
    int sockfd = socket(AF_INET, SOCK_STREAM, 0);
    if (sockfd < 0) {
        perror("socket");
        return 1;
    }

    return 0;
}
```

#### 2. **Socket 的绑定（仅服务器端）**

**绑定 Socket** 是将 Socket 绑定到特定的 IP 地址和端口号。此步骤通常仅在服务器端执行，用于指定服务器监听的地址和端口。

##### **Python 示例**

```python
import socket

# 创建一个 TCP 套接字
sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# 绑定到 IP 地址和端口
sock.bind(('localhost', 12345))
```

##### **C++ 示例**

```cpp
#include <sys/socket.h>
#include <netinet/in.h>
#include <cstring>
#include <unistd.h>

int main() {
    int sockfd = socket(AF_INET, SOCK_STREAM, 0);

    struct sockaddr_in server_addr;
    server_addr.sin_family = AF_INET;
    server_addr.sin_addr.s_addr = INADDR_ANY;  // 绑定到所有网络接口
    server_addr.sin_port = htons(12345);       // 端口号

    if (bind(sockfd, (struct sockaddr*)&server_addr, sizeof(server_addr)) < 0) {
        perror("bind");
        return 1;
    }

    return 0;
}
```

#### 3. **Socket 的监听（仅服务器端）**

**监听 Socket** 是使服务器端的 Socket 进入监听状态，准备接受客户端的连接请求。

##### **Python 示例**

```python
# 监听连接请求
sock.listen(5)  # 允许最多 5 个连接排队
```

##### **C++ 示例**

```cpp
if (listen(sockfd, 5) < 0) {
    perror("listen");
    return 1;
}
```

#### 4. **Socket 的连接（客户端）**

**连接到服务器** 是客户端通过 Socket 连接到服务器端的 IP 地址和端口。

##### **Python 示例**

```python
# 创建一个 TCP 套接字
sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# 连接到服务器
sock.connect(('localhost', 12345))
```

##### **C++ 示例**

```cpp
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <cstring>
#include <unistd.h>

int main() {
    int sockfd = socket(AF_INET, SOCK_STREAM, 0);

    struct sockaddr_in server_addr;
    server_addr.sin_family = AF_INET;
    server_addr.sin_port = htons(12345);
    inet_pton(AF_INET, "127.0.0.1", &server_addr.sin_addr);

    if (connect(sockfd, (struct sockaddr*)&server_addr, sizeof(server_addr)) < 0) {
        perror("connect");
        return 1;
    }

    return 0;
}
```

#### 5. **Socket 的接受（仅服务器端）**

**接受连接** 是服务器端接受客户端的连接请求，并创建一个新的 Socket 用于与客户端通信。

##### **Python 示例**

```python
# 接受客户端连接
client_socket, client_address = sock.accept()
```

##### **C++ 示例**

```cpp
#include <sys/socket.h>
#include <netinet/in.h>
#include <unistd.h>
#include <cstring>

int main() {
    int sockfd = socket(AF_INET, SOCK_STREAM, 0);

    struct sockaddr_in server_addr;
    server_addr.sin_family = AF_INET;
    server_addr.sin_addr.s_addr = INADDR_ANY;
    server_addr.sin_port = htons(12345);

    bind(sockfd, (struct sockaddr*)&server_addr, sizeof(server_addr));
    listen(sockfd, 5);

    int client_sockfd = accept(sockfd, nullptr, nullptr);
    if (client_sockfd < 0) {
        perror("accept");
        return 1;
    }

    return 0;
}
```

#### 6. **Socket 关闭**

在通信结束后，应关闭 Socket 以释放资源。

##### **Python 示例**

```python
# 关闭 Socket
sock.close()
```

##### **C++ 示例**

```cpp
close(sockfd);
```

### 总结

Socket 的创建与连接是网络编程的基础步骤：

1. **创建 Socket**：通过系统调用创建网络端点。
2. **绑定 Socket**（服务器端）：将 Socket 绑定到指定的 IP 地址和端口。
3. **监听**（服务器端）：使 Socket 进入监听状态，等待连接请求。
4. **连接**（客户端）：连接到服务器端的指定 IP 地址和端口。
5. **接受连接**（服务器端）：接受客户端的连接请求，并建立新的 Socket。
6. **关闭 Socket**：结束通信并释放资源。

这些操作构成了网络应用程序的基础，通过正确使用这些操作，可以实现各种网络通信功能。