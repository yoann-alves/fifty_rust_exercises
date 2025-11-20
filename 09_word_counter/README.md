# Exercise 09: Word Counter

## 🎯 Objectives

Create a word counter program that:

- Counts total words in a string
- Counts total characters
- Counts total lines
- Tracks word frequency using a HashMap

## 📚 Concepts

- String parsing and splitting
- HashMap for key-value storage
- Iterators and counting
- Entry API for HashMap updates

## 📖 Background

**Word frequency analysis** is fundamental in text processing. It tells you which words appear most often in a text.

**Real-world uses:**

```
Search engines:  Rank pages by keyword frequency
Spam filters:    Detect suspicious word patterns
Text analysis:   Find themes in documents
Compression:     Encode frequent words efficiently
```

**Example analysis:**

```
Text: "hello world hello rust"

Word count: 4
Character count: 23 (with spaces) or 19 (without)
Lines: 1

Frequency:
  "hello" → 2 times
  "world" → 1 time
  "rust"  → 1 time
```

**Challenges in counting words:**

- What counts as a word boundary? (spaces, punctuation, newlines)
- Case sensitivity: is "Hello" the same as "hello"?
- Punctuation: is "world!" the same as "world"?
- Contractions: is "don't" one word or two?

You'll need to decide these rules.

## ⚙️ Requirements

**First Pass:**

- ✅ Counts words in a string
- ✅ Counts characters
- ✅ Counts lines
- ✅ Uses HashMap for word frequency
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain what counts as a "word"
- ✅ **Word normalization**:
  - Define your word boundary rules
  - Handle case sensitivity (your choice)
  - Handle punctuation (your choice)
- ✅ **Display results**:
  - Show statistics clearly
  - Show word frequencies
  - Sort by frequency (most common first)
- ✅ **Edge cases**:
  - Empty string
  - Only whitespace
  - No words (just punctuation)
- ✅ **HashMap usage**: Use entry API efficiently

## 🚫 Constraints

- Standard library only
- Must use HashMap for word frequency

## 💡 Approaches

**Counting strategies:**

- Words: split text somehow, count pieces
- Characters: iterate and count, or use string length
- Lines: count newline characters, or split by lines

**Word normalization options:**

- Lowercase everything for case-insensitive counting
- Remove punctuation from word boundaries
- Trim whitespace from words

**HashMap patterns:**

- Check if key exists, then update
- Use entry API for cleaner code
- Initialize with default value if missing

**Output formatting:**

- Collect HashMap into vector for sorting
- Sort by value (frequency) descending
- Display top N most common words

**Different definitions of "character":**

- Include spaces? ("hello world" = 11 or 10?)
- Count bytes vs Unicode graphemes?
- Special characters count?

## ✅ Validation

Test with this text:

```
Hello world
Hello Rust
Rust is great
```

Expected output (approximately):

```
Statistics:
  Words: 6
  Characters: 33 (with spaces) or 28 (without)
  Lines: 3

Word Frequency:
  hello: 2
  rust: 2
  world: 1
  is: 1
  great: 1
```

Edge cases to test:

```
Input: ""
Output: 0 words, 0 chars, 0 lines

Input: "   "
Output: 0 words, 3 chars, 0 lines

Input: "hello"
Output: 1 word, 5 chars, 1 line

Input: "Hello hello HELLO"
If case-insensitive: "hello": 3
If case-sensitive: "Hello": 1, "hello": 1, "HELLO": 1
```

Test punctuation handling:

```
Input: "hello, world! hello."
Desired: "hello": 2, "world": 1
(or however you define word boundaries)
```

## 🔍 Challenge

Display the top 10 most frequent words only, or add support for excluding common words (the, a, is, etc.) to find more meaningful frequent words.

---

**Previous:** [08_palindrome_checker](../08_palindrome_checker/README.md) | **Next:** [10_random_numbers](../10_random_numbers/README.md)
