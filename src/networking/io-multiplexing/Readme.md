# 常见平台的 I/O 复用模型

I/O 复用是指在单个线程中处理多个 I/O 操作的能力。它允许程序在等待 I/O 操作完成时，继续处理其他任务。不同平台提供了不同的 I/O 复用模型，以下是一些常见的平台 I/O 复用模型的概述：

#### 1. **Linux 下的 I/O 复用模型**

**1.1. `select`**

- **概述**：`select` 是最早的 I/O 复用机制之一。它允许程序检查多个文件描述符是否可读、可写或是否有异常状态。
- **优点**：简单，广泛支持。
- **缺点**：性能在处理大量文件描述符时下降，`select` 的文件描述符集有最大限制（通常为 1024）。

```c
#include <sys/select.h>
#include <unistd.h>
#include <stdio.h>

int main() {
    fd_set readfds;
    FD_ZERO(&readfds);
    FD_SET(0, &readfds);  // 监听标准输入

    // 设置超时时间
    struct timeval timeout;
    timeout.tv_sec = 5;
    timeout.tv_usec = 0;

    int result = select(1, &readfds, NULL, NULL, &timeout);
    if (result > 0) {
        if (FD_ISSET(0, &readfds)) {
            printf("Data is available to read\n");
        }
    } else if (result == 0) {
        printf("Timeout\n");
    } else {
        perror("select");
    }

    return 0;
}
```

**1.2. `poll`**

- **概述**：`poll` 提供了比 `select` 更好的扩展性。它使用 `pollfd` 结构数组来监视多个文件描述符。
- **优点**：支持更多的文件描述符，没有 `select` 的最大限制。
- **缺点**：性能仍然随着文件描述符的增加而下降，`poll` 也会线性扫描所有文件描述符。

```c
#include <poll.h>
#include <unistd.h>
#include <stdio.h>

int main() {
    struct pollfd fds[1];
    fds[0].fd = 0;           // 标准输入
    fds[0].events = POLLIN;  // 可读事件

    int result = poll(fds, 1, 5000);  // 5秒超时
    if (result > 0) {
        if (fds[0].revents & POLLIN) {
            printf("Data is available to read\n");
        }
    } else if (result == 0) {
        printf("Timeout\n");
    } else {
        perror("poll");
    }

    return 0;
}
```

**1.3. `epoll`**

- **概述**：`epoll` 是 Linux 特有的 I/O 复用机制，设计用于处理大量文件描述符。它提供了更高效的性能和更低的资源消耗。
- **优点**：高效，支持大规模文件描述符，没有 `select` 和 `poll` 的限制。
- **缺点**：只在 Linux 上可用。

```c
#include <sys/epoll.h>
#include <unistd.h>
#include <stdio.h>

#define MAX_EVENTS 10

int main() {
    int epoll_fd = epoll_create1(0);
    if (epoll_fd < 0) {
        perror("epoll_create1");
        return 1;
    }

    struct epoll_event event;
    event.events = EPOLLIN;
    event.data.fd = 0;  // 标准输入

    if (epoll_ctl(epoll_fd, EPOLL_CTL_ADD, 0, &event) < 0) {
        perror("epoll_ctl");
        close(epoll_fd);
        return 1;
    }

    struct epoll_event events[MAX_EVENTS];
    int nfds = epoll_wait(epoll_fd, events, MAX_EVENTS, 5000);  // 5秒超时
    if (nfds > 0) {
        for (int i = 0; i < nfds; i++) {
            if (events[i].events & EPOLLIN) {
                printf("Data is available to read\n");
            }
        }
    } else if (nfds == 0) {
        printf("Timeout\n");
    } else {
        perror("epoll_wait");
    }

    close(epoll_fd);
    return 0;
}
```

**1.4. `io_uring`**

