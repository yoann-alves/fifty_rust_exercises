# Exercise 34: Duplicate File Finder

## 🎯 Objectives

Create a duplicate file finder:

- Find duplicate files using content hashing
- List all duplicate groups
- Display space that could be saved
- Optional: safely delete duplicates

## 📚 Concepts

- Cryptographic hashing
- File I/O and content reading
- HashMap for grouping
- Memory-efficient processing (streaming large files)
- Safe file operations

## 📖 Background

**Duplicate files** waste disk space and create confusion. Finding them manually is tedious.

**Hashing solves this problem:**

```
File A: "Hello World"  → Hash: a591a6d4...
File B: "Hello World"  → Hash: a591a6d4... (same!)
File C: "Goodbye"      → Hash: 8f434346... (different)

Same hash = identical content, even if names differ
```

**Why SHA-256?**

- Cryptographically secure
- Collision-resistant (virtually impossible for two different files to have same hash)
- Industry standard

**The challenge:** A directory might have thousands of files. How do you find duplicates efficiently without comparing every file to every other file?

## ⚙️ Requirements

**First Pass:**

- ✅ Scans a directory for files
- ✅ Computes hash for each file
- ✅ Groups files by hash
- ✅ Shows which files are duplicates
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain the duplicate detection strategy
- ✅ **Efficient algorithm**:
  - Pre-filter by file size (different sizes can't be duplicates)
  - Only hash files that have potential duplicates
  - Handle large files without loading them entirely into memory
- ✅ **Useful output**:
  - Group duplicates together
  - Show file paths and sizes
  - Calculate total wasted space
  - Show space that could be recovered
- ✅ **Safety features**:
  - Preview mode (show what would be deleted)
  - Confirmation before deletion
  - Keep one copy (user chooses which)
  - Handle symlinks appropriately
- ✅ **Error handling**:
  - Permission denied on files
  - Files that disappear during scan
  - Hash computation failures
  - Deletion failures

## 🚫 Constraints

- Use `sha2` crate for SHA-256 hashing (allowed for this exercise)
- Handle files efficiently (don't load entire file into memory)
- Standard library for file operations
- Ensure safe deletion (no accidental data loss)

## 💡 Approaches

**Optimization strategies:**

- First group files by size (fast, no I/O)
- Only hash files where size matches others
- Read files in chunks for hashing
- Consider parallel processing for multiple files

**Data structures:**

- Map from size → list of files
- Map from hash → list of files
- Only report groups with multiple files

**Deletion strategies:**

- Keep oldest file (by modification time)
- Keep newest file
- Keep file with shortest path
- Let user choose interactively
- Dry-run mode shows what would happen

**Progress indication:**

- Show which file is being processed
- Display progress bar for large scans
- Estimate time remaining

## ✅ Validation

Test with this directory structure:

```
test_files/
├── photo1.jpg      (2 MB, content: [image data A])
├── photo1_copy.jpg (2 MB, content: [image data A]) ← duplicate!
├── document.pdf    (1 MB, content: [pdf data B])
├── backup/
│   ├── photo1.jpg  (2 MB, content: [image data A]) ← duplicate!
│   └── report.pdf  (500 KB, content: [pdf data C])
```

Expected output:

```
Scanning test_files/...
Found 5 files (7.5 MB total)

Analyzing by size...
Computing hashes for 3 files...

Duplicate Groups Found: 1

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Group 1: 3 identical files (2.0 MB each)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  test_files/photo1.jpg
  test_files/photo1_copy.jpg
  test_files/backup/photo1.jpg

Wasted space in this group: 4.0 MB

Summary:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Total files scanned:    5
Duplicate groups:       1
Total wasted space:     4.0 MB
Space recoverable:      4.0 MB (keep 1 copy per group)
```

Interactive deletion:

```
Group 1: Which file to keep?
1. test_files/photo1.jpg (modified: 2024-01-10)
2. test_files/photo1_copy.jpg (modified: 2024-01-15) [newest]
3. test_files/backup/photo1.jpg (modified: 2024-01-12)

Keep which? (1-3, or 's' to skip): 1

Will delete:
  - test_files/photo1_copy.jpg (2.0 MB)
  - test_files/backup/photo1.jpg (2.0 MB)

Proceed? (y/n): y
✓ Deleted 2 files, recovered 4.0 MB
```

Edge cases to handle:

```
Empty directory          → "No files found"
All files unique         → "No duplicates found"
Permission denied        → Skip file, show warning
File deleted during scan → Skip gracefully
Symlinks                 → Follow or skip (your choice)
```

## 🔍 Challenge

Implement similarity detection for near-duplicates: find images that are similar but not identical (different resolutions, slight edits), or text files that are mostly the same but have minor differences.

---

**Previous:** [33_file_organizer](../33_file_organizer/README.md) | **Next:** [35_text_merger](../35_text_merger/README.md)
