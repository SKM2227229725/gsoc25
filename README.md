GSoC Project Summary: Improving Spilling Execution in DataFusion

Contributor: SeoYoung Lee (@ding-young)
Mentor: Yongting You (@2010YOU01)
Organization: Apache DataFusion

Goal

The goal of this project was to improve how DataFusion handles memory pressure.
Instead of queries failing when memory runs out, the aim was to make them slow down gracefully using disk (spilling)—with a focus on external sorting.

Key Contributions

Getting started & initial improvements

Improved out-of-memory (OOM) error messages
Enabled memory tracking by default
Added peak memory tracking in the external sorter

Compression for spill files

Added LZ4 and Zstd compression support
Reduced disk usage and I/O
Updated metrics and added benchmarks

Better benchmarks & profiling

Improved benchmark scripts to clearly show failed queries
Added tools to measure peak memory usage

Multi-level merge improvements

Helped review and stabilize multi-level merge
Removed outdated APIs
Verified memory usage during merge

Memory tracking fixes

Fixed incorrect memory accounting in multiple components
Replaced rough estimates with accurate tracking

Other fixes & improvements

Fixed crashes in row conversion
Improved handling of string data
Added benchmarks for string-related operations
Current Status & Future Work

Some queries still fail under strict memory limits, but the main issues have been identified.

Next steps:

Reduce memory usage in merge structures
Control spill batch sizes more efficiently
Limit merge complexity to avoid high memory peaks

Future scope:

Apply similar improvements to other operators like aggregation and joins
Key Learnings
Memory management is complex, especially with variable-size data like strings
Memory tracked by the application and actual system memory can differ
Strong testing and benchmarking are essential to debug such issues
Acknowledgements

Thanks to mentor Yongting You, Andrew Lamb, Roi Luvaton, and the DataFusion community for their support.
Also grateful to Google for this GSoC opportunity.
