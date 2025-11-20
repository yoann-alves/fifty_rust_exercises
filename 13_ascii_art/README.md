# Exercise 13: ASCII Art

## 🎯 Objectives

Create an ASCII art generator that:

- Converts text into ASCII art
- Uses character patterns to form large letters
- Supports multiple font styles
- Handles multi-line output

## 📚 Concepts

- Multi-dimensional data structures (storing letter patterns)
- String manipulation and concatenation
- Pattern matching for character mapping
- File organization (separating font data)

## 📖 Background

**ASCII Art** uses text characters to create visual representations. Instead of pixels, you use letters, numbers, and symbols to draw.

**Text-to-ASCII art** is one common form: turning regular text into large, stylized letters made of characters.

Example - the word "HI" in ASCII art:

```
H   H  III
H   H   I
HHHHH   I
H   H   I
H   H  III
```

**Each letter is a pattern:**

- Letters are typically 5-7 lines tall
- Each line contains the characters that form that row
- Multiple letters are placed side-by-side

**Font styles** create different looks:

```
Block style:
████  ███
█  █  █  █
████  ███
█  █  █  █
████  ███

Banner style:
#   #  ###
#   #   #
#####   #
#   #   #
#   #  ###
```

Different fonts = different patterns for the same letter.

## ⚙️ Requirements

**First Pass:**

- ✅ Converts text to ASCII art
- ✅ At least one font style works
- ✅ Handles basic alphabet (A-Z)
- ✅ Multi-line output properly formatted
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain how fonts are structured
- ✅ **Multiple fonts**:
  - At least 2-3 different styles available
  - User can select which font to use
  - Easy to switch between fonts
- ✅ **Character support**:
  - Full alphabet (A-Z)
  - Numbers (0-9)
  - Basic punctuation (., !, ?, space)
  - Handle unsupported characters gracefully
- ✅ **Edge cases**:
  - Empty string input
  - Very long text
  - Mixed case handling
  - Special characters
- ✅ **Code organization**:
  - Font data separated from rendering logic
  - Easy to add new fonts
  - Clean, maintainable structure

## 🚫 Constraints

- Standard library only
- No external crates
- Fonts embedded in code (no external files)

## 💡 Approaches

**Storing letter patterns:**

- Each letter needs multiple lines (rows)
- Could use a map: character → array of strings
- Could use structs with pattern data
- Could use 2D arrays or vectors

**Rendering strategy:**

- Build output line by line
- For each line, concatenate the same line from each letter
- Handle spacing between letters
- Handle spacing between words

**Font selection:**

- Store multiple font definitions
- Let user choose by name or number
- Switch font before rendering

**Character alignment:**

- All letters same height within a font
- Consistent spacing between letters
- Proper handling of narrow vs wide letters

Pick an approach that makes the code easy to extend with new fonts.

## ✅ Validation

Basic test - "HI":

```
Input: "HI"
Font: standard

Output:
H   H  III
H   H   I
HHHHH   I
H   H   I
H   H  III
```

Word test - "RUST":

```
Should produce readable ASCII art
All letters aligned
Consistent height
Proper spacing
```

Number test - "2024":

```
Should render numbers correctly
Same height as letters
Readable digits
```

Edge cases to verify:

```
Input: ""           → Empty or message
Input: "a"          → Single character works
Input: "Hello"      → Mixed case handled
Input: "Hi!"        → Punctuation works
Input: "X Y Z"      → Spaces between words
Input: "@#$"        → Unknown chars handled
```

Different fonts produce different styles:

```
Font: standard → Clean, readable
Font: block    → Bold, thick letters
Font: banner   → Decorative style
```

## 🔍 Challenge

Add a "shadow" effect where letters have a drop shadow, or implement color support using ANSI escape codes to make colorful ASCII art.

---

**Previous:** [12_guess_number](../12_guess_number/README.md) | **Next:** [14_unit_converter](../14_unit_converter/README.md)
