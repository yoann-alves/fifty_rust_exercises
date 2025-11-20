# Exercise 43: Linked List

## 🎯 Objectives

Implement your own linked list from scratch:

- Generic LinkedList<T> data structure
- Operations: push, pop, insert, remove
- Implement Iterator trait
- Understand ownership in complex structures

## 📚 Concepts

- Box and pointer-based structures
- Recursive data structures
- Ownership and borrowing in self-referential structures
- Iterator trait implementation
- Memory management

## 📖 Background

**Linked lists** are fundamental data structures made of nodes connected by pointers:

```
[Data|Next] -> [Data|Next] -> [Data|Next] -> None

Example:
[5|•] -> [3|•] -> [8|None]
```

**Performance characteristics:**

- Adding to front: instant (O(1))
- Removing from front: instant (O(1))
- Accessing middle element: slow (O(n)) - must walk from start
- Dynamic size: grows and shrinks as needed

**Types of linked lists:**

- Singly-linked: each node points only to the next
- Doubly-linked: each node points to both next and previous

**Why they matter:**

- Foundation for understanding pointers and memory
- Used in implementing other data structures (queues, stacks)
- Common in systems programming

**The ownership challenge:**
Each node "owns" the next node. When the list is dropped, all nodes must be properly cleaned up without stack overflow.

## ⚙️ Requirements

**First Pass:**

- ✅ LinkedList<T> struct exists
- ✅ Can push to front
- ✅ Can pop from front
- ✅ Tracks length
- ✅ Works with integers
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Doc comments explaining the structure
- ✅ **Complete operations**:
  - push_front, push_back
  - pop_front, pop_back
  - insert at index
  - remove at index
  - get element at index
  - clear all elements
  - is_empty check
- ✅ **Generic**: Works with any type T
- ✅ **Iterator support**:
  - Can iterate with for loops
  - Provides iter() for borrowing
  - Provides into_iter() for consuming
- ✅ **Trait implementations**:
  - Display for printing
  - Debug for debugging
  - Clone (if T: Clone)
  - Drop for cleanup
  - PartialEq for comparison
- ✅ **Edge cases**:
  - Empty list operations return None
  - Single element handled correctly
  - Out of bounds returns error/None
  - No memory leaks
- ✅ **Performance**: O(1) for front operations

## 🚫 Constraints

- Implement yourself (no std::collections::LinkedList)
- Standard library only
- Must properly clean up memory (no leaks)
- Safe Rust preferred

## 💡 Approaches

**Structure options:**

- Box for heap allocation
- Option for "maybe has next node"
- Separate Node struct vs inline
- Track length or compute it?

**Ownership patterns:**

- Who owns each node?
- How to traverse without consuming?
- How to modify while iterating?

**Iterator strategies:**

- Borrowing iterator (iter)
- Mutable iterator (iter_mut)
- Consuming iterator (into_iter)
- What does each yield?

**Memory management:**

- How to drop long chains without stack overflow?
- When to use take() vs clone()?
- Recursive vs iterative cleanup?

Think about how the chain of ownership works: list owns first node, first node owns second node, etc.

## ✅ Validation

Basic operations should work:

```
Create empty list
Push 3, 2, 1 to front
List is now: 1 -> 2 -> 3
Length: 3

Pop from front returns: 1
Pop from front returns: 2
Pop from front returns: 3
Pop from front returns: None
List is empty
```

Insertion example:

```
List: 1 -> 3
Insert 2 at position 1
List: 1 -> 2 -> 3
```

Iterator usage:

```
List: 1 -> 2 -> 3

for item in list.iter():
    prints: 1, 2, 3

List still exists after iteration
```

Generic types:

```
LinkedList<String> works
LinkedList<Person> works
LinkedList<Vec<i32>> works
```

Display output:

```
Empty list: []
List with items: [1 -> 2 -> 3]
```

Edge cases:

```
Pop from empty → None
Insert beyond length → Error
Get index 100 on 3-item list → None
Single item, then pop → becomes empty
```

## 🔍 Challenge

Implement a doubly-linked list where each node can navigate both forward and backward, or implement a circular linked list where the last node points back to the first.

---

**Previous:** [42_matrix](../42_matrix/README.md) | **Next:** [44_binary_tree](../44_binary_tree/README.md)
