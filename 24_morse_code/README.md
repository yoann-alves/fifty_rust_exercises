# Exercise 24: Morse Code

## 🎯 Objectives

Create a Morse code translator:

- Convert text to Morse code
- Convert Morse code back to text
- Handle spacing between letters and words
- Support alphabet and numbers

## 📚 Concepts

- HashMap for bidirectional mapping
- String parsing and building
- Character encoding/decoding
- Delimiter handling

## 📖 Background

**Morse Code** is a communication system that encodes text as sequences of dots (.) and dashes (-).

**Basic examples:**

```
A: .-
B: -...
C: -.-.
S: ...
O: ---

SOS: ... --- ...
HELLO: .... . .-.. .-.. ---
```

**Spacing rules matter:**

- Dots and dashes within a letter: no space
- Between letters: one space
- Between words: three spaces (or seven by strict standard)

**The challenge:** preserve word boundaries when converting back and forth.

## ⚙️ Requirements

**First Pass:**

- ✅ Text to Morse conversion works
- ✅ Morse to text conversion works
- ✅ Handles A-Z and 0-9
- ✅ Proper spacing between letters
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Include reference for Morse mappings
- ✅ **Full character support**:
  - All letters A-Z (case-insensitive)
  - All digits 0-9
  - Common punctuation (., ?, !)
- ✅ **Proper spacing**:
  - Letter separation with single space
  - Word separation with triple space
  - Handle multiple spaces correctly
- ✅ **Edge cases**:
  - Empty strings
  - Unknown characters (skip or error?)
  - Mixed case input
  - Extra whitespace
- ✅ **Error handling**: Invalid Morse sequences should be handled gracefully
- ✅ **Round-trip test**: text → morse → text should match original

## 🚫 Constraints

- Standard library only
- Must use HashMap (not just match expressions)
- Support both encoding and decoding

## 💡 Approaches

**HashMap setup:**

- One HashMap for text→morse
- Another HashMap for morse→text
- Or create one and derive the other

**Encoding strategy:**

- Convert characters to uppercase
- Look up each character in HashMap
- Join with appropriate spacing
- Handle word boundaries

**Decoding strategy:**

- Split by word separators (triple space)
- Split each word by letter separators (single space)
- Look up each Morse sequence
- Rebuild text

**Character handling:**

- What to do with unsupported characters?
- Skip them silently?
- Return an error?
- Replace with placeholder?

**Morse reference** (you'll need to look up or define the complete mapping):

```
A: .-      N: -.      0: -----
B: -...    O: ---     1: .----
C: -.-.    P: .--.    2: ..---
... and so on
```

## ✅ Validation

Text to Morse:

```
"SOS"           → "... --- ..."
"HELLO"         → ".... . .-.. .-.. ---"
"HELLO WORLD"   → ".... . .-.. .-.. ---   .-- --- .-. .-.. -.."
"A1"            → ".- .----"
```

Morse to text:

```
"... --- ..."                                → "SOS"
".... . .-.. .-.. ---"                       → "HELLO"
".... . .-.. .-.. ---   .-- --- .-. .-.. -.." → "HELLO WORLD"
```

Round-trip (should preserve original):

```
"HELLO WORLD" → morse → "HELLO WORLD" ✓
"SOS 123"     → morse → "SOS 123" ✓
```

Edge cases:

```
""            → ""
"hello"       → same as "HELLO" (case insensitive)
"A  B  C"     → handle multiple spaces
"CAFÉ"        → handle unsupported characters (É)
```

Invalid Morse (should handle gracefully):

```
"......"      → Unknown sequence
".-.-.-.-"    → Not a valid character
""            → Empty input
```

## 🔍 Challenge

Add audio output: play actual Morse code beeps with proper timing (dot = 1 unit, dash = 3 units, space between dots/dashes = 1 unit, between letters = 3 units, between words = 7 units).

---

**Previous:** [23_rle_compression](../23_rle_compression/README.md) | **Next:** [25_pig_latin](../25_pig_latin/README.md)
