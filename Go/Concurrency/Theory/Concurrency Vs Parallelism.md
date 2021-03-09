# Concurrency Vs Parallelism 
*Concurrency* is not *parallelism*

>Concurrency is a property of the code; parallelism is a property of the running program.

Even if you write a program that can run sections concurrently; if the cpu is only single core the code will always run sections in sequence. We write code that we **hope** will run in parallel but the runtime will determine if it does.

[[GOMAXPROCS]] will ensure that it uses the correct number of os threads automatically.