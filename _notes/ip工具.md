---
title: ip工具
date: 2025-03-08 14:20:08
feed: show
---
相比于传统的`ifconfig`命令，`ip`是Linux系统中较新的网络配置工具集（`iproute2`包中的一部分）。`ifconfig`在一些较老的Linux发行版中使用较多，但`ip`功能更强大、更灵活，并且在现代的Linux系统网络管理中逐渐成为主流。
# 使用ip address得到的信息介绍
在 Linux 中使用 `ip address` 命令（通常简写为 `ip addr`）可以显示系统中所有网络接口的 IP 地址配置和状态信息。输出内容可能看起来有些复杂，但每一行都有明确的含义。以下是对其输出的逐行解析，结合一个典型的示例来说明：

### 示例输出
假设运行 `ip addr` 后得到以下输出：
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 00:16:17:2a:3b:4c brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.100/24 brd 192.168.1.255 scope global dynamic eth0
       valid_lft 86399sec preferred_lft 86399sec
    inet6 fe80::216:17ff:fe2a:3b4c/64 scope link 
       valid_lft forever preferred_lft forever
```

### 逐行解析

#### 第一行：接口名称和状态
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
```
- **`1:`**：接口的索引号（每个网络接口都有一个唯一的数字标识）。
- **`lo:`**：网络接口的名称，这里是 `lo`，表示回环接口（loopback）。
- **`<LOOPBACK,UP,LOWER_UP>`**：接口的标志（flags），表示接口的属性和状态：
  - `LOOPBACK`：这是一个回环接口，用于本地通信。
  - `UP`：接口已启用。
  - `LOWER_UP`：物理层（数据链路层）已激活。
- **`mtu 65536`**：最大传输单元（Maximum Transmission Unit），表示该接口支持的最大数据包大小（单位：字节）。这里是 65536 字节。
- **`qdisc noqueue`**：队列规则（queueing discipline），`noqueue` 表示没有特定的流量控制队列。
- **`state UNKNOWN`**：接口状态，这里是 `UNKNOWN`（回环接口通常如此）。
- **`group default`**：接口所属的分组，默认是 `default`。
- **`qlen 1000`**：传输队列长度（queue length），表示可以排队的最大数据包数量。

#### 第二行：链路层信息
```
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
```
- **`link/loopback`**：链路类型，这里是 `loopback`，表示回环接口。
- **`00:00:00:00:00:00`**：MAC 地址（硬件地址）。回环接口没有真实的物理地址，因此是全零。
- **`brd 00:00:00:00:00:00`**：广播地址（broadcast address），回环接口没有广播地址，因此也是全零。

#### 第三行：IPv4 地址信息
```
    inet 127.0.0.1/8 scope host lo
```
- **`inet`**：表示这是 IPv4 地址。
- **`127.0.0.1/8`**：IP 地址和子网掩码。`127.0.0.1` 是回环地址，`/8` 表示子网掩码为 `255.0.0.0`。
- **`scope host`**：地址的作用范围，`host` 表示仅在本机有效。
- **`lo`**：该地址绑定到的接口名称。

#### 第四行：IPv4 地址有效期
```
       valid_lft forever preferred_lft forever
```
- **`valid_lft forever`**：地址的有效寿命（valid lifetime），`forever` 表示永久有效。
- **`preferred_lft forever`**：地址的首选寿命（preferred lifetime），`forever` 表示永久首选。

#### 第五行及第六行：IPv6 地址信息
```
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
```
- **`inet6`**：表示这是 IPv6 地址。
- **`::1/128`**：IPv6 回环地址，`/128` 表示子网掩码全为 1（单一地址）。
- **`scope host`**：作用范围为本机。
- **`valid_lft` 和 `preferred_lft`**：同 IPv4，均为永久有效。

---

#### 另一个接口示例（eth0）
```
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 00:16:17:2a:3b:4c brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.100/24 brd 192.168.1.255 scope global dynamic eth0
       valid_lft 86399sec preferred_lft 86399sec
    inet6 fe80::216:17ff:fe2a:3b4c/64 scope link 
       valid_lft forever preferred_lft forever
```
- **`2: eth0:`**：接口索引为 2，名称为 `eth0`（通常是以太网接口）。
- **`<BROADCAST,MULTICAST,UP,LOWER_UP>`**：
  - `BROADCAST`：支持广播。
  - `MULTICAST`：支持多播。
  - `UP` 和 `LOWER_UP`：接口和物理层都已激活。
- **`mtu 1500`**：以太网常见的 MTU 值。
- **`qdisc fq_codel`**：流量控制队列类型，`fq_codel` 是一种公平队列算法。
- **`state UP`**：接口状态为启用。
- **`link/ether 00:16:17:2a:3b:4c`**：真实的 MAC 地址。
- **`brd ff:ff:ff:ff:ff:ff`**：广播地址（全 1）。
- **`inet 192.168.1.100/24`**：IPv4 地址为 `192.168.1.100`，子网掩码为 `/24`（即 `255.255.255.0`）。
- **`brd 192.168.1.255`**：子网的广播地址。
- **`scope global`**：地址作用范围为全局（可用于网络通信）。
- **`dynamic`**：地址是动态分配的（例如通过 DHCP）。
- **`valid_lft 86399sec`**：地址有效期为 86399 秒（约 24 小时）。
- **`inet6 fe80::216:17ff:fe2a:3b4c/64`**：IPv6 链接本地地址（link-local），以 `fe80::` 开头。
- **`scope link`**：作用范围为本地链接。

### 总结
`ip address` 命令的输出可以分为以下几部分：
1. **接口信息**：接口名称、状态、属性（如 MTU、队列等）。
2. **链路层信息**：MAC 地址和广播地址。
3. **网络层信息**：IPv4 和 IPv6 地址、子网掩码、作用范围、有效期等。

