# Exercise 32: Directory Tree

## 🎯 Objectives

Create a directory tree viewer:

- Display folder structure hierarchically
- Recursively traverse subdirectories
- Show file sizes
- Support maximum depth option
- Similar to Unix `tree` command

## 📚 Concepts

- Filesystem traversal
- Recursion
- Tree visualization
- Command-line options
- File metadata reading

## 📖 Background

**Directory trees** show the structure of folders and files in a visual hierarchy.

**The Unix `tree` command** displays nested folders like this:

```
project/
├── src/
│   ├── main.rs (1.2 KB)
│   └── lib.rs (854 bytes)
├── tests/
│   └── integration.rs (2.1 KB)
└── Cargo.toml (312 bytes)
```

**Box-drawing characters** create the visual structure:

- `├──` for items with siblings below
- `└──` for the last item in a directory
- `│` for vertical continuation lines

**Recursion** naturally fits tree traversal - each directory spawns new branches.

**Depth limiting** prevents overwhelming output in deep hierarchies.

## ⚙️ Requirements

**First Pass:**

- ✅ Lists files and directories recursively
- ✅ Shows hierarchical structure with indentation
- ✅ Displays file sizes
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain traversal approach
- ✅ **Tree formatting**:
  - Box-drawing characters (├── └── │) or ASCII (|-- +--)
  - Proper indentation for nesting
  - Visual parent-child relationships
- ✅ **File information**:
  - Sizes in readable units (B, KB, MB, GB)
  - Distinguish files from directories
  - Total size summary
- ✅ **Depth control**:
  - Maximum depth flag/option
  - Indicate truncated branches
- ✅ **Filtering**:
  - Show/hide hidden files (starting with .)
  - Filter by extension
  - Directories-only mode
- ✅ **Statistics**:
  - Total file count
  - Total directory count
  - Combined file size
- ✅ **Error handling**:
  - Permission denied
  - Symlinks (avoid infinite loops)
  - Unreadable entries
- ✅ **Edge cases**:
  - Empty directories
  - Very deep nesting
  - Large number of files

## 🚫 Constraints

- Standard library only (std::fs)
- No external filesystem crates
- Handle errors gracefully

## 💡 Approaches

**Traversal strategy:**

- Recursive descent through directories
- Track current depth
- Stop at max depth
- Sort entries (directories first, or alphabetically)

**Formatting approaches:**

- Simple: use spaces/dashes for indentation
- Advanced: track which levels need continuation lines
- Consider whether each item is the last in its directory

**Size formatting:**

- Convert bytes to appropriate units
- Decide on decimal places
- Handle zero-size files

**CLI design:**

- Path as argument
- Optional flags for depth, filtering
- Consider subcommands vs flags

**Error strategies:**

- Skip inaccessible entries
- Log errors but continue
- Or fail fast on first error

## ✅ Validation

Basic structure:

```
test_dir/
├── file1.txt (100 B)
├── file2.txt (250 B)
└── subdir/
    └── file3.txt (500 B)

2 directories, 3 files (850 B total)
```

With depth limit:

```
test_dir/
├── file1.txt (100 B)
├── file2.txt (250 B)
└── subdir/ [...]

(1 directory not shown due to depth limit)
```

Hidden files:

```
# Without filtering
test_dir/
├── .hidden (10 B)
├── visible.txt (50 B)
└── .config/
    └── settings.conf (100 B)

# With --no-hidden
test_dir/
└── visible.txt (50 B)
```

Complex structure:

```
project/
├── src/
│   ├── main.rs (1.2 KB)
│   ├── lib.rs (854 B)
│   └── utils/
│       ├── helpers.rs (2.1 KB)
│       └── constants.rs (512 B)
├── tests/
│   └── integration.rs (1.8 KB)
└── Cargo.toml (312 B)

3 directories, 6 files (6.8 KB total)
```

Error scenarios:

```
Permission denied → "subdir/ [Permission Denied]"
Symlink loop → Detect and avoid infinite recursion
Empty directory → Show directory with no children
```

## 🔍 Challenge

Add pattern filtering (show only .rs files), colorize output by file type, or show git status indicators (modified, untracked, ignored).

---

**Previous:** [31_log_analyzer](../31_log_analyzer/README.md) | **Next:** [33_file_organizer](../33_file_organizer/README.md)
