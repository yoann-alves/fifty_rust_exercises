# Exercise 03: FizzBuzz

## 🎯 Objectives

Create a program that prints numbers from 1 to 100, but:

- Print "Fizz" if the number is divisible by 3
- Print "Buzz" if the number is divisible by 5
- Print "FizzBuzz" if divisible by both 3 and 5
- Otherwise, print the number itself

## 📚 Concepts

- Loops (iteration)
- Modulo operator (checking divisibility)
- Conditional logic
- String formatting

## 📖 Background

**FizzBuzz** is a classic programming exercise often used in interviews. It tests basic programming skills: loops, conditionals, and divisibility.

**The rules are simple:**

```
1 → "1"
2 → "2"
3 → "Fizz"     (divisible by 3)
4 → "4"
5 → "Buzz"     (divisible by 5)
6 → "Fizz"     (divisible by 3)
...
15 → "FizzBuzz" (divisible by both!)
```

**The trick:** Order matters when checking conditions. If you check for 3 and 5 separately before checking for both, you'll never reach the FizzBuzz case.

**Divisibility test:** A number is divisible by N if `number % N == 0`

## ⚙️ Requirements

**First Pass:**

- ✅ Prints numbers 1 to 100
- ✅ Correct Fizz/Buzz/FizzBuzz logic
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Brief comment explaining the logic
- ✅ **Clean conditionals**: Proper order of checks
- ✅ **Idiomatic Rust**: Use appropriate iteration patterns

## 🚫 Constraints

- Standard library only
- No external crates
- Must print exactly 100 lines

## 💡 Approaches

**Loop options:**

- Range-based iteration
- While loop with counter
- Iterator methods

**Conditional structures:**

- If/else chain
- Match expression
- Separate checks vs combined check

**Key question:** In what order should you check divisibility? Think about which cases overlap.

## ✅ Validation

First 15 lines should be:

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

Other important checks:

```
Line 30: FizzBuzz
Line 45: FizzBuzz
Line 60: FizzBuzz
Line 99: Fizz
Line 100: Buzz
```

## 🔍 Challenge

Make FizzBuzz configurable: allow the user to specify the range (not just 1-100) and the divisors (not just 3 and 5). For example, "Bizz" for 7, "Fuzz" for 11.

Or implement FizzBuzz as a function that returns a String for any given number, then write tests for it.

---

**Previous:** [02_calculator](../02_calculator/README.md) | **Next:** [04_temperature_conversion](../04_temperature_conversion/README.md)
