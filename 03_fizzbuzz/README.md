# Exercise 03: FizzBuzz

## 🎯 Objectives

Create a program that prints numbers from 1 to 100, but:

- Print "Fizz" if the number is divisible by 3
- Print "Buzz" if the number is divisible by 5
- Print "FizzBuzz" if divisible by both 3 and 5
- Otherwise, print the number itself

## 📚 Concepts

- Loops (iteration from 1 to 100)
- Modulo operator (checking divisibility)
- Conditional logic (multiple conditions)
- String formatting and printing

## ⚙️ Requirements

**First Pass:**

- ✅ Prints all numbers 1-100 with correct Fizz/Buzz logic
- ✅ Correct output for all cases
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Brief comment explaining the logic
- ✅ **Clean conditionals**: Order matters - think about which condition to check first
- ✅ **Consider extending**:
  - Make the range configurable (1 to N)
  - Make the divisors configurable (not just 3 and 5)
  - Add tests (unit tests for individual number logic)
- ✅ **Idiomatic code**: Use Rust's iteration patterns effectively

## 🚫 Constraints

- Standard library only
- No external crates
- Must print exactly 100 lines of output

## 💡 Approaches

Loops:

- `for` loop with range
- `while` loop with counter
- Iterator methods

Conditional logic:

- Nested `if/else`
- Match expression
- Pattern matching with guards

Think about: What order should you check the conditions?

## ✅ Validation

First few lines of output should be:

```
1
2
Fizz
4
Buzz
Fizz
7
8
Fizz
Buzz
11
Fizz
13
14
FizzBuzz
```

Last line (100) should be: `Buzz`

---

**Previous:** [calculator_02](../calculator_02/README.md) | **Next:** [temperature_conversion_04](../temperature_conversion_04/README.md)
