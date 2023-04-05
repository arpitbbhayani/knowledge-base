Writing concurrent programs can be easy, but ensuring their correctness and optimality can be tricky, especially when dealing with multi-threaded programs. In this article, we'll discuss some best practices for writing good multi-threaded programs that are both correct and efficient.

## Ensuring Correctness: Locking and Atomic Instructions

When dealing with multi-threaded programs, it's important to ensure that the program's correctness is maintained even when multiple threads are accessing the same resources simultaneously. This is where locking and atomic instructions come into play.

Locking is a technique used to synchronize access to shared resources. By using locks, we can ensure that only one thread can access a shared resource at a time, thus preventing race conditions and ensuring correctness.

Atomic instructions, on the other hand, are low-level operations that are executed atomically, meaning that they are indivisible and can't be interrupted by other threads. These operations are useful when updating shared resources, as they ensure that the update is performed atomically and that no other thread can interfere with the update.

## Ensuring Optimality: Fairness and Efficient Logic

In addition to ensuring correctness, it's also important to ensure that our multi-threaded programs are efficient and optimal. One way to achieve this is by ensuring fairness, which means that all threads are given an equal chance to execute and that no thread is starved and all threads complete nearly at the same time.

## Counting prime numbers

For example, let's consider the problem of counting prime numbers to 200 million. We can use a sequential approach to check each number for divisibility by any of its peers. However, this approach can be slow and inefficient. By adding threads, we can speed up the process, but it's important to ensure that the workload is evenly distributed among the threads to avoid bottlenecks.

### Approach 1: Threads handling a range

We can divide the workload among 10 threads, with each thread handling an equal range of numbers. But this isn't optimal.

The smaller numbers can be quickly checked for primality which means the threads handling larger numbers will take longer to complete.

### Approach 2: Threads as workers

Let's have a global variable called `currentNum`, which is updated atomically to keep track of the next unprocessed number.

Each thread can then loop until all numbers have been processed, incrementing `currentNum` atomically to check the next unprocessed number for primality.

By using this approach, we can ensure both correctness and optimality, with all threads completing their work nearly simultaneously.

## Conclusion

In summary, writing good multi-threaded programs requires careful consideration of correctness and optimality.

By using locking and atomic instructions, we can ensure correctness, while threading with fairness and efficient logic can ensure optimality. With these best practices in mind, we can write multi-threaded programs that are both correct and efficient.