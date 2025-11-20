# Exercise 22: Roman Numerals

## 🎯 Objectives

Create a Roman numeral converter:

- Convert integer to Roman numerals (1 → "I", 4 → "IV")
- Convert Roman numerals to integer ("IX" → 9)
- Validate Roman numeral strings
- Handle numbers 1-3999

## 📚 Concepts

- Mapping between number systems
- String building and parsing
- Pattern recognition
- Subtraction rule in Roman numerals
- Validation logic

## 📖 Background

**Roman numerals** use letters to represent values:

```
I = 1, V = 5, X = 10, L = 50, C = 100, D = 500, M = 1000
```

**Subtraction rule**: Smaller value before larger means subtract:

```
IV = 4 (5-1), IX = 9 (10-1), XL = 40 (50-10), XC = 90,
CD = 400, CM = 900
```

**Examples in daily life:**

- Clock faces often use Roman numerals
- Movie copyright dates: MCMXCIV = 1994
- Book chapters and page numbering
- Monarch names: Louis XIV, Elizabeth II

## ⚙️ Requirements

**First Pass:**

- ✅ Integer to Roman conversion works
- ✅ Roman to integer conversion works
- ✅ Handles basic numerals (1-100 at minimum)
- ✅ Both functions correctly inverse each other
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain conversion rules
- ✅ **Full range**: Support 1-3999
- ✅ **Subtraction cases**: Handle all: IV, IX, XL, XC, CD, CM
- ✅ **Validation**:
  - Detect invalid Roman numerals
  - Check for illegal patterns
  - Verify proper ordering
  - Handle edge cases
- ✅ **Edge cases**:
  - Numbers at boundaries (1, 3999)
  - Invalid input (0, negative, > 3999)
  - Malformed Roman strings
  - Empty strings
- ✅ **Round-trip test**: int → roman → int gives original
- ✅ **Error handling**: Return Result or Option for invalid input

## 🚫 Constraints

- Standard library only
- No external crates
- Support range 1-3999 (standard Roman numeral range)
- Must handle subtraction cases

## 💡 Approaches

**Integer to Roman**:

- Start with largest values
- Subtract and append corresponding symbols
- Include subtraction cases in your mappings
- Build string iteratively

**Roman to Integer**:

- Iterate through string
- Look at current and next character
- If current < next: subtract current
- Otherwise: add current
- Sum total

**Mapping strategies:**

- Array/Vec of tuples: (value, symbol)
- Match expression
- HashMap
- Include both regular and subtraction cases

**Validation approach:**

- Check allowed characters only
- Verify ordering rules
- No more than 3 consecutive same symbols (except M)
- Subtraction rules followed correctly

## ✅ Validation

Integer to Roman:

```
1    → "I"
4    → "IV"
9    → "IX"
27   → "XXVII"
49   → "XLIX"
94   → "XCIV"
444  → "CDXLIV"
1994 → "MCMXCIV"
3999 → "MMMCMXCIX"
```

Roman to Integer:

```
"I"        → 1
"IV"       → 4
"IX"       → 9
"LVIII"    → 58
"MCMXCIV"  → 1994
```

Round-trip test (should match):

```
58 → "LVIII" → 58 ✓
1994 → "MCMXCIV" → 1994 ✓
```

Invalid cases (should error):

```
"IIII"     → Invalid (more than 3 I's)
"VV"       → Invalid (V not repeatable)
"IC"       → Invalid (illegal subtraction)
"XM"       → Invalid (illegal subtraction)
""         → Invalid (empty)
"ABC"      → Invalid (non-Roman chars)
```

## 🔍 Challenge

Implement a validator that explains WHY a Roman numeral is invalid, not just that it is.

---

**Previous:** [21_balanced_parentheses](../21_balanced_parentheses/README.md) | **Next:** [23_rle_compression](../23_rle_compression/README.md)
