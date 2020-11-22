# Why is Concurrency Hard?

## Race Conditions
A race condition occurs when two or more operations must execute in a certain order but this has not been programmed correctly. Most of the time this shows up in a **data race** where one operation attempts to read a variable that another operation is trying to write to.

```go
var data int
go func () {
	data ++
}
if data == 0 {
	fmt.Printf("the value is %v.\n,data")
}
```
This type of error normally happens when you are thing sequentially. It can be helpful to imagine what would happen if a large amount of time parses between operations. What is an hour passes before you reach the **if** statement.

## Atomicity
When something is considered atomic this means that within the context that it is operating, it is indivisible or uninterruptible. These terms mean that within the defined context the atomic process will happen it it's entirety without anything happening in that context simultaneously.
### Example
```go
i++
```
Three things actually happen in this line.
- Retrieve the value of **i**.
- Increment the value of **i**.
- Store the value of **i**.
Each of these operations are atomic but the combination might not be depending on the context. This implies that combining a sequence of atomic commands is not always atomic. So then you need to decide in what context would you need a sequence of commands to be atomic.

If something is atomic it is safe within concurrent contexts. Most statements, functions, methods and programs are not atomic so we employ a number of techniques to achieve the needed atomicty.

## Memory Access Synchronization
The name of part of the program that needs exclusive access to a shared resource is the **critical section**. If the following example there are 3 critical sections.
```go
var data int
go func() {data++} ()
if data == 0 {
	fmt.Println("the value is 0")
} else {
		fmt.Printf("the value is %v.\n",data)
}
```
- The goroutine, which is incrementing the *data* variable.
- The *if* statement, which checks whether the value of data is 0.
- Our *fmt.Printf*, which retrieves the value of data for output.
Go has methods for protecting these critical sections. One example is [[Sync.Mutex]] that allows your to **lock** and **unlock** access to shared memory.

## Deadlocks, Livelocks and Starvation
Even when your program is logically correct there can still be issues.
### Deadlock
A deadlocked program is one in which all concurrent processes are waiting on one another. In this state, the program will never recover without outside intervention. 
```go
type value struct {
	mu sync.Mutex
	value int
}

var wg sync.WaitGroup
printSum := func(v1, v2 *value) {
	defer wg.Done()
	v1.mu.Lock()
	defer v1.mu.Unlock()
	
	time.Sleep(2 * time.Second)
	v2.mu.Lock()
	defer v2.mu.Unlock()
	
	fmt.Printf("sum=%v\n", v1.value+v2.value)
}

var a, b value

wg.Add(2)
go printSum(&a, &b)
go printSum(&b, &a)
wg.Wait()
```

### Livelock
Livelocks are programs that are actively doing work but that work doesn't move the state of the program forward.

### Starvation
Starvation is any situation where a concurrent process cannot get all the resources it needs to perform work. This can be caused by a *greedy* process locking some access for too long. This means that other processes won't be able to access the resource. However constant locking and unlocking can cause processes to run slowly. **TIP** start with constraining memory access only to critical sections and then change if performance is getting slowed down.

## Determining Concurrency Safety
The biggest problem is **people**. Concurrency is hard and people have to overcome that complexity. It is very important that code is well commented to explain the concurrent aspects so that it can be easily understood by others.
