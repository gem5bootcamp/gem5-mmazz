## Data of 100 runs:

Numbers of threads 16\
The average of algorithm 1 is: 0.614 \
The average of algorithm 2 is: 0.482\
The average of algorithm 3 is: 0.433\
The average of algorithm 4 is: 0.428\
The average of algorithm 5 is: 0.249\
The average of algorithm 6 is: 0.243

Numbers of threads 8\
The average of algorithm 1 is: 0.56\
The average of algorithm 2 is: 0.474\
The average of algorithm 3 is: 0.467\
The average of algorithm 4 is: 0.45\
The average of algorithm 5 is: 0.153\
The average of algorithm 6 is: 0.153

Numbers of threads 4\
The average of algorithm 1 is: 0.539\
The average of algorithm 2 is: 0.448\
The average of algorithm 3 is: 0.45\
The average of algorithm 4 is: 0.434\
The average of algorithm 5 is: 0.118\
The average of algorithm 6 is: 0.114

Numbers of threads 2\
The average of algorithm 1 is: 0.598\
The average of algorithm 2 is: 0.428\
The average of algorithm 3 is: 0.427\
The average of algorithm 4 is: 0.412\
The average of algorithm 5 is: 0.152\
The average of algorithm 6 is: 0.153



Speed up one thread vs 16\
The average of algorithm 1 is:  2.252\
The average of algorithm 2 is:  2.568\
The average of algorithm 3 is:  2.894\
The average of algorithm 4 is:  3.234\
The average of algorithm 5 is:  5.522\
The average of algorithm 6 is:  5.679

- Question 1: The performance remains more or less the same, as shown in the data provided.
- Question 2:
    - a) : No, the performance remains nearly the same until reaching 16 threads, where it begins to drop.
    - b)With a single thread, the average execution time for Algorithm 6 is 1.38. The speedup for 2, 4, 8, and 16 threads is shown in the table provided.

- Question 3:
    - a) The most significant optimization is adding padding between the result addresses. This is evident in Algorithm 5, which consistently achieves the best performance across all runs.
    - b) This optimization ensures that all threads write to distinct memory locations on separate cache lines. By doing so, it prevents cache line contention and invalidation. Each thread operates on its own cache line, avoiding interference and ensuring optimal memory access patterns.



# Gem5

Data for 16 threads

Time Simulated\
The value of algorithm 1 is: 0.000917\
The value of algorithm 2 is: 0.000915\
The value of algorithm 3 is: 0.000686\
The value of algorithm 4 is: 0.000687\
The value of algorithm 5 is: 0.000145\
The value of algorithm 6 is: 0.000114

Read shearing\
The value of algorithm 1 is: 2380\
The value of algorithm 2 is: 599\
The value of algorithm 3 is: 2385\
The value of algorithm 4 is: 610\
The value of algorithm 5 is: 2404\
The value of algorithm 6 is: 650

Write shearing (xbar_latency=10, 16 threads with 16 cores)\
The value of algorithm 1 is: 32906\
The value of algorithm 2 is: 32863\
The value of algorithm 3 is: 32814\
The value of algorithm 4 is: 32776\
The value of algorithm 5 is: 192\
The value of algorithm 6 is: 245

Hits ratio\
The value of algorithm 1 is:  0.859\
The value of algorithm 2 is:  0.933\
The value of algorithm 3 is:  0.868\
The value of algorithm 4 is:  0.941\
The value of algorithm 5 is:  0.932\
The value of algorithm 6 is:  0.994


SpeedUp from 1 core to 16 with 16 threads:\
The value of algorithm 1 is:  0.088\
The value of algorithm 2 is:  0.089\
The value of algorithm 3 is:  0.118\
The value of algorithm 4 is:  0.118\
The value of algorithm 5 is:  0.559\
The value of algorithm 6 is:  2.816


Time Simulated (xbar_latency=25, 16 threads with 16 cores)\
The value of algorithm 1 is:  0.001760\
The value of algorithm 6 is:  0.000131

Time Simulated(xbar_latency=10, 16 threads with 16 cores)\
The value of algorithm 1 is: 0.000917\
The value of algorithm 6 is: 0.000114

Time Simulated (xbar_latency=1, 16 threads with 16 cores)\
The value of algorithm 1 is:  0.000349\
The value of algorithm 6 is:  0.000104

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

