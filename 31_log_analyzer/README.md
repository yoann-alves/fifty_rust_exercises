# Exercise 31: Log Analyzer

## 🎯 Objectives

Create a log file analyzer:

- Read and parse log files
- Count messages by severity (ERROR, WARN, INFO, DEBUG)
- Filter logs by level and/or date
- Display statistics and filtered results

## 📚 Concepts

- File I/O and line parsing
- Pattern matching and extraction
- Filtering and aggregation
- Date/time parsing
- Statistics collection

## 📖 Background

**Log files** record what happens in a system over time. Each line typically contains:

```
2024-01-15 10:23:45 INFO Application started
2024-01-15 10:24:12 ERROR Database connection failed
2024-01-15 10:24:13 WARN Retrying connection...
```

**Log levels** indicate severity (from least to most critical):

```
DEBUG → INFO → WARN → ERROR → FATAL
```

**Common questions when analyzing logs:**

- How many errors occurred?
- When did the first ERROR appear?
- What were all the WARN messages between 2pm and 4pm?
- Are there patterns (spikes, gaps, repeated messages)?

**Real-world log files** can be:

- Gigabytes in size
- Have mixed formats
- Contain malformed lines
- Span days or months

Your job: build a tool that makes sense of log chaos.

## ⚙️ Requirements

**First Pass:**

- ✅ Reads log file line by line
- ✅ Identifies log levels (ERROR, WARN, INFO, DEBUG)
- ✅ Counts occurrences of each level
- ✅ Displays statistics
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain parsing strategy
- ✅ **Complete parsing**:
  - Extract timestamp
  - Extract log level
  - Extract message text
  - Handle multiple common formats
- ✅ **Filtering**:
  - By log level (show only ERROR)
  - By date/time range
  - By keyword in message
  - Combine multiple filters
- ✅ **Rich statistics**:
  - Count per level
  - Timeline (errors per hour/day)
  - First/last occurrence
  - Most common messages
- ✅ **Display options**:
  - Summary statistics only
  - Full filtered output
  - Export to file
- ✅ **Error handling**:
  - Skip malformed lines gracefully
  - Handle file read errors
  - Report unparseable dates
- ✅ **Performance**:
  - Handle large files (100MB+)
  - Don't load entire file into memory

## 🚫 Constraints

- Standard library only
- No external log parsing libraries
- Must handle large files efficiently (streaming, not loading all at once)

## 💡 Approaches

**Parsing strategies:**

- Split line by whitespace or delimiter
- Use pattern matching to identify components
- Store structured data (timestamp, level, message)
- Handle variations in format

**Log level identification:**

- Look for keywords: ERROR, WARN, INFO, DEBUG
- Case-insensitive matching
- Default to INFO if unclear

**Filtering logic:**

- Level filter: keep only matching severity
- Date filter: parse timestamp, check if in range
- Keyword filter: search in message text
- Chain filters together

**Statistics tracking:**

- Keep counters for each level
- Group by time period (hour, day)
- Track first/last seen
- Identify duplicates

**Memory efficiency:**

- Process line-by-line (streaming)
- Don't store all lines if just counting
- Use iterators

## ✅ Validation

**Sample log file (test.log):**

```
2024-01-15 10:00:00 INFO Application started
2024-01-15 10:00:05 DEBUG Loading configuration
2024-01-15 10:00:10 INFO Configuration loaded
2024-01-15 10:01:00 ERROR Database connection failed
2024-01-15 10:01:05 WARN Retrying connection (attempt 1)
2024-01-15 10:01:10 WARN Retrying connection (attempt 2)
2024-01-15 10:01:15 INFO Database connected
2024-01-15 10:02:00 ERROR File not found: config.yml
2024-01-15 10:02:05 FATAL Application crashed
```

**Expected statistics:**

```
Total entries: 9
DEBUG: 1
INFO: 3
WARN: 2
ERROR: 2
FATAL: 1
```

**Filter by level (ERROR only):**

```
2024-01-15 10:01:00 ERROR Database connection failed
2024-01-15 10:02:00 ERROR File not found: config.yml

Found 2 matching entries.
```

**Filter by time range (10:01:00 to 10:01:59):**

```
2024-01-15 10:01:00 ERROR Database connection failed
2024-01-15 10:01:05 WARN Retrying connection (attempt 1)
2024-01-15 10:01:10 WARN Retrying connection (attempt 2)
2024-01-15 10:01:15 INFO Database connected

Found 4 matching entries.
```

**Filter by keyword ("connection"):**

```
2024-01-15 10:01:00 ERROR Database connection failed
2024-01-15 10:01:05 WARN Retrying connection (attempt 1)
2024-01-15 10:01:10 WARN Retrying connection (attempt 2)
2024-01-15 10:01:15 INFO Database connected

Found 4 matching entries.
```

**Timeline statistics:**

```
Activity by hour:
10:00 - 3 entries (2 INFO, 1 DEBUG)
10:01 - 4 entries (1 INFO, 2 WARN, 1 ERROR)
10:02 - 2 entries (1 ERROR, 1 FATAL)
```

**Edge cases to handle:**

```
Empty file           → "No log entries found"
Malformed lines      → Skip with optional warning
Mixed date formats   → Parse flexibly or use consistent format
Huge files (1GB+)    → Still works (streaming)
```

## 🔍 Challenge

Add anomaly detection: identify unusual patterns like sudden spikes in errors, repeated identical error messages (potential infinite loop), or suspicious time gaps in logging that might indicate system downtime.

---

**Previous:** [30_config_parser](../30_config_parser/README.md) | **Next:** [32_directory_tree](../32_directory_tree/README.md)
