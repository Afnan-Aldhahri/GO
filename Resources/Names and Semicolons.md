
#Names

We need to spend some time talking about **naming** in Go because Naming is really important.

**Package names**

The package name is an accessor for the contents. 

Anyone could call your package, so be careful what name you choose .

package name should be good: short, expressive ,and  to the point.

Conventionally,packages are given lower case , single-word names.

No need for underscores or mixedCaps. 

packages names need not be unique among all source code.

Another convention is that the package name is the base name of its source directory;

the package in src/encoding/base64 is imported as "encoding/base64" but has name base64, not encoding_base64 and not encodingBase64.

Another short example is once.Do; once.Do(setup) reads well and would not be improved by writing once.

DoOrWaitUntilDone(setup). Long names don't automatically make things more readable.

A helpful doc comment can often be more valuable than an extra long name.

**Getters**

Go doesn't provide automatic support for getters and setters.

you have to provide getters and setters yourself.

it's not necessary to put Get into the getter's name.

If you have a field called owner (lower case, unexported), the getter method should be called 

Owner (upper case, exported), not GetOwner. 

The use of upper-case names for export provides the hook to discriminate the field from the method.

A setter function, if needed, will likely be called SetOwner. 

Both names read well in practice:

    owner := obj.Owner()
    if owner != user {
    obj.SetOwner(user)
    }

**Interface names**

One-method interfaces are named by the method name plus an -er suffix or similar modification to construct an agent noun:

Reader, Writer, Formatter, CloseNotifier etc.

**Read, Write, Close, Flush, String** and so on have recognized signatures and meanings. 

So, don't give your method one of those names unless it has the same signature and meaning, otherwise you will get confused .



**MixedCaps**

Conventionally, in Go use **MixedCaps**  rather than underscores to write multiword names.
 
---------------------------------------------------------------------------------

#Semicolons

Go's formal grammar uses semicolons to end statements Like C .

However, those semicolons do not appear in the source.

alternatively, the lexer uses a simple principle to insert semicolons automatically as it scans, so the input text is mostly free of them :

If the last token before a newline is an identifier (which includes words like int and float64),

a basic literal such as a number or string constant, or one of the tokens

    break continue fallthrough return ++ -- ) }
    
    
the lexer always inserts a semicolon after the token.


A semicolon can also be ignored immediately before a closing brace, 

so a statement such as

    go func() { for { dst <- <-src } }()
    
needs no semicolons. 

Go programs have semicolons only in places such as for loop clauses, 

to separate the initializer, condition, and continuation elements.


One consequence of the semicolon insertion rules is that you cannot put the opening brace of a control structure

(if, for, switch, or select) on the next line.

If you do, a semicolon will be inserted before the brace, which could cause unwanted effects.

Write them like this

    if i < f() {
        g()
    }
    not like this
    if i < f()  // wrong!
    {           // wrong!
    g()
    }
