# Exercise 35: Text File Merger

## 🎯 Objectives

Create a text file merger utility:

- Merge multiple text files into one
- Support different merge modes (concatenate, interleave, zip)
- Handle different text encodings
- Flexible output options

## 📚 Concepts

- Multiple file I/O
- Text encoding handling
- Different merge strategies
- Line ending normalization
- Buffered reading and writing

## 📖 Background

**File merging** is a common task when combining data from multiple sources. Different merge strategies serve different purposes:

**Concatenate** - Files stacked end-to-end:

```
file1: A, B, C
file2: D, E
file3: F, G, H
Result: A, B, C, D, E, F, G, H
```

**Interleave** - Round-robin, one line from each file:

```
file1: A1, A2, A3
file2: B1, B2
file3: C1, C2, C3
Result: A1, B1, C1, A2, B2, C2, A3, C3
```

**Zip** - Side-by-side columns:

```
file1: A1, A2
file2: B1, B2
file3: C1, C2
Result: A1|B1|C1
        A2|B2|C2
```

**Text encoding challenges:**

- Files might be UTF-8, ASCII, Latin-1, etc.
- Line endings vary: `\n` (Unix), `\r\n` (Windows), `\r` (old Mac)
- BOM (Byte Order Mark) may or may not be present
- Invalid characters need handling

## ⚙️ Requirements

**First Pass:**

- ✅ Concatenates multiple files
- ✅ Writes output to new file
- ✅ Takes input and output filenames
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain each merge mode
- ✅ **Merge modes**:
  - Concatenate (sequential)
  - Interleave (round-robin lines)
  - Zip (side-by-side with delimiter)
- ✅ **Encoding**:
  - Detect input encoding
  - Handle UTF-8, ASCII
  - Deal with BOM if present
  - Error on invalid encoding
- ✅ **Line endings**:
  - Preserve original
  - Or normalize to Unix/Windows
  - Handle mixed inputs
- ✅ **Features**:
  - Separators between files
  - Skip empty lines (optional)
  - Handle files of different lengths
  - Progress indicator for large files
- ✅ **Error handling**:
  - Missing files
  - Permission denied
  - Write failures
  - Invalid encoding
- ✅ **Performance**: Stream large files (don't load all into memory)

## 🚫 Constraints

- Standard library for file I/O
- May use `encoding_rs` or similar for encoding detection
- Must handle files larger than available memory
- Proper error handling

## 💡 Approaches

**Merge strategies:**

- Concatenate: Read each file completely, append to output
- Interleave: Open all files, read one line from each in rotation
- Zip: Open all files, read corresponding lines, join with delimiter

**Handling different file lengths:**

- Interleave: Continue with remaining files when some end
- Zip: Pad with spaces, or skip, or show empty columns

**Encoding detection:**

- Check for BOM markers
- Try parsing as UTF-8
- Fall back to ASCII or Latin-1
- Report errors for unknown encodings

**Line ending handling:**

- Read with any ending
- Write with chosen ending
- Option to preserve original

**Memory efficiency:**

- Don't load entire files
- Read and write line by line
- Use buffered I/O

**CLI design:**

- Mode as first argument or flag
- List of input files
- Output file specified with flag
- Optional parameters (delimiter, separator, etc.)

## ✅ Validation

**Test files:**

```
file_a.txt:
Line A1
Line A2
Line A3

file_b.txt:
Line B1
Line B2

file_c.txt:
Line C1
Line C2
Line C3
Line C4
```

**Concatenate mode:**

```
Input: file_a.txt file_b.txt file_c.txt
Output:
Line A1
Line A2
Line A3
Line B1
Line B2
Line C1
Line C2
Line C3
Line C4
```

**Interleave mode:**

```
Input: file_a.txt file_b.txt file_c.txt
Output:
Line A1
Line B1
Line C1
Line A2
Line B2
Line C2
Line A3
Line C3
Line C4
```

**Zip mode (delimiter: " | "):**

```
Input: file_a.txt file_b.txt file_c.txt
Output:
Line A1 | Line B1 | Line C1
Line A2 | Line B2 | Line C2
Line A3 |          | Line C3
        |          | Line C4
```

**With separator:**

```
Input: file_a.txt file_b.txt (separator: "---")
Output:
Line A1
Line A2
Line A3
---
Line B1
Line B2
```

**Edge cases:**

```
Empty file      → Handle gracefully
Single file     → Copy to output
No files        → Error message
All empty files → Empty output
```

## 🔍 Challenge

Implement a "sorted merge" mode that combines pre-sorted files while maintaining sort order (like the merge step in merge sort), or add CSV-aware merging that respects quoted fields and headers.

---

**Previous:** [34_duplicate_finder](../34_duplicate_finder/README.md) | **Next:** [36_library](../36_library/README.md)
