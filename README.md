# UDP to TCP Converter (udp2tcp-proxy)

A lightweight, high-performance UDP to TCP protocol converter that captures UDP datagrams and forwards them over TCP connections with automatic reconnection and batch processing support.

## Features

- **Multi-threaded** - Handle multiple UDP ports simultaneously
- **Batch processing** - Collect multiple UDP packets before TCP transmission (reduces overhead)
- **Automatic reconnection** - Maintains TCP connection with retry logic
- **TCP_NODELAY** - Disables Nagle's algorithm for low latency
- **Non-blocking sends** - Uses `MSG_NOSIGNAL` to prevent SIGPIPE
- **Small footprint** - Minimal dependencies, pure C implementation

## Use Cases

- Tunneling UDP traffic (DNS, VPN, gaming) through TCP-only networks
- Bypassing firewall restrictions that block UDP
- Protocol conversion for legacy systems
- Network debugging and testing
- IoT sensor data aggregation

## build
- gcc udp2tcp.c -o udp2tcp -pthread

# Install system-wide (optional)
sudo install -m 755 udp2tcp /usr/local/bin

### Prerequisites
- Linux/Unix system
- GCC compiler
- pthread library

## Usage
- ./udp2tcp <udp_port> <count> <tcp_ip> <tcp_port> <threads>
