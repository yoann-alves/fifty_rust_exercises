# Exercise 30: Config File Reader

## 🎯 Objectives

Create a configuration file parser:

- Parse key=value pairs into a data structure
- Support comments (lines starting with #)
- Support sections ([section_name])
- Handle whitespace properly
- Provide structured access to config data

## 📚 Concepts

- File I/O and line-by-line parsing
- HashMap for key-value storage
- String trimming and splitting
- Nested data structures (sections)
- Configuration file formats

## 📖 Background

**Config files** are everywhere in software. They let users customize behavior without changing code.

**INI-style format** is one of the simplest:

```ini
# This is a comment
key = value
another_key = another value

[section_name]
setting = 123
enabled = true
```

**Structure breakdown:**

- **Comments**: Lines starting with `#` are ignored
- **Sections**: Headers like `[database]` group related settings
- **Key-value pairs**: `host = localhost` assigns values to keys
- **Whitespace**: Usually flexible, trimmed away

**Real-world examples:**

```ini
# Database configuration
[database]
host = localhost
port = 5432
user = admin

[logging]
level = debug
file = /var/log/app.log
```

## ⚙️ Requirements

**First Pass:**

- ✅ Parses key=value pairs
- ✅ Ignores comment lines (#)
- ✅ Handles basic sections
- ✅ Reads from file
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain the config format and parser behavior
- ✅ **Robust parsing**:
  - Trim whitespace around keys and values
  - Handle whitespace around `=` sign
  - Empty lines ignored
  - Inline comments: `key = value # comment`
- ✅ **Section handling**:
  - Group keys by section
  - Handle keys before any section (default/global section)
  - Access pattern: get value from specific section
- ✅ **Advanced features**:
  - Multi-line values (optional)
  - Type parsing (convert to int, bool, etc.)
  - Default values if key missing
  - Case-insensitive keys (optional)
- ✅ **Error handling**:
  - Malformed lines (no `=` sign)
  - Invalid section names
  - Duplicate keys (decide: error or overwrite?)
  - File reading errors
  - Report line numbers in errors
- ✅ **Edge cases**:
  - Empty file
  - Only comments
  - Section with no keys
  - Keys before any section
  - `=` character in value: `url = https://example.com/path=value`

## 🚫 Constraints

- Standard library only
- No config parsing crates (like `ini` or `toml`)
- Use HashMap or similar for storage
- Proper error handling with Result

## 💡 Approaches

**Data structure choices:**

- Flat HashMap with dotted keys: `"database.host"`
- Nested HashMap: section → HashMap of keys
- Custom Config struct with methods
- Vec of sections, each containing HashMap

**Parsing strategy:**

- Read file line by line
- Track current section as you parse
- Split on `=` to get key and value
- Trim whitespace from both
- Store in appropriate section

**Comment handling:**

- Check if line starts with `#`
- Or find `#` in line and strip everything after
- Be careful with `#` inside values

**Section detection:**

- Check if line starts with `[` and ends with `]`
- Extract section name between brackets
- Switch "current section" context

**Error reporting:**

- Track line number as you parse
- Include line number in error messages
- Decide if you stop on first error or collect all

## ✅ Validation

**Sample config file:**

```ini
# Application Configuration
[database]
host = localhost
port = 5432
user = admin

[logging]
level = debug  # Set to info for production
file = /var/log/app.log

[features]
enabled = true
max_connections = 100
```

**Expected result:**

```
Section "database":
  host → "localhost"
  port → "5432"
  user → "admin"

Section "logging":
  level → "debug"
  file → "/var/log/app.log"

Section "features":
  enabled → "true"
  max_connections → "100"
```

**Edge cases to test:**

```ini
# Comment at top
global_key = global_value

[section1]
key1 = value1

# Empty section
[section2]

[section3]
key_with_equals = value=with=equals
key_with_spaces   =   value with spaces
```

**Expected parsing:**

```
Default/global section:
  global_key → "global_value"

Section "section1":
  key1 → "value1"

Section "section2":
  (empty, no keys)

Section "section3":
  key_with_equals → "value=with=equals"
  key_with_spaces → "value with spaces"
```

**Error cases:**

```
Line without = sign:
  "invalid line" → Error: "Line 5: Invalid format, expected key=value"

Invalid section:
  "[unclosed" → Error: "Line 3: Invalid section format"

Duplicate key behavior (your choice):
  key = value1
  key = value2
  → Either error or second value overwrites first
```

## 🔍 Challenge

Add config writing: serialize your Config structure back to a formatted file with sections and comments preserved. Or implement environment variable expansion: `path = ${HOME}/data` becomes `path = /home/username/data`.

---

**Previous:** [29_csv_parser](../29_csv_parser/README.md) | **Next:** [31_log_analyzer](../31_log_analyzer/README.md)
