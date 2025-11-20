# Exercise 47: Producer-Consumer

## 🎯 Objectives

Implement the producer-consumer pattern:

- Multiple producers generating work
- Multiple consumers processing work
- Channel-based communication (mpsc)
- Work queue management
- Graceful shutdown mechanism

## 📚 Concepts

- Producer-Consumer pattern
- Multi-producer single-consumer channels
- Thread synchronization
- Work distribution
- Graceful shutdown
- Channel closure and signaling

## 📖 Background

**Producer-Consumer pattern** is a classic concurrency design where:

- **Producers** generate tasks/data
- **Consumers** process tasks/data
- **Queue** decouples producers from consumers

This enables load balancing and parallel processing.

**Real-world examples:**

```
Web server:
  - Producers: incoming HTTP requests
  - Queue: request queue
  - Consumers: worker threads handling requests

Print spooler:
  - Producers: applications sending print jobs
  - Queue: print queue
  - Consumers: printer drivers

Video encoding:
  - Producers: video frames being read
  - Queue: frame buffer
  - Consumers: encoding threads
```

**Common use cases:**

- Task processing systems
- Message queues
- Pipeline architectures
- Background job processing

## ⚙️ Requirements

**First Pass:**

- ✅ N producer threads generating work
- ✅ M consumer threads processing work
- ✅ Use mpsc channel for communication
- ✅ Tasks flow from producers to consumers
- ✅ System completes all work before exiting
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain the pattern and your design
- ✅ **Configurable**:
  - Number of producers (configurable)
  - Number of consumers (configurable)
  - Queue capacity (bounded vs unbounded)
  - Task generation rate
- ✅ **Shutdown mechanisms**:
  - Graceful: finish all pending work
  - Immediate: stop accepting new work
  - Timeout-based
  - Signal-based (Ctrl+C)
- ✅ **Monitoring**:
  - Track tasks generated
  - Track tasks processed
  - Track tasks pending
  - Monitor consumer utilization
- ✅ **Error handling**:
  - Task processing failures
  - Producer failures
  - Consumer failures
  - Channel closure
- ✅ **Backpressure**:
  - Handle full queue scenarios
  - Producer blocking when appropriate

## 🚫 Constraints

- Use `std::sync::mpsc` for channels
- Standard library threading
- No leaked threads (clean shutdown)

## 💡 Approaches

**Channel types:**

- Unbounded channel: unlimited queue size
- Bounded channel: fixed capacity, producers block when full

**Work distribution:**

- Automatic via channel (first available consumer gets task)
- Round-robin if you manage it manually
- Priority-based if you use multiple channels
- Work stealing for advanced load balancing

**Shutdown strategies:**

- Close sender: consumers detect and exit
- Sentinel value: special "stop" task
- Shared atomic flag: check before each operation
- Timeout: consumers exit after idle period

**Thread coordination:**

- Join handles to wait for completion
- Shared counters for statistics
- Mutex-wrapped receiver for multiple consumers
- Atomic operations for lock-free counting

**Error handling:**

- Continue on task failure
- Retry failed tasks
- Dead letter queue for failures
- Graceful degradation

Pick the strategies that fit your design goals.

## ✅ Validation

Your system should handle these scenarios:

**Basic operation:**

```
Starting system: 3 producers, 2 consumers

Producer 0 created task 0
Producer 1 created task 100
Consumer 0 processing task 0
Consumer 1 processing task 100
Producer 2 created task 200
Producer 0 created task 1
Consumer 0 processing task 200
...

All producers finished
All consumers finished
Total tasks: 150
```

**Statistics tracking:**

```
Statistics (updated every second):
  Produced: 45
  Consumed: 32
  Pending: 13
  Failed: 0

Statistics (final):
  Produced: 150
  Consumed: 150
  Pending: 0
  Failed: 3
```

**Graceful shutdown:**

```
Running... Press Ctrl+C to stop

^C
Shutdown signal received
Producer 0 shutting down gracefully
Producer 1 shutting down gracefully
Producer 2 shutting down gracefully
Finishing pending work...
Consumer 0 finished
Consumer 1 finished

Final stats: 147 tasks completed
```

**Backpressure (bounded queue):**

```
Queue capacity: 10 items

Producer 0: fast (created 50 tasks)
Producer 1: fast (created 50 tasks)
Producer 2: blocked (queue full, waiting...)
Consumer 0: slow (processing...)
Consumer 1: slow (processing...)

Queue: [██████████] 10/10 FULL
Producer 2: resuming (queue has space)
```

**Error handling:**

```
Consumer 0 processing task 10
Task 10 failed: simulated error
Consumer 0 continuing...
Consumer 1 processing task 11
Task 11 completed successfully

Final stats:
  Success: 147
  Failed: 3
```

## 🔍 Challenge

Implement work stealing where idle consumers can steal tasks from busy consumers' local queues, or create a priority queue system where high-priority tasks jump to the front of the queue.

---

**Previous:** [46_concurrent_downloader](../46_concurrent_downloader/README.md) | **Next:** [48_chat_server](../48_chat_server/README.md)
