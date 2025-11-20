# 🦀 Fifty Rust Exercises

A structured journey through Rust fundamentals - from zero to maybe competent.

## 📖 Purpose

50 hands-on exercises designed to build solid Rust foundations through deliberate practice.
Based on "The Rust Programming Language" (The Book) with emphasis on:

- Writing code from scratch (no copy-paste)
- Understanding every line
- Testing rigorously
- Building muscle memory

## 🎯 Rules

1. **TYPE everything** - Never copy-paste, even from your own code
2. **UNDERSTAND every line** - If you don't know why, STOP and research
3. **READ error messages** - The Rust compiler is your best teacher
4. **TEST your code** - Normal case, edge cases, error cases
5. **No external dependencies** - stdlib only (unless explicitly allowed)

## 🗂️ Structure

Each exercise is a **Cargo workspace** with two independent projects:

```
exercises/
├── 01_hello_custom/              # Level 1: Basic Syntax (1-15)
│   ├── Cargo.toml                # Workspace definition
│   ├── README.md                 # Exercise instructions
│   ├── pass1/                    # First pass: Make it work
│   │   ├── Cargo.toml
│   │   └── src/main.rs
│   └── pass2/                    # Second pass: Make it excellent
│       ├── Cargo.toml
│       └── src/main.rs
├── 02_calculator/
├── ...
├── 16_anagram_finder/            # Level 2: Collections (16-25)
├── ...
├── 26_file_reader/               # Level 3: Files & Errors (26-35)
├── ...
├── 36_library/                   # Level 4: Structs & Traits (36-45)
├── ...
└── 46_concurrent_downloader/     # Level 5: Concurrency (46-50)
```

## 🚀 Getting Started

1. **Prerequisites**: Rust installed (`rustup`)

2. **Clone this repo**:

```bash
git clone https://github.com/yoann-alves/fifty_rust_exercises.git
cd fifty_rust_exercises
```

3. **Start with exercise 1 - First pass**:

```bash
cd exercises/01_hello_custom/pass1
cargo run
```

4. **Read the exercise README** before coding
5. **Implement, test, iterate**
6. **When ready, move to second pass**:

```bash
cd ../pass2
# Refactor and improve for production quality
cargo run
cargo clippy
cargo fmt
```

7. **Move to next exercise**

## 📚 Resources

- [The Rust Book](https://doc.rust-lang.org/book/)
- [Rust By Example](https://doc.rust-lang.org/rust-by-example/)
- [Rust Standard Library](https://doc.rust-lang.org/std/)

See [docs/RESOURCES.md](docs/RESOURCES.md) for more.

## 🎓 Learning Path

**Recommended approach:**

1. Read "The Rust Book" completely (code the examples)
2. Do all 50 exercises (first pass - make it work)
3. Re-read "The Rust Book" (with experience)
4. Redo all 50 exercises (second pass - make it excellent)

## 🤝 Contributing

This is a personal learning journey, but suggestions for exercise improvements are welcome!

## 📜 License

MIT License - Feel free to use, modify, share.

---

**Remember**: Excellence absolute. No compromises. Ever.
