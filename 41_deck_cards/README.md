# Exercise 41: Deck of Cards

## 🎯 Objectives

Create a playing card system:

- Enums for Suit and Rank
- Card and Deck structs
- Operations: shuffle, deal, sort
- Poker hand evaluation
- Generic card game foundation

## 📚 Concepts

- Enum design and matching
- Struct composition
- Randomization (shuffling)
- Sorting with custom comparators
- Pattern matching for game logic
- Combinatorics (hand evaluation)

## 📖 Background

**Standard deck:**

- 52 cards total
- 4 suits: ♠ Spades, ♥ Hearts, ♦ Diamonds, ♣ Clubs
- 13 ranks per suit: A, 2-10, J, Q, K
- Different games use different card orderings

**Poker hands** (ranked highest to lowest):

```
Royal Flush:      A♠ K♠ Q♠ J♠ 10♠
Straight Flush:   9♥ 8♥ 7♥ 6♥ 5♥
Four of a Kind:   7♠ 7♥ 7♦ 7♣ 2♠
Full House:       K♠ K♥ K♦ 3♣ 3♥
Flush:            A♦ J♦ 9♦ 6♦ 3♦
Straight:         8♠ 7♥ 6♦ 5♣ 4♠
Three of a Kind:  Q♠ Q♥ Q♦ 7♣ 2♠
Two Pair:         J♠ J♥ 4♦ 4♣ 9♠
Pair:             10♠ 10♥ K♦ 5♣ 2♠
High Card:        A♠ K♥ 8♦ 5♣ 2♠
```

**Card colors:**

- Red suits: Hearts ♥, Diamonds ♦
- Black suits: Spades ♠, Clubs ♣

## ⚙️ Requirements

**First Pass:**

- ✅ Suit enum (4 suits)
- ✅ Rank enum (13 ranks)
- ✅ Card struct combining suit and rank
- ✅ Deck struct with 52 cards
- ✅ Shuffle deck randomly
- ✅ Deal cards from deck
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Doc comments with examples
- ✅ **Enum traits**:
  - Display (show as ♠A, ♥K, ♦7, ♣2)
  - Ord (enable sorting)
  - Methods for color and value
- ✅ **Deck operations**:
  - Create new full deck
  - Shuffle using proper algorithm
  - Deal N cards
  - Deal multiple hands
  - Count remaining cards
  - Reset to full deck
  - Sort by various criteria
- ✅ **Poker evaluation**:
  - Identify hand type
  - Compare two hands
  - Find best 5-card hand from 7 cards
  - Handle tie-breaking
- ✅ **Extras**:
  - Support multiple decks
  - Optional jokers
  - Remove specific cards
  - Pretty display format

## 🚫 Constraints

- Use `rand` crate for shuffling (allowed)
- Standard library for everything else
- Proper enum and trait usage

## 💡 Approaches

**Representing cards:**

- Enums for Suit and Rank
- Struct combining both
- Derive common traits
- Implement Display for pretty output

**Shuffling algorithms:**

- Fisher-Yates shuffle
- Random swap method
- Library shuffle functions

**Deck storage:**

- Vec of Cards
- Track dealt cards
- Or remove from Vec when dealing

**Poker evaluation strategies:**

- Check each hand type from highest to lowest
- Count rank frequencies
- Check for sequences
- Check all same suit
- Combine checks for complex hands

**Sorting approaches:**

- By rank only
- By suit then rank
- Custom comparison function
- Separate comparators for different games

## ✅ Validation

Basic deck operations:

```
Create deck    → 52 cards
Shuffle        → randomized order
Deal 5 cards   → 5 cards in hand, 47 in deck
Deal 5 more    → 5 cards in hand, 42 in deck
Reset deck     → back to 52 cards
```

Card display:

```
Ace of Spades      → ♠A
King of Hearts     → ♥K
Seven of Diamonds  → ♦7
Two of Clubs       → ♣2
```

Poker hand identification:

```
♠A ♠K ♠Q ♠J ♠10        → Royal Flush
♥7 ♥7 ♦7 ♣7 ♠2         → Four of a Kind
♠K ♥K ♦K ♣3 ♥3         → Full House
♦A ♦J ♦9 ♦6 ♦3         → Flush
♠8 ♥7 ♦6 ♣5 ♠4         → Straight
♠Q ♥Q ♦Q ♣7 ♠2         → Three of a Kind
♠10 ♥10 ♦4 ♣4 ♠9       → Two Pair
♠7 ♦7 ♥K ♣2 ♠A         → Pair
♠A ♥K ♦8 ♣5 ♠2         → High Card
```

Hand comparison:

```
Full House vs Flush           → Full House wins
Straight Flush vs Four Kind   → Straight Flush wins
Two Pair vs Pair              → Two Pair wins
```

Dealing multiple players:

```
4 players, 5 cards each → 4 hands of 5 cards
Remaining in deck       → 32 cards
```

## 🔍 Challenge

Implement other card games: Blackjack (with dealer AI and betting), Go Fish (card matching), Uno (special cards and rules), or Solitaire (game logic and win detection).

---

**Previous:** [40_bank_simulator](../40_bank_simulator/README.md) | **Next:** [42_matrix](../42_matrix/README.md)
