The Mark and Sweep garbage collection algorithm is a simple DFS traversal with two phases - Mark and Sweep. In the mark phase, it marks all the objects that are reachable from the root, and the Sweep phase clears off all the unreachable ones.

This crude algorithm is slow and requires a program pause which means everything stops when the GC is cleaning up. This affects the performance and throughput of the program.

So, can we write a GC that runs concurrently with the program and does not need to always stop the world?

The foundation of concurrent Garbage Collector is based on a concept called Tricolour Abstraction which was developed by Dijkstra and Lamport, known for their work on core algorithms and distributed systems.

## States of an object

While tracing the objects across the heap we can see that each object can be in one of the 3 states: unprocessed, processing, and processed; and this becomes our three colors

White: unprocessed objects
Grey: visited but whose children are yet to be visited
Black: done processing

### The garbage collection flow

Every node starts white. Once we see an object we color it Grey and once we are done visiting its children we mark it Black. This way we have 3 sets of objects: white, great, and black, and the objects move from white to grey and from grey to black.

A key thing to note here is that we will never have an object that moves directly from white to black; i.e. there will never be an edge that connects one black and one white node.

### How does Tricoloration make it better?

Because a black node is never connected to a white node, we ensure correctness i.e. a live object will never be cleaned up.

Our GC flow can now be simplified as

- pick the object from the grey set
- color all the children of the node grey
- move the grey object to the black

repeat the flow until the grey set is empty. Once done, we can just visit the white set, which now contains all the unreachable objects, and clean them up.

### Speedup

Now that we segregated the objects into sets we can ensure a quick cleanup by putting more threads at work on the grey set. It is hard to make a crude DFS concurrent and structuring it as sets make implementation much simpler.

We make our system reactive by keeping an eye on the grey set and triggering GC as soon as it hits some threshold.

This method of garbage collection is called "on-the-fly" which runs concurrently with the program and mutates the color of the objects as part of program execution and does not wait for a separate GC cycle. This reduces the load on GC and minimizes the pause.