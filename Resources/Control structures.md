#Control structures


##If
In Go a simple if looks like this:

if x > 0 {
    return y
}

Braces are obligatory.

Writing simple if statements on multiple lines is a good habit especially when the body contains a control statement 

such as a return or break.

Since if and switch accept an initialization statement, it's common to see one used to set up a local variable.

    if err := file.Chmod(0664); err != nil {
    log.Print(err)
    return err
    }
    
    
when an if statement doesn't flow into the next statement—that is, the body ends in break, continue, goto, or return—the unnecessary else is omitted.

    f, err := os.Open(name)
    if err != nil {
    return err
    }
    


---------------------------------------------

##For

The Go for loop is somehow look like in C ,but mot exactly the same .

 It unifies for and while and there is no do-while. There are three forms, only one of which has semicolons.

    // Like a C for
    for init; condition; post { }
    // Like a C while
    for condition { }
    // Like a C for(;;)
    for { }
    
Short declarations make it easy to declare the index variable right in the loop.

    sum := 0
    for i := 0; i < 10; i++ {
    sum += i
    }
    
If you're looping over an array, slice, string, or map, or reading from a channel, a range clause can manage the loop.

    for key, value := range oldMap {
    newMap[key] = value
    }
    
If you just need the first item in the range (the key or index), omit the second:

    for key := range m {
    if key.expired() {
        delete(m, key)
    }
    }

---------------------------------
##Switch

Go's switch is more general than C's. 

The expressions need not be constants or even integers, 

GO examine the cases top to bottom until it find a match .

In case if the switch has no expression it switches on true.

So, you can write a switch as  if-else-if-else sequences.

    func unhex(c byte) byte {
       switch {
    case '0' <= c && c <= '9':
        return c - '0'
    case 'a' <= c && c <= 'f':
        return c - 'a' + 10
    case 'A' <= c && c <= 'F':
        return c - 'A' + 10
    }
    return 0
    }
    
 Cases can be presented in comma-separated lists.

    func shouldEscape(c byte) bool {
    switch c {
    case ' ', '?', '&', '=', '#', '+', '%':
        return true
    }
    return false
    }
    
Break statements can be used to terminate a switch early. 

    Loop:
    for n := 0; n < len(src); n += size {
    		switch {
    		case src[n] < sizeOne:
       if validateOnly {
       break
       }
       size = 1
       update(src[n])
       
       case src[n] < sizeTwo:
       
       if n+1 >= len(src) {
       err = errShortInput
       break Loop
       }
       if validateOnly {
       break
       }
       size = 2
       update(src[n] + src[n+1]<<shift)
       } 
    }
    
 *continue statement* applies only to loops.

Example :

    // Compare returns an integer comparing the two byte slices,
    // lexicographically.
    // The result will be 0 if a == b, -1 if a < b, and +1 if a > b
    func Compare(a, b []byte) int {
    for i := 0; i < len(a) && i < len(b); i++ {
        switch {
        case a[i] > b[i]:
            return 1
        case a[i] < b[i]:
            return -1
        }
    }
    switch {
    case len(a) > len(b):
        return 1
    case len(a) < len(b):
        return -1
    }
    return 0
    }

