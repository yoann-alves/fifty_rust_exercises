# Exercise 23: RLE Compression

## 🎯 Objectives

Implement Run-Length Encoding (RLE) compression:

- Encode strings by counting consecutive characters
- Decode RLE strings back to original
- Handle edge cases properly
- Verify encode/decode round-trip

## 📚 Concepts

- String iteration and character grouping
- Consecutive element counting
- String building
- Parsing numbers from strings
- Reversible encoding/decoding

## 📖 Background

**Run-Length Encoding (RLE)** is a simple compression algorithm that replaces consecutive identical characters with the character followed by its count.

Examples:

```
"aaabbc"  → "a3b2c1"
"hello"   → "h1e1l2o1"
"wwwww"   → "w5"
```

**When is RLE useful?**

- Images with solid color regions
- Simple graphics
- Data with many consecutive repeats
- NOT useful for text with few repeats (can even expand size!)

**Compression vs Expansion:**

```
Good:  "aaaaaaa" → "a7"        (7 chars → 2 chars, 71% smaller)
Bad:   "abcdef"  → "a1b1c1d1e1f1"  (6 chars → 12 chars, 200% larger!)
```

## ⚙️ Requirements

**First Pass:**

- ✅ Encode function works
- ✅ Decode function works
- ✅ Round-trip works (encode → decode returns original)
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain the RLE algorithm
- ✅ **Edge cases**:
  - Empty string
  - Single character
  - No consecutive repeats
  - Very long runs (100+ same character)
- ✅ **Format choice**: Decide on output format and stick to it
  - Standard: "a3b2c1" (always include count)
  - Compact: "a3b2c" (omit count of 1)
  - Pick one and be consistent
- ✅ **Error handling**: Decode returns Result for invalid input
- ✅ **Round-trip verification**: Test that encode(decode(x)) = x

## 🚫 Constraints

- Standard library only
- No external compression crates
- Must implement both encode and decode

## 💡 Approaches

**Encoding strategies:**

- Iterate through string character by character
- Keep counter for current character
- When character changes, output previous char + count
- Handle last group of characters

**Decoding strategies:**

- Parse character-number pairs
- Repeat each character by its count
- Build output string
- Validate format while parsing

**Format decisions to make:**

- Do you include "1" for single characters? ("a1" vs "a")
- Character-first or count-first? ("a3" vs "3a")
- How do you handle numbers in the original string? ("123" → ?)

**Optimization ideas:**

- Avoid repeated allocations
- Use efficient string building
- Consider when NOT to compress (expansion case)

## ✅ Validation

Encoding examples:

```
"aaabbc"       → "a3b2c1"
"aaa"          → "a3"
"abc"          → "a1b1c1"  (or "abc" if you omit 1s)
"aaaaaaaaaa"   → "a10"
""             → ""
"a"            → "a1"
"hello"        → "h1e1l2o1"
```

Decoding examples:

```
"a3b2c1"       → "aaabbc"
"a3"           → "aaa"
"a10"          → "aaaaaaaaaa"
"h1e1l2o1"     → "hello"
```

Round-trip tests (must return original):

```
"hello"  → encode → decode → "hello" ✓
"aaabbc" → encode → decode → "aaabbc" ✓
"x"      → encode → decode → "x" ✓
""       → encode → decode → "" ✓
```

Compression analysis:

```
Input: "aaaaaaa"
Encoded: "a7"
Original: 7 bytes → Compressed: 2 bytes (71% reduction) ✓

Input: "abcdef"
Encoded: "a1b1c1d1e1f1"
Original: 6 bytes → "Compressed": 12 bytes (100% expansion!) ✗
```

Invalid decode cases (should error):

```
"abc"          → Error: no counts
"a"            → Error: missing count
"3a"           → Error: wrong order (if count-last format)
"ax"           → Error: 'x' is not a number
```

## 🔍 Challenge

Implement a smarter version that detects when compression would expand the string and returns the original instead. Or handle numbers in the original string using an escape character scheme.

---

**Previous:** [22_roman_numerals](../22_roman_numerals/README.md) | **Next:** [24_morse_code](../24_morse_code/README.md)
