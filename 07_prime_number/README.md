# Exercise 07: Prime Number

## 🎯 Objectives

Create a program that works with prime numbers:

- Check if a number is prime
- Find all prime numbers up to n
- Store results in a `Vec<u64>`

## 📚 Concepts

- Functions and return values
- Boolean logic
- Vectors (dynamic arrays)
- Loops and iteration
- Algorithm optimization

## 📖 Background

**A prime number** is a natural number greater than 1 that cannot be formed by multiplying two smaller natural numbers.

Examples of primes:

```
2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37...
```

**Key facts:**

- 1 is NOT a prime number (by definition)
- 2 is the ONLY even prime number
- All other primes are odd
- There are infinitely many primes

**Why check only up to √n?**

```
If n = a × b, then one of a or b must be ≤ √n
Example: 36 = 6 × 6
If we check up to 6, we'll find all factors
```

## ⚙️ Requirements

**First Pass:**

- ✅ Function checks if a number is prime
- ✅ Finds all primes up to given n
- ✅ Stores results in a `Vec`
- ✅ Handles edge cases (0, 1, 2)
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Function documentation explaining what it does
- ✅ **Optimized checking**:
  - Don't test divisors beyond √n
  - Skip even numbers after testing 2
  - Handle special cases early
- ✅ **Edge cases tested**:
  - Numbers 0, 1, 2
  - Large numbers
  - Negative numbers (if applicable)
- ✅ **Clear output**:
  - Show the primes found
  - Display count of primes
  - Handle large lists gracefully

## 🚫 Constraints

- Standard library only
- No external crates
- Must use `Vec` to store primes
- Implement your own prime checking logic

## 💡 Approaches

**Checking if a single number is prime:**

- Test divisibility by all numbers from 2 to n-1
- Test only up to √n (more efficient)
- Test 2, then only odd numbers
- Return early when factor found

**Finding all primes up to n:**

- Check each number individually with your prime function
- Use the Sieve of Eratosthenes algorithm
- Build the Vec as you find primes

**Vec strategies:**

- Push primes one by one
- Pre-allocate capacity for better performance
- Filter and collect from a range

Choose whatever makes sense to you.

## ✅ Validation

Your prime checker should give:

```
is_prime(0)  → false
is_prime(1)  → false
is_prime(2)  → true
is_prime(3)  → true
is_prime(4)  → false
is_prime(17) → true
is_prime(18) → false
is_prime(97) → true
```

Finding all primes up to 30:

```
[2, 3, 5, 7, 11, 13, 17, 19, 23, 29]
Count: 10 primes
```

Finding all primes up to 100:

```
Count: 25 primes
```

Benchmark expectations:

```
n = 100       → instant
n = 10,000    → very fast
n = 100,000   → should complete in reasonable time
n = 1,000,000 → depends on your algorithm
```

## 🔍 Challenge

Implement the Sieve of Eratosthenes algorithm and compare its speed to your original approach. Can you find all primes up to 1,000,000 in under a second?

---

**Previous:** [06_factorial](../06_factorial/README.md) | **Next:** [08_palindrome_checker](../08_palindrome_checker/README.md)