- **概述**：`io_uring` 是 Linux 5.1 引入的异步 I/O 机制，提供了高效的异步 I/O 操作。
- **优点**：高效，支持异步 I/O，减少系统调用开销。
- **缺点**：需要 Linux 5.1 及以上版本支持。

```c
#include <liburing.h>
#include <fcntl.h>
#include <unistd.h>
#include <stdio.h>

int main() {
    struct io_uring ring;
    io_uring_queue_init(32, &ring, 0);

    // 添加提交队列请求
    struct io_uring_sqe *sqe = io_uring_get_sqe(&ring);
    io_uring_prep_read(sqe, 0, NULL, 0, 0);

    io_uring_submit(&ring);

    // 等待完成
    struct io_uring_cqe *cqe;
    io_uring_wait_cqe(&ring, &cqe);
    if (cqe->res < 0) {
        perror("I/O error");
    } else {
        printf("Read completed successfully\n");
    }

    io_uring_cqe_seen(&ring, cqe);
    io_uring_queue_exit(&ring);
    return 0;
}
```

#### 2. **Windows 下的 I/O 复用模型**

**2.1. I/O 完成端口 (IOCP)**

- **概述**：IOCP 是 Windows 提供的高效 I/O 复用机制，支持高性能的异步 I/O 操作。
- **优点**：高效，支持大规模并发 I/O 操作。
- **缺点**：实现复杂。

```cpp
#include <windows.h>
#include <iostream>

int main() {
    HANDLE iocp = CreateIoCompletionPort(INVALID_HANDLE_VALUE, NULL, 0, 0);
    if (iocp == NULL) {
        std::cerr << "CreateIoCompletionPort failed" << std::endl;
        return 1;
    }

    // 使用 IOCP 进行异步 I/O 操作
    // ...

    CloseHandle(iocp);
    return 0;
}
```

#### 3. **BSD 系统中的 I/O 复用模型**

**3.1. `kqueue`**

- **概述**：`kqueue` 是 BSD 系统提供的高效 I/O 复用机制，支持事件通知。
- **优点**：高效，支持多种事件类型。
- **缺点**：仅在 BSD 系统上可用（包括 macOS）。

```c
#include <sys/types.h>
#include <sys/event.h>
#include <unistd.h>
#include <stdio.h>

int main() {
    int kq = kqueue();
    if (kq < 0) {
        perror("kqueue");
        return 1;
    }

    struct kevent change;
    EV_SET(&change, 0, EVFILT_READ, EV_ADD, 0, 0, NULL);

    struct kevent event;
    int nev = kevent(kq, &change, 1, &event, 1, NULL);
    if (nev > 0) {
        printf("Data is available to read\n");
    } else if (nev == 0) {
        printf("Timeout\n");
    } else {
        perror("kevent");
    }

    close(kq);
    return 0;
}
```

**3.2. `dev/poll`**

- **概述**：`dev/poll` 是 Solaris 系统中的 I/O 复用机制，支持大量文件描述符。
- **优点**：高效，支持大规模文件描述符。
- **缺点**：仅在 Solaris 系统上可用。

```c
#include <sys/types.h>
#include <sys/poll.h>
#include <unistd.h>
#include <stdio.h>

int main() {
    struct pollfd pfd;
    pfd.fd = 0;           // 标准输入
    pfd.events = POLLIN;  // 可读事件

    int ret = poll(&pfd, 1, 5000);  // 5秒超时
    if (ret > 0) {
        if (pfd.revents & POLLIN) {
            printf("Data is available to read\n");
        }
    } else if (ret == 0) {
        printf("Timeout\n");
    } else {
        perror("poll");
    }

    return 0;
}
```

### 总结

不同平台提供了不同的 I/O 复用模型：

- **Linux**：`select`、`poll`、`epoll`、`io_uring`。
- **Windows**：I/O 完成端口 (IOCP)。
- **BSD 系统**：`kqueue`、`dev/poll`。

选择合适的 I/O 复用模型可以提升程序的性能和扩展性。