# UDP to TCP Converter (udp2tcp-proxy)

A lightweight, high-performance UDP to TCP protocol converter that captures UDP datagrams and forwards them over TCP connections with automatic reconnection and batch processing support.

## ✨ Features

- 🧵 **Multi-threaded** - Handle multiple UDP ports simultaneously
- 📦 **Batch processing** - Collect multiple UDP packets before TCP transmission (reduces overhead)
- 🔄 **Automatic reconnection** - Maintains TCP connection with retry logic
- ⚡ **TCP_NODELAY** - Disables Nagle's algorithm for low latency
- 🚫 **Non-blocking sends** - Uses `MSG_NOSIGNAL` to prevent SIGPIPE
- 🪶 **Small footprint** - Minimal dependencies, pure C implementation

## 🎯 Use Cases

- 🚇 Tunneling UDP traffic (DNS, VPN, gaming) through TCP-only networks
- 🔥 Bypassing firewall restrictions that block UDP
- 🔄 Protocol conversion for legacy systems
- 🐛 Network debugging and testing
- 📡 IoT sensor data aggregation

## 🔨 build

- gcc udp2tcp.c -o udp2tcp -pthread

## 📦 Install system-wide (optional)
sudo install -m 755 udp2tcp /usr/local/bin

### Prerequisites
- 🐧 Linux/Unix system
- 🔨 GCC compiler
- 📚 pthread library

## 🚀 Usage
- ./udp2tcp <udp_port> <count> <tcp_ip> <tcp_port> <threads>

## 📊 Architecture Diagram
┌─────────────┐      ┌──────────────────────┐      ┌─────────────┐
│   UDP       │      │   udp2tcp-proxy      │      │   TCP       │
│   Clients   │─────►│                      │─────►│   Server    │
│             │      │  ┌─────┐ ┌─────┐     │      │             │
│  ┌───────┐  │      │  │ W1  │ │ W2  │     │      │  ┌───────┐  │
│  │Packet1│  │      │  ├─────┤ ├─────┤     │      │  │Packet1│  │
│  │Packet2│  │      │  │Batch│ │Batch│     │      │  │Packet2│  │
│  │PacketN│  │      │  └─────┘ └─────┘     │      │  │PacketN│  │
│  └───────┘  │      │      ↓  ↓           │      │  └───────┘  │
└─────────────┘      │  ┌──────────────┐    │      └─────────────┘
                     │  │   TCP Send   │    │
                     │  │  (batched)   │    │
                     │  └──────────────┘    │
                     │       ↓ ↓ ↓          │
                     │  🔄 Auto-reconnect  │
                     └──────────────────────┘

## ⚙️ Configuration Tuning
┌─────────────────────────────────────────────────────────────┐
│  📊 BATCH SIZE GUIDE                                        │
├──────────────┬──────────────────────────────────────────────┤
│  🎯 1-5      │  Latency-sensitive (gaming, VoIP)           │
│  ⚖️ 10-20    │  Balanced for general use                   │
│  🚀 32-64    │  Throughput optimized (bulk data)            │
├──────────────┼──────────────────────────────────────────────┤
│  💻 THREADS                                                 │
│  1-2         │  Low traffic or single-core                  │
│  4-8         │  High traffic on multi-core                  │
│  CPU_cores*2 │  Heavy workloads (formula)                   │
└──────────────┴──────────────────────────────────────────────┘
