# Exercise 36: Library Management System

## 🎯 Objectives

Create a library management system with:

- Structs for Book, Author, and Library
- Methods for add, remove, and search operations
- Implement Display and Debug traits
- Manage collections of books and authors

## 📚 Concepts

- Struct definition and methods
- Trait implementation (Display, Debug)
- Ownership and borrowing
- Collections (Vec, HashMap)
- Option and Result types

## 📖 Background

**Libraries manage books** with various operations:

```
Add:    Library receives new book → stored in collection
Search: User looks for "Rust" → returns matching books
Remove: Book leaves library → removed from collection
```

**Data relationships:**

- A Library contains many Books
- A Book has one Author (or could have multiple)
- An Author can write many Books

**Rust's approach to OOP:**

- Structs hold data
- `impl` blocks add methods
- Traits define shared behavior
- No inheritance—use composition instead

**Example library operations:**

```
"Add 'The Rust Book' by Steve Klabnik, ISBN 978-1593278281"
"Find all books about Rust"
"Remove book with ISBN 978-1593278281"
"How many books do we have?"
```

## ⚙️ Requirements

**First Pass:**

- ✅ Book struct with fields (title, author, ISBN, year)
- ✅ Author struct with fields (name, birth year)
- ✅ Library struct managing books
- ✅ Methods: add_book, remove_book, find_book
- ✅ Basic functionality works
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Doc comments on all public items
- ✅ **Trait implementations**:
  - Display for Book (human-readable format)
  - Display for Author
  - Display for Library (summary)
  - Debug for all structs
  - PartialEq for comparisons
  - Clone where appropriate
- ✅ **Search capabilities**:
  - Search by title (partial match)
  - Search by author name
  - Search by ISBN (exact match)
  - Search by year range
  - List all books
  - List books by specific author
- ✅ **Error handling**:
  - Return Result for operations that can fail
  - Handle duplicates (same ISBN)
  - Handle not found cases
  - Validate input (empty titles, invalid ISBNs, etc.)
- ✅ **Optional features**:
  - Borrow/return book tracking
  - Book availability status
  - Total books count
  - Books by genre/category
  - Book ratings
  - Sorting (by title, author, year)

## 🚫 Constraints

- Standard library only
- No external crates
- Use appropriate collection types (Vec, HashMap, etc.)
- Implement at least Display and Debug traits

## 💡 Approaches

**Struct design considerations:**

- What fields does a Book need?
- Should Author be a separate struct or just a String?
- How should Library store books? Vec? HashMap?
- What makes a good unique identifier for books?

**Collection choices:**

- Vec: Simple, ordered, good for iteration
- HashMap: Fast lookup by key (ISBN?)
- Both: Vec for ordering, HashMap for fast lookup?

**Search strategies:**

- Linear search through Vec
- Filter and collect matching items
- HashMap lookup for exact matches
- String contains for partial matches

**Trait implementation:**

- Display: How should a book appear when printed?
- Debug: What info is useful for debugging?
- PartialEq: When are two books considered equal?

**Method design:**

- Should add_book return success/failure?
- Should remove_book return the removed book?
- Should search return references or owned values?

## ✅ Validation

Your library should handle these scenarios:

```
Creating a library:
Library::new("City Library") → empty library with name

Adding books:
add_book(Book { title: "The Rust Book", isbn: "978-1593278281", ... })
→ Book added successfully

Searching:
find_by_title("Rust") → returns all books with "Rust" in title
find_by_isbn("978-1593278281") → returns that specific book
find_by_author("Klabnik") → returns all books by that author

Removing:
remove_book("978-1593278281") → returns the removed book
remove_book("invalid-isbn") → returns None or error

Display:
println!("{}", book) → "The Rust Book by Steve Klabnik (2018)"
println!("{}", library) → "City Library: 15 books"
```

Edge cases to handle:

```
Empty library → searches return empty results
Duplicate ISBN → error or replace?
Empty title → invalid, return error
Book not found → None or error
Multiple books with same title → all returned in search
```

Example workflow:

```
1. Create library
2. Add "The Rust Book" (2018)
3. Add "Programming Rust" (2017)
4. Search for "Rust" → finds both
5. Search for author "Klabnik" → finds one
6. Remove by ISBN → book removed
7. Search again → only one found
```

## 🔍 Challenge

Add persistence by saving/loading the library to/from JSON or a binary format. Then implement a borrowing system that tracks who has which book, due dates, and calculates late fees.

---

**Previous:** [35_text_merger](../35_text_merger/README.md) | **Next:** [37_contacts](../37_contacts/README.md)
