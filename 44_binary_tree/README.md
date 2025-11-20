# Exercise 44: Binary Tree

## 🎯 Objectives

Implement a binary search tree (BST):

- Create Node and BinaryTree structures
- Operations: insert, search, delete
- Tree traversals: inorder, preorder, postorder
- Understand recursive data structures

## 📚 Concepts

- Binary tree structure
- Recursive algorithms
- Tree traversal strategies
- Binary search tree property
- Node ownership patterns
- Generic programming

## 📖 Background

**Binary Search Tree (BST)** is a hierarchical data structure where:

- Each node has at most 2 children (left, right)
- Left child < parent < right child
- This property enables efficient searching

**Example BST:**

```
       5
      / \
     3   7
    / \ / \
   1  4 6  9
```

**Performance characteristics:**

- Balanced tree: O(log n) for search, insert, delete
- Unbalanced (degenerate): O(n) worst case - becomes like a linked list

**Tree traversals** visit nodes in different orders:

**Inorder (Left, Root, Right):**

```
Tree:     5
         / \
        3   7
       /
      1

Visits: 1, 3, 5, 7  (sorted order!)
```

**Preorder (Root, Left, Right):**

```
Same tree
Visits: 5, 3, 1, 7  (useful for copying tree structure)
```

**Postorder (Left, Right, Root):**

```
Same tree
Visits: 1, 3, 7, 5  (useful for deletion - children before parent)
```

## ⚙️ Requirements

**First Pass:**

- ✅ Insert elements maintaining BST property
- ✅ Search for elements
- ✅ At least one traversal (inorder recommended)
- ✅ Works with comparable types
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain BST property and traversals
- ✅ **Complete operations**:
  - Insert with duplicate handling strategy
  - Search/contains
  - Delete (handle all cases: no children, one child, two children)
  - Find minimum/maximum
  - Calculate height/depth
  - Count total nodes
  - Check if empty
- ✅ **All traversals**:
  - Inorder (sorted)
  - Preorder
  - Postorder
  - Level-order/breadth-first (optional)
- ✅ **Generic**: Works with any type that can be compared (Ord)
- ✅ **Validation**:
  - Method to verify BST property is maintained
  - Check tree structure is correct
- ✅ **Edge cases**:
  - Empty tree operations
  - Single node tree
  - Deleting root node
  - Deleting nodes with 0, 1, or 2 children

## 🚫 Constraints

- Standard library only
- Implement yourself (no external tree crates)
- No self-balancing required (but understand the concept)

## 💡 Approaches

**Structure design:**

- Node contains value and optional left/right children
- Tree wraps the root node
- Consider using Box for heap allocation
- Track size for O(1) node count

**Insertion strategies:**

- Start at root, compare values
- Go left if smaller, right if larger
- Insert when you find an empty spot
- What to do with duplicates? (ignore, count, allow)

**Search approach:**

- Similar to insertion - compare and navigate
- BST property makes this efficient
- Return found/not found

**Deletion is tricky - three cases:**

1. **Leaf node (no children)**: Just remove it
2. **One child**: Replace node with its child
3. **Two children**: Find inorder successor (smallest in right subtree) or predecessor, replace value, delete successor

**Traversal methods:**

- Recursive: natural fit for tree structure
- Iterative: use explicit stack
- Which to use? Both have merit

**Memory management:**

- Nodes need to own their children
- Consider using Option<Box<Node>>
- Handle ownership transfer during deletion

## ✅ Validation

Building a tree:

```
Operations:
insert(5)
insert(3)
insert(7)
insert(1)
insert(9)

Result:
       5
      / \
     3   7
    /     \
   1       9

size() → 5
```

Search operations:

```
search(5) → true
search(1) → true
search(100) → false
min() → 1
max() → 9
```

Traversals of tree [5, 3, 7, 1, 9, 4, 6]:

```
Tree structure:
       5
      / \
     3   7
    / \ / \
   1  4 6  9

inorder()   → [1, 3, 4, 5, 6, 7, 9]  (sorted!)
preorder()  → [5, 3, 1, 4, 7, 6, 9]
postorder() → [1, 4, 3, 6, 9, 7, 5]
```

Deletion cases:

```
Starting tree: [5, 3, 7, 1, 9]

delete(1)  → removes leaf
Result: [5, 3, 7, 9]

delete(7)  → removes node with one child (9)
Result: [5, 3, 9]

delete(5)  → removes root with two children
Result: tree restructured, BST property maintained
```

Edge cases:

```
Empty tree:
  - inorder() → []
  - min() → None
  - delete(5) → false

Single node tree [5]:
  - delete(5) → empty tree
  - min() → Some(5)
  - max() → Some(5)
```

Validation check:

```
Valid BST: is_valid_bst() → true

After operations that maintain BST property:
is_valid_bst() → should still be true
```

## 🔍 Challenge

Implement a self-balancing tree like AVL or Red-Black tree, add range queries to find all values between min and max, create a visualization method that pretty-prints the tree structure, or add parent pointers to enable O(1) successor/predecessor operations.

---

**Previous:** [43_linked_list](../43_linked_list/README.md) | **Next:** [45_graph](../45_graph/README.md)
