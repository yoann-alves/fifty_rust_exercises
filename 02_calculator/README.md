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

## 📖 Background

**Calculators** are fundamental programs that demonstrate input processing, computation, and error handling.

**Basic arithmetic operations:**

```
Addition:       5 + 3 = 8
Subtraction:    10 - 4 = 6
Multiplication: 6 * 7 = 42
Division:       8 / 2 = 4
```

**Division is special** because it can fail:

```
8 / 2 = 4     ✓ Valid
5 / 0 = ???   ✗ Undefined (error!)
```

**Real calculators handle errors gracefully:**

- They don't crash when given invalid input
- They show helpful error messages
- They let you try again

Your job: build a calculator that performs basic math and handles problems elegantly.

## ⚙️ Requirements

**First Pass:**

- ✅ Performs all four operations (+, -, \*, /)
- ✅ Handles division by zero without crashing
- ✅ Works with numbers (integers or floats)
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Comments explaining key logic
- ✅ **Edge cases**:
  - Invalid operation symbols
  - Non-numeric input
  - Very large/small numbers
  - Negative numbers
- ✅ **Error messages**: Clear, helpful messages for each error type
- ✅ **Clean structure**: Organized, readable code
- ✅ **No panics**: All error cases handled gracefully

## 🚫 Constraints

- Standard library only
- No external crates
- Handle errors properly (no `.unwrap()` or `.expect()`)

## 💡 Approaches

**Input formats to consider:**

- Command-line args: `program 5 + 3`
- Interactive prompts: ask for each piece
- Single expression: "5 + 3"
- Multiple lines: number, operator, number separately

**Operation handling strategies:**

- Pattern matching on operator
- If/else chains
- Function lookup
- Enum for operations

**Number types:**

- Integers (whole numbers)
- Floating-point (decimals)
- Which makes more sense for your calculator?

**Error handling approaches:**

- Return Result types
- Option types for maybe-valid operations
- Custom error types
- Simple error messages

Pick the approach that feels right for your design.

## ✅ Validation

Your calculator should produce these results:

```bash
5 + 3   → 8
10 - 4  → 6
6 * 7   → 42
8 / 2   → 4
9 / 3   → 3
```

Error cases to handle:

```
5 / 0       → Error: Division by zero
5 % 3       → Error: Unknown operation '%'
abc + 5     → Error: Invalid number 'abc'
5 +         → Error: Missing second number
```

With floating-point numbers:

```
5.5 + 2.3   → 7.8
10.0 / 4.0  → 2.5
-5 + 3      → -2
```

## 🔍 Challenge

Add support for more operations (%, ^, sqrt) or allow chaining multiple operations in one expression like "5 + 3 \* 2".

---

**Previous:** [01_hello_custom](../01_hello_custom/README.md) | **Next:** [03_fizzbuzz](../03_fizzbuzz/README.md)
