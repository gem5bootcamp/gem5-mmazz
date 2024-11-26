## Data of 100 runs:

Numbers of threads 16
The average of algorithm 1 is: 0.614
The average of algorithm 2 is: 0.482
The average of algorithm 3 is: 0.433
The average of algorithm 4 is: 0.428
The average of algorithm 5 is: 0.249
The average of algorithm 6 is: 0.243

Numbers of threads 8
The average of algorithm 1 is: 0.56
The average of algorithm 2 is: 0.474
The average of algorithm 3 is: 0.467
The average of algorithm 4 is: 0.45
The average of algorithm 5 is: 0.153
The average of algorithm 6 is: 0.153

Numbers of threads 4
The average of algorithm 1 is: 0.539
The average of algorithm 2 is: 0.448
The average of algorithm 3 is: 0.45
The average of algorithm 4 is: 0.434
The average of algorithm 5 is: 0.118
The average of algorithm 6 is: 0.114

Numbers of threads 2
The average of algorithm 1 is: 0.598
The average of algorithm 2 is: 0.428
The average of algorithm 3 is: 0.427
The average of algorithm 4 is: 0.412
The average of algorithm 5 is: 0.152
The average of algorithm 6 is: 0.153

- Question 1: Is more or less the same ass we can see in the data.
- Question 2:
    - a) No, we can see that its almost the same until we reach 16 threads, that the performance drops.
    - b) It's:
        - 2 threads: 9.02
        - 4 threads: 12.10
        - 8 threads: 9.02
        - 16 threads: 5.68
- Question 3:
    - a)The most important optimization is adding padding between the result addresses.
    This is evident in Algorithm 5, where it consistently shows the best performance across all runs.
    - b) The hardware optimization works by ensuring that all threads write to
    different locations in memory that are on separate cache lines.
    This approach prevents cache line contention and invalidation, as each thread
    operates on a distinct cache line, avoiding interference with others.
