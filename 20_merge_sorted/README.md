# Exercise 20: Merge Sorted Lists

## 🎯 Objectives

Merge two sorted Vecs into one sorted Vec:

- Takes two already-sorted Vecs as input
- Produces single sorted Vec as output
- Optimal O(n+m) time complexity (single pass)
- Generic implementation

## 📚 Concepts

- Two-pointer technique
- Merge algorithm (from merge sort)
- Maintaining sorted invariant
- Generic programming with trait bounds
- Algorithm efficiency analysis

## 📖 Background

**The merge operation** is a fundamental building block in computer science, used in:

- Merge sort algorithm
- External sorting (when data doesn't fit in memory)
- Combining sorted database results
- Streaming data processing

**The challenge:** You have two Vecs that are already sorted. You need to combine them into one sorted Vec **without** re-sorting everything (which would waste the fact that they're already sorted).

**Example:**

```
List A: [1, 5, 9, 12]
List B: [2, 7, 10, 15, 20]

Naive approach: Concatenate → [1, 5, 9, 12, 2, 7, 10, 15, 20]
                Then sort → [1, 2, 5, 7, 9, 10, 12, 15, 20]
                Time: O((n+m) log(n+m))

Smart approach: Merge while preserving order
                Result: [1, 2, 5, 7, 9, 10, 12, 15, 20]
                Time: O(n+m)
```

**The two-pointer technique:**
Think of it like merging two lines of people ordered by height. You always pick the shorter person from the front of either line until both lines are empty.

## ⚙️ Requirements

**First Pass:**

- ✅ Merges two sorted Vecs correctly
- ✅ Result is sorted
- ✅ Works with integer Vecs
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain the algorithm and its complexity
- ✅ **Generic implementation**: Works with any `T: Ord`
- ✅ **Optimal algorithm**: True O(n+m) time - no sorting after merge
- ✅ **Edge cases**:
  - One or both Vecs empty
  - Vecs of very different sizes
  - All elements of one Vec smaller than the other
  - Duplicate elements across both Vecs
- ✅ **Input validation**: Document what happens if inputs aren't actually sorted
- ✅ **Performance**: Verify linear time with benchmarks

## 🚫 Constraints

- Standard library only
- No external crates
- Cannot use built-in merge functions
- Must achieve O(n+m) time complexity (not O((n+m) log(n+m)))

## 💡 Approaches

**The two-pointer strategy:**

- Keep track of position in each Vec
- Compare elements at current positions
- Take the smaller one, advance that pointer
- Continue until both Vecs exhausted
- Handle any remaining elements

**Design decisions to consider:**

- Should function take ownership or borrow?
- Return new Vec or modify in-place?
- Index-based iteration vs iterator pattern?

**Handling duplicates:**
When the same value appears in both Vecs, what do you do? Keep both? Which one first? Document your choice.

**Verification strategy:**

- Result length = sum of input lengths
- Result maintains sorted order
- All elements accounted for

## ✅ Validation

Basic merging:

```
Vec1: [1, 3, 5, 7]
Vec2: [2, 4, 6, 8]
Result: [1, 2, 3, 4, 5, 6, 7, 8]
```

Non-overlapping ranges:

```
Vec1: [1, 2, 3]
Vec2: [4, 5, 6]
Result: [1, 2, 3, 4, 5, 6]
```

Interleaved values:

```
Vec1: [1, 5, 9]
Vec2: [2, 3, 7, 8]
Result: [1, 2, 3, 5, 7, 8, 9]
```

Empty Vec:

```
Vec1: []
Vec2: [1, 2, 3]
Result: [1, 2, 3]
```

Duplicates:

```
Vec1: [1, 1, 2]
Vec2: [1, 3, 3]
Result: [1, 1, 1, 2, 3, 3]
```

Performance comparison (200,000 total elements):

```
Your merge (optimal):     ~2ms
Concat then sort (naive): ~30ms
Speedup: ~15x
```

Generic types:

```
Works with: Vec<i32>, Vec<f64>, Vec<String>, Vec<char>
```

## 🔍 Challenge

Extend your solution to merge K sorted Vecs (not just 2) efficiently. The naive approach of merging them one by one is suboptimal - can you use a min-heap to do better?

---

**Previous:** [19_remove_duplicates](../19_remove_duplicates/README.md) | **Next:** [21_balanced_parentheses](../21_balanced_parentheses/README.md)
