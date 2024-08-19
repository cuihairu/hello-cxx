### 网络协议

- **[网络协议概述](networking/protocols/overview.md)**
  - 网络协议的定义与作用
  - 协议层次结构
  - 协议与标准化组织

- **[传输层协议：TCP 与 UDP](networking/protocols/tcp-udp.md)**
  - **TCP（传输控制协议）**
    - 连接建立与断开
    - 数据传输与重传机制
    - 流量控制与拥塞控制
    - TCP的三次握手与四次挥手
  - **UDP（用户数据报协议）**
    - 无连接特性
    - 数据报文格式
    - 应用场景
    - UDP与TCP的比较

- **[应用层协议：HTTP、FTP、DNS 等](networking/protocols/application-layer.md)**
  - **HTTP（超文本传输协议）**
    - HTTP请求与响应
    - 状态码及其含义
    - HTTP/1.0、HTTP/1.1、HTTP/2 的比较
    - HTTPS与TLS/SSL
  - **FTP（文件传输协议）**
    - FTP的工作模式（主动模式与被动模式）
    - 命令与响应
    - FTP的安全性考虑
  - **DNS（域名系统）**
    - DNS查询过程
    - DNS记录类型（A记录、CNAME记录、MX记录等）
    - DNS的缓存与负载均衡

- **[协议解析与数据包捕获](networking/protocols/packet-capture.md)**
  - **数据包结构**
    - 数据包的组成部分（头部、负载）
    - 数据包的格式（以太网帧、IP包、TCP/UDP段）
  - **协议解析**
    - 数据包的解析方法
    - 使用Wireshark等工具进行协议分析
  - **数据包捕获**
    - 捕获工具的使用（如tcpdump、Wireshark）
    - 数据包捕获的技巧与方法

这些内容提供了关于网络协议的全面概述，包括传输层和应用层的主要协议、数据包结构的解析以及协议分析的工具和方法。这些知识对于理解网络通信的机制和调试网络应用程序是非常重要的。