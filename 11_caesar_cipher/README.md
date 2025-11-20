# Exercise 11: Caesar Cipher

## 🎯 Objectives

Create a Caesar cipher encoder/decoder:

- Encrypts text by shifting letters by n positions
- Decrypts text by shifting backwards
- Preserves non-alphabetic characters (spaces, punctuation, numbers)
- Handles both uppercase and lowercase

## 📚 Concepts

- Character manipulation
- Modular arithmetic (wrapping around alphabet)
- Command-line argument parsing
- String transformation
- Encoding vs decoding logic

## 📖 Background

**Caesar Cipher** is one of the simplest encryption techniques, named after Julius Caesar who used it in his private correspondence.

**How it works:**
Each letter is shifted by a fixed number of positions in the alphabet.

Example with shift of 3:

```
Plaintext:  HELLO WORLD
Ciphertext: KHOOR ZRUOG

A → D    (shift forward 3 positions)
B → E
...
X → A    (wraps around)
Y → B
Z → C
```

**Key properties:**

- Only letters are shifted
- Spaces, punctuation, numbers stay the same
- Case is preserved (A→D, a→d)
- Alphabet wraps around (Z→C with shift 3)

**Decryption** is just encryption with the opposite shift:

```
Encrypt with shift +3
Decrypt with shift -3
```

## ⚙️ Requirements

**First Pass:**

- ✅ Encodes text with given shift
- ✅ Decodes text (reverse shift)
- ✅ Preserves non-letters
- ✅ Works with uppercase and lowercase
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain the cipher algorithm
- ✅ **CLI handling**:
  - Parse command-line arguments
  - Clear usage/help message
  - Handle invalid input gracefully
- ✅ **Edge cases**:
  - Shift of 0 (no change)
  - Negative shifts
  - Shifts > 26 (wrap around properly)
  - Empty string
  - Only non-alphabetic characters
- ✅ **Case preservation**: "Hello" with shift 1 → "Ifmmp"
- ✅ **Error handling**: Invalid arguments, out of range values

## 🚫 Constraints

- Standard library only
- No external crates
- Must handle both encoding and decoding
- Non-alphabetic characters must remain unchanged

## 💡 Approaches

**Character transformation:**

- Work with character codes
- Apply shift with wraparound
- Treat uppercase and lowercase separately
- Leave non-letters alone

**Wraparound strategy:**

- Use modular arithmetic
- Handle negative shifts
- Normalize large shifts (shift 27 = shift 1)

**CLI design options:**

- Positional arguments
- Flags/options
- Interactive mode
- Subcommands (encode/decode)

**Structure ideas:**

- Separate encode/decode functions
- Single shift function that handles both
- Helper for character transformation
- Validator for input

## ✅ Validation

Your implementation should handle these cases:

```
Encode "HELLO" with shift 3:
→ "KHOOR"

Encode "hello world!" with shift 5:
→ "mjqqt btwqi!"
(space and ! unchanged)

Encode "xyz" with shift 3:
→ "abc"
(wraps around Z→A)

Decode "KHOOR" with shift 3:
→ "HELLO"

Encode "Test123" with shift 1:
→ "Uftu123"
(case preserved, numbers unchanged)

Encode "ABC" with shift 26:
→ "ABC"
(full rotation = no change)

Encode "ABC" with shift 0:
→ "ABC"
(no shift = no change)
```

Edge cases:

```
Input: ""           Shift: 5  → ""
Input: "123!@#"     Shift: 10 → "123!@#"
Input: "Hello"      Shift: -1 → "Gdkkn"
```

## 🔍 Challenge

Implement a brute-force decoder that tries all 26 possible shifts and shows which one produces readable English text (frequency analysis or dictionary matching).

---

**Previous:** [10_random_numbers](../10_random_numbers/README.md) | **Next:** [12_guess_number](../12_guess_number/README.md)
