# Exercise 06: Factorial

## 🎯 Objectives

Create a program that calculates factorial (n!):

- Implement an iterative version
- Implement a recursive version
- Handle large numbers properly
- Compare both approaches

## 📚 Concepts

- Recursion vs iteration
- Integer overflow
- Large number handling
- Error handling for edge cases

## 📖 Background

**Factorial** is the product of all positive integers less than or equal to n:

```
5! = 5 × 4 × 3 × 2 × 1 = 120
0! = 1 (by definition)
1! = 1
```

**The recursive definition:**

```
n! = n × (n-1)!
0! = 1 (base case)
```

**Growth is explosive:**

```
10! = 3,628,800
20! = 2,432,902,008,176,640,000
30! = 265,252,859,812,191,058,636,308,480,000,000
```

**The overflow problem:** Standard integers (u64) can only hold up to 20!. Beyond that, you need larger types or special handling.

## ⚙️ Requirements

**First Pass:**

- ✅ Recursive version works
- ✅ Iterative version works
- ✅ Both produce same results
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain the overflow limits
- ✅ **Edge cases**:
  - 0! = 1
  - 1! = 1
  - Negative numbers → error
  - Numbers that overflow → error
- ✅ **Overflow handling**:
  - Detect overflow before it happens
  - Return clear error when n is too large
  - Document maximum supported n
- ✅ **Comparison**: Show that both methods give identical results
- ✅ **Clean errors**: Helpful messages for invalid input

## 🚫 Constraints

- Standard library only
- No external crates for big integers
- Must implement BOTH recursive and iterative versions
- Use `u128` for calculations (Rust's largest built-in unsigned integer)

## 💡 Approaches

**Two implementation styles:**

- Recursive: elegant, follows mathematical definition
- Iterative: loop-based, typically more efficient

**Overflow prevention strategies:**

- Use checked arithmetic operations
- Pre-calculate maximum safe n
- Return `Option<u128>` or `Result<u128, Error>`
- Test before multiplying

**Questions to consider:**

- What's the largest n where n! fits in u128?
- Which version is safer for deep recursion?
- How do you detect overflow before it corrupts the result?
- Should you cache results?

**Input/output design:**

- Calculate single value
- Calculate range (1! through 10!)
- Interactive mode
- Command-line arguments

## ✅ Validation

Both implementations should produce identical results:

```
0!  = 1
1!  = 1
5!  = 120
10! = 3,628,800
15! = 1,307,674,368,000
20! = 2,432,902,008,176,640,000
```

**Overflow behavior:**

```
34! = 295,232,799,039,604,140,847,618,609,643,520,000,000  (fits in u128)
35! = overflow (should return error, not wrap around)
```

**Error cases:**

```
Input: -5     → Error: "Factorial not defined for negative numbers"
Input: 100    → Error: "Result would overflow (max n = 34)"
```

**Comparison test:**

```
For n = 0 to 20:
  recursive(n) == iterative(n) ✓
```

## 🔍 Challenge

Implement arbitrary-precision factorial that can calculate 100! or even 1000! by representing numbers as strings or vectors of digits, or add memoization to make recursive version competitive with iterative.

---

**Previous:** [05_fibonacci](../05_fibonacci/README.md) | **Next:** [07_prime_number](../07_prime_number/README.md)
