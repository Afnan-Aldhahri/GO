
# Initialization

**initialization** in Go is very robust. 

Complex structures can be built during initialization and the ordering issues among initialized objects,

even among different packages, are handled correctly.

## Constants

 * Constants are created at **compile time** , even when defined as locals in functions.
 
 * Constants  can only be numbers, characters (runes), strings or booleans. 
 
 **1<<3** is a constant expression, while **math.Sin(math.Pi/4)** is *not* because the function call 
 
 to math.Sin needs to happen at *run time*.

In Go, enumerated constants are created using the iota enumerator. 

Since iota can be part of an expression and expressions can be implicitly repeated, 

it is easy to build intricate sets of values.

    type ByteSize float64
    const (
    _           = iota // ignore first value by assigning to blank identifier
    KB ByteSize = 1 << (10 * iota)
    MB
    GB
    TB
    PB
    EB
    ZB
    YB
    )
    
Another example :

    func (b ByteSize) String() string {
    switch {
    case b >= YB:
        return fmt.Sprintf("%.2fYB", b/YB)
    case b >= ZB:
        return fmt.Sprintf("%.2fZB", b/ZB)
    case b >= EB:
        return fmt.Sprintf("%.2fEB", b/EB)
    case b >= PB:
        return fmt.Sprintf("%.2fPB", b/PB)
    case b >= TB:
        return fmt.Sprintf("%.2fTB", b/TB)
    case b >= GB:
        return fmt.Sprintf("%.2fGB", b/GB)
    case b >= MB:
        return fmt.Sprintf("%.2fMB", b/MB)
    case b >= KB:
        return fmt.Sprintf("%.2fKB", b/KB)
    }
    return fmt.Sprintf("%.2fB", b)
    }
The expression YB prints as 1.00YB, while ByteSize(1e13) prints as 9.09TB.


------------------------------------------------------
## Variables

Variables can be initialized just like constants but computed at **run time**.

    var (
    home   = os.Getenv("HOME")
    user   = os.Getenv("USER")
    gopath = os.Getenv("GOPATH")
    )
