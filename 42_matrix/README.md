# Exercise 42: Matrix

## 🎯 Objectives

Create a generic matrix library:

- Matrix<T> struct for any numeric type
- Operations: addition, multiplication, transpose
- Implement Add and Mul traits
- Generic over numeric types
- Proper dimension handling

## 📚 Concepts

- Generic programming with type parameters
- Trait bounds (numeric types)
- Operator overloading (Add, Mul traits)
- 2D data structures
- Matrix mathematics

## 📖 Background

**Matrices** are rectangular arrays of numbers used in mathematics, graphics, physics, and machine learning.

**Basic operations:**

```
Addition (element-wise):
[1 2]   [5 6]   [6  8]
[3 4] + [7 8] = [10 12]

Multiplication (dot product):
[1 2]   [5 6]   [19 22]
[3 4] × [7 8] = [43 50]

Transpose (flip rows/columns):
[1 2 3]ᵀ   [1 4]
[4 5 6]  = [2 5]
           [3 6]
```

**Dimension rules:**

- Addition: both matrices must have same dimensions (2×3 + 2×3 = 2×3)
- Multiplication: inner dimensions must match (2×3 × 3×2 = 2×2)
- Transpose: dimensions swap (2×3 becomes 3×2)

**Why generics?**
A matrix can hold integers, floats, or any numeric type. Generic programming lets you write the code once and use it for all numeric types.

## ⚙️ Requirements

**First Pass:**

- ✅ Matrix<T> struct works
- ✅ Add two matrices (element-wise)
- ✅ Multiply two matrices (dot product)
- ✅ Transpose matrix
- ✅ Works with at least one numeric type (e.g., i32)
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Doc comments explaining operations
- ✅ **Multiple numeric types**: Works with i32, i64, f32, f64
- ✅ **Trait implementations**:
  - Add trait (use `+` operator)
  - Mul trait (use `*` operator)
  - Display trait (pretty printing)
  - Debug, Clone, PartialEq
- ✅ **Full operations**:
  - Addition, subtraction
  - Matrix multiplication
  - Scalar multiplication
  - Transpose
  - Determinant (square matrices)
  - Identity matrix, zero matrix
- ✅ **Accessors**:
  - Get/set element at (row, col)
  - Get dimensions
  - Access rows/columns
- ✅ **Error handling**:
  - Dimension mismatch errors
  - Out of bounds access
  - Operations on incompatible matrices
- ✅ **Edge cases**:
  - Empty matrices
  - 1×1 matrices
  - Non-square matrices

## 🚫 Constraints

- May use `num_traits` crate for numeric trait bounds (recommended)
- Standard library for everything else
- No external matrix libraries (you're building the library!)

## 💡 Approaches

**Storage options:**

- Nested vectors: `Vec<Vec<T>>`
- Flat vector with row-major order: `Vec<T>`
- Which is more cache-friendly?

**Generic bounds:**

- What traits does T need? (Add, Mul, Copy, Zero, One?)
- Look into `num_traits` crate for `Num` trait
- Or define your own trait bounds

**Operation strategies:**

- Addition: loop through each element
- Multiplication: triple nested loop (row × column)
- Transpose: swap indices (i,j) → (j,i)
- How to handle dimension mismatches?

**Trait implementation:**

- Implementing `Add` lets you use `matrix1 + matrix2`
- Implementing `Mul` lets you use `matrix1 * matrix2`
- What should the Output type be? (Another Matrix? Result<Matrix>?)

**Constructor patterns:**

- From nested vec
- From flat vec with dimensions
- Special constructors: identity, zero
- How to validate input dimensions?

## ✅ Validation

Basic operations:

```
Create 2×3 matrix:
[1 2 3]
[4 5 6]

Create another 2×3:
[7  8  9]
[10 11 12]

Addition:
[8  10 12]
[14 16 18]
```

Matrix multiplication:

```
A (2×3):        B (3×2):        Result (2×2):
[1 2 3]         [7  8]          [58  64]
[4 5 6]    ×    [9  10]    =    [139 154]
                [11 12]
```

Transpose:

```
Original (2×3):   Transposed (3×2):
[1 2 3]           [1 4]
[4 5 6]           [2 5]
                  [3 6]
```

Special matrices:

```
Identity 3×3:     Zero 2×3:
[1 0 0]           [0 0 0]
[0 1 0]           [0 0 0]
[0 0 1]
```

Generic types:

```
Matrix<i32> with integers
Matrix<f64> with floats
Both support same operations
```

Error cases:

```
[2×3] + [3×2]  → Error: dimension mismatch
[2×3] × [2×3]  → Error: incompatible for multiplication
get(10, 10)    → Error: out of bounds
```

Round-trip tests:

```
Original: [1 2]
          [3 4]

Transpose twice:
→ [1 3]  → [1 2]  (back to original)
  [2 4]    [3 4]
```

## 🔍 Challenge

Implement determinant calculation for square matrices, matrix inverse using Gaussian elimination, or optimize multiplication using Strassen's algorithm for large matrices.

---

**Previous:** [41_deck_cards](../41_deck_cards/README.md) | **Next:** [43_linked_list](../43_linked_list/README.md)
