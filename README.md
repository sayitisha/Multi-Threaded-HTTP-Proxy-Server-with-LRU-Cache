# Multi-Threaded HTTP Proxy Server with LRU Cache (C, Linux)

A high-performance multi-threaded HTTP proxy server implemented in C using POSIX sockets on Linux.  
The server forwards client HTTP requests to remote web servers and integrates a thread-safe LRU cache to optimize performance and reduce redundant network calls.

---

## 🚀 Features

- Multi-threaded request handling (concurrent client connections)
- POSIX socket programming (TCP/IP)
- Thread-safe LRU caching mechanism
- HTTP request parsing and forwarding
- Mutex and semaphore-based concurrency control
- Low-level I/O operations in C
- Load-tested for concurrent client handling

---

## 🧠 Architecture Overview

Client → Proxy Server → Remote Web Server → Proxy → Client

### Core Components:

- **Socket Layer**
  - `socket()`, `bind()`, `listen()`, `accept()`
  - `connect()` for remote servers
  - `send()` / `recv()` for communication

- **Thread Model**
  - Main thread listens for connections
  - Spawns new thread per client
  - Each thread processes request independently

- **LRU Cache**
  - Hash map for O(1) lookup
  - Doubly linked list for recency tracking
  - Thread-safe using mutex locks and semaphores
  - Automatic eviction of least recently used items

- **Concurrency Control**
  - Mutex locks to protect shared cache
  - Semaphores for synchronization
  - Prevention of race conditions

---

## 📸 Demo

### First Request (Cache Miss)

When the website is opened for the first time, the URL is not present in the cache.

![Cache Miss Demo](demo.png)

Console output:
- `URL not found`
- Cache miss occurs
- Data fetched from remote server
- Entry added to cache

---

### Second Request (Cache Hit)

When the same website is opened again, the response is retrieved directly from the cache.

Console output:
- `LRU Track Before`
- `LRU Track After`
- `Data retrieved from the cache`

This significantly reduces latency and avoids redundant network calls.

---

## 🛠️ Technologies Used

- C (System Programming)
- POSIX Sockets
- TCP/IP Protocol
- Linux
- Multi-threading (pthreads)
- Mutex & Semaphores
- Dynamic Memory Management

---

## 🧪 How to Run

```bash
gcc proxy.c -o proxy -lpthread
./proxy <port_number>
