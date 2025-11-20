# Exercise 40: Bank Account Simulator

## 🎯 Objectives

Create a bank account simulation system:

- Account struct with balance tracking
- Operations: deposit, withdraw, transfer
- Transaction history with timestamps
- Validation and business rules
- Multiple account management

## 📚 Concepts

- Struct design for financial data
- Transaction modeling
- State validation
- Decimal precision (financial calculations)
- Audit trail (transaction history)
- Error handling for business rules

## 📖 Background

**Banking systems** need to track money movements with precision and accountability.

**Core banking operations:**

```
Deposit:   Add money to account
Withdraw:  Remove money from account
Transfer:  Move money between accounts
```

**Critical requirements:**

- **Atomicity**: Transfers must be all-or-nothing (both accounts update or neither does)
- **Audit trail**: Every transaction recorded with timestamp
- **Validation**: No negative balances, no invalid amounts
- **Precision**: Money calculations need exact decimal arithmetic (not floating point errors)

**Transaction history** provides accountability:

```
Account 12345 - Transaction History
─────────────────────────────────────
Jan 15 10:00  Deposit        +$1,000.00  Balance: $1,000.00
Jan 15 10:05  Withdrawal     -$250.00    Balance: $750.00
Jan 15 10:10  Transfer In    +$500.00    Balance: $1,250.00
Jan 15 10:15  Deposit        +$200.00    Balance: $1,450.00
```

**Business rules** protect accounts:

- Can't withdraw more than balance (overdraft prevention)
- Can't transfer to same account
- Can't operate on frozen/closed accounts
- All amounts must be positive

## ⚙️ Requirements

**First Pass:**

- ✅ Account struct with balance
- ✅ Deposit increases balance
- ✅ Withdraw decreases balance
- ✅ Transfer moves money between accounts
- ✅ No negative balances allowed
- ✅ Transaction history recorded
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Doc comments on public items
- ✅ **Rich Account model**:
  - Account number (unique identifier)
  - Account holder name
  - Balance (consider decimal precision)
  - Account type (Checking, Savings, etc.)
  - Creation date
  - Status (Active, Frozen, Closed)
- ✅ **Transaction tracking**:
  - Transaction ID
  - Type (Deposit, Withdrawal, Transfer)
  - Amount
  - Timestamp
  - Description/memo
  - Source/destination for transfers
  - Resulting balance after transaction
- ✅ **Business rules enforced**:
  - No negative balances
  - Minimum balance requirements (optional)
  - Daily withdrawal limits (optional)
  - Transfer limits (optional)
  - Account status validation
- ✅ **Complete operations**:
  - Create account
  - Deposit with validation
  - Withdraw with sufficient funds check
  - Atomic transfer (both succeed or both fail)
  - Get current balance
  - View transaction history
  - Close account
- ✅ **History features**:
  - Filter by date range
  - Filter by transaction type
  - Calculate totals (deposits, withdrawals)
  - Generate monthly statements
- ✅ **Multi-account system**:
  - Bank struct managing multiple accounts
  - Find account by number
  - List all accounts
  - Generate summaries
- ✅ **Error handling**:
  - Insufficient funds
  - Invalid amounts (negative, zero)
  - Account not found
  - Account frozen/closed
  - Transfer to same account

## 🚫 Constraints

- Standard library only (or `rust_decimal`/`bigdecimal` for precision)
- Proper error handling with Result
- Transfers must be atomic
- Transaction history must be immutable (append-only)

## 💡 Approaches

**Account representation:**

- Struct with fields for number, holder, balance, type, status
- Vec or HashMap for transaction history
- Enums for account type and status

**Balance precision:**

- f64 is risky (floating point errors: 0.1 + 0.2 ≠ 0.3)
- Consider `rust_decimal` crate for exact decimal math
- Or work in cents (integers) and convert for display
- Always round to 2 decimal places for display

**Transaction history:**

- Append-only (never modify past transactions)
- Each transaction knows resulting balance
- Store chronologically
- Include enough context to reconstruct account state

**Transfer atomicity:**

- Check if source has funds BEFORE modifying anything
- Withdraw from source first
- If deposit fails, rollback (or use two-phase approach)
- Both accounts update or neither does

**Error handling:**

- Return Result from all operations
- Custom error types for different failure reasons
- Don't panic on business rule violations

**Multi-account management:**

- HashMap for fast lookups by account number
- Generate unique account numbers
- Bank struct owns all accounts

## ✅ Validation

Basic operations:

```
Create account for Alice
Deposit $1,000 → Balance: $1,000
Withdraw $250  → Balance: $750
Withdraw $1,000 → Error: Insufficient funds (need $1,000, have $750)
```

Transfer between accounts:

```
Alice starts with $1,000
Bob starts with $0

Transfer $300 from Alice to Bob
Alice now has $700
Bob now has $300

Try transfer $1,000 from Alice to Bob
Error: Insufficient funds
Both balances unchanged (atomic failure)
```

Transaction history:

```
Account: ACC-001 (Alice - Checking)
Balance: $1,450.00

1. 2024-01-15 10:00:00 | Deposit      | +$1,000.00 | Balance: $1,000.00
2. 2024-01-15 10:05:00 | Withdrawal   | -$250.00   | Balance: $750.00
3. 2024-01-15 10:10:00 | Transfer In  | +$500.00   | From: ACC-002 | Balance: $1,250.00
4. 2024-01-15 10:15:00 | Deposit      | +$200.00   | Balance: $1,450.00
```

Monthly statement:

```
Monthly Statement - January 2024
Account: ACC-001 (Alice - Checking)

Opening Balance:       $0.00
Total Deposits:        $1,200.00
Total Withdrawals:     $250.00
Total Transfers In:    $500.00
Total Transfers Out:   $0.00
Closing Balance:       $1,450.00

Transaction Count: 4
```

Error cases to handle:

```
Deposit -$100           → Error: Amount must be positive
Deposit $0              → Error: Amount must be positive
Withdraw from empty     → Error: Insufficient funds
Transfer to same account → Error: Cannot transfer to self
Operate on closed account → Error: Account is closed
Account not found       → Error: Account ACC-999 does not exist
```

Multiple accounts:

```
Bank Summary:
ACC-001: Alice  (Checking) - $1,450.00
ACC-002: Bob    (Savings)  - $200.00
ACC-003: Carol  (Checking) - $3,200.00

Total Accounts: 3
Total Deposits: $4,850.00
```

## 🔍 Challenge

Add compound interest calculation for savings accounts (daily, monthly, or yearly compounding), implement overdraft protection with configurable fees, support recurring transactions (like monthly deposits), or add multi-currency support with exchange rates.

---

**Previous:** [39_calculator_history](../39_calculator_history/README.md) | **Next:** [41_deck_cards](../41_deck_cards/README.md)
