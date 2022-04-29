"Best" Garbage Collector is a myth.

If you are ever writing your Garbage Collector or trying to pick one for your workload, there are 7 metrics that you should be evaluating a GC algorithm on.

No one garbage collector can be the best across all 7 properties and it was found that any GC algorithm is at least 15% better than other algorithms on at least one of the characteristics. Hence it all boils down to the needs of your specific workload to pick one over the other. The key characteristics are

# Safety

A garbage collector is safe when it never reclaims the space of a LIVE object and always cleans up only the dead objects.

Although this looks like an obvious requirement, some GC algorithms claim space of LIVE objects just to gain that extra ounce of performance.

# Throughput

A garbage collector should be as little time cleaning up the garbage as possible; this way it would ensure that the CPU is spent on doing actual work and not just cleaning up the mess.

Most garbage collectors hence run small cycles frequently and a major cycle does deep cleaning once a while. This way they maximize the overall throughput and ensure we spend more time doing actual work.

# Completeness

A garbage collector is said to be complete when it eventually reclaims all the garbage from the heap.

It is not desirable to do a complete clean-up every time the GC is executed, but eventually, a GC should guarantee that the garbage is cleaned up ensuring zero memory leaks.

# Pause Time

Some garbage collectors pause the program execution during the cleanup and this induces a "pause". Long pauses affect the throughput of the system and may lead to unpredictable outcomes; so a GC is designed and tuned to minimize the pause time.

The garbage collector needs to pause the execution because it needs to either run defragmentation where the heap objects are shuffled freeing up larger contiguous memory segments.

# Space overhead

Garbage collectors require auxiliary data structures to track objects efficiently and the memory required to do so is pure overhead. An efficient GC should have this space overhead as low as possible allowing sufficient memory for the program execution.

# Language Specific Optimizations

Most GC algorithms are generic but when bundled with the programing language the GC can exploit the language patterns and object allocation nuances. So, it is important to pick the GC that can leverage these details and make its execution as efficient as possible.

For example, in some programming languages, GC runs in constant time by exploiting how objects are allocated on the heap.

# Scalability

Most GC are efficient in cleaning up a small chunk of memory, but a scalable GC would run efficiently even on a server with large RAM. Similarly, a GC should be able to leverage multiple CPU cores, if available, to speed up the execution.