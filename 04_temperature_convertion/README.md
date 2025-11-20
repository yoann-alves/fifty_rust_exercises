# Exercise 04: Temperature Conversion

## 🎯 Objectives

Create a temperature converter that:

- Converts between Celsius and Fahrenheit
- Takes user input for temperature and conversion direction
- Validates input (handles invalid numbers, invalid directions)

## 📚 Concepts

- User input handling
- Floating-point arithmetic
- Input validation
- Error handling and recovery

## 📖 Background

**Temperature scales** measure heat using different reference points:

**Celsius (°C):**

- Water freezes at 0°C
- Water boils at 100°C
- Used in most of the world

**Fahrenheit (°F):**

- Water freezes at 32°F
- Water boils at 212°F
- Used primarily in the United States

**The conversion formulas:**

```
Celsius to Fahrenheit:  F = C × 9/5 + 32
Fahrenheit to Celsius:  C = (F - 32) × 5/9
```

**Interesting fact:** -40°C and -40°F are the same temperature!

## ⚙️ Requirements

**First Pass:**

- ✅ Converts Celsius → Fahrenheit correctly
- ✅ Converts Fahrenheit → Celsius correctly
- ✅ Takes user input for value and direction
- ✅ Handles invalid input without crashing
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Comments explaining conversion formulas
- ✅ **Validation**:
  - Non-numeric input rejected gracefully
  - Invalid conversion direction handled
  - Edge cases work (absolute zero, extreme temps)
- ✅ **User experience**:
  - Clear prompts
  - Helpful error messages
  - Option to convert multiple values
- ✅ **Precision**: Appropriate decimal places in output
- ✅ **Clean code**: Conversion logic separated from I/O

## 🚫 Constraints

- Standard library only
- No external crates
- Must handle errors gracefully (no panics)

## 💡 Approaches

**Input formats to consider:**

- Two separate prompts: first temperature, then direction
- Single input: "32F" or "0C" parsed together
- Menu system: select conversion type, then enter value
- Command-line arguments: `program 32 F`

**Direction specification options:**

- Single letters: "C" or "F"
- Full words: "celsius", "fahrenheit"
- Numbered menu: 1 for C→F, 2 for F→C
- Arrows: "C→F" or "F→C"

**Error handling strategies:**

- Re-prompt on invalid input
- Provide example of valid input
- Show what went wrong
- Exit gracefully vs. retry loop

**Output formatting:**

- How many decimal places?
- Include units in output?
- Round or truncate?

## ✅ Validation

Test these conversions:

```
Celsius to Fahrenheit:
0°C    → 32°F
100°C  → 212°F
37°C   → 98.6°F
-40°C  → -40°F

Fahrenheit to Celsius:
32°F   → 0°C
212°F  → 100°C
98.6°F → 37°C
-40°F  → -40°C
```

Edge cases to verify:

```
Absolute zero:  -273.15°C → -459.67°F
Room temp:      20°C → 68°F
Body temp:      37°C → 98.6°F
```

Invalid inputs should be handled:

```
Input: "abc"       → Error: not a number
Input: "32X"       → Error: invalid direction
Input: ""          → Error: no input provided
```

## 🔍 Challenge

Add Kelvin scale support (K = C + 273.15), or allow conversions in a single direction multiple times without restarting the program.

---

**Previous:** [03_fizzbuzz](../03_fizzbuzz/README.md) | **Next:** [05_fibonacci](../05_fibonacci/README.md)
