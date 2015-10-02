
#Data

##Arrays



 arrays in **Go** and **C** are *different* .
 
 In Go:

Arrays are *values*.

Assigning one array to another copies all the elements.

So, if you pass an array to a function, the function will get a *copy* of the array, not a *pointer* to it.

The size of an array is part of its type.

The types [10]int and [20]int are distinct.

If you want C-like behavior, you can pass a pointer to the array.

    func Sum(a *[3]float64) (sum float64) {
    for _, v := range *a {
        sum += v
    }
    return
     }

    array := [...]float64{7.0, 8.5, 9.1}
    x := Sum(&array)  // Note the explicit address-of operator
---------------------------------------------------------------------------

##Maps

Maps are a strong built-in data structure that connect values of one type (the key) with 

values of another type (the element or value) .

The *key* can be :

integers, floating point and complex numbers, strings, pointers,

interfaces (as long as the dynamic type supports equality), structs and arrays.

*Maps* can be constructed using the usual composite literal syntax with colon-separated key-value pairs, so it's easy to build them during initialization.

    var timeZone = map[string]int{
    "UTC":  0*60*60,
    "EST": -5*60*60,
    "CST": -6*60*60,
    "MST": -7*60*60,
    "PST": -8*60*60,
    }
    
    
To *test* for presence in the map without worrying about the actual value, you can use the blank identifier (_) in place of the usual variable for the value.

    _, present := timeZone[tz]

To *delete* a map entry, use the delete built-in function, whose arguments are the map and the key to be deleted. 

    delete(timeZone, "PDT")  // Now on Standard Time
    
---------------------------------------------------------------------------------

##Printing

 The functions live in the *fmt package* and have capitalized names: **fmt.Printf, fmt.Fprintf, fmt.Sprintf **.
 
 The string functions (**Sprintf etc.**) return a string rather than filling in a provided buffer.

You don't need to provide a format string. 

For each of Printf, Fprintf and Sprintf there is another pair of functions, for instance Print and Println. 

In this example each line produces the same output.

    fmt.Printf("Hello %d\n", 23)
    fmt.Fprint(os.Stdout, "Hello ", 23, "\n")
    fmt.Println("Hello", 23)
    fmt.Println(fmt.Sprint("Hello ", 23))
 

The numeric formats such as %d do not take flags for signedness or size,like C, instead, the printing routines use the type of the argument to decide these properties.

    var x uint64 = 1<<64 - 1
    fmt.Printf("%d %x; %d %x\n", x, x, int64(x), int64(x))
prints
18446744073709551615 ffffffffffffffff; -1 -1

     
