# Exercise 37: Contact Manager

## 🎯 Objectives

Create a contact management system:

- Store contacts with name, email, phone
- CRUD operations (Create, Read, Update, Delete)
- Save and load from JSON file
- Search and filter contacts
- Data persistence between program runs

## 📚 Concepts

- Struct design with multiple fields
- CRUD pattern implementation
- JSON serialization/deserialization
- File I/O for persistence
- Data validation
- Collection manipulation

## 📖 Background

**Contact managers** are everywhere - phones, email clients, CRM systems. They all share the same core operations:

**CRUD pattern** (fundamental to database applications):

```
Create: Add new contact
Read:   View one or all contacts
Update: Modify existing contact
Delete: Remove contact
```

**Persistence** means data survives program restarts:

```
Without persistence:  Close program → data lost
With persistence:     Close program → data saved to disk → reopen → data restored
```

**JSON** is a human-readable text format for storing structured data:

```json
{
  "name": "Alice",
  "email": "alice@example.com",
  "phone": "555-1234"
}
```

Your job: build a system that manages contacts and remembers them between sessions.

## ⚙️ Requirements

**First Pass:**

- ✅ Store contacts (name, email, phone minimum)
- ✅ Add new contact
- ✅ List all contacts
- ✅ Delete contact
- ✅ Save to JSON file
- ✅ Load from JSON file
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Doc comments on public functions
- ✅ **Complete CRUD**:
  - Create with validation
  - Read individual contact by ID
  - Update existing contact fields
  - Delete by ID or name
- ✅ **Search capabilities**:
  - Find by name (partial match)
  - Find by email
  - Find by phone number
  - List by filters
- ✅ **Validation**:
  - Email format check
  - Phone format check
  - Required fields enforced
  - Duplicate detection
- ✅ **Robust persistence**:
  - Auto-save after changes
  - Handle corrupted JSON gracefully
  - Create backup files
- ✅ **Error handling**:
  - Invalid input
  - File I/O errors
  - JSON parse errors
  - Contact not found

## 🚫 Constraints

- Use `serde` and `serde_json` crates for JSON (allowed)
- Standard library for file operations
- Proper error handling with Result types

## 💡 Approaches

**Data structures to consider:**

- Contact struct: what fields?
- Manager struct: how to store contacts? Vec? HashMap?
- ID system: auto-incrementing? UUID?

**Storage strategies:**

- Where to save the file?
- When to save? (after every change? on exit? both?)
- How to handle missing file on first run?

**Search methods:**

- Linear search through Vec
- HashMap for fast lookups
- Filter iterators
- Case-insensitive matching

**Validation approaches:**

- Check email has @ and .
- Count digits in phone number
- Reject empty names
- Prevent duplicate emails

**Error scenarios:**

- What if file doesn't exist yet?
- What if JSON is malformed?
- What if disk is full?
- What if contact ID doesn't exist?

## ✅ Validation

Basic operations should work:

```
# Create contacts
Add "Alice Smith" alice@example.com 555-1234
→ Contact added with ID 1

Add "Bob Jones" bob@example.com 555-5678
→ Contact added with ID 2

# Read contacts
List all
→ 1: Alice Smith (alice@example.com, 555-1234)
→ 2: Bob Jones (bob@example.com, 555-5678)

Get 1
→ Alice Smith (alice@example.com, 555-1234)

# Update contact
Update 1 phone 555-9999
→ Contact 1 updated

# Delete contact
Delete 2
→ Contact 2 deleted

List all
→ 1: Alice Smith (alice@example.com, 555-9999)
```

Search functionality:

```
Search name "alice"
→ Found: Alice Smith

Search email "@example.com"
→ Found: Alice Smith

Search phone "555"
→ Found: Alice Smith
```

Persistence test:

```
# First run
Add "Alice" alice@example.com 555-1234
Exit program

# Second run (restart program)
List all
→ 1: Alice (alice@example.com, 555-1234)  ✓ Data persisted!
```

Validation errors:

```
Add "Bob" "notanemail" 555-1234
→ Error: Invalid email format

Add "" bob@example.com 555-1234
→ Error: Name cannot be empty

Update 999 phone 555-0000
→ Error: Contact not found
```

JSON file format (example):

```json
[
  {
    "id": 1,
    "name": "Alice Smith",
    "email": "alice@example.com",
    "phone": "555-1234"
  }
]
```

## 🔍 Challenge

Add vCard import/export format, implement fuzzy name matching for duplicate detection (e.g., "John Smith" vs "J. Smith"), or add contact groups/categories with tagging system.

---

**Previous:** [36_library](../36_library/README.md) | **Next:** [38_todo_advanced](../38_todo_advanced/README.md)
