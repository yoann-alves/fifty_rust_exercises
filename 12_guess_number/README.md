# Exercise 12: Guess the Number

## 🎯 Objectives

Create a number guessing game where:

- Computer picks a secret random number
- Player tries to guess it
- Program gives hints ("too high" / "too low")
- Game ends when player guesses correctly

## 📚 Concepts

- Random number generation
- Loop control (game loop)
- User input handling
- Comparison logic
- Input validation

## 📖 Background

**The guessing game** is a classic programming exercise that teaches interactive programming.

**How it works:**

```
Computer picks: 42 (secret)
Player guesses: 50 → "Too high!"
Player guesses: 30 → "Too low!"
Player guesses: 40 → "Too low!"
Player guesses: 42 → "Correct! You win!"
```

**Game flow:**

1. Generate random number in a range (e.g., 1-100)
2. Loop: get guess, compare, give feedback
3. Exit loop when guess matches secret
4. Show results (attempts, congratulations)

**This teaches:**

- Managing game state
- Interactive loops
- User feedback
- Input validation

## ⚙️ Requirements

**First Pass:**

- ✅ Generates random number in range
- ✅ Accepts player guesses
- ✅ Gives "too high" or "too low" hints
- ✅ Ends game on correct guess
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Code comments explaining game flow
- ✅ **Enhanced features**:
  - Track number of attempts
  - Show attempt count when player wins
  - Play again option
  - Configurable difficulty (range size)
- ✅ **Input validation**:
  - Handle non-numeric input gracefully
  - Handle out-of-range guesses
  - Invalid inputs don't count as attempts
  - Clear error messages
- ✅ **User experience**:
  - Welcome message with rules
  - Clear prompts for input
  - Congratulations message with stats
- ✅ **Edge cases**:
  - First guess is correct
  - Many attempts needed
  - Repeated same guess

## 🚫 Constraints

- Use `rand` crate for random number generation
- Standard library for I/O
- Must be interactive (not CLI arguments)

## 💡 Approaches

**Game structure:**

- One-time setup: generate secret number
- Loop: get input → validate → compare → feedback
- Exit: when guess equals secret

**Random number generation:**

- Pick range (1-100 is common)
- Generate once at start
- Keep secret until end

**Difficulty levels:**

- Easy: smaller range (1-50)
- Medium: standard range (1-100)
- Hard: larger range (1-1000)
- Let player choose before game starts

**Tracking attempts:**

- Counter variable
- Increment on each valid guess
- Display at end

**Input validation:**

- Read line from stdin
- Try to parse as number
- Check if in valid range
- Loop again if invalid (don't count as attempt)

**Enhancement ideas:**

- Limited attempts mode (game over if exceeded)
- Hints (narrow the range)
- Score system (fewer attempts = better score)
- Difficulty adjustment (range changes with performance)

## ✅ Validation

Example gameplay session:

```
Welcome to Guess the Number!
I'm thinking of a number between 1 and 100.

Your guess: 50
Too low! Try again.

Your guess: 75
Too high! Try again.

Your guess: 60
Too low! Try again.

Your guess: 68
Correct! You got it in 4 attempts!

Play again? (y/n):
```

Test scenarios to verify:

```
Guess = 42 on first try → Win in 1 attempt
Binary search (1-100)   → Should win in ~6-7 attempts
Input "abc"             → Error, doesn't count as attempt
Input "150" (out of range) → Error, doesn't count
```

Invalid input handling:

```
Your guess: hello
Invalid input! Please enter a number.

Your guess: 150
Out of range! Please guess between 1 and 100.

Your guess: 50
Too high! Try again.
```

## 🔍 Challenge

Add a "hard mode" where the program doesn't tell you if your guess is too high or too low - only if it's correct or wrong. Or implement a two-player mode where one person picks the number and the other guesses.

---

**Previous:** [11_caesar_cipher](../11_caesar_cipher/README.md) | **Next:** [13_ascii_art](../13_ascii_art/README.md)
