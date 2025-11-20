# Exercise 02: Basic Calculator

## 🎯 Objectives

Create a calculator program that:

- Takes two numbers as input
- Takes an operation (+, -, \*, /)
- Displays the result
- Handles division by zero gracefully

## 📚 Concepts

- Parsing strings to numbers
- Mathematical operations
- Error handling (division by zero, invalid input)
- Pattern matching or conditional logic

## ⚙️ Requirements

**First Pass:**

- ✅ Performs all four operations correctly
- ✅ Handles division by zero (no crash)
- ✅ Works with integers or floats
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Clear comments explaining logic
- ✅ **Edge cases handled**:
  - Invalid operation symbols
  - Non-numeric input
  - Very large numbers (overflow)
  - Negative numbers
- ✅ **Error messages**: User-friendly messages for each error type
- ✅ **Clean structure**: Consider separating parsing and calculation logic
- ✅ **No panics**: All error cases handled gracefully

## 🚫 Constraints

- Standard library only
- No external crates
- No `.unwrap()` or `.expect()` in final version

## 💡 Approaches

Input methods (choose one or mix):

- All at once: `cargo run -- 5 + 3`
- Interactive prompts
- Single-line input: "5 + 3"
- Multiple prompts (number, operator, number)

Operation handling:

- Match expression
- If/else chains
- Function dispatch

## ✅ Validation

Your calculator should handle:

```bash
5 + 3  → 8
10 - 4 → 6
6 * 7  → 42
8 / 2  → 4
5 / 0  → Error: Division by zero
```

---

**Previous:** [hello_custom_01](../hello_custom_01/README.md) | **Next:** [fizzbuzz_03](../fizzbuzz_03/README.md)
