# Advanced C Network Message Processor

A high-performance network message processing system built in C for learning advanced systems programming concepts. This project handles 5G Layer 2 protocol messages and IP packets with multi-processing architecture, custom memory management, and real-time analysis capabilities.

## 🎯 Project Goals

This is a learning project designed to master advanced C programming through hands-on implementation of:

- **Message Generation**: Create realistic 5G MAC PDU and IP packet structures
- **Custom Buffer Management**: Lock-free ring buffers and memory pool allocators
- **Multi-Processing**: Process pools with IPC mechanisms (shared memory, message queues, semaphores)
- **Protocol Analysis**: Parse and analyze 5G Layer 2 and IP/TCP/UDP protocols
- **Performance Optimization**: Cache-aware design, CPU affinity, and profiling

## 🏗️ Architecture Overview

```
┌─────────────────┐
│   Generator     │  Creates 5G MAC PDUs & IP packets
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Ring Buffer    │  Lock-free shared memory buffer
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Worker Pool    │  Multi-process/thread workers
│  (fork/pthread) │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│    Analyzer     │  Protocol parsing & statistics
└─────────────────┘
```

## 🚀 Features

### Message Generation
- IPv4/IPv6 packet generation with configurable parameters
- 5G NR MAC PDU generation (R/F/LCID subheaders)
- Realistic traffic patterns and randomization
- Configurable payload sizes and rates

### Buffer Management
- Lock-free single-producer/single-consumer ring buffer
- Custom memory pool allocator with free list
- Buffer leak detection and profiling
- Statistics tracking (drops, utilization, latency)

### Multi-Processing
- Fork-based worker process pool
- POSIX shared memory segments
- Message queue-based IPC
- Semaphore synchronization
- Unix domain socket control channel
- Optional pthread worker threads

### Protocol Analysis
- IPv4/IPv6 header parsing and checksum validation
- TCP/UDP/ICMP payload extraction
- 5G MAC PDU decoding (headers, subheaders, SDUs)
- RLC AM/UM segment reassembly
- Flow tracking with 5-tuple hash tables
- Real-time throughput and error rate metrics

### Performance & Optimization
- CPU affinity and NUMA awareness
- Cache-aligned data structures
- Profiling integration (perf, gprof)
- Valgrind/Helgrind testing
- Hot path optimization

## 📁 Project Structure

```
advanced-c-network-processor/
├── src/
│   ├── generator/      # Message generation modules
│   ├── buffer/         # Ring buffer & memory pool
│   ├── workers/        # Multi-processing logic
│   ├── analyzer/       # Protocol parsing & analysis
│   ├── ipc/            # IPC mechanisms
│   └── main.c          # Main entry point
├── include/
│   ├── common.h        # Common definitions
│   ├── messages.h      # Protocol structures
│   ├── buffer.h        # Buffer interfaces
│   └── stats.h         # Statistics structures
├── tests/
│   ├── unit/           # Unit tests
│   └── integration/    # Integration tests
├── docs/
│   ├── architecture.md
│   └── api-reference.md
├── config/
│   └── default.conf    # Configuration file
├── Makefile
├── README.md
└── roadmap.html        # Development roadmap
```

## 🛠️ Technologies & Concepts

**Core C Concepts:**
- Struct packing and memory alignment
- Bitwise operations and bit fields
- Pointer arithmetic and manual memory management
- Function pointers and callbacks
- Volatile and atomic operations

**Systems Programming:**
- POSIX IPC (shared memory, message queues, semaphores)
- Process management (fork, exec, wait)
- Thread programming (pthread)
- Signal handling
- Unix domain sockets

**Networking:**
- IPv4/IPv6 protocol stack
- TCP/UDP/ICMP protocols
- 5G NR Layer 2 (MAC, RLC)
- Checksum algorithms
- Packet parsing techniques

**Performance Engineering:**
- Lock-free data structures
- Custom memory allocators
- Cache optimization
- CPU pinning and NUMA
- Profiling and benchmarking

## 📚 Prerequisites

**Required Knowledge:**
- Strong C fundamentals (pointers, memory management, structs)
- Basic understanding of networking concepts
- Linux/Unix system calls
- Command-line tools and debugging

**Development Environment:**
- GCC or Clang compiler
- GNU Make
- Linux environment (Ubuntu/Debian recommended)
- Valgrind for memory debugging
- GDB for debugging

**Recommended Reading:**
- "The Linux Programming Interface" by Michael Kerrisk
- "Computer Networks" by Andrew Tanenbaum
- 3GPP TS 38.321 (5G NR MAC protocol specification)
- RFC 791 (IPv4), RFC 8200 (IPv6)

## 🚦 Getting Started

### Build

```bash
make all
```

### Run

```bash
# Run with default configuration
./bin/network_processor

# Run with custom config
./bin/network_processor -c config/custom.conf

# Run with specific parameters
./bin/network_processor --workers 4 --rate 10000 --protocol ip
```

### Test

```bash
# Run unit tests
make test

# Run with valgrind
make valgrind

# Run stress test
make stress-test
```

## 📊 Configuration

The system is configured via `config/default.conf`:

```ini
[generator]
protocol = 5g_mac      # 5g_mac, ip, both
rate = 5000            # messages per second
payload_size = 1500    # bytes

[buffer]
size = 4096            # ring buffer size (power of 2)
pool_size = 8192       # memory pool buffers

[workers]
count = 4              # number of worker processes
affinity = true        # enable CPU affinity

[analyzer]
flow_tracking = true
stats_interval = 1     # seconds
```

## 🎓 Learning Path

This project follows a structured 12-week roadmap:

1. **Weeks 1-2**: Foundation & message generation
2. **Weeks 3-4**: Advanced buffering system
3. **Weeks 5-7**: Multi-processing architecture
4. **Weeks 8-10**: Message analysis & processing
5. **Weeks 11-12**: Integration, testing & optimization

See `roadmap.html` for detailed milestones and task breakdowns.

## 🔍 Key Learning Outcomes

By completing this project, you will gain deep expertise in:

- **Low-level memory management** and custom allocators
- **Concurrent programming** with processes and threads
- **IPC mechanisms** and synchronization primitives
- **Protocol implementation** and binary data parsing
- **Performance optimization** and profiling techniques
- **Production-quality C code** with proper error handling

## 📈 Performance Goals

- **Throughput**: Process 100K+ messages/second
- **Latency**: <10μs average processing time per message
- **Memory**: Zero memory leaks, efficient buffer utilization
- **CPU**: Balanced load across worker processes

## 🧪 Testing Strategy

- **Unit tests**: Each module tested independently
- **Integration tests**: End-to-end pipeline validation
- **Stress tests**: High load scenarios
- **Memory tests**: Valgrind leak and race detection
- **Performance tests**: Profiling and benchmarking

## 🤝 Contributing

This is a personal learning project, but feel free to fork and adapt it for your own learning journey!

## 📝 License

MIT License - Feel free to use this for learning purposes

## 🔗 Resources

- [3GPP 5G Specifications](https://www.3gpp.org/specifications-technologies/specifications-by-series)
- [RFC Editor - Internet Standards](https://www.rfc-editor.org/)
- [Linux Man Pages](https://man7.org/linux/man-pages/)
- [Beej's Guide to Network Programming](https://beej.us/guide/bgnet/)

## 📧 Contact

Questions or suggestions? Open an issue or reach out!

---

**Note**: This project is for educational purposes. It implements simplified versions of protocols for learning systems programming concepts.
