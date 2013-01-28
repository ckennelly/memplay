memplay - A Memory Allocation Tracer and Replayer
(c) 2013 - Chris Kennelly (chris@ckennelly.com)

Overview
========

Analyzing the performance characteristics of memory allocators is a nuanced process.  Reliable reproduction of "real world" allocation patterns may be impossible due to inherent nondeterminism in the program being studied.

memplay has two components, a tracer and a replayer.

* The tracer provides lightweight instrumentation around libc's `malloc` and `free` calls, recording these calls during the execution of the analyzed program.
* The replayer reads recorded allocation metadata and performs allocations against an arbitrary malloc/realloc/free implementation.  While a total ordering of allocations is not provided for multithreaded runs, allocations otherwise occur deterministically according to the input file and respect its implicit partial ordering.

For a multithreaded server application that relies on dynamic memory allocation, the order of connection initiation and activity complicates the analysis of allocator performance.  Replay reduces the impact of nondeterminism during test execution.
