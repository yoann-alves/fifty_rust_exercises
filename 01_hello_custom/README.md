# Exercise 01: Hello Custom

## 🎯 Objectives

Create a CLI program that:

- Takes a name as input
- Prints "Hello, [name]!"
- Prints "Hello, World!" if no name is provided

## 📚 Concepts

- Getting user input (CLI args, stdin, or other)
- String handling
- Control flow (handling the "no input" case)

## ⚙️ Requirements

**First Pass:**

- ✅ Works with provided input
- ✅ Works without input
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt` - code follows Rust style
- ✅ **Documented**: Function-level comment explaining what the program does
- ✅ **Edge cases handled**:
  - Empty string input → treat as "World"
  - Whitespace-only input → treat as "World"
  - Leading/trailing whitespace → trimmed
- ✅ **Error handling**: No `.unwrap()` or `.expect()` - handle errors properly
- ✅ **Variable naming**: Clear, intention-revealing names
- ✅ **Code you're proud of**: You'd show this in a code review

## 🚫 Constraints

- Standard library only
- No external crates

## 💡 Approaches

You can get input several ways:

- Command-line arguments
- Standard input
- Interactive prompt
- Or invent your own approach

**Choose the method that makes sense to you.** There's no "correct" way.

## ✅ Validation

```bash
# However you implement it, these should work:
$ cargo run
Hello, World!

$ cargo run
# (if using stdin) User types: Alice
Hello, Alice!
```

---

**Next:** [calculator_02](../calculator_02/README.md)
