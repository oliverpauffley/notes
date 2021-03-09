# Pool
Pool is a concurrent safe implementation of the object pool pattern. A pool is a way to create and make available a fixed number of things for use.
```go
myPool := &sync.Pool{
	New: func() interface{} {
		fmt.Println("creating new instance.")
		return struct{}{}
	},
}

myPool.Get()
instance := myPool.Get()
myPool.Put(instance)
myPool.Get()
```
When you call `myPool.Get()` a new instance of pool is created. `myPool.Put()` will put an instance back into the pool ready for use. Pool is useful for *pre-warming* some objects that might take some time to create so that they can be ready to use quickly when requested. 

Remember:
- When using `sync.Pool`, give it a `New` member variable this is thread-safe.
- When you receive an instance from `Get`, remember that you don't know it's state.
- Call `Put` when finished with a defer.
- Objects in the pool should be uniform.