# Exercise 10: Random Number Generator

## 🎯 Objectives

Create a random number generator that:

- Generates n random numbers within a specified range
- Calculates the mean (average) of generated numbers
- Calculates the median of generated numbers
- Uses the `rand` crate

## 📚 Concepts

- External crate usage (Cargo dependencies)
- Random number generation
- Statistical calculations (mean, median)
- Sorting algorithms
- Floating-point arithmetic

## 📖 Background

**Random number generation** is fundamental in programming - for simulations, games, cryptography, testing, and statistics.

**Statistical measures** help us understand data:

**Mean (Average)**:

```
Numbers: [2, 4, 6, 8, 10]
Mean = (2 + 4 + 6 + 8 + 10) / 5 = 30 / 5 = 6
```

**Median (Middle value)**:

```
Odd count [1, 3, 5, 7, 9] → median is 5 (middle)
Even count [1, 2, 3, 4] → median is (2 + 3) / 2 = 2.5 (average of two middles)
```

**Important**: The median requires sorted data:

```
Unsorted: [45, 12, 67, 23, 89]
Sorted:   [12, 23, 45, 67, 89]
Median:   45 (middle element)
```

## ⚙️ Requirements

**First Pass:**

- ✅ Generates n random numbers in a range
- ✅ Calculates mean correctly
- ✅ Calculates median correctly
- ✅ Uses `rand` crate
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain the statistical calculations
- ✅ **Configurable**:
  - User specifies how many numbers
  - User specifies min/max range
  - Integer or floating-point numbers
- ✅ **Edge cases**:
  - n = 0 → handle gracefully
  - n = 1 → mean and median are the same
  - min = max → all numbers identical
  - min > max → invalid range error
- ✅ **Display**:
  - Show generated numbers (if reasonable)
  - Clear mean and median output
  - Additional stats (min, max, count)
- ✅ **Correct median**: Handle both odd and even counts properly

## 🚫 Constraints

- **Must use** the `rand` crate (external dependency required)
- Standard library for statistics calculations
- No statistics crates - implement mean/median yourself

## 💡 Approaches

**Adding dependencies:**

- Edit `Cargo.toml`
- Add `rand` under `[dependencies]`
- Cargo will download on next build

**Random generation strategies:**

- Thread-local RNG for simplicity
- Range-based generation
- Integer vs floating-point generation

**Mean calculation:**

- Sum all values
- Divide by count
- Watch out for integer division vs float division

**Median calculation:**

- Must sort the array first
- Find middle element(s)
- Handle odd vs even count differently
- Consider: do you modify original array or copy?

**Input/configuration:**

- Hard-coded values
- Command-line arguments
- Interactive prompts
- Configuration file

## ✅ Validation

Example runs:

```bash
# Generate 10 numbers between 1 and 100
Generated 10 numbers: [23, 67, 12, 89, 45, 34, 78, 56, 91, 28]

Statistics:
Mean:   52.3
Median: 50.5
Min:    12
Max:    91
Count:  10
```

Edge case examples:

```
# Single number
Numbers: [42]
Mean: 42.0
Median: 42.0

# Even count (median is average of middle two)
Numbers: [1, 2, 3, 4]
Sorted:  [1, 2, 3, 4]
Median: (2 + 3) / 2 = 2.5

# Odd count (median is middle element)
Numbers: [5, 1, 9, 3, 7]
Sorted:  [1, 3, 5, 7, 9]
Median: 5
```

Verify your calculations:

- Mean should be within the specified range (approximately)
- Median calculation matches manual sorting
- Edge cases don't crash the program

## 🔍 Challenge

Add more statistical measures: mode (most frequent value), standard deviation, or generate numbers following a specific distribution (normal, exponential) instead of uniform random.

---

**Previous:** [09_word_counter](../09_word_counter/README.md) | **Next:** [11_caesar_cipher](../11_caesar_cipher/README.md)
