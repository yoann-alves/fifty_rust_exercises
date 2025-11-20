# Exercise 29: CSV Parser

## 🎯 Objectives

Create a CSV (Comma-Separated Values) parser:

- Parse CSV files into structured data
- Handle quoted fields
- Handle commas within quoted fields
- Handle edge cases properly

## 📚 Concepts

- File I/O and line parsing
- String parsing with state
- Struct design for data representation
- Error handling for malformed data

## 📖 Background

**CSV format** looks simple but has hidden complexity:

```
name,age,city
Alice,30,Paris
Bob,25,London
```

**The challenge:** special characters inside fields:

```
Simple:    Alice,30,Paris           → 3 fields, easy split
Quoted:    Alice,30,"Paris, France" → comma inside quotes!
Escaped:   Bob,25,"He said ""Hi"""  → quotes inside quotes!
```

**Common CSV rules:**

- Fields separated by commas
- Fields can be quoted with `"`
- Commas inside quotes don't split fields
- Quote inside quoted field: doubled `""`
- Some CSVs have headers, some don't

**Real-world complications:**

```
name,age,city
Alice,,Paris              ← empty field
,"",London                ← empty fields with quotes
Carol,35,"Paris, France"  ← comma in field
Dave,40,"Said ""Hi"""     ← quote in field
```

## ⚙️ Requirements

**First Pass:**

- ✅ Parses simple CSV (no quotes needed yet)
- ✅ Stores data in structs
- ✅ Reads from file
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain your parsing approach
- ✅ **Quoted fields**:
  - Handles `"value"` → `value`
  - Handles `"value, with, commas"` → preserves commas
  - Handles `"quote ""inside"" field"` → `quote "inside" field`
- ✅ **Edge cases**:
  - Empty fields
  - Trailing commas
  - Missing columns (rows with different field counts)
  - Empty file
  - File with only headers
- ✅ **Error handling**:
  - Unclosed quotes
  - File not found
  - Malformed CSV
  - Clear error messages
- ✅ **Data structure**: Choose appropriate way to store parsed data

## 🚫 Constraints

- Standard library only
- No CSV parsing crates (build it yourself)
- Must handle quoted fields correctly

## 💡 Approaches

**Parsing strategies:**

**Naive approach:**

- Split on comma
- Works for simple cases only
- Breaks on quoted fields

**Character-by-character:**

- Walk through string one char at a time
- Track whether inside quotes
- Build fields as you go

**State machine:**

- State: normal field vs quoted field
- Transition on comma and quote characters
- Accumulate characters into current field

**Data representation options:**

- Vector of vectors: `Vec<Vec<String>>`
- Vector of structs: `Vec<Person>`
- HashMap per row: `Vec<HashMap<String, String>>`
- Generic row type

**Quote handling logic:**

- When you see `"` → entering/exiting quoted field
- When inside quotes, ignore commas
- When you see `""` → single quote in output
- Track state carefully

**Header handling:**

- First row might be column names
- Use for field mapping
- Or treat all rows as data

## ✅ Validation

**Simple CSV (simple.csv):**

```
name,age,city
Alice,30,Paris
Bob,25,London
```

Should parse to:

```
Record 1: name="Alice", age="30", city="Paris"
Record 2: name="Bob", age="25", city="London"
```

**Quoted fields (quoted.csv):**

```
name,age,city
Alice,30,"Paris, France"
Bob,25,"New York"
```

Should parse to:

```
Record 1: name="Alice", age="30", city="Paris, France"
Record 2: name="Bob", age="25", city="New York"
```

**Empty fields (empty.csv):**

```
name,age,city
Alice,,Paris
,25,London
Carol,35,
```

Should parse to:

```
Record 1: name="Alice", age="", city="Paris"
Record 2: name="", age="25", city="London"
Record 3: name="Carol", age="35", city=""
```

**Escaped quotes (complex.csv):**

```
id,name,quote
1,Alice,"She said ""Hello"""
2,Bob,"Simple text"
```

Should parse to:

```
Record 1: id="1", name="Alice", quote="She said "Hello""
Record 2: id="2", name="Bob", quote="Simple text"
```

**Error cases (should fail gracefully):**

```
Unclosed quote:          name,"Paris
Mismatched columns:      Alice,30,Paris (when expecting 4 fields)
File doesn't exist:      missing.csv
```

## 🔍 Challenge

Add CSV writing: take your parsed data structures and write them back out as properly formatted CSV with correct quoting (quote fields that contain commas or quotes, escape quotes properly).

---

**Previous:** [28_grep_simple](../28_grep_simple/README.md) | **Next:** [30_config_parser](../30_config_parser/README.md)
