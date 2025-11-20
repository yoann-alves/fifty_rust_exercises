# Exercise 26: File Reader

## 🎯 Objectives

Create a file reading utility that:

- Reads a file line by line
- Counts lines, words, and bytes
- Uses proper error handling with Result
- Works like Unix `wc` (word count) command

## 📚 Concepts

- File I/O
- Error handling with Result
- Buffered reading
- Line iteration
- Counting and statistics

## 📖 Background

**File reading** is everywhere in programming:

```
Configuration files:  Read settings
Log files:            Analyze events
Data files:           Process information
Text files:           Count, search, transform
```

**The Unix `wc` command** counts lines, words, and bytes:

```bash
$ wc myfile.txt
  42  312  1847 myfile.txt
  ↑    ↑    ↑
lines words bytes
```

**Word counting** needs definition:

```
"Hello  world" → 2 words (multiple spaces = 1 separator)
"Hello\nworld" → 2 words (newline = separator)
"Hello, world!" → 2 words (punctuation attached or separate?)
```

**Bytes vs Characters:**

```
ASCII:     1 character = 1 byte
UTF-8:     1 character = 1-4 bytes
"café" → 4 characters, 5 bytes (é takes 2 bytes)
```

## ⚙️ Requirements

**First Pass:**

- ✅ Opens and reads a file
- ✅ Counts lines
- ✅ Counts words
- ✅ Counts bytes
- ✅ Uses Result for error handling (no `.unwrap()` or `.expect()`)
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Brief explanation of what the program does
- ✅ **Error handling**:
  - File not found
  - Permission denied
  - I/O errors during reading
  - Clear error messages
- ✅ **Efficient reading**:
  - Use buffered I/O (don't load entire file into memory)
  - Process line by line
- ✅ **Edge cases**:
  - Empty file
  - File with no final newline
  - Very long lines
  - Binary files (non-text)

## 🚫 Constraints

- Standard library only
- No external crates for core functionality
- Must use proper Result error handling
- Cannot use `.unwrap()` or `.expect()` in production code

## 💡 Approaches

**File reading options:**

- Open file, create buffered reader, iterate lines
- Read entire file into string (memory-heavy)
- Read chunks/blocks (complex but efficient)

**Error handling patterns:**

- Return Result from functions
- Use `?` operator to propagate errors
- Match on Result types
- Provide context with error messages

**Word counting strategies:**

- Split by whitespace
- Count non-empty parts
- Define rules for punctuation
- Handle consecutive separators

**Line counting:**

- Count newline characters
- Count iterations from line iterator
- Handle last line without newline

**Byte counting:**

- Get file size from metadata
- Or accumulate as you read
- Remember: UTF-8 characters can be multiple bytes

## ✅ Validation

Create test files to verify:

**test1.txt:**

```
Hello world
This is a test
```

Expected output:

```
Lines: 2
Words: 6
Bytes: 26
```

**empty.txt:**

```
(empty file)
```

Expected output:

```
Lines: 0
Words: 0
Bytes: 0
```

**test2.txt:**

```
One
Two  Three
Four

```

Expected output:

```
Lines: 4
Words: 4
Bytes: 18
```

**Error cases:**

```
$ your_program nonexistent.txt
Error: File not found: nonexistent.txt

$ your_program /root/protected.txt
Error: Permission denied: /root/protected.txt
```

**Compare with Unix wc:**

```bash
$ wc test.txt
  2   6  26 test.txt

$ your_program test.txt
Lines: 2
Words: 6
Bytes: 26
```

## 🔍 Challenge

Add character counting (separate from bytes) to handle UTF-8 properly, and track the most frequently occurring word in the file.

---

**Previous:** [25_pig_latin](../25_pig_latin/README.md) | **Next:** [27_file_copier](../27_file_copier/README.md)
