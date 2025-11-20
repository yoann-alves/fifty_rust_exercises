# Exercise 49: Parallel Sorter

## 🎯 Objectives

Implement parallel sorting with performance comparison:

- Sort arrays using parallel algorithms
- Compare parallel vs sequential performance
- Benchmark with different input sizes
- Measure speedup and efficiency

## 📚 Concepts

- Parallel algorithms
- Divide and conquer
- Thread spawning and coordination
- Performance measurement
- Amdahl's Law
- Work distribution

## 📖 Background

**Parallel sorting** divides data into chunks, sorts them independently on different threads, then merges the results.

**Why parallel sorting?**

```
Sequential on 1M numbers:  400ms
Parallel on 4 cores:       ~100ms (ideal 4x speedup)
Reality:                   120ms (3.3x actual speedup)
```

**The speedup challenge:**

- More cores = faster... theoretically
- Reality: overhead from thread management, merging
- **Amdahl's Law**: Some parts must be sequential (the merge)

**Divide and conquer strategy:**

```
[5, 2, 8, 1, 9, 3, 7, 4]
       ↓ Split
[5, 2, 8, 1] [9, 3, 7, 4]
       ↓ Sort in parallel
[1, 2, 5, 8] [3, 4, 7, 9]
       ↓ Merge
[1, 2, 3, 4, 5, 7, 8, 9]
```

**Trade-offs:**

- Small arrays: overhead > benefit, stay sequential
- Large arrays: parallel wins significantly
- Sweet spot: depends on hardware

## ⚙️ Requirements

**First Pass:**

- ✅ Parallel sort implementation works
- ✅ Sequential sort for comparison
- ✅ Time measurement for both
- ✅ Correctly sorts integer arrays
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain complexity and approach
- ✅ **Multiple implementations**:
  - Manual threading version
  - Rayon version (if using that crate)
  - Sequential baseline
- ✅ **Comprehensive benchmarks**:
  - Various sizes: 100, 1K, 10K, 100K, 1M elements
  - Different patterns: random, sorted, reversed, mostly-sorted
  - Multiple runs for statistical validity
  - Calculate speedup and efficiency
- ✅ **Performance metrics**:
  - Execution time
  - Speedup ratio (sequential / parallel)
  - Efficiency percentage (speedup / cores used)
  - Identify overhead
- ✅ **Optimizations**:
  - Threshold for switching to sequential
  - Minimize allocations
  - Tune chunk sizes
- ✅ **Generic**: Works with any sortable type (not just integers)

## 🚫 Constraints

- Can use `rayon` crate for comparison (optional)
- Standard library for manual threading approach
- Must run multiple iterations for accurate benchmarks
- Must verify correctness (output is actually sorted)

## 💡 Approaches

**Algorithm choices:**

- Merge sort (classic divide-and-conquer)
- Quick sort (pivot-based partitioning)
- Any other parallel-friendly algorithm

**Threading strategies:**

- Manual: spawn threads at each split
- Thread pool: reuse threads efficiently
- Rayon: work-stealing parallelism

**Optimization techniques:**

- Sequential threshold (avoid thread overhead on small data)
- In-place vs copy (memory trade-offs)
- Cache-friendly memory access

**Benchmarking approach:**

- Warm-up runs (avoid cold start bias)
- Multiple iterations (average out noise)
- Different data patterns (best/worst/average cases)
- Correctness checks (is output sorted?)

**Measuring performance:**

- Wall-clock time
- CPU time vs wall time
- Speedup = Time(sequential) / Time(parallel)
- Efficiency = Speedup / Number_of_cores
- Overhead = (Ideal_time - Actual_time)

## ✅ Validation

Expected behavior:

```rust
// Small array - might be slower parallel
Input: [5, 2, 8, 1] (4 elements)
Sequential: 0.001ms
Parallel:   0.015ms (overhead dominates)

// Large array - parallel wins
Input: 1,000,000 random integers
Sequential: 387ms
Parallel:   72ms (5.4x speedup on 8 cores)
```

Performance patterns:

```
Size        Sequential  Parallel   Speedup
100         0.01ms      0.15ms     0.07x (worse!)
1,000       0.18ms      0.12ms     1.50x
10,000      2.45ms      0.68ms     3.60x
100,000     32.10ms     6.80ms     4.72x
1,000,000   387.50ms    72.40ms    5.35x
```

Different data patterns:

```
Random data:        387ms → 72ms  (5.4x speedup)
Already sorted:     245ms → 48ms  (5.1x speedup)
Reverse sorted:     410ms → 78ms  (5.3x speedup)
Mostly sorted:      298ms → 58ms  (5.1x speedup)
```

Correctness verification:

```
Input:  [5, 2, 8, 1, 9, 3]
Sequential output: [1, 2, 3, 5, 8, 9] ✓
Parallel output:   [1, 2, 3, 5, 8, 9] ✓
Match: YES ✓
```

Efficiency analysis:

```
8-core CPU results:
Best speedup: 5.35x
Efficiency: 67% (5.35/8)
Why not 8x? Merge overhead, memory copies, sequential bottleneck
```

## 🔍 Challenge

Implement sample sort (scales better to many cores), add GPU acceleration, create an adaptive algorithm that chooses sequential/parallel based on data size and characteristics, or visualize the sorting process in real-time showing which threads are working on which chunks.

---

**Previous:** [48_chat_server](../48_chat_server/README.md) | **Next:** [50_web_scraper](../50_web_scraper/README.md)
