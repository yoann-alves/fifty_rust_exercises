# Exercise 46: Concurrent Downloader

## 🎯 Objectives

Create a multi-threaded file downloader:

- Download multiple URLs concurrently
- Use threads for parallelism
- Track download progress for each file
- Handle errors per thread independently
- Thread-safe progress reporting

## 📚 Concepts

- Multi-threading
- Shared state and synchronization
- Channel communication
- HTTP requests
- Error handling across threads
- Progress tracking

## 📖 Background

**Downloading files one at a time is slow.** If you have 10 files to download, waiting for each one to finish before starting the next wastes time.

**Concurrent downloading** means starting multiple downloads at once:

```
Sequential (slow):
File1: [========] 10s
File2:            [========] 10s
File3:                       [========] 10s
Total: 30 seconds

Concurrent (fast):
File1: [========] 10s
File2: [========] 10s
File3: [========] 10s
Total: 10 seconds
```

**Real-world challenges:**

- Each download needs its own thread
- Threads need to report progress back to main program
- One download failing shouldn't crash the others
- Need to limit how many downloads run at once (not 1000 threads!)
- Files need to be saved safely without conflicts

**Progress tracking** makes users happy:

```
Downloading...
file1.zip: 45% (4.5 MB / 10 MB) - 1.2 MB/s
file2.pdf: 90% (900 KB / 1 MB) - 850 KB/s
file3.jpg: 100% - Complete ✓
```

## ⚙️ Requirements

**First Pass:**

- ✅ Download multiple URLs at the same time
- ✅ Each download runs in its own thread
- ✅ Show basic progress (how many files completed)
- ✅ Handle download failures without crashing
- ✅ Save downloaded files to disk
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain how concurrency works
- ✅ **Rich progress**:
  - Bytes downloaded for each file
  - Download speed (KB/s or MB/s)
  - Time remaining estimate
  - Real-time updates while downloading
- ✅ **Thread management**:
  - Limit concurrent downloads (e.g., max 5 at once)
  - Queue remaining downloads
  - Don't create unlimited threads
- ✅ **Error handling**:
  - Retry failed downloads (configurable number of attempts)
  - Continue downloading other files if one fails
  - Collect and report all errors at the end
  - Handle timeouts
- ✅ **Features**:
  - Resume partial downloads (use HTTP Range headers)
  - Verify checksums after download (optional)
  - Custom output directory
  - Extract filename from URL automatically
- ✅ **Thread communication**:
  - Send progress updates from threads to main
  - Report status changes
  - Clean shutdown (wait for all threads to finish)
- ✅ **User experience**:
  - Nice progress bars or indicators
  - Summary statistics at the end
  - Clear error messages

## 🚫 Constraints

- Use `reqwest` crate for HTTP requests
- Use `std::thread` for threading (or `rayon` for thread pools)
- Use channels (`mpsc`) for thread communication
- Handle all errors with `Result`

## 💡 Approaches

**Threading strategies:**

- One thread per download (simple but doesn't scale)
- Thread pool with fixed number of workers (better)
- Work queue where threads grab next task when ready

**Progress tracking methods:**

- Channels to send updates from worker threads to main
- Shared state with Arc and Mutex (more complex)
- Progress bars (consider using a crate)

**Download implementation:**

- Stream bytes in chunks (don't load entire file in memory)
- Track bytes downloaded vs total size
- Calculate speed from bytes per second
- Handle Content-Length header for total size

**Error recovery:**

- Retry with exponential backoff (wait 1s, 2s, 4s, 8s...)
- Save partial downloads to resume later
- Time out stuck downloads
- Continue with other downloads on failure

**Filename handling:**

- Extract from URL path
- Check Content-Disposition header
- Generate unique names if conflicts
- Sanitize filenames (remove invalid characters)

**Thread communication patterns:**

- Send messages from threads (Started, Progress, Complete, Failed)
- Main thread receives and displays updates
- Use channels that close when all senders drop

## ✅ Validation

Your downloader should handle these scenarios:

```bash
# Basic usage
$ cargo run -- https://example.com/file1.zip https://example.com/file2.pdf
Downloading 2 files...
✓ file1.zip (10.5 MB) - 2.3s
✓ file2.pdf (1.2 MB) - 0.8s
Complete: 2/2 files (11.7 MB total)
```

Progress during download:

```
[1/3] file1.zip    [======>   ] 60% (6.3 MB / 10.5 MB) 2.1 MB/s ETA: 2s
[2/3] file2.pdf    [=========>] 95% (1.1 MB / 1.2 MB) 1.4 MB/s ETA: 0s
[3/3] file3.jpg    [==========] 100% Complete ✓
```

Error handling:

```
[1/3] file1.zip - Success ✓
[2/3] invalid-url - Failed: Connection timeout
[3/3] file3.jpg - Success ✓

Summary:
Success: 2/3
Failed: 1/3
Total downloaded: 11.7 MB
```

Retry behavior:

```
Downloading file1.zip...
Attempt 1/3: Connection timeout
Retrying in 2s...
Attempt 2/3: Success ✓
```

Concurrent limit (max 3 at once):

```
Starting downloads (max 3 concurrent):
→ file1.zip (downloading)
→ file2.pdf (downloading)
→ file3.jpg (downloading)
→ file4.mp4 (queued)
→ file5.zip (queued)

file2.pdf complete!
→ file4.mp4 (downloading)
```

## 🔍 Challenge

Implement bandwidth throttling to limit download speed per file or globally, or add support for downloading a single large file using multiple parallel connections (split into chunks and download simultaneously).

---

**Previous:** [45_graph](../45_graph/README.md) | **Next:** [47_producer_consumer](../47_producer_consumer/README.md)
