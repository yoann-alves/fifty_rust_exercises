# Exercise 25: Pig Latin Converter

## 🎯 Objectives

Create a Pig Latin translator:

- Convert English words to Pig Latin
- Handle consonant rule: move consonants to end + "ay"
- Handle vowel rule: add "way" to end
- Preserve punctuation and capitalization
- Translate entire sentences word by word

## 📚 Concepts

- String manipulation and transformation
- Character classification (vowel vs consonant)
- Pattern matching
- Punctuation handling
- Case preservation

## 📖 Background

**Pig Latin** is a language game that transforms English words using simple rules:

**Rule 1 - Words starting with consonants:**
Move all initial consonants to the end and add "ay"

```
"hello"  → "ellohay"   (h moved)
"string" → "ingstray"  (str moved)
"glove"  → "oveglay"   (gl moved)
```

**Rule 2 - Words starting with vowels:**
Simply add "way" to the end

```
"apple" → "appleway"
"eat"   → "eatway"
"ice"   → "iceway"
```

**Complications:**

- "qu" is treated as a consonant pair: "queen" → "eenquay"
- Capital letters should move with their consonants: "Hello" → "Ellohay"
- Punctuation stays at the end: "Hello!" → "Ellohay!"

## ⚙️ Requirements

**First Pass:**

- ✅ Basic consonant rule works (single consonant)
- ✅ Basic vowel rule works
- ✅ Converts individual words correctly
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain the transformation rules
- ✅ **Consonant clusters**: Handle multiple consonants ("string" → "ingstray")
- ✅ **Special cases**:
  - "qu" as a unit ("queen" → "eenquay")
  - "y" as vowel or consonant depending on position
- ✅ **Punctuation**: Preserve periods, commas, exclamation marks, etc.
- ✅ **Capitalization**:
  - First letter capital moves correctly
  - All-caps words stay all-caps
- ✅ **Sentences**: Process multiple words while preserving spacing
- ✅ **Edge cases**:
  - Single letters
  - Empty strings
  - Words with apostrophes
  - Numbers mixed with text

## 🚫 Constraints

- Standard library only
- No external crates
- Must correctly implement both vowel and consonant rules

## 💡 Approaches

**Vowel detection:**

- Define what counts as a vowel (a, e, i, o, u, sometimes y)
- Case-insensitive checking

**Consonant handling:**

- Find where the first vowel appears
- Everything before it is the consonant cluster
- Move the entire cluster

**Punctuation strategy:**

- Detect and separate punctuation before processing
- Apply transformation to the word part
- Reattach punctuation after

**Capitalization preservation:**

- Check original capitalization pattern
- Apply transformation
- Restore capitalization to result

**Sentence processing:**

- Split into words
- Transform each independently
- Reconstruct with original spacing

## ✅ Validation

Basic transformations:

```
"hello"    → "ellohay"
"apple"    → "appleway"
"eat"      → "eatway"
"string"   → "ingstray"
"glove"    → "oveglay"
"queen"    → "eenquay"
```

With capitalization:

```
"Hello"    → "Ellohay"
"HELLO"    → "ELLOHAY"
"Apple"    → "Appleway"
"STRING"   → "INGSTRAY"
```

With punctuation:

```
"hello!"   → "ellohay!"
"Hello?"   → "Ellohay?"
"world."   → "orldway."
"Wait..."  → "Aitway..."
```

Full sentences:

```
"Hello world"           → "Ellohay orldway"
"I eat apples"          → "Iway eatway applesway"
"The quick brown fox."  → "Ethay ickquay ownbray oxfay."
```

Edge cases:

```
"a"      → "away"
"I"      → "Iway"
"by"     → "ybay"
""       → ""
"rhythm" → "ythmrhay" (no vowels until y)
```

## 🔍 Challenge

Implement reverse translation: convert Pig Latin back to English. This is significantly harder because you need to figure out where the original word boundaries were!

---

**Previous:** [24_morse_code](../24_morse_code/README.md) | **Next:** [26_file_reader](../26_file_reader/README.md)
