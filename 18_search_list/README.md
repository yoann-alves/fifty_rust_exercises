# Exercise 18: List Search

## 🎯 Objectives

Implement search algorithms:

- Linear Search (works on any list)
- Binary Search (works on sorted lists)
- Compare their performance
- Make both work with different data types

## 📚 Concepts

- Search algorithms
- Algorithm complexity (O notation)
- Generic functions
- Trait bounds
- Performance measurement

## 📖 Background

**Search algorithms** find elements in collections, but they have different requirements and speeds.

**Linear Search** - The simple approach:

```
Array: [5, 2, 8, 1, 9]
Looking for 8:
  Check 5? No
  Check 2? No
  Check 8? Yes! Found at index 2
```

- Checks every element until found
- Works on any data (sorted or not)
- O(n) time - slow for large lists

**Binary Search** - The fast approach:

```
Sorted array: [1, 2, 5, 8, 9]
Looking for 8:
  Middle is 5. 8 > 5, search right half
  Right half: [8, 9]. Middle is 8. Found!
```

- Only works on **sorted** data
- Cuts search space in half each step
- O(log n) time - fast even for huge lists

**Performance difference:**

```
1,000,000 elements:
- Linear: might check 500,000 items on average
- Binary: only checks ~20 items
```

## ⚙️ Requirements

**First Pass:**

- ✅ Linear search finds elements
- ✅ Binary search finds elements
- ✅ Returns index when found, nothing when not found
- ✅ Works with numbers
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain how each algorithm works
- ✅ **Generic**: Works with any comparable type (integers, strings, etc.)
- ✅ **Performance comparison**:
  - Test with different list sizes
  - Show time difference
  - Test searching at different positions (start, middle, end)
- ✅ **Edge cases**:
  - Empty list
  - Single element
  - Element not in list
  - Multiple occurrences (which index to return?)
- ✅ **Verification**:
  - Both algorithms give same answer
  - Binary search only used on sorted data

## 🚫 Constraints

- Standard library only
- Implement the algorithms yourself (no `.binary_search()` or similar)
- Binary search must only be called on sorted data

## 💡 Approaches

**For Linear Search:**

- Loop through each element
- Compare with target
- Return index if match
- Return "not found" if loop completes

**For Binary Search:**

- Keep track of search range (start, end)
- Check middle element
- Adjust range based on comparison
- Repeat until found or range is empty
- Can be done with loop or recursion

**Making it generic:**

- Linear search needs: ability to check equality
- Binary search needs: ability to compare (less than, greater than)

**Benchmarking ideas:**

- Create lists of various sizes
- Time how long searches take
- Try searching for first, middle, last elements
- Try searching for non-existent elements
- Calculate average times

## ✅ Validation

Basic functionality:

```
List: [1, 3, 5, 7, 9, 11, 13]

Search for 7:
  Linear:  found at index 3
  Binary:  found at index 3

Search for 6:
  Linear:  not found
  Binary:  not found

Search for 1:
  Linear:  found at index 0
  Binary:  found at index 0

Search for 13:
  Linear:  found at index 6
  Binary:  found at index 6
```

Edge cases:

```
Empty list [], search for 5:
  Linear:  not found
  Binary:  not found

Single element [5], search for 5:
  Linear:  found at index 0
  Binary:  found at index 0

Single element [5], search for 3:
  Linear:  not found
  Binary:  not found
```

Performance example (approximate times will vary):

```
List size: 100,000 elements (sorted)
Searching for middle element:

Linear Search:  ~0.5 ms  (checked ~50,000 elements)
Binary Search:  ~0.001 ms  (checked ~17 elements)
Speedup: 500x faster
```

Works with different types:

```
Vec<i32>:     [1, 2, 3] - works ✓
Vec<String>:  ["a", "b", "c"] - works ✓
Vec<f64>:     [1.5, 2.7, 3.9] - works ✓
```

## 🔍 Challenge

Implement jump search or interpolation search, which can be even faster than binary search in certain situations.

---

**Previous:** [17_sorting](../17_sorting/README.md) | **Next:** [19_remove_duplicates](../19_remove_duplicates/README.md)
