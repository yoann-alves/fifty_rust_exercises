# Exercise 28: Simple Grep

## 🎯 Objectives

Create a simplified grep utility:

- Search for pattern in a file
- Display matching lines
- Show line numbers
- Support case-insensitive search option

## 📚 Concepts

- File I/O and line-by-line reading
- String pattern matching
- Command-line arguments and flags
- Filtering and searching

## 📖 Background

**grep** (Global Regular Expression Print) is one of the most-used Unix tools. It searches text for patterns and shows matching lines.

**How grep works:**

```bash
$ grep "error" logfile.txt
Line 42: error: connection timeout
Line 108: error: invalid response
```

**Common grep features:**

- Pattern matching in files
- Line numbers for context
- Case-insensitive searching
- Counting matches
- Highlighting matches

**Your simplified version** will use basic string matching (not full regex) but follow the same principle: find lines containing a pattern.

## ⚙️ Requirements

**First Pass:**

- ✅ Searches file for a text pattern
- ✅ Displays matching lines
- ✅ Shows line numbers
- ✅ Takes pattern and filename as input
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain how pattern matching works
- ✅ **Case-insensitive option**: Add a flag to ignore case when matching
- ✅ **Enhanced output**:
  - Count total matches
  - Show filename when searching multiple files
  - Optional: highlight matched text
  - Optional: show context lines around matches
- ✅ **Error handling**:
  - File not found
  - Permission denied
  - Empty pattern
  - Clear error messages
- ✅ **Edge cases**:
  - No matches found
  - Empty file
  - Pattern appears multiple times on same line
  - Very long lines

## 🚫 Constraints

- Standard library only
- No regex crates (basic string matching only)
- Efficient file reading (buffered I/O)

## 💡 Approaches

**Command-line interface options:**

- Simple: `program <pattern> <file>`
- With flags: `program -i <pattern> <file>`
- Multiple files: `program <pattern> <file1> <file2> ...`

**Pattern matching strategies:**

- Substring search
- Case-sensitive vs case-insensitive
- Whole line matching
- Start/end of line matching

**Display formats:**

- Basic: `42: matching line here`
- With file: `file.txt:42: matching line here`
- With highlighting: `42: text [MATCH] more text`

**Flag parsing:**

- Check for `-i` or `--ignore-case`
- Store search options
- Handle multiple flags

**Reading efficiently:**

- Line-by-line reading
- Buffered I/O
- Don't load entire file into memory

## ✅ Validation

**test.txt:**

```
Hello World
hello world
HELLO WORLD
Goodbye World
World of Rust
```

**Case-sensitive search:**

```bash
$ program "Hello" test.txt
1: Hello World
3: HELLO WORLD
Found 2 matches.
```

**Case-insensitive search:**

```bash
$ program -i "hello" test.txt
1: Hello World
2: hello world
3: HELLO WORLD
Found 3 matches.
```

**Partial match:**

```bash
$ program "World" test.txt
1: Hello World
4: Goodbye World
5: World of Rust
Found 3 matches.
```

**No matches:**

```bash
$ program "Python" test.txt
No matches found.
```

**Error handling:**

```bash
$ program "test" nonexistent.txt
Error: File not found: nonexistent.txt

$ program "" test.txt
Error: Search pattern cannot be empty
```

## 🔍 Challenge

Add support for multiple search patterns (OR logic), or implement context lines (-A/-B/-C flags) to show lines before/after matches like real grep does.

---

**Previous:** [27_file_copier](../27_file_copier/README.md) | **Next:** [29_csv_parser](../29_csv_parser/README.md)
