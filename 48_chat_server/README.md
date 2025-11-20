# Exercise 48: Basic Chat Server

## 🎯 Objectives

Create a multi-client chat server:

- TCP listener accepting connections
- Broadcast messages to all clients
- Handle multiple simultaneous clients
- One thread per client connection
- Shared state for client management
- Clean disconnect handling

## 📚 Concepts

- TCP networking
- Thread-per-client model
- Shared mutable state
- Broadcasting to multiple clients
- Connection handling
- Concurrent I/O

## 📖 Background

**Chat servers** are the backbone of real-time communication. They manage multiple clients, route messages, and handle connections/disconnections.

**Basic architecture:**

```
Server listens on port 8080
↓
Client A connects → Server spawns thread A
Client B connects → Server spawns thread B
Client C connects → Server spawns thread C
↓
Client A sends "Hello"
↓
Server broadcasts to B and C
```

**Real-world examples:**

- IRC servers
- Slack/Discord (simplified)
- Game chat systems
- Collaborative editing tools

**Key challenges:**

- Multiple clients reading/writing simultaneously
- Keeping track of who's connected
- Broadcasting without blocking
- Handling disconnects gracefully
- Thread-safe access to shared client list

## ⚙️ Requirements

**First Pass:**

- ✅ TCP server listening on a port
- ✅ Accept multiple client connections
- ✅ Spawn thread per client
- ✅ Broadcast messages to all clients
- ✅ Handle client disconnect
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Doc comments explaining architecture
- ✅ **Features**:
  - Username/nickname support
  - Join/leave notifications
  - Private messages (whisper)
  - User list command
  - Server commands (/help, /list, /quit)
- ✅ **Message formatting**:
  - Timestamps on messages
  - Sender identification
  - System messages vs user messages
- ✅ **Error handling**:
  - Connection errors
  - Read/write errors
  - Client timeout
  - Invalid messages
- ✅ **Client management**:
  - Track connected clients
  - Remove disconnected clients
  - Prevent duplicate usernames
  - Client count/statistics
- ✅ **Robustness**:
  - Handle partial reads
  - Handle slow clients
  - Buffer overflow protection
  - Clean shutdown (Ctrl+C)

## 🚫 Constraints

- Use `std::net` for TCP
- Use `std::thread` for threading
- Standard library only (no async frameworks for now)
- Must handle shared state safely

## 💡 Approaches

**Server structure:**

- Need a way to accept connections
- Need to store list of connected clients
- Need thread-safe access to client list

**Threading model:**

- One thread per client (simple)
- Thread pool (more efficient)
- Main thread accepts, worker threads handle

**Broadcasting strategy:**

- Loop through all clients and send
- Queue messages for each client
- Use channels between threads

**Shared state:**

- HashMap of clients
- Vector of client handles
- Need synchronization (Mutex, RwLock)
- Need shared ownership (Arc)

**Client handling:**

- Read messages in a loop
- Parse commands vs regular messages
- Write to client stream
- Detect disconnect (read returns 0 or error)

**Data structures to consider:**

- Client ID (unique identifier)
- Client struct (name, stream, etc.)
- Message format (sender, text, timestamp)

## ✅ Validation

**Server output:**

```
Server listening on 127.0.0.1:8080

Alice connected (ID: 0)
Bob connected (ID: 1)
Carol connected (ID: 2)
Bob disconnected
Alice disconnected
Carol disconnected

Server stopped.
```

**Client session (Alice):**

```
$ telnet localhost 8080
Enter your name: Alice
*** Alice joined the chat
Hello everyone!
*** Bob joined the chat
Bob: Hi Alice!
Nice to meet you!
Bob: Same here
*** Bob left the chat
/list
Users online: Alice, Carol
/quit
*** You left the chat
```

**Client session (Bob):**

```
$ telnet localhost 8080
Enter your name: Bob
*** Bob joined the chat
Alice: Hello everyone!
Hi Alice!
Alice: Nice to meet you!
Same here
/quit
*** Bob left the chat
```

**Broadcast test:**

```
# All clients see all messages
Alice: Hello
Bob: Hi
Carol: Hey there
Alice: How is everyone?
Bob: Doing great!
Carol: All good!
```

**Commands:**

```
/help
Available commands:
  /help - Show this help
  /list - List all users
  /msg <user> <text> - Private message
  /quit - Disconnect

/list
Users online: Alice, Bob, Carol

/msg Alice Hey there!
[Private] You → Alice: Hey there!
```

**Edge cases to verify:**

```
Empty username → reject or assign default
Duplicate username → reject or append number
Client crashes → server detects and removes
Multiple quick connects → all handled
```

## 🔍 Challenge

Add authentication (username/password database), implement chat rooms/channels (clients can join different rooms), add file transfer capability, or implement flood protection (rate limit messages per client).

---

**Previous:** [47_producer_consumer](../47_producer_consumer/README.md) | **Next:** [49_parallel_sorter](../49_parallel_sorter/README.md)
