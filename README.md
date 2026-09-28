# keyStore

A lightweight Redis-style key-value store written in C++. It uses Linux `epoll` for non-blocking network I/O, accepts commands through the Redis Serialization Protocol (RESP), and persists data to disk.

## Features

- Single-threaded event loop powered by `epoll`
- Non-blocking client connections
- RESP command parsing and responses
- String, list, and hash data structures
- Key expiration
- Automatic persistence to `server/dump` every 30 seconds
- Graceful shutdown on `Ctrl+C`
- Up to 32 simultaneous clients

## Requirements

- Linux or WSL (`epoll` is Linux-specific)
- A C++ compiler with C++11 support or newer
- GNU Make
- Optional: `redis-cli` for interacting with the server

## Build and run

```bash
cd server
make
./server
```

The server listens on port `6379` by default. Pass a different port as the first argument:

```bash
./server 6380
```

## Usage

Connect with `redis-cli`:

```bash
redis-cli -p 6379
```

Example session:

```text
SET language cpp
GET language
LPUSH tasks build
LGET tasks
HSET user:1 name Rajeev
HGET user:1 name
```

## Supported commands

| Category | Commands |
| --- | --- |
| General | `PING`, `ECHO`, `FLUSHALL` |
| Keys and strings | `SET`, `GET`, `KEYS`, `TYPE`, `DEL`, `EXISTS`, `RENAME`, `EXPIRE` |
| Lists | `LLEN`, `LGET`, `LPUSH`, `RPUSH`, `LPOP`, `RPOP`, `LREM`, `LINDEX`, `LSET` |
| Hashes | `HSET`, `HGET`, `HDEL`, `HEXISTS`, `HGETALL`, `HKEYS`, `HVALS`, `HLEN` |

## Project structure

```text
server/
├── include/    # Header files
├── src/        # Server, database, command handling, and entry point
├── build/      # Compiled object files
├── Makefile
└── dump        # Persisted database snapshot
```

## Author

K Rajeev
