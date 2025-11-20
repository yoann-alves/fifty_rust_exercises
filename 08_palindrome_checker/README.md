# Exercise 08: Palindrome Checker

## 🎯 Objectives

Create a program that checks if a string is a palindrome:

- Returns true if the string reads the same forwards and backwards
- Ignores spaces and punctuation
- Case-insensitive comparison
- Handles Unicode characters correctly

## 📚 Concepts

- String manipulation and comparison
- Character iteration and filtering
- Case conversion
- Unicode handling in Rust

## 📖 Background

**A palindrome** is a word, phrase, or sequence that reads the same backward as forward.

Simple examples:

```
"racecar"     → reads same both ways ✓
"hello"       → "olleh" backwards ✗
"noon"        → same both ways ✓
```

**Real-world palindromes** often ignore spaces, punctuation, and case:

```
"A man, a plan, a canal: Panama"
→ Remove spaces/punctuation: "AmanaplanacanalPanama"
→ Lowercase: "amanaplanacanalpanama"
→ Reversed: "amanaplanacanalpanama"
→ They match! ✓
```

**Why this matters:**

- Text processing and pattern recognition
- String manipulation skills
- Understanding Unicode vs ASCII
- Algorithm design (forward/backward comparison)

## ⚙️ Requirements

**First Pass:**

- ✅ Identifies simple palindromes correctly
- ✅ Case-insensitive ("Racecar" works)
- ✅ Ignores spaces ("race car" works)
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Function documentation with examples
- ✅ **Complete filtering**:
  - Ignores all whitespace (spaces, tabs, newlines)
  - Ignores punctuation and special characters
  - Handles empty strings (decide on behavior)
- ✅ **Unicode support**:
  - Works with accented characters
  - Handles multi-byte characters correctly
  - Proper case conversion for international text
- ✅ **Test coverage**: Multiple test cases showing it works

## 🚫 Constraints

- Standard library only
- No external crates
- Must handle Unicode properly (not just ASCII)

## 💡 Approaches

**Comparison strategies:**

- Reverse the cleaned string and compare
- Two pointers from start/end moving inward
- Iterator-based comparison

**Filtering the string:**

- Remove unwanted characters first, then check
- Filter during comparison (don't create new string)
- Use iterator chains

**Case handling:**

- Convert everything to lowercase
- Convert everything to uppercase
- Case-insensitive comparison

**Unicode considerations:**

- Characters vs bytes (use `.chars()` not `.bytes()`)
- Lowercase conversion for international characters
- Accented letters and special symbols

Think about: which approach is clearest? Most efficient? Easiest to test?

## ✅ Validation

Your program should correctly identify these:

**True palindromes:**

```
"racecar"                           → true
"A man a plan a canal Panama"       → true
"Was it a car or a cat I saw?"      → true
"Madam"                             → true
"nurses run"                        → true
"No 'x' in Nixon"                   → true
"noon"                              → true
"a"                                 → true
""                                  → (decide: true or false?)
```

**Not palindromes:**

```
"hello"                             → false
"rust"                              → false
"almost"                            → false
"palindrome"                        → false
```

**Unicode cases:**

```
"été"                               → true (French: summer)
"Ана"                               → true (Cyrillic)
"妈妈"                              → false (Chinese: mother, not palindrome)
```

**Edge cases to verify:**

```
"   "                               → (whitespace only)
"!!!"                               → (punctuation only)
"A B C B A"                         → true
"Able was I, ere I saw Elba"        → true (Napoleon quote)
```

## 🔍 Challenge

Extend to find the longest palindromic substring within a larger text, or check if a number is a palindrome when written in words (e.g., 11 → "eleven" → false, but conceptually interesting).

---

**Previous:** [07_prime_number](../07_prime_number/README.md) | **Next:** [09_word_counter](../09_word_counter/README.md)
