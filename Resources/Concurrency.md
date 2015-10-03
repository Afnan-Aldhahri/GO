
# Concurrency

##Share by communicating


As we study in our class, **Concurrent programming**  is always difficult since it require 

to implement correct access to shared variables. 

Go support  different ways in which shared values are passed around on **channels** and, so, never  shared by separate threads of execution.

Only one goroutine has access to the value at any given time.

Data races cannot occur.

GO has a slogan:

>> Do not communicate by sharing memory; instead, share memory by communicating.

* Using channels to control access makes it easier to write clear, correct programs.

* One way to think about this model is to consider a typical single-threaded program running on one CPU. 

* It has no need for synchronization primitives. 

* Now run another such instance; it too needs no synchronization. 

* Now let those two communicate; if the communication is the synchronizer, there's still no need for other synchronization. 

------------------------------------
## Goroutines

 * A goroutine has a simple model: it is a function executing concurrently with other goroutines in the same address space. 
 
 * It is lightweight, costing little more than the allocation of stack space. 
 
   And the stacks start small, so they are cheap, and grow by allocating (and freeing) heap storage as required.

* Goroutines are multiplexed onto multiple OS threads so if one should block, such as while waiting for I/O,

 others continue to run.
 
 * Their design hides many of the complexities of thread creation and management.

Prefix a function or method call with the **go** keyword to run the call in a *new goroutine*. 

When the call completes, the goroutine exits, silently. 

(The effect is similar to the Unix shell's & notation for running a command in the background.)

    go list.Sort()  // run list.Sort concurrently; don't wait for it.
    
A function literal can be handy in a goroutine invocation.

    func Announce(message string, delay time.Duration) {
    go func() {
        time.Sleep(delay)
        fmt.Println(message)
    }()  // Note the parentheses - must call the function.
    }

These examples aren't too practical because the functions have no way of signaling completion. For that, we need channels.

---------------------------------------------------

## Channels

Like maps, channels are allocated with make, and the resulting value acts as a reference to an underlying data structure. 

If an optional integer parameter is provided, it sets the buffer size for the channel.

The default is zero, for an unbuffered or synchronous channel.

    ci := make(chan int)            // unbuffered channel of integers
    cj := make(chan int, 0)         // unbuffered channel of integers
    cs := make(chan *os.File, 100)  // buffered channel of pointers to Files
    
Unbuffered channels combine communication—the exchange of a value—with synchronization—guaranteeing 

that two calculations (goroutines) are in a known state.

 A channel can allow the launching goroutine to wait for the sort to complete.

    c := make(chan int)  // Allocate a channel.
    // Start the sort in a goroutine; when it completes, signal on the channel.
    go func() {
    list.Sort()
    c <- 1  // Send a signal; value does not matter.
    }()
    doSomethingForAWhile()
    <-c   // Wait for sort to finish; discard sent value.
    

A buffered channel can be used like a semaphore, for instance to limit throughput. 

In this example, incoming requests are passed to handle, which sends a value into the channel, processes the request, 

and then receives a value from the channel to ready the “semaphore” for the next consumer. 

    var sem = make(chan int, MaxOutstanding)
    func handle(r *Request) {
    sem <- 1    // Wait for active queue to drain.
    process(r)  // May take a long time.
    <-sem       // Done; enable next request to run.
    }
    func Serve(queue chan *Request) {
    for {
        req := <-queue
        go handle(req)  // Don't wait for handle to finish.
    }
    }
    
[Previous] (https://github.com/Afnan-Aldhahri/GO/blob/master/Resources/Initialization.md ) - 
[Home] (https://github.com/Afnan-Aldhahri/GO/blob/master/README.md ) -
[ Next](https://github.com/Afnan-Aldhahri/GO/blob/master/Resources/Run%20your%20first%20program.md)
