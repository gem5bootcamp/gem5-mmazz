# Homework 2: Design space exploration


## NAS Parallel Benchmarks

- BT: This version is optimized for memory performance.  It uses much less
memory than the original version due to the size reduction of working
arrays.
- FT: Summary of changes from NPB2.3-serial
    - Reduce the use of memory for big arrays by 1/3
    - Random number generator is made parallelizable
- CG: Except for removal of some working buffers (used in the MPI
program).

## Answers

- Performance Comparison:
    - Compare the performance of the Big core and Little core configurations. What are the key differences in IPC and execution time?
        - As we can see in the data the IPC and execution time difference between the big and little core
        is almost 2 to 3x in all cases.
    - How do the two configurations perform across different workloads?
        - a
    - When changing the cache and memory configurations, does the performance gap between the Big and Little cores change?
        - No, the performance gap does not change
- Cache Impact:
    - How does changing the cache configuration affect performance? Discuss the trade-offs observed between your three-level cache and the alternative cache.
        - We can see that the only workload that make a difference between cache type (a L4 cache), is with FT.
        The explanation of this is because this workload fill up the L3 having a lot of L3 cache misses, in comparison to the other
        workload. This can be see in the data below.
- Insights and Conclusions:
    - Summarize your findings. What architectural choices led to the best performance? What recommendations would you make for future designs?
        - a


### IPC
| Processor Type | Cache Type | Workload | IPC      |
|----------------|------------|----------|----------|
| Big            | L3         | bt       | 3.102892 |
| Big            | L3         | cg       | 2.027297 |
| Big            | L3         | ft       | 2.001440 |
| Big            | L4         | bt       | 3.101280 |
| Big            | L4         | cg       | 2.026320 |
| Big            | L4         | ft       | 2.718968 |
| Little         | L3         | bt       | 0.921771 |
| Little         | L3         | cg       | 0.942454 |
| Little         | L3         | ft       | 0.837150 |
| Little         | L4         | bt       | 0.921546 |
| Little         | L4         | cg       | 0.942212 |
| Little         | L4         | ft       | 0.936042 |

### Sim seconds
| Processor Type | Cache Type | Workload | Time     |
|----------------|------------|----------|----------|
| Big            | L3         | bt       | 0.045368 |
| Big            | L3         | cg       | 0.065844 |
| Big            | L3         | ft       | 0.091457 |
| Big            | L4         | bt       | 0.045391 |
| Big            | L4         | cg       | 0.065876 |
| Big            | L4         | ft       | 0.067322 |
| Little         | L3         | bt       | 0.152718 |
| Little         | L3         | cg       | 0.141636 |
| Little         | L3         | ft       | 0.218653 |
| Little         | L4         | bt       | 0.152756 |
| Little         | L4         | cg       | 0.141672 |
| Little         | L4         | ft       | 0.195552 |

### L3 Misses
| Processor Type | Cache Type | Workload | L3 Misses |
|----------------|------------|----------|---------|
| Big            | L3         | bt       | 9191    |
| Big            | L3         | cg       | 22932   |
| Big            | L3         | ft       | 1990524 |
| Big            | L4         | bt       | 9192    |
| Big            | L4         | cg       | 22951   |
| Big            | L4         | ft       | 1992218 |
| Little         | L3         | bt       | 8945    |
| Little         | L3         | cg       | 22805   |
| Little         | L3         | ft       | 1989100 |
| Little         | L4         | bt       | 8946    |
| Little         | L4         | cg       | 22808   |
| Little         | L4         | ft       | 1991272 |

