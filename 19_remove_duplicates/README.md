# Exercise 19: Remove Duplicates

## 🎯 Objectives

Remove duplicate elements from a collection:

- Keep only unique elements
- Preserve original order (one version)
- Sort the result (another version)
- Compare different approaches

## 📚 Concepts

- Set data structures
- Collection manipulation
- Order preservation vs sorting
- Algorithm complexity
- Performance trade-offs

## 📖 Background

**Removing duplicates** is a common task with different requirements depending on context:

```
Original: [5, 2, 5, 1, 2, 3]

Preserve order (keep first):
[5, 2, 1, 3]

Sorted result:
[1, 2, 3, 5]
```

**Real-world examples:**

- Cleaning user input lists
- Processing log files
- Database query results
- Merging datasets

**Different approaches have different costs:**

- Some are fast but use extra memory
- Some are slower but use less memory
- Some preserve order, others don't
- Some work in-place, others create new collections

## ⚙️ Requirements

**First Pass:**

- ✅ Removes all duplicate elements
- ✅ Works with a collection of integers
- ✅ Produces correct output
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain trade-offs of each approach
- ✅ **Two versions**:
  - Order-preserving (first occurrence kept)
  - Sorted result
- ✅ **Try multiple approaches**: At least 2-3 different methods
- ✅ **Generic**: Works with different types (not just integers)
- ✅ **Edge cases**:
  - Empty collection
  - No duplicates present
  - All elements identical
  - Single element
- ✅ **Performance notes**: Document complexity of each approach

## 🚫 Constraints

- Standard library only
- Implement the logic yourself (don't just call `.dedup()`)
- Can use standard collections (HashSet, etc.)

## 💡 Approaches

**Method 1: Using a set**

- Track which elements you've seen
- Skip elements already encountered
- Keeps order of first occurrence

**Method 2: Sort first**

- Sort the collection
- Walk through removing consecutive duplicates
- Changes order but can be efficient

**Method 3: Nested checking**

- For each element, scan ahead for duplicates
- Simple to understand
- May be slower for large collections

**Method 4: Combinations**

- Mix and match techniques
- Consider in-place vs creating new collection

**Things to think about:**

- Memory usage (extra storage vs in-place)
- Time complexity (how fast for large inputs?)
- Order preservation (does it matter?)
- Generic constraints (what traits do you need?)

## ✅ Validation

Test with these inputs:

```
Input:  [1, 2, 2, 3, 4, 4, 4, 5]
Preserve order: [1, 2, 3, 4, 5]
Sorted:         [1, 2, 3, 4, 5]

Input:  [5, 2, 5, 1, 2]
Preserve order: [5, 2, 1]
Sorted:         [1, 2, 5]

Input:  [7, 7, 7, 7]
Output: [7]

Input:  []
Output: []

Input:  [1, 2, 3]  (no duplicates)
Output: [1, 2, 3]

Input:  [42]  (single element)
Output: [42]
```

Should work with different types:

```
Integers: [1, 2, 2, 3] → [1, 2, 3]
Strings:  ["a", "b", "a"] → ["a", "b"]
Characters: ['x', 'y', 'x'] → ['x', 'y']
```

## 🔍 Challenge

Implement an in-place version that removes duplicates from the original collection without allocating a new one, keeping memory usage minimal.

---

**Previous:** [18_search_list](../18_search_list/README.md) | **Next:** [20_merge_sorted](../20_merge_sorted/README.md)
