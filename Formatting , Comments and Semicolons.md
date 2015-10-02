
# Formatting , Comments and Semicolons

 The **gofmt** program  examine a Go program and give out the source in a standard style of indentation 
 
 and vertical alignment, retaining  comments.
 
As an example, there's no need to spend time adjust the comments with the structure.
Gofmt will do that for you. Given the declaration

    type T struct {
    name string // name of the object
    value int // its value
    }
    
gofmt will line up the columns:

    type T struct {
    name    string // name of the object
    value   int    // its value
    }


**Indentation**

Use spaces only if you need to because when we use tabs for indentation gofmt emits them by default.


**Line length**

 If a line was too long, wrap it and indent with an extra tab becuse Go has no line length limit
 
**Parentheses**

 control structures (if, for, switch) do not have parentheses in their syntax.
 
--------------------------------------------
**Commentary**

 // line comments like C++
 
 ** /* */ ** block comments like C
 
 usually programmers use this for multiple line when you want to writ long description about a method for example.
 
 Howver, /* */ works for one line too.
 
 


