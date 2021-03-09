# [[Stack]] Vs [[Heap]]
storing data on the heap is slower than storing data on the stack. Also moving around between different data on the heap is slower than moving through the stack.

When code calls a function, the values passed into the function, including potentially pointers to data on the heap are pushed onto the stack. When the function is over the values get popped off the stack.

[[Ownership]] in rust helps to handle where data is stored and what happens after you are finished using it.