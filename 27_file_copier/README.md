# Exercise 27: File Copier

## 🎯 Objectives

Create a file copying utility:

- Copy file from source to destination
- Show progress during copy
- Handle errors properly
- Work efficiently even with large files

## 📚 Concepts

- File I/O (reading and writing)
- Buffered I/O for performance
- Progress tracking
- Error handling
- Filesystem operations

## 📖 Background

**File copying** is a fundamental operation in computing. Every time you copy a file in your file manager, something similar happens under the hood.

**Naive approach** (reading entire file into memory):

```
Read all 1GB into memory → Write all 1GB to disk
Problem: Uses 1GB of RAM!
```

**Buffered approach** (reading in chunks):

```
Read 64KB chunk → Write 64KB chunk → Repeat
Memory usage: Just 64KB no matter file size
```

**Progress feedback** is crucial for large files:

```
Without progress: User thinks program froze
With progress: "Copying... 45% (450MB/1GB)" - User knows it's working
```

**Real-world considerations:**

- What if source doesn't exist?
- What if destination already exists?
- What if disk runs out of space mid-copy?
- What if user doesn't have write permissions?

## ⚙️ Requirements

**First Pass:**

- ✅ Copies file from source to destination
- ✅ Takes source and destination paths as input
- ✅ Shows some form of progress
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain how the copying works
- ✅ **Error handling**:
  - Source file doesn't exist
  - Can't read source (permissions)
  - Can't write destination (permissions)
  - Destination already exists
  - Disk full during copy
  - Source and destination are the same
- ✅ **Progress display**:
  - Show percentage or bytes copied
  - Update during copy (not just at end)
  - Clear indication when complete
- ✅ **Efficiency**:
  - Use buffered I/O (not loading entire file)
  - Handle large files (test with 100MB+)
  - Reasonable memory usage
- ✅ **Verification**:
  - Confirm copy succeeded
  - Destination size matches source

## 🚫 Constraints

- Standard library only
- Must use buffered reading/writing (no loading entire file)
- Proper error handling (no `.unwrap()` or `.expect()`)

## 💡 Approaches

**Copying strategy:**

- Open source file for reading
- Create destination file for writing
- Read in chunks (buffer)
- Write each chunk
- Repeat until done

**Buffer size options:**

- Small (1KB) - many operations, slower
- Medium (64KB) - good balance
- Large (1MB) - fewer operations, more memory
- Experiment to find what works

**Progress tracking ideas:**

- Get total file size first
- Count bytes as you copy
- Calculate percentage
- Display every so often

**Progress display styles:**

```
Simple counter: "Copied 5MB..."
Percentage: "50% complete"
Progress bar: "[=====>    ]"
Dots: "......" (one per chunk)
```

**Error prevention:**

- Check if files exist before starting
- Verify permissions
- Ask before overwriting
- Compare paths to avoid self-copy

## ✅ Validation

Your program should handle these scenarios:

**Small file (1KB):**

```bash
$ ./copier small.txt copy.txt
Copying small.txt → copy.txt
[====================] 100% (1024 bytes)
Done!
```

**Large file (100MB):**

```bash
$ ./copier large.bin copy.bin
Copying large.bin → copy.bin
[=====>           ] 25% (25MB/100MB)
[==========>      ] 50% (50MB/100MB)
[===============> ] 75% (75MB/100MB)
[====================] 100% (100MB/100MB)
Done! Copied in 2.3 seconds
```

**Error cases:**

```bash
# Source doesn't exist
$ ./copier missing.txt copy.txt
Error: Source file not found: missing.txt

# Destination exists
$ ./copier source.txt existing.txt
Error: existing.txt already exists. Overwrite? [y/N]

# No permission
$ ./copier source.txt /root/denied.txt
Error: Permission denied: /root/denied.txt

# Same file
$ ./copier file.txt file.txt
Error: Source and destination are the same file
```

**Verification:**

```bash
# After copy, these should match:
$ ls -l source.txt copy.txt
-rw-r--r--  1 user  staff  1048576 Nov 20 10:00 source.txt
-rw-r--r--  1 user  staff  1048576 Nov 20 10:01 copy.txt

# Sizes match ✓
```

## 🔍 Challenge

Add resume capability: if the copy is interrupted (Ctrl+C, power loss), allow resuming from where it left off instead of starting over. Or implement verification with checksums to guarantee the copy is bit-perfect.

---

**Previous:** [26_file_reader](../26_file_reader/README.md) | **Next:** [28_grep_simple](../28_grep_simple/README.md)
