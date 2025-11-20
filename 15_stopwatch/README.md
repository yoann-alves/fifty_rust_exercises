# Exercise 15: Simple Stopwatch

## 🎯 Objectives

Create an interactive stopwatch that:

- Starts timing on command
- Stops timing on command
- Resets timer to zero
- Displays elapsed time

## 📚 Concepts

- Time measurement
- Duration handling and formatting
- Program state management
- Interactive command loop

## 📖 Background

**A stopwatch** measures elapsed time between events:

```
Start  → Timer begins counting
Stop   → Timer pauses (keeps accumulated time)
Resume → Timer continues from where it stopped
Reset  → Timer goes back to zero
```

**Real stopwatches** need to handle:

- Running state vs stopped state
- Accumulated time across multiple start/stop cycles
- Displaying time while running
- Formatting time (seconds, minutes, hours)

**Example use case:**

```
Start timer → Run for 5 seconds → Stop
Display shows: 00:00:05

Start again → Run for 3 more seconds → Stop
Display shows: 00:00:08 (accumulated time)

Reset
Display shows: 00:00:00
```

## ⚙️ Requirements

**First Pass:**

- ✅ Start command begins timing
- ✅ Stop command pauses timing
- ✅ Reset command clears timer
- ✅ Displays elapsed time
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain timing logic
- ✅ **State management**:
  - Track if stopwatch is running or stopped
  - Accumulate time across stop/start cycles
  - Handle invalid commands gracefully (e.g., stop when already stopped)
- ✅ **Display features**:
  - Format time nicely (HH:MM:SS or MM:SS.mmm)
  - Show running state indicator
  - Update display while running (optional)
- ✅ **Commands**:
  - Start/Resume
  - Stop/Pause
  - Reset
  - Display current time
  - Help (show available commands)
  - Quit
- ✅ **Edge cases**:
  - Stop when already stopped → should not error
  - Start when already running → should not error
  - Reset while running → should work
  - Very long durations (hours+) → display correctly

## 🚫 Constraints

- Standard library only
- Must use `std::time::Instant` and `Duration`
- No external crates

## 💡 Approaches

**State to track:**

- Is the stopwatch currently running?
- When did it start (if running)?
- How much time was accumulated before (if stopped)?

**Time calculation:**

- When running: current instant - start instant + accumulated time
- When stopped: just show accumulated time
- When reset: clear everything

**Command parsing:**

- Read input from user
- Match against known commands
- Execute appropriate action
- Loop until quit

**Display formatting:**

- Convert duration to hours/minutes/seconds
- Format as string with padding
- Consider milliseconds precision

**State transitions:**

```
Stopped → Start → Running
Running → Stop → Stopped
Any state → Reset → Stopped (with zero time)
```

## ✅ Validation

Example session:

```
=== Stopwatch ===
Commands: start, stop, reset, time, quit

> time
00:00:00.000

> start
Stopwatch started.

> time
00:00:03.245

> stop
Stopwatch stopped. Elapsed: 00:00:05.123

> time
00:00:05.123

> start
Stopwatch resumed.

> time
00:00:08.456

> stop
Stopwatch stopped. Elapsed: 00:00:08.789

> reset
Stopwatch reset.

> time
00:00:00.000

> quit
Goodbye!
```

Test scenarios to verify:

```
Start → wait 5s → stop → should show ~5 seconds
Stop → start → wait 3s → stop → should show ~8 seconds total
Reset → should show 00:00:00
Multiple start/stop cycles → time accumulates correctly
```

Invalid command handling:

```
> stop
(when already stopped) → "Stopwatch is not running"

> start
(when already running) → "Stopwatch is already running"
```

## 🔍 Challenge

Add lap time functionality: press a "lap" command while running to record the current time without stopping, then continue timing. Display all lap times at the end.

---

**Previous:** [14_unit_converter](../14_unit_converter/README.md) | **Next:** [16_anagram_finder](../16_anagram_finder/README.md)
