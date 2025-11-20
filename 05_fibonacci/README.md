# Exercise 05: Fibonacci

## 🎯 Objectives

Create a program that calculates the nth Fibonacci number:

- Implement a recursive version
- Implement an iterative version
- Measure and compare performance of both approaches

## 📚 Concepts

- Recursion (function calling itself)
- Iteration (loops)
- Performance measurement
- Algorithm efficiency (time complexity)
- Stack overflow risks

## 📖 Background

**The Fibonacci sequence** is one of the most famous sequences in mathematics. Each number is the sum of the two preceding ones:

```
Position:  0, 1, 2, 3, 4, 5,  6,  7,  8,  9, 10...
Fibonacci: 0, 1, 1, 2, 3, 5,  8, 13, 21, 34, 55...
```

**The mathematical definition:**

```
F(0) = 0
F(1) = 1
F(n) = F(n-1) + F(n-2)  for n > 1
```

**Why this exercise matters:**

- Shows the dramatic difference between naive recursion and iteration
- Demonstrates that "elegant" doesn't always mean "efficient"
- Teaches performance measurement fundamentals
- Illustrates exponential vs linear time complexity

**Real-world occurrence:**

- Nature: flower petals, pine cones, shells
- Art: golden ratio approximation
- Computer science: algorithm analysis teaching example

## ⚙️ Requirements

**First Pass:**

- ✅ Recursive implementation works correctly
- ✅ Iterative implementation works correctly
- ✅ Both produce identical results
- ✅ Measures and displays execution time for both
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain why one approach is faster than the other
- ✅ **Edge cases**:
  - F(0) → 0
  - F(1) → 1
  - Large n (recursive becomes impractical)
- ✅ **Performance analysis**:
  - Test multiple values (e.g., 10, 20, 30, 40)
  - Display timing in appropriate units
  - Comment on when recursive becomes unusable
- ✅ **Error handling**: Handle invalid input (negative numbers)
- ✅ **Overflow awareness**: Consider what happens with very large Fibonacci numbers

## 🚫 Constraints

- Standard library only
- No external crates
- Must implement BOTH recursive and iterative versions
- Use `std::time::Instant` for performance measurement

## 💡 Approaches

**Two fundamentally different strategies:**

**Recursive approach:**

- Directly follows the mathematical definition
- Elegant and simple to write
- Recalculates same values many times
- Exponential time complexity

**Iterative approach:**

- Uses a loop to build up from F(0)
- Each value calculated exactly once
- Linear time complexity
- More code but vastly faster

**Performance measurement considerations:**

- When to start/stop the timer
- What units to display (seconds, milliseconds, microseconds)
- Should you warm up before measuring?
- Multiple runs for accuracy?

**Bonus considerations:**

- Memoization (caching results)
- Matrix exponentiation method
- Closed-form formula (Binet's formula)

## ✅ Validation

Both implementations should produce identical results:

```
F(0)  = 0
F(1)  = 1
F(2)  = 1
F(5)  = 5
F(10) = 55
F(15) = 610
F(20) = 6765
F(30) = 832040
```

**Performance comparison** (approximate on modern CPU):

```
Testing F(30):
Recursive:  ~20-50ms
Iterative:  <1μs

Testing F(40):
Recursive:  several seconds (over 1 billion calls!)
Iterative:  still <1μs

Testing F(50):
Recursive:  don't even try (would take days)
Iterative:  still <1μs
```

**Expected behavior:**

```
Enter n: 35

Calculating F(35) recursively...
Result: 9227465
Time: 142.35ms

Calculating F(35) iteratively...
Result: 9227465
Time: 0.82μs

Speedup: 173,598x faster!
```

**Warning signs:**

- Recursive F(45) takes multiple seconds
- Recursive F(50) might freeze your program
- Stack overflow possible with very large n

## 🔍 Challenge

Implement memoization for the recursive version (cache previously calculated values) and compare its performance to the naive recursive approach. Can you make recursive competitive with iterative?

---

**Previous:** [04_temperature_conversion](../04_temperature_conversion/README.md) | **Next:** [06_factorial](../06_factorial/README.md)
