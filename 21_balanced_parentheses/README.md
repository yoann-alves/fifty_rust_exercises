# Exercise 21: Balanced Parentheses

## 🎯 Objectives

Check if parentheses/brackets/braces are balanced:

- Support three types: `()`, `{}`, `[]`
- Verify correct nesting and closing order
- Return whether the string is balanced

## 📚 Concepts

- Stack data structure (LIFO - Last In First Out)
- Using Vec as stack (push/pop)
- Matching pairs algorithm
- String iteration and character checking

## 📖 Background

**Balanced brackets** means every opening bracket has a matching closing bracket in the correct order:

```
Valid examples:
  ()              Simple pair
  ()[]{}          Multiple pairs
  {[()]}          Nested properly
  ((()))          Deep nesting

Invalid examples:
  (]              Wrong bracket type
  ([)]            Wrong order (crossing)
  (((             Never closed
  )))             Never opened
  }{              Closed before opened
```

**The stack approach:**
When you see an opening bracket, remember it. When you see a closing bracket, it must match the most recent opening bracket you haven't closed yet. This "most recent unclosed" behavior is exactly what a stack gives you.

## ⚙️ Requirements

**First Pass:**

- ✅ Checks all three bracket types: `()`, `{}`, `[]`
- ✅ Returns true for balanced, false for unbalanced
- ✅ Handles basic nesting patterns
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain the algorithm approach
- ✅ **Complex patterns**:
  - Deep nesting: `{{{{()}}}}`
  - Mixed types: `{[()]}`
  - Multiple sequences: `(){}[]`
- ✅ **Edge cases**:
  - Empty string (is this balanced? decide and document)
  - Only opening brackets
  - Only closing brackets
  - Mismatched types: `(]`, `{)`
  - Uneven counts: `())`, `(()`
- ✅ **String handling**:
  - Decide: ignore non-bracket characters or reject them?
  - Document your choice
- ✅ **Clear interface**: Easy to understand what true/false means

## 🚫 Constraints

- Standard library only
- Use Vec as your stack (no external stack crate)
- Must implement the algorithm yourself

## 💡 Approaches

**Stack-based algorithm idea:**

- Walk through the string character by character
- Opening bracket: remember it somehow
- Closing bracket: check if it matches the last opening
- At the end: have you closed everything?

**Matching strategy options:**

- Match expressions to pair brackets
- HashMap to store pairs
- Simple if/else chains
- Helper function to check if two brackets match

**Non-bracket characters:**

- Ignore them: `"if (x == 3) { }"` would be valid
- Reject them: only pure bracket strings allowed
- Your choice, just be consistent

**Stack with Vec:**
Vec has the operations you need. Think about what operations a stack needs.

## ✅ Validation

Valid (balanced) strings:

```
"()"           → true
"()[]{}"       → true
"{[()]}"       → true
"((()))"       → true
""             → true (probably)
"{[({[()]})]}" → true
```

Invalid (unbalanced) strings:

```
"(]"           → false (wrong type)
"([)]"         → false (wrong order)
"((("          → false (not closed)
")))"          → false (not opened)
"{[}"          → false (incomplete)
"}"            → false (only closing)
"([{}])"       → ... wait, is this valid? Test it!
```

With other characters (if you support them):

```
"if (x[0] == 3) { return; }"  → true
"func(a, b[i])"               → true
```

## 🔍 Challenge

Make your checker report exactly WHERE and WHAT is wrong:

```
"({[}])"  → "Mismatched bracket at position 3: expected ']' but found '}'"
"((())"   → "Unclosed bracket '(' at position 0"
"())"     → "Unexpected closing bracket ')' at position 2"
```

---

**Previous:** [20_merge_sorted](../20_merge_sorted/README.md) | **Next:** [22_roman_numerals](../22_roman_numerals/README.md)
