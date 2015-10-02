# Functions

##Multiple return values

In GO, functions and methods can return multiple values.

Here's a simple-minded function to grab a number from a position in a byte slice, returning the number and the next position.

    func nextInt(b []byte, i int) (int, int) {
    for ; i < len(b) && !isDigit(b[i]); i++ {
    }
    x := 0
    for ; i < len(b) && isDigit(b[i]); i++ {
        x = x*10 + int(b[i]) - '0'
    }
    return x, i
    }
    
You could use it to scan the numbers in an input slice b like this:

    for i := 0; i < len(b); {
        x, i = nextInt(b, i)
        fmt.Println(x)
    }
    
-------------------------------------------
##Named result parameters

In GO, just like the incoming parameters,the return parameters of function can have names and used as regular variables. 

if the function executes a return statement with no arguments, the current values of the result parameters are used as the returned values.

The names are not obligatory but they can make code more understandable.

If we name the results of nextInt it becomes obvious which returned int is which.

    func nextInt(b []byte, pos int) (value, nextPos int) {
    
  

    func ReadFull(r Reader, buf []byte) (n int, err error) {
    for len(buf) > 0 && err == nil {
        var nr int
        nr, err = r.Read(buf)
        n += nr
        buf = buf[nr:]
    }
    return
    }
-----------------------------------------------------
##Defer

Go's defer statement set up a function call (the deferred function) to be run immediately before the function executing the defer returns. 

    // Contents returns the file's contents as a string.
    func Contents(filename string) (string, error) {
      f, err := os.Open(filename)
    if err != nil {
        return "", err
    }
    defer f.Close()  // f.Close will run when we're finished.
    var result []byte
    buf := make([]byte, 100)
    for {
        n, err := f.Read(buf[0:])
        result = append(result, buf[0:n]...) // append is discussed later.
        if err != nil {
            if err == io.EOF {
                break
            }
            return "", err  // f will be closed if we return here.
        }
    }
    return string(result), nil // f will be closed if we return here.
    }

but what is the benefit of Deferring a call to a function such as Close?
There are tow main feature :

**First**, it guarantees that you will never forget to close the file.

**Second**, it means that the close sits near the open, which is much clearer than placing it at the end of the function.

The arguments to the deferred function (which include the receiver if the function is a method) are evaluated when the defer executes, not when the call executes. Besides avoiding worries about variables changing values as the function executes, this means that a single deferred call site can defer multiple function executions. Here's a silly example.

    for i := 0; i < 5; i++ {
    defer fmt.Printf("%d ", i)
    }
Deferred functions are executed in *Last In First Out order*, so this code will cause 4 3 2 1 0 to be printed when the function returns.

Another examples :

    func trace(s string)   { fmt.Println("entering:", s) }
    func untrace(s string) { fmt.Println("leaving:", s) }
    // Use them like this:
    func a() {
    trace("a")
    defer untrace("a")
    // do something....
    }

