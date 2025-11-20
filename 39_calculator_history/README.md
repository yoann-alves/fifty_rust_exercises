# Exercise 39: Calculator with History

## 🎯 Objectives

Create a stack-based calculator with history:

- Evaluate expressions in Reverse Polish Notation (RPN)
- Maintain complete operation history
- Implement undo and redo functionality
- Support stack manipulation commands
- Optional: Save/load history to file

## 📚 Concepts

- Stack data structure
- Reverse Polish Notation (postfix notation)
- Command pattern for undo/redo
- State management
- Expression evaluation

## 📖 Background

**Reverse Polish Notation (RPN)** is a mathematical notation where operators come after operands. It eliminates the need for parentheses and follows the natural evaluation order of a stack.

**How RPN works:**

```
Traditional (Infix):  3 + 4
RPN (Postfix):        3 4 +

Traditional:  (3 + 4) × 5
RPN:          3 4 + 5 ×

Traditional:  3 + 4 × 5
RPN:          3 4 5 × +
```

**Stack evaluation process:**

1. Numbers get pushed onto the stack
2. Operators pop operands, compute, push result
3. Final stack top is the answer

Example: `3 4 + 5 ×`

```
Step 1: Push 3        Stack: [3]
Step 2: Push 4        Stack: [3, 4]
Step 3: Add           Stack: [7]      (pop 4 and 3, push 3+4)
Step 4: Push 5        Stack: [7, 5]
Step 5: Multiply      Stack: [35]     (pop 5 and 7, push 7×5)
```

**Why RPN is useful:**

- No operator precedence ambiguity
- No parentheses needed
- Natural for calculators (HP calculators use it)
- Easy to evaluate with a stack
- History is naturally a sequence of operations

## ⚙️ Requirements

**First Pass:**

- ✅ Evaluates RPN expressions
- ✅ Basic operations: +, -, ×, ÷
- ✅ Keeps history of operations
- ✅ Undo last operation
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain RPN concept and how the calculator works
- ✅ **Extended operations**:
  - Arithmetic: +, -, ×, ÷, % (modulo)
  - Advanced math: ^ (power), sqrt, abs, sin, cos, log
  - Stack manipulation: dup, swap, drop, clear, roll
  - Constants: pi, e
- ✅ **Complete history**:
  - Record every operation with timestamp
  - Display full history
  - Clear history
  - Optional: Save/load history to file
- ✅ **Undo/Redo system**:
  - Undo multiple operations
  - Redo undone operations
  - Show how many undo/redo available
  - Preserve redo stack until new operation
- ✅ **Interactive mode**:
  - REPL interface (read-eval-print loop)
  - Help command listing all operations
  - Pretty-print stack state
  - Exit/quit command
- ✅ **Error handling**:
  - Stack underflow (not enough operands)
  - Division by zero
  - Invalid operations/syntax
  - Invalid numbers
  - Can't undo when history empty

## 🚫 Constraints

- Standard library only
- No external calculator crates
- Implement your own stack (Vec is fine)
- Proper error handling (no panics on user input)

## 💡 Approaches

**Stack management:**

- Use a Vec as your stack
- Track stack state for undo
- Consider: separate struct for calculator state

**RPN evaluation strategies:**

- Parse input into tokens
- Process each token: number → push, operator → pop-compute-push
- Handle whitespace and multi-digit numbers

**History tracking options:**

- Store list of operations
- Store full calculator states (snapshots)
- Store both for flexibility

**Undo/Redo mechanism:**

- Save state before each operation
- Keep undo stack of previous states
- Keep redo stack when undoing
- Clear redo stack on new operation

**Interactive mode:**

- Loop reading user input
- Parse and execute commands
- Display results after each operation
- Handle special commands (help, quit, history, etc.)

**Command types to support:**

- Numbers (push to stack)
- Binary operators (pop 2, push 1)
- Unary operators (pop 1, push 1)
- Stack operations (manipulate without math)
- Meta commands (undo, redo, help, etc.)

## ✅ Validation

**Basic RPN evaluation:**

```
> 3 4 +
Stack: [7.0]

> 5 ×
Stack: [35.0]

> 2 ÷
Stack: [17.5]
```

**Complex expression:**

```
> 3 4 + 2 × 7 ÷
Stack: [2.0]

Breakdown:
  3 4 +   → 7
  7 2 ×   → 14
  14 7 ÷  → 2
```

**Stack operations:**

```
> 5
Stack: [5.0]

> dup
Stack: [5.0, 5.0]

> ×
Stack: [25.0]

> sqrt
Stack: [5.0]
```

**History display:**

```
> history
1. push 3
2. push 4
3. add → 7.0
4. push 2
5. multiply → 14.0
6. push 7
7. divide → 2.0
```

**Undo and Redo:**

```
> 3 4 +
Stack: [7.0]

> 5 ×
Stack: [35.0]

> undo
Stack: [7.0]
(Undone: multiply)

> undo
Stack: [3.0, 4.0]
(Undone: add)

> redo
Stack: [7.0]
(Redone: add)

> redo
Stack: [35.0]
(Redone: multiply)
```

**Error handling:**

```
> 5 +
Error: Stack underflow (need 2 operands, have 1)

> 5 0 ÷
Error: Division by zero

> xyz
Error: Invalid number: 'xyz'

> undo
Error: Nothing to undo

> 1 2 3 sqrt
Error: sqrt requires exactly 1 operand
```

**Interactive session:**

```
RPN Calculator
Type 'help' for commands, 'quit' to exit

> 10 5 + 3 ×
Stack: [45.0]

> stack
Stack (1 item):
  0: 45.0

> clear
Stack: []

> 3.14159 2 ^
Stack: [9.8696]

> help
Available operations:
  Arithmetic: +, -, ×, ÷, %
  Advanced: ^, sqrt, abs
  Stack: dup, swap, drop, clear
  Constants: pi, e
  History: undo, redo, history
  Other: help, quit

> quit
Goodbye!
```

**Advanced operations:**

```
> 2 8 ^
Stack: [256.0]

> sqrt
Stack: [16.0]

> pi
Stack: [16.0, 3.14159]

> ×
Stack: [50.265]

> swap
Stack: [3.14159, 50.265]
```

## 🔍 Challenge

Implement variable storage (like HP calculator's STO/RCL commands), add support for complex numbers, or create a converter that translates between infix notation and RPN with proper parentheses handling.

---

**Previous:** [38_todo_advanced](../38_todo_advanced/README.md) | **Next:** [40_bank_simulator](../40_bank_simulator/README.md)
