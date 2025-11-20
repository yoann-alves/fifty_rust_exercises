# Exercise 14: Unit Converter

## 🎯 Objectives

Create a unit converter that:

- Converts between different units (length, weight, temperature)
- Provides an interactive menu system
- Validates all user input
- Supports multiple conversion categories

## 📚 Concepts

- Menu-driven program flow
- Conversion formulas and calculations
- Input validation and error handling
- Program state management
- Enum usage for categories and units

## 📖 Background

**Unit conversion** is fundamental in science, engineering, cooking, and international communication. Different regions use different measurement systems:

```
United States:    Miles, pounds, Fahrenheit
Most of world:    Kilometers, kilograms, Celsius
Science:          Meters, kilograms, Kelvin
```

**Conversion approaches:**

- Direct formulas: `miles = kilometers × 0.621371`
- Via base unit: `feet → meters → kilometers`
- Temperature: Special formulas since they're not proportional

**Common conversions:**

```
Length:
  1 meter = 3.28084 feet
  1 kilometer = 0.621371 miles
  1 inch = 2.54 centimeters

Weight:
  1 kilogram = 2.20462 pounds
  1 pound = 16 ounces
  1 ounce = 28.3495 grams

Temperature:
  Celsius to Fahrenheit: (C × 9/5) + 32
  Fahrenheit to Celsius: (F - 32) × 5/9
  Celsius to Kelvin: C + 273.15
```

## ⚙️ Requirements

**First Pass:**

- ✅ At least 3 categories (length, weight, temperature)
- ✅ At least 3 units per category
- ✅ Interactive menu for selection
- ✅ Performs conversions correctly
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Document conversion formulas used
- ✅ **Categories**:
  - Length (meter, kilometer, mile, foot, inch, etc.)
  - Weight (kilogram, gram, pound, ounce, etc.)
  - Temperature (Celsius, Fahrenheit, Kelvin)
  - Optional: Volume, speed, area, time, etc.
- ✅ **Input validation**:
  - Invalid menu choices handled gracefully
  - Non-numeric values rejected
  - Out-of-range values (e.g., negative Kelvin below absolute zero)
  - Edge cases (zero, very large numbers)
- ✅ **User experience**:
  - Clear menu structure
  - Easy navigation between categories
  - Option to perform multiple conversions
  - Clean exit option
- ✅ **Code organization**:
  - Well-structured functions
  - Appropriate use of enums
  - Clear conversion logic
- ✅ **Display**: Show results with appropriate precision (decimal places)

## 🚫 Constraints

- Standard library only
- No external crates
- Must be interactive (not just one-shot)
- Must validate all user input

## 💡 Approaches

**Menu structures to consider:**

- Two-level menu (pick category, then pick conversion)
- Flat menu (all conversions at once)
- Code-based (type "LM" for length-miles)
- Natural language ("convert 10 meters to feet")

**Conversion strategies:**

- Direct formulas for each pair
- Hub-and-spoke: convert everything to/from a base unit
- Conversion factor tables
- Chain conversions (A→B→C if no direct A→C)

**Data organization:**

- Enums for categories and units
- Structs to hold conversion state
- Functions per category vs generic converter
- Match expressions vs lookup tables

**Error handling philosophy:**

- Crash on invalid input?
- Loop until valid?
- Provide defaults?
- Show helpful error messages?

## ✅ Validation

Example interaction:

```
=== Unit Converter ===
1. Length
2. Weight
3. Temperature
4. Exit

Choose category: 1

=== Length Conversion ===
Available units: meters, kilometers, miles, feet, inches

From unit: meters
To unit: feet
Enter value: 10

10 meters = 32.81 feet

Convert again? (y/n): y

From unit: kilometers
To unit: miles
Enter value: 5

5 kilometers = 3.11 miles

Convert again? (y/n): n
```

Test conversions:

```
10 meters = 32.8084 feet ✓
5 kilometers = 3.10686 miles ✓
100°C = 212°F ✓
0°C = 273.15 Kelvin ✓
1 kg = 2.20462 pounds ✓
16 ounces = 1 pound ✓
```

Invalid input handling:

```
Choose category: 99
Invalid choice. Please try again.

Enter value: abc
Invalid number. Please enter a numeric value.

Enter temperature in Kelvin: -300
Error: Temperature below absolute zero (-273.15°C)
```

## 🔍 Challenge

Add support for compound units (like miles per hour to kilometers per hour), or implement a unit parser that understands expressions like "5ft 10in to cm".

---

**Previous:** [13_ascii_art](../13_ascii_art/README.md) | **Next:** [15_stopwatch](../15_stopwatch/README.md)
