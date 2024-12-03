# Homework 1: Cache Coherence

- Question 1: The performance remains more or less the same, as shown in the data provided.
- Question 2:
    - a) : No, the performance remains nearly the same until reaching 16 threads, where it begins to drop.
    - b)With a single thread, the average execution time for Algorithm 6 is 1.38. The speedup for 2, 4, 8, and 16 threads is shown in the table provided.

- Question 3:
    - a) The most significant optimization is adding padding between the result addresses. This is evident in Algorithm 5, which consistently achieves the best performance across all runs.
    - b) This optimization ensures that all threads write to distinct memory locations on separate cache lines. By doing so, it prevents cache line contention and invalidation. Each thread operates on its own cache line, avoiding interference and ensuring optimal memory access patterns.

## Data of 100 runs:

Numbers of threads 16
| Algorithm | Average |
|-----------|---------|
| 1         | 0.614   |
| 2         | 0.482   |
| 3         | 0.433   |
| 4         | 0.428   |
| 5         | 0.249   |
| 6         | 0.243   |

Numbers of threads 8
| Algorithm | Average |
|-----------|---------|
| 1         | 0.56    |
| 2         | 0.474   |
| 3         | 0.467   |
| 4         | 0.45    |
| 5         | 0.153   |
| 6         | 0.153   |

Numbers of threads 4
| Algorithm | Average |
|-----------|---------|
| 1         | 0.539   |
| 2         | 0.448   |
| 3         | 0.45    |
| 4         | 0.434   |
| 5         | 0.118   |
| 6         | 0.114   |

Numbers of threads 2
| Algorithm | Average |
|-----------|---------|
| 1         | 0.598   |
| 2         | 0.428   |
| 3         | 0.427   |
| 4         | 0.412   |
| 5         | 0.152   |
| 6         | 0.153   |

Speed up one thread vs 16
| Algorithm | Speed-up |
|-----------|----------|
| 1         | 2.252    |
| 2         | 2.568    |
| 3         | 2.894    |
| 4         | 3.234    |
| 5         | 5.522    |
| 6         | 5.679    |


# Gem5

- Question 4:
    - a) The speed up is 2.816.
    - b) It is similar to the real system, except that here Algorithm 2 behaves similarly to Algorithm 1, whereas on the real hardware, Algorithm 2 resembles Algorithms 3 and 4 instead.
- Question 5:
    - The optimization with the biggest impact on the hit ratio is chunking the array. This is evident when comparing Algorithms 1 and 2.
- Question 6:
     - The optimization that reduces read sharing the most is chunking the array. This can be observed in the table comparing Algorithms 2, 4, and 6, which utilize chunking. In algorithms that do not use chunking, one core fetches the memory line, and all other cores access addresses within that same line. By contrast, chunking ensures that each core operates on a distinct portion of the data, significantly reducing read sharing.

- Question 7:
    - The algorithms that reduce write sharing are those that use padding in the result addresses. This is evident from the data for Algorithms 5 and 6, which show a significant reduction in write sharing. This improvement occurs because each core writes to distinct memory lines, avoiding conflicts where multiple cores attempt to write to the same cache line.
- Question 8:
    - a) The most important hardware characteristic is write sharing, we can see this because
    the biggest drop in time is in algorithm 5 and 6 which are those that significantly reduce
    write sharing.
    - b) The hardware reason why write shearing is the most important factor when optimizing, is because
        the protocol used, MESI, make it that when a core writes a line, this entired line gets invalidated
        in all other cores, so every core needs to mantein coherence every time it writes.
      Having to go to a lower level of cache.
        Meanwhile, the fact that MESI allows for core to core shearing of addresses when read, mitigates the performance
        loss from cache misses.
- Question 9:
    - As we increase the cache-to-cache latency, we can see that the difference between algorithms increase.
    - Showing that reducing writebacks is more impactful as latency increase.

## Data for 16 threads

Time Simulated
| Algorithm | Value     |
|-----------|-----------|
| 1         | 0.000917  |
| 2         | 0.000915  |
| 3         | 0.000686  |
| 4         | 0.000687  |
| 5         | 0.000145  |
| 6         | 0.000114  |

Read shearing
| Algorithm | Value |
|-----------|-------|
| 1         | 2380  |
| 2         | 599   |
| 3         | 2385  |
| 4         | 610   |
| 5         | 2404  |
| 6         | 650   |

Write shearing (xbar_latency=10, 16 threads with 16 cores)
| Algorithm | Value  |
|-----------|--------|
| 1         | 32906  |
| 2         | 32863  |
| 3         | 32814  |
| 4         | 32776  |
| 5         | 192    |
| 6         | 245    |

Hits ratio
| Algorithm | Value  |
|-----------|--------|
| 1         | 0.859  |
| 2         | 0.933  |
| 3         | 0.868  |
| 4         | 0.941  |
| 5         | 0.932  |
| 6         | 0.994  |


SpeedUp from 1 core to 16 with 16 threads:
| Algorithm | Value  |
|-----------|--------|
| 1         | 0.088  |
| 2         | 0.089  |
| 3         | 0.118  |
| 4         | 0.118  |
| 5         | 0.559  |
| 6         | 2.816  |


Time Simulated (xbar_latency=25, 16 threads with 16 cores)
| Algorithm | Value     |
|-----------|-----------|
| 1         | 0.001760  |
| 6         | 0.000131  |

Time Simulated(xbar_latency=10, 16 threads with 16 cores)
| Algorithm | Value     |
|-----------|-----------|
| 1         | 0.000917  |
| 6         | 0.000114  |

Time Simulated (xbar_latency=1, 16 threads with 16 cores)
| Algorithm | Value     |
|-----------|-----------|
| 1         | 0.000349  |
| 6         | 0.000104  |

