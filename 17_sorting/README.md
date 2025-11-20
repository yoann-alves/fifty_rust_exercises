# Exercise 17: Custom Sorting

## 🎯 Objectives

Implement sorting algorithms from scratch:

- Bubble Sort
- Insertion Sort
- Quick Sort
- Compare their performance on different data sizes

## 📚 Concepts

- Sorting algorithms
- Algorithm complexity (Big O notation)
- Generic functions with trait bounds
- Performance measurement
- In-place vs. allocating algorithms

## 📖 Background

**Sorting** is ordering elements according to some criteria (usually ascending).

**Different algorithms have different characteristics:**

```
Bubble Sort:
- Compares neighbors, swaps if wrong order
- Repeats until sorted
- Simple but slow: O(n²)

Insertion Sort:
- Builds sorted section one item at a time
- Finds right spot for each new element
- Good for small or nearly-sorted data: O(n²)

Quick Sort:
- Picks a "pivot" element
- Puts smaller items left, larger items right
- Recursively sorts each side
- Fast on average: O(n log n)
```

**Performance matters:**

- Small arrays (100 items): all algorithms fast enough
- Large arrays (10,000+ items): algorithm choice critical
- Already sorted data: some algorithms struggle, others excel

**Real-world context:**

- Databases sort millions of records
- Graphics engines sort objects by distance
- Search engines sort results by relevance

## ⚙️ Requirements

**First Pass:**

- ✅ Three sorting algorithms implemented
- ✅ Correctly sort arrays of integers
- ✅ Verify with test cases
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain each algorithm and its complexity
- ✅ **Generic**:
  - Work with any comparable type (integers, floats, strings, etc.)
  - Use proper trait bounds
- ✅ **Performance comparison**:
  - Test multiple sizes (100, 1K, 10K elements)
  - Test different patterns (random, sorted, reversed)
  - Measure and display timing
  - Show which algorithm is fastest for each scenario
- ✅ **Statistics** (optional but nice):
  - Count comparisons
  - Count swaps/moves
  - Display for small examples

## 🚫 Constraints

- Standard library only
- Don't use built-in `.sort()` or sorting crates
- Must implement all three algorithms yourself
- Use `std::time::Instant` for timing

## 💡 Approaches

**Bubble Sort concept:**

- Look at pairs of neighbors
- Swap if wrong order
- Keep going until a full pass has no swaps

**Insertion Sort concept:**

- Maintain a sorted section (starts with first element)
- Take next unsorted element
- Find where it belongs in sorted section
- Shift elements to make room
- Insert it

**Quick Sort concept:**

- Pick a pivot (any element)
- Rearrange so smaller elements are left, larger are right
- Now pivot is in final position
- Do the same for left and right sections
- Base case: sections of 0 or 1 elements are already sorted

**Making it generic:**

- Work with slices instead of specific types
- Use trait bounds for comparison
- Consider what operations you need (compare, swap)

**Performance testing:**

- Generate test data (random numbers)
- Time each algorithm
- Run multiple times and average
- Test different scenarios (best case, worst case, average case)

## ✅ Validation

All algorithms should sort correctly:

```
Input:  [5, 2, 8, 1, 9]
All three algorithms produce: [1, 2, 5, 8, 9]

Input:  [3, 3, 1, 2, 3]  (duplicates)
Output: [1, 2, 3, 3, 3]

Input:  [1]  (single element)
Output: [1]

Input:  []  (empty)
Output: []
```

Generic capability:

```
Should work with:
- Integers: [5, 2, 8, 1, 9]
- Floats: [3.14, 1.41, 2.71]
- Strings: ["dog", "cat", "bird", "ant"]
- Characters: ['z', 'a', 'm', 'k']
```

Performance comparison example:

```
Testing with 1,000 random integers:
  Bubble Sort:    42.3 ms
  Insertion Sort: 18.7 ms
  Quick Sort:      1.2 ms
  Winner: Quick Sort

Testing with 1,000 already sorted:
  Bubble Sort:     8.1 ms  (best case!)
  Insertion Sort:  0.5 ms  (excellent!)
  Quick Sort:      1.1 ms
  Winner: Insertion Sort

Testing with 10,000 random integers:
  Bubble Sort:    4,231 ms  (slow!)
  Insertion Sort: 1,843 ms
  Quick Sort:       12 ms
  Winner: Quick Sort (by far!)
```

## 🔍 Challenge

**Optimize each algorithm:**

- Bubble Sort: Stop early if a pass makes no swaps (already sorted)
- Insertion Sort: Use binary search to find insertion position faster
- Quick Sort: Use "median-of-three" to pick better pivots

**Or implement a hybrid sort:** Use Quick Sort for large sections, switch to Insertion Sort for small sections (this is what many real-world sorts do).

---

**Previous:** [16_anagram_finder](../16_anagram_finder/README.md) | **Next:** [18_search_list](../18_search_list/README.md)
