# Exercise 01: Hello Custom

## 🎯 Objectives

Create a CLI program that:

- Takes a name as input
- Prints "Hello, [name]!"
- Prints "Hello, World!" if no name is provided

## 📚 Concepts

- Getting user input
- String handling
- Control flow (handling the "no input" case)

## 📖 Background

**Command-line programs** are the foundation of system tools. They take input, process it, and produce output.

**The classic "Hello World"** is usually static, but real programs need to be dynamic:

```
Static:   Always prints "Hello, World!"
Dynamic:  Prints "Hello, Alice!" when given a name
```

**Input methods vary:**

- Some programs read from arguments: `program Alice`
- Some read from stdin: user types when prompted
- Some use configuration files
- Some combine multiple methods

Your job: make the program greet someone by name, or use a default greeting.

## ⚙️ Requirements

**First Pass:**

- ✅ Greets with provided name
- ✅ Greets with "World" when no name given
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Brief comment explaining the program
- ✅ **Edge cases**:
  - Empty string → treat as "World"
  - Only whitespace → treat as "World"
  - Extra whitespace → trimmed away
- ✅ **Error handling**: Handle errors properly (no `.unwrap()` or `.expect()`)
- ✅ **Clean code**: Clear variable names, readable logic

## 🚫 Constraints

- Standard library only
- No external crates

## 💡 Approaches

**Input sources to consider:**

- Command-line arguments
- Standard input (keyboard)
- Interactive prompt
- Environment variables
- Configuration file
- Hard-coded default

**String handling:**

- Trimming whitespace
- Checking for empty strings
- Formatting output

**Error scenarios:**

- What if input fails?
- What if nothing is provided?
- What if user provides multiple inputs?

Pick whatever approach makes sense for your design.

## ✅ Validation

Your program should produce these results:

```bash
# With no input
$ cargo run
Hello, World!

# With a name (exact method depends on your implementation)
$ cargo run
Alice
Hello, Alice!

# Empty or whitespace should default to World
$ cargo run

Hello, World!
```

Edge cases to verify:

```
Input: "Alice"      → "Hello, Alice!"
Input: "  Bob  "    → "Hello, Bob!"
Input: ""           → "Hello, World!"
Input: "   "        → "Hello, World!"
```

## 🔍 Challenge

Add support for greeting multiple people at once:

```
Input: Alice Bob Carol
Output: Hello, Alice, Bob, and Carol!
```

Or implement greeting in different languages based on a flag.

---

**Next:** [02_calculator](../02_calculator/README.md)
