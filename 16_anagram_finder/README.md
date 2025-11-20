# Exercise 16: Anagram Finder

## 🎯 Objectives

Create an anagram finder that:

- Checks if two words are anagrams
- Finds all anagrams of a word in a word list
- Ignores spaces, punctuation, and case
- Groups words by their anagram sets

## 📚 Concepts

- String normalization
- Character sorting and comparison
- HashMap for grouping
- File I/O (reading word lists)
- Collection filtering

## 📖 Background

**Anagrams** are words formed by rearranging the letters of another word, using all original letters exactly once.

Classic examples:

```
"listen" ↔ "silent"
"evil" ↔ "live" ↔ "vile"
"dormitory" ↔ "dirty room"
"astronomer" ↔ "moon starer"
```

**The core insight:** Two words are anagrams if they contain the exact same letters with the same frequencies.

**Anagram signatures:** A canonical form that's identical for all anagrams:

```
"listen" → sort letters → "eilnst"
"silent" → sort letters → "eilnst"
Same signature = anagrams!
```

This lets you group thousands of words efficiently.

## ⚙️ Requirements

**First Pass:**

- ✅ Check if two words are anagrams
- ✅ Case-insensitive comparison
- ✅ Works with a basic word list
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain your anagram detection approach
- ✅ **Word list handling**:
  - Read from file OR use hardcoded list
  - Handle missing/invalid files gracefully
  - One word per line format
- ✅ **Full features**:
  - Find all anagrams of a given word
  - Group all words into anagram sets
  - Display anagram groups
  - Ignore spaces and punctuation in multi-word phrases
- ✅ **Edge cases**:
  - Empty strings
  - Single letters
  - No anagrams found
  - Duplicate words
  - Special characters
- ✅ **Performance**: Efficient for large word lists (thousands of words)

## 🚫 Constraints

- Standard library only
- No external crates
- Must implement anagram logic yourself (no library anagram checkers)

## 💡 Approaches

**Anagram detection strategies:**

- Sort both strings' characters and compare
- Count character frequencies and compare counts
- Create a "signature" (normalized, sorted form) for each word

**Normalization:**

- Convert to lowercase
- Remove spaces, punctuation
- Keep only letters

**Finding anagrams in a list:**

- Linear scan: compare target with each word (simple but slow)
- Signature grouping: preprocess all words by signature (fast lookups)

**Data structures:**

- Vec for simple word storage
- HashMap<Signature, Vec<Word>> for grouping
- HashSet to avoid duplicates

**Word list sources:**

- Hardcoded Vec (good for testing)
- Read from file (more practical)
- System dictionary (/usr/share/dict/words on Unix)

## ✅ Validation

Basic anagram checks:

```
"listen" and "silent" → true
"evil" and "live" → true
"hello" and "world" → false
"Astronomer" and "Moon starer" → true
"abc" and "cab" → true
```

Finding anagrams in a list:

```
Word list: ["listen", "silent", "enlist", "hello", "evil", "vile", "live"]

Find anagrams of "listen":
→ silent, enlist

Find anagrams of "evil":
→ vile, live
```

Anagram groups:

```
Word list: ["listen", "silent", "enlist", "evil", "vile", "live", "hello"]

Group 1: listen, silent, enlist
Group 2: evil, vile, live
Group 3: hello (no anagrams)
```

Edge cases:

```
"" and "" → true
"a" and "a" → true
"ABC" and "cab" → true (case-insensitive)
"a b c" and "cab" → true (ignore spaces)
"hello" and "world" → false
```

## 🔍 Challenge

Find the largest anagram group in a real dictionary file. Some dictionaries have groups with 7+ anagrams! Can you also handle multi-word anagram phrases?

---

**Previous:** [15_stopwatch](../15_stopwatch/README.md) | **Next:** [17_sorting](../17_sorting/README.md)
