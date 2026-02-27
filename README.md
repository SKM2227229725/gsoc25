GSoC'25 Project Summary: Improving Spilling Execution in DataFusion
Contributor: SeoYoung Lee (@ding-young)
Mentor: Yongting You (@2010YOU01)
Organization: Apache DataFusion

Goal
Make spilling more robust and performant so that memory-intensive queries degrade gracefully instead of failing under memory pressure. Focus on external sorting as a testbed.

Key Contributions
Onboarding & small fixes – Improved OOM error messages, enabled memory tracking by default, added peak memory tracking in ExternalSorter.

Compression for spill files – Added support for LZ4 and Zstd compression in SpillManager, updated metrics, and added benchmarks (reduces disk I/O and file size).

Enhanced benchmarks & profiling – Made benchmark scripts (TPC-H, ClickBench) explicitly mark failed queries; added a utility to profile peak RSS and allocator memory.

Multi‑level merge stabilization – Helped review and validate multi‑level merge, removed obsolete APIs, verified memory consumption during merge phases.

Memory accounting fixes – Corrected accounting for sliced StringViewArray, IPC alignment, and cursor memory in loser trees (replaced fixed 2× multiplier with accurate tracking).

Additional fixes – Fixed row converter panics, improved row format conversion for strings, added benchmarks for string conversions.

Current Status & Future Work
Some queries still fail under memory limits; root causes identified.

Planned improvements:

Optimize loser tree cursor to release memory earlier.

Bound spilled batch sizes (e.g., 256–512 KB) instead of row count only.

Limit merge degree to reduce peak memory during merge.

Future: Extend work to other spilling operators (hash aggregation, sort‑merge join).

Key Lessons
Memory management is tricky, especially with variable‑sized data like strings; application‑level accounting and system RSS don’t always align.

Comprehensive tests and benchmarks are essential to reproduce spilling scenarios and diagnose failures.

Acknowledgements
Thanks to mentor Yongting You, Andrew Lamb, Roi Luvaton, and the DataFusion community for guidance and collaboration. Grateful to Google for the GSoC opportunity.

