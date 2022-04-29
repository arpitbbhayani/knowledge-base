The Mark-and-Sweep garbage collection algorithm is one of the most common and widely adopted garbage collection algorithms out there. It leverages the power of Graph data structure along with DFS to power the cleanup.

Almost all programming languages support allocating objects in heap and referring them via pointers to another object. This reference creates a small graph of all the references linked to the one root node.

The root node could be a global variable (object) or something allocated on the thread stack, and anything and everything referenced from that becomes the child nodes and the process continues.

### Indirect Collection Algorithm

The mark-and-Sweep garbage collection algorithm is an indirect collection algorithm, which means it does not have any direct information about the garbage, instead, it identifies the garbage by eliminating everything LIVE.

# When is the GC triggered?

The garbage collection is triggered when the runtime environment is unable to allocate any new object on the heap. When the language tries to fire `new` and it is unable to allocate space, it first triggers a quick garbage collection and then tries to re-allocate; if not successful again it throws an OutOfMemory exception, and in most cases, it is a fatal error.

# Mark-and-Sweep Algorithm

Although the algorithm is primarily split into two phases Mark and Sweep; to build a better understanding we split it into 4.

## Prepare the root list

The first step of this algorithm is to extract and prepare the root list, and the roots could be global variables or variables referenced in the thread stack. These become the seed objects on which we then trigger a DFS.

## Mark the roots and proceed

Once we identified all the roots, we mark all the roots as `LIVE` and proceed with the Mark phase. A super optimization that some implementations apply is to invoke the Mark phase for every root as it would help us keep the stack smaller.

## Mark

The mark phase is just a Depth First Search traversal on one root node and the idea is to mark every node as `LIVE` that is reachable from the root node. Once all the nodes are marked, we can conclude that the nodes that remain unmarked are garbage; and the ones to be cleaned up.

## Sweep

The nodes left unmarked are the garbage and hence in the sweep phase, the GC iterates through all the objects and frees the unmarked objects, and resets the marked object to prepare them for the next cycle.