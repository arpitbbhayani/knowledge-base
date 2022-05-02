Our programs need memory, typically in the form of variables and objects, to do their job. The objects are either allocated on Stack or Heap.

## Stack allocated objects

A locally declared variable "int a = 10;" is allocated on the stack i.e. the stack frame of the function call and hence when the function returns the stack frame is popped, making the variable non-existent. Hence variables allocated on Stack do not need to be freed explicitly.

## Heap allocated objects

A variable allocated on the heap is typically done through functions like the "new" or "malloc". The object space allocated for such entities is in RAM and they outlive the function scope and execution, and hence they need to be explicitly freed as we are done with it.

## Why do we need a Heap?

Objects assigned on Heap need to be garbage collected, but why do we need the heap in the first place? There are 3 main reasons:

- We cannot grow your stack-allocated objects dynamically,
- We need dynamically growing objects like Arrays, LinkedList, Trees
- We might need objects that could be larger than what Stack can fit in
- We might need to share the same object across multiple threads
- We do not want our functions to copy and pass bulk objects

## Garbage Collection: Explicit De-allocation

Primitive programming languages like C and C++ do not have their garbage collection instead expect the developer to not only allocate the object but also deallocate it explicitly. Hence we see the functions like "malloc" and "free".

The objects we allocate using "malloc" will continue to exist unless they are reclaimed using "free". The explicit need to "Free-ing" the allocated object is called Explicit Deacclocation.

Although cleaning up the mess we created is a good idea, it is not reliable that we rely on the engineers and developers to always free the objects they allocated. Hence this gives rise to the need for automatic cleanup of unused variables- automatic garbage collection.

The two key side-effects of not cleaning up the unused objects we allocate are

- Memory Leak: Leading to an eventual process crash
- Dangling Pointer: Program behaving unpredictably

Hence, to reduce human error, and make the process more reliable and performant the runtimes of the programming languages implement their automatic garbage collection.